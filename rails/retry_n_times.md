# Retry n times

[Example found here](https://github.com/robertomiranda/rails/blob/5a58ba3366ec6092fcd0e69340acd93f347d2576/activerecord/lib/active_record/secure_token.rb#L36-L43)
```
def generate_unique_secure_token(attribute)
  10.times do |i|
    SecureRandom.hex(12).tap do |token|
      if exists?(attribute => token)
        raise "Couldn't generate a unique token in 10 attempts!" if i == 9
      else
        return token
      end
    end
  end
end
```
