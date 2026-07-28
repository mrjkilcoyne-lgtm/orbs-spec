# API Documentation

## Scope
Documenting REST, GraphQL, or gRPC interfaces: clarity, completeness, and examples that work.

## Core principles
- API docs are a contract: they specify what inputs do what, what outputs are returned, and what errors occur. Precision is non-negotiable; ambiguity breaks integrations.
- Rate limiting, authentication, and error codes are not optional details—they're central to using the API. Hide them in a footnote and integrators spend days debugging.
- Real-world examples (with actual sample payloads) are essential; generated stubs from schemas are necessary but insufficient.
- Versioning and deprecation policies must be explicit; when are old versions supported? What happens when you stop supporting a version?
- Provide SDKs or client libraries in popular languages; a 1-hour integration for users saves 100 hours of support questions.

## Apex practices
- Structure each endpoint as: description → request (method, path, parameters, authentication) → response (status codes, payload examples) → errors (with fixes).
- Use OpenAPI/Swagger YAML or JSON; it enables interactive exploration (Swagger UI, ReDoc) and code generation.
- Test your examples; nothing undermines trust like copy-pasted snippets that don't work. Automation (CI running example code) ensures they stay fresh.
- Provide a sandbox or test environment; developers want to play before committing.

## Pitfalls
- Assuming schemas are self-documenting; developers still need prose explaining intent, constraints, and use cases.
- Omitting error scenarios; covering happy paths leaves users stranded when they hit errors.
- Separating authentication and rate limits from the core docs; they're core, not afterthoughts.

## Tools & references
OpenAPI 3.0 specification, Swagger UI / ReDoc, Postman collections (testable examples), GraphQL schema documentation, gRPC proto docs.
