# Sending Emails

change your environment setting e.g. config/environments/development.rb

```
  config.action_mailer.raise_delivery_errors = true
  config.action_mailer.delivery_method = :smtp
  config.action_mailer.smtp_settings = {
    :address              => <YOUR_HOST>
    :port                 => 25, # depends
    :user_name            =>  <YOUR_USER>,
    :password             =>  <YOUR_PASSWORD>,
    :authentication       => "plain",
    :enable_starttls_auto => false # depends if SSL or none like here
  }
end

```

send a test mail

```
ActionMailer::Base.mail(
   from: "m.deimel@miceportal.com",
   to: "michael@deimel.de",
   subject: "test",
   body:  "test"
 ).deliver_now
```
