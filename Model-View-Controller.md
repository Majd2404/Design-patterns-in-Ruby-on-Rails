# Architectural Patterns in Ruby on Rails

## MVC (Model-View-Controller)
The **MVC (Model-View-Controller)** pattern is the core architectural pattern in Rails. It separates the application into three main components:

- **Model**: Manages the data and business logic.
- **View**: Handles the presentation and UI.
- **Controller**: Manages user input and coordinates between the Model and View.

### Example:
```ruby
# app/models/user.rb
class User < ApplicationRecord
  validates :name, presence: true
end

# app/controllers/users_controller.rb
class UsersController < ApplicationController
  def index
    @users = User.all
  end
end

# app/views/users/index.html.erb
<% @users.each do |user| %>
  <p><%= user.name %></p>
<% end %>
```

---

