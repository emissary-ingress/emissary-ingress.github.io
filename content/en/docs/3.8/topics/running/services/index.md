# Available plugins

You may need an API Gateway to enforce policies specific to your organization. Emissary supports custom policies through external service plugins. The policy logic specific to your organization is implemented in the external service, and Emissary is configured to send RPC requests to your service.

Currently, Emissary supports plugins for authentication,
access logging, rate limiting, and tracing.

* [AuthService](auth-service) Plugin
* [LogService](log-service) Plugin
* [RateLimitService](rate-limit-service) Plugin
* [TracingService](tracing-service) Plugin
