# Lesson: Dynamic Web Apps with Rack

## Notes

- Web servers are just big Ruby apps that respond to the user in an HTTP response rather than via `puts` statements.
  - We use the `#write` method in place of `puts`.
- The `#write` method can be called many times to build up the full response. The response isn't sent back to the user until `#finish` is called.
