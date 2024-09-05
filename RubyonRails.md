# Ruby on Rails 

1. Rails API Mode
- Rails has an API-only mode (`--api` flag) that generates a lighter framework for building APIs, excluding features like view rendering and session management.
- Command to generate an API-only Rails application:
```bash
rails new my_api --api
```

2. Routing
- In an API, the routing layer maps incoming HTTP requests to controller actions.
- Use RESTful routing to map your resources:
```ruby
Rails.application.routes.draw do
  resources :users
  resources :products
end
```
- Define custom routes where needed and use namespace for versioning:
```ruby
namespace :v1 do
  resources :users
end
```

3. Controllers
- API controllers inherit from ActionController::API instead of ActionController::Base.
- Focus on returning JSON responses using render json: :
```ruby
class UsersController < ApplicationController
  def index
    users = User.all
    render json: users, status: :ok
  end
end
```

4. Serializers
- Use serializers to format JSON output. You can use ActiveModelSerializers or FastJSONAPI:
```ruby
class UserSerializer < ActiveModel::Serializer
  attributes :id, :name, :email
end
```
- This ensures the API returns structured and filtered JSON responses.

5. Authentication
- Token-based authentication: APIs often use JWT (JSON Web Tokens) for stateless authentication.
- Implement JWT with libraries like jwt or devise-jwt for token management.
- Example of generating and decoding JWT tokens:
```ruby
class JsonWebToken
  SECRET_KEY = Rails.application.secret_key_base

  def self.encode(payload, exp = 24.hours.from_now)
    payload[:exp] = exp.to_i
    JWT.encode(payload, SECRET_KEY)
  end

  def self.decode(token)
    body = JWT.decode(token, SECRET_KEY)[0]
    HashWithIndifferentAccess.new body
  rescue
    nil
  end
end
```

6. Authorization
- Authorization defines what resources a user can access. Use libraries like `Pundit` or `CanCanCan ` for managing permissions.

7. Error Handling
- Consistent error responses are crucial for API usability.
- Use a global error handler in ApplicationController:
```ruby
class ApplicationController < ActionController::API
  rescue_from ActiveRecord::RecordNotFound, with: :not_found
  rescue_from ActiveRecord::RecordInvalid, with: :unprocessable_entity

  def not_found(error)
    render json: { error: error.message }, status: :not_found
  end

  def unprocessable_entity(error)
    render json: { error: error.record.errors.full_messages }, status: :unprocessable_entity
  end
end
```

8. Versioning
API versioning helps manage changes to your API over time.
Implement versioning using namespaces in routes or the `Accept` header:
```ruby
namespace :v1 do
  resources :products
end
```

9. Pagination
- APIs with large datasets should support pagination. Use gems like `kaminari` or `will_paginate` to paginate records:
```ruby
users = User.page(params[:page]).per(10)
render json: users
```

10. Throttling and Rate Limiting
- Prevent abuse by limiting the number of requests a client can make over a certain period using libraries like Rack::Attack.
- Example configuration in config/initializers/rack_attack.rb:
```ruby
Rack::Attack.throttle('req/ip', limit: 60, period: 1.minute) do |req|
  req.ip
end
```

11. CORS (Cross-Origin Resource Sharing)
Configure CORS to allow your API to be accessed from different domains. Use the `rack-cors` gem to handle this:
```ruby
# Gemfile
gem 'rack-cors'

# config/initializers/cors.rb
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'
    resource '*', headers: :any, methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

12. Testing
- Write unit and integration tests to ensure the stability of your API.
- RSpec is a widely used testing framework in Rails. For API requests, use RSpec request specs:
```ruby
require 'rails_helper'

RSpec.describe "Products API", type: :request do
  it "returns a list of products" do
    get '/products'
    expect(response).to have_http_status(:ok)
    expect(JSON.parse(response.body).size).to eq(Product.count)
  end
end
```

13. Documentation
- APIs need documentation for developers. Use Swagger to auto-generate documentation for your Rails API.
- The rswag gem integrates Swagger with Rails:
```ruby
# Gemfile
gem 'rswag'

# To generate Swagger documentation
bundle exec rswag:specs:swaggerize
```

14. Background Jobs
- Use background job processing for tasks that should not block API responses (e.g., sending emails).
- Common libraries are Sidekiq, Resque, or Delayed Job.

15. Database Management
- Use PostgreSQL for production APIs due to its robustness.
- Configure your database in config/database.yml and ensure proper indexing for performance.

16. Security
- SSL: Always enforce SSL in production for security.
- Parameter Whitelisting: Use strong parameters in controllers to avoid mass assignment vulnerabilities:
```ruby
def user_params
  params.require(:user).permit(:name, :email, :password)
end
```

17. Logging and Monitoring
- Set up logging using tools like Lograge for better insights.
- Use services like New Relic, Datadog, or Sentry to monitor API performance and errors.

18. Deployment
- Deploy to cloud providers like AWS, Heroku, or DigitalOcean.
- Ensure you have proper environment configurations for production, including database credentials and secret keys.