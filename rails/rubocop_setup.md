# Setup Rubocop 

based on this great artcle https://evilmartians.com/chronicles/rubocoping-with-legacy-bring-your-ruby-code-up-to-standard

it uses:
* https://github.com/rubocop-hq/rubocop
* https://github.com/testdouble/standard
* https://github.com/rubocop-hq/rubocop-performance
* https://github.com/rubocop-hq/rubocop-rails
* https://github.com/rubocop-hq/rubocop-rspec 

## add gems to Gemfile

```
group :development, :test do
  ....
  gem "rubocop", "~> 0.80.0"
  gem "standard", "~> 0.2.0", require: false # https://github.com/testdouble/standard
  gem "rubocop-performance", require: false
  gem "rubocop-rails", require: false
  gem "rubocop-rspec", require: false
end

```

## .rubocop.yml

```
inherit_mode:
  merge:
    - Exclude

require:
  - rubocop-performance
  - standard/cop/semantic_blocks

inherit_gem:
  standard: config/base.yml

inherit_from:
  - .rubocop_rails.yml
  - .rubocop_rspec.yml
  - .rubocop_strict.yml

AllCops:
  TargetRubyVersion: 2.6 # TODO ADJUST RUBY VERSION
  DisabledByDefault: true
  Include:
    - '**/*.rb'
  Exclude:    
    - '**/tmp/**/*'
    - '**/vendor/**/*'
    - '**/node_modules/**/*'

Layout/LineLength:
  Max: 130

Style/StringLiterals:
  Enabled: true
  EnforcedStyle: double_quotes

Style/HashSyntax:
  Enabled: true
  EnforcedStyle: ruby19_no_mixed_keys
```

## copy all other setting 

```
curl -O https://gist.githubusercontent.com/stereosupersonic/7ca195f10ef8ac4655aa6b7aa2040637/raw/b5a0b74ac2f5e0023219b82e3d17ad6104df2b2f/.rubocop_strict.yml
curl -O https://gist.githubusercontent.com/stereosupersonic/a79470b9a599d9a67758d170deafe340/raw/64087838ec46e5acad09fd8a2189829c518412d5/.rubocop_rails.yml
curl -O https://gist.githubusercontent.com/stereosupersonic/608bc8142bd502e5fbbec6a5b20b34a5/raw/5cfba4b3dd2ddb2036a6769771cfabc979ce1c22/.rubocop_rspec.yml

```
#### run autocorrection

```
bundle exec rubocop -a
``` 

or add ignore everything for now

```
bundle exec rubocop \
  --auto-gen-config \
  --auto-gen-only-exclude \
  --exclude-limit=10000
```
