# Create and verify tokens with mess

## gernate url safe token
```
token = Base64.urlsafe_encode64 Rails.application.message_verifier(:my_token).generate(["my message", 2.days.since])
```

## verify token
```
  Rails.application.message_verifier(:my_token).verify Base64.urlsafe_decode64(token) #=> ["my message", Sat, 04 Jun 2016 15:57:43 UTC +00:00]
```
