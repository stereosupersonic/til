# Searching/Filtering Pattern


```
class Admin::ListEventsInteractor
  include ActiveModel::Model

  attr_accessor :fl_uid, :done_by, :type, :source

  def call
    scope = Event.recent
    filters = [fl_uid_filter, done_by_filter, type_filter, source_filter].compact

    filters.each do |filter|
      scope = scope.merge(filter)
    end
    scope
  end

  private

  def fl_uid_filter
    Event.where(fl_uid: fl_uid) if fl_uid.present?
  end

  def done_by_filter
    Event.where(done_by: done_by) if done_by.present?
  end

  def type_filter
    Event.where(type: type) if type.present?
  end

  def source_filter
    Event.where(source: source) if source.present?
  end
end
```
