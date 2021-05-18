# CurrentAttributes

https://api.rubyonrails.org/classes/ActiveSupport/CurrentAttributes.html

ActiveSupport::CurrentAttributes allows to store some objects and access them anywhere in the code. It’s thread-safe and resets automatically on each request. It can be used to store request information such as current user, action, IP address and use them in models, services and any other place without passing them directly. Some real word example - imagine a case when you need to log all model changes with information who changed it. Passing this data everywhere can be really painful. We can use CurrentAttributes to store them and use them in after_save callback on the tracked model.

```

class Current < ActiveSupport::CurrentAttributes
  attribute :user, :ip, :controller, :action
end

class SampleController < ApplicationController
  before_action :set_context

  def set_context
    Current.user = current_user
    Current.ip = request.remote_ip
    Current.controller = params[:controller]
    Current.action = params[:action]
  end
end


class MyModel < ApplicationRecord
  has_many :object_changes

  after_save :save_object_changes

  private

  def save_object_changes
    object_changes.create!(
      user_id: Current.user.id,
      ip: Current.ip,
      controller: Current.controller,
      action: Current.action,
      changes: previous_changes
    )
  end
end

```
