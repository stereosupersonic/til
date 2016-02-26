# Deploy a simple rails app on aws

## create a rails application with an dockerfile like

```
FROM ruby:2.2.2

RUN apt-get update -yqq && apt-get install -y build-essential

EXPOSE 3000

# for postgres
RUN apt-get install -y libpq-dev

# for nokogiri
RUN apt-get install -y libxml2-dev libxslt1-dev

# for capybara-webkit
RUN apt-get install -y libqt4-webkit libqt4-dev xvfb

# some tools
RUN apt-get install -y vim

# for a JS runtime
RUN apt-get install -y nodejs

RUN mkdir /app
WORKDIR /app
COPY Gemfile /app/
COPY Gemfile.lock /app/
RUN bundle install

COPY . /app/
```

Build the image

```
 docker build -t sterosupersonic/bugs .
```


create a Dockerrun.aws.json file
```
{
  "AWSEBDockerrunVersion": "1",
  "Image": {
    "Name": "sterosupersonic/bugs ",
    "Update": "true"
  },
  "Ports": [
    {
      "ContainerPort": "3000"
    }
  ],
  "Logging": "/var/log/nginx"
}
```
