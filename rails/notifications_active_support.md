# Notifications ActiveSupport


## call

```
 ActiveSupport::Notifications.instrument(:track_info_creation, event_name: :track_info_exits) do |payload|
   payload[:data] = { track_info: track_info.id, artist: track.artist, title: track.title }
   payload[:track] = track
   ... # do something
   payload[:foo] = :bar
 end

```

## consume

```
ActiveSupport::Notifications.subscribe(:track_info_creation) do |*args|
  event = ActiveSupport::Notifications::Event.new(*args)

  # do something with the received data
  if event.payload[:foo] == :bar
    CreateEventJob.perform_later(
      name: event.payload[:event_name],
      state: :ok,
      done_at: event.end,
      data: event.payload[:data],
      meta_data: event.payload[:meta_data],
      duration: event.duration,
      station: event.payload[:track]&.station,
      track: event.payload[:track]
    )
  end
end


```
