# avoid race conditions with uniq index

```
class AddUniqIndexToPreventDublicatedGuideSessions < ActiveRecord::Migration
  disable_ddl_transaction!

  def change
    reversible do |direction|
      direction.up { execute("SET SESSION statement_timeout = 0;") }
      direction.down { execute("SET SESSION statement_timeout = 0;") }
    end

    add_index :guide_sessions, [:subscription_id, :week, :day], unique: true, algorithm: :concurrently
  end
end

```
