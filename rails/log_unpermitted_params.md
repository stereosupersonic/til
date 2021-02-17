# log unpermitted attributes (strong params)


```
# config/initializers/strong_params.rb

ActionController::Parameters.action_on_unpermitted_parameters = if Rails.env.test?
                                                                  :raise
                                                                else
                                                                  :log
                                                                end

ActiveSupport::Notifications.subscribe("unpermitted_parameters.action_controller") do |*args|
  event = ActiveSupport::Notifications::Event.new(*args)
  unpermitted_keys = event.payload[:keys]
  Rails.logger.error("Unpermitted parameters: #{unpermitted_keys.inspect} ")
end

```
