# mock every instance

## before
```
lucian_client = Lucian::Client.new
allow(Lucian::Client).to receive(:new).and_return lucian_client
expect(lucian_client).to receive(:fetch_bw_plan).with(request_object).and_return [[]]

```

## after
```
expect_any_instance_of(Lucian::Client).to receive(:fetch_bw_plan).with(request_object).and_return [[]]

```

doc: https://relishapp.com/rspec/rspec-mocks/docs/working-with-legacy-code/any-instance

commit: https://github.com/freeletics/fl-backend-rails/pull/636/commits/7fd2c4a213158fe5d7d569779196b871a14c5892
