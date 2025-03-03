# Architectural Patterns in Ruby on Rails

## CQRS (Command Query Responsibility Segregation)
**CQRS** separates read and write operations to optimize performance and scalability.

### Example:
```ruby
# app/commands/create_user.rb
class CreateUser
  def self.call(params)
    user = User.new(params)
    user.save!
  end
end

# app/queries/fetch_users.rb
class FetchUsers
  def self.call
    User.select(:id, :name, :email).order(:created_at)
  end
end
```

- **Command (`CreateUser`)** handles database modifications.
- **Query (`FetchUsers`)** handles read operations.