# Turbo Frames

https://turbo.hotwired.dev/handbook/frames

## Polling with interval

1. generate controller

```
rails g stimulus refresh
rails g controller data
```

2. add route for data

```
# config/routes.rb
Rails.application.routes.draw do
  resource :data, only: :show
  root to: 'welcome#index'
end
```

3. add endpoint with random data

```
# app/controllers/data_controller.rb
class DataController < ApplicationController
  def show
    @rand = rand()
  end
end

# app/views/data/show.html.erb
<%= turbo_frame_tag "data" do %>
  <%= @rand %>
<% end %>
```

4. show polled data

```
# app/views/welcome/index.html.erb
<%= turbo_frame_tag "data", src: data_path, data: {
  controller: :refresh } do %>
  Default content
<% end %>

```


5. stimulus controller

```
# app/javascript/controllers/refresh_controller.js
import { Controller } from "@hotwired/stimulus"

// Connects to data-controller="refresh"
export default class extends Controller {
  static values = {
    src: String,
    interval: 1000 // millisec
  }

  connect() {
    this.interval = setInterval(() => {
      this.element.reload()
    }, this.intervalValue)
  }

  disconnect() {
    clearInterval(this.interval)
  }
}
```
