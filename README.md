# AWS API Gateway + Lambda + Cognito (Java)

Serverless Java backend: **Amazon Cognito** for auth, **API Gateway** for HTTP, **Lambda** for handlers.

## Status

Greenfield repo. System design is documented; implementation not started.

## Design

See **[docs/DESIGN.md](docs/DESIGN.md)** for:

- Architecture (API Gateway → Lambda → Cognito)
- Public auth APIs and Cognito-protected APIs
- Sequence flows (signup → confirm → login → protected calls)
- Security, IAM, errors, observability, and implementation roadmap

## Planned stack

| Layer | Choice |
|-------|--------|
| Runtime | Java 21 |
| Build | Maven (multi-module) |
| IaC | AWS SAM |
| Auth | Cognito User Pool + API Gateway Cognito authorizer |

## Quick mental model

```
Client
  → POST /auth/signup|confirm|login|refresh   (public)
  → GET  /me , /protected/echo                (JWT via Cognito authorizer)
  → API Gateway → Java Lambdas → Cognito (auth flows only)
```
