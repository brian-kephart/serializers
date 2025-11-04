# README

This repo reproduces an issue with custom serializers in Rails 8.1.0 and 8.1.1.

The relevant code can be perused in the commit labeled "Reproduce custom serializer issue".

Custom serializers are configured in config/initializers/custom_serializers.rb.

There is a test case in test/serializers/custom_serializers_test.rb, but since the issue is related to code loading, which is different in the test environment, the test always passes because the issue is not successfully reproduced in that environment.

Repro steps, after checking out this repo and running `bin/setup --skip-server`:
```ruby
# rails console
my_model = MyModel.new "my_attr" => 42
ActiveJob::Serializers.serialize my_model # ActiveJob::SerializationError
```
