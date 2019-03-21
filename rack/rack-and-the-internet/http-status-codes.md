# Lesson: HTTP Status Codes

## Notes

### Why Status Codes Are Important for the Client

- Status codes allow your server to tell something special to the client. The responses you send need to be effective to both a human user and to the browser itself.
- HTTP has an agreed upon contract for different "status codes". A status code is a 3-digit integer where the first digit represents the class of the response, and the remaining two digits represent a specific status. There are 5 primary values that the first digit can take.
  - 1xx: Informational (request received and continuing process)
  - 2xx: Success (request successfully received, understood, and accepted)
  - 3xx: Redirection (further action must be taken to complete request)
  - 4xx: Client Error (request contains bad syntax and can't be completed)
  - 5xx: Server Error (server couldn't complete request)

### Status Codes in Rack

- In Rack, we are able to set the response's status code by setting the `status_code` attribute. By default, Rack sets a status code of `200`.