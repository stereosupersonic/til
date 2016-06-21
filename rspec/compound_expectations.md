# compound expectations

## compound-expectations https://relishapp.com/rspec/rspec-expectations/docs/compound-expectations
```
expect do
  do_something
end.to have_enqueued_job(OptivoSyncJob).once.and have_enqueued_job(OptivoSyncJob).with(1234)

```
