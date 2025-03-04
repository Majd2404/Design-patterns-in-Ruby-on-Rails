# Dependency Injection in Ruby on Rails

Dependency Injection (DI) is a design pattern where dependencies (objects/services) are provided to a class rather than being created inside it. This improves flexibility, testability, and decoupling in the application.

## Why Use Dependency Injection?

+ Reduces tight coupling between classes.
+ Makes code easier to test by allowing mock dependencies.
+ Enhances flexibility and reusability.

## Real Example: Using DI in Rails

Let's say we have a PaymentService that processes payments, and we want to inject different payment providers (e.g., StripePayment, PaypalPayment).

+ Step 1: Define Payment Providers
Each payment provider follows the same interface.

```ruby

# app/services/payment_providers/stripe_payment.rb
class StripePayment
  def charge(amount)
    puts "Charging $#{amount} via Stripe"
  end
end

# app/services/payment_providers/paypal_payment.rb
class PaypalPayment
  def charge(amount)
    puts "Charging $#{amount} via PayPal"
  end
end

```

+ Step 2: Create the Payment Service with Dependency Injection
Instead of hardcoding a payment provider, we inject it via the constructor.

```ruby

# app/services/payment_service.rb
class PaymentService
  def initialize(payment_provider)
    @payment_provider = payment_provider
  end

  def process_payment(amount)
    @payment_provider.charge(amount)
  end
end

```

+ Step 3: Inject Dependency in Controller
Now, we decide which provider to use when initializing PaymentService.

```ruby 

# app/controllers/payments_controller.rb
class PaymentsController < ApplicationController
  def create
    payment_provider = params[:provider] == "paypal" ? PaypalPayment.new : StripePayment.new
    payment_service = PaymentService.new(payment_provider)

    payment_service.process_payment(100) # Charge $100
    render json: { message: "Payment processed successfully!" }
  end
end

```

