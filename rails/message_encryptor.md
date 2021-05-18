# Message Encryptor

https://api.rubyonrails.org/classes/ActiveSupport/MessageEncryptor.html

It’s pretty similar to [MessageVerifier](https://api.rubyonrails.org/classes/ActiveSupport/MessageVerifier.html) but it keeps the content of the message safe and impossible to read without the key.

It can be used to send sensitive information between services on the client-side (for example in url) or to encrypt data before storing it in the database.

```
key = SecureRandom.random_bytes(32)
crypt = ActiveSupport::MessageEncryptor.new(key)

message = crypt.encrypt_and_sign('my message')

crypt.decrypt_and_verify(message)
=> "my message"

```
