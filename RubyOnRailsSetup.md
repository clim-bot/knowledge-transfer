# Ruby on Rails Setup

## Installation
Install rails
```bash
gem install rails
```

create new rails app
```bash
rails new jwt_auth_app --api -d sqlite3
```

## Add Required Gems

Add to Gemfile
```ruby
gem 'bcrypt', '~> 3.1.7'
gem 'jwt', '~> 2.2'
gem 'rspec-rails', '~> 5.0'
```

Install gems
```bash
bundle install
rails generate rspec:install
```

## Generate User Model and Authentication
Create a user model with fields for email and password
```bash
rails g model User email:string password_digest:string
```

Run the migration
```bash
rails db:migrate
```

Modify `app/modles/user.rb`
```ruby
class User < ApplicationRecord
  has_secure_password # method to set and authenticate against a BCrypt password
  validates :email, presence: true, uniqueness: true
end
```

## Create Authntication Controller
Create a controller for handling auth
```bash
rails generate controller Auth
```

Modify `app/controllers/auth_controller.rb`:
```ruby
class AuthController < ApplicationController
  before_action :authorize_request, except: :login

  # POST /login
  def login
    @user = User.find_by_email(params[:email])
    if @user&.authenticate(params[:password])
      token = encode_token({ user_id: @user.id })
      render json: { token: token }, status: :ok
    else
      render json: { error: 'Invalid email or password' }, status: :unauthorized
    end
  end

  private

  # Encode a JWT token
  def encode_token(payload)
    JWT.encode(payload, Rails.application.secrets.secret_key_base)
  end

  # Decode a JWT token
  def decode_token
    auth_header = request.headers['Authorization']
    token = auth_header.split(' ').last if auth_header
    begin
      JWT.decode(token, Rails.application.secrets.secret_key_base)[0]
    rescue
      nil
    end
  end

  # Authorize requests
  def authorize_request
    decoded_token = decode_token
    if decoded_token
      @current_user = User.find_by(id: decoded_token['user_id'])
    else
      render json: { error: 'Unauthorized' }, status: :unauthorized
    end
  end
end
```

## Add Routes
Add routes for auth in `config/routes.rb`
```ruby
Rails.application.routes.draw do
  post '/login', to: 'auth#login'
end
```

## Testing with RSpec
Set up tests for auth in `spec/requiests/auth_spec.rb`
```ruby
require 'rails_helper'

RSpec.describe 'Authentication', type: :request do
  let(:user) { User.create(email: 'test@example.com', password: 'password') }

  describe 'POST /login' do
    context 'with valid credentials' do
      it 'returns a token' do
        post '/login', params: { email: user.email, password: 'password' }
        expect(response).to have_http_status(:ok)
        expect(JSON.parse(response.body)).to have_key('token')
      end
    end

    context 'with invalid credentials' do
      it 'returns an error' do
        post '/login', params: { email: user.email, password: 'wrong_password' }
        expect(response).to have_http_status(:unauthorized)
        expect(JSON.parse(response.body)).to have_key('error')
      end
    end
  end
end
```

Run the test
```bash
bundle exec rspec
```

## Initialize Database and Test
Create Rails console for testing
```bash
rails console
User.create(email: 'user@example.com', password: 'password')
```

Run the service
```bash
rails server
```

Test the login endpoint
```bash
curl -X POST -d "email=user@example.com&password=password" http://localhost:3000/login
```

## Configure Secret Key Base for JWT
Ensure that yous etup your scret key base in `config/secrets.yml` or use environment variables:
```yaml
development:
  secret_key_base: <%= ENV["SECRET_KEY_BASE"] %>
```

Generate a secret key base using:
```bash
rails secret
```

Generate a .env file
```bash
touch .env
```

```.env
SECRET_KEY_BASE=secret_key_here
```









