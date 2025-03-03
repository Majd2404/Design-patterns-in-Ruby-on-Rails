# Architectural Patterns in Ruby on Rails

## Repository Pattern
The **Repository Pattern** abstracts the database queries from the domain logic, making it easier to maintain and test.

### Example:
```ruby
# app/repositories/user_repository.rb
class UserRepository
  def self.find_by_email(email)
    User.find_by(email: email)
  end
end

# app/controllers/users_controller.rb
class UsersController < ApplicationController
  def show
    @user = UserRepository.find_by_email(params[:email])
  end
end
```