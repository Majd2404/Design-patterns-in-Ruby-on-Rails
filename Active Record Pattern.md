# Architectural Patterns in Ruby on Rails

## Active Record Pattern
Rails follows the **Active Record** pattern, where models directly interact with the database, encapsulating both data and business logic.

### Example:
```ruby
class User < ApplicationRecord
  validates :email, presence: true, uniqueness: true
end
```
This allows:
- Querying: `User.all`, `User.find(1)`
- Creating: `User.create(name: "Majd", email: "majd@example.com")`
- Validations and associations