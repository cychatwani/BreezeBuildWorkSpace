# Breeze Workspace Agent Guide

`breeze-workspace` is a standalone Spring Boot service and Git repository. Keep its Gradle build, tests, configuration, and deployment independent of other BreezeBuild services. Define and verify cross-service API contracts when a feature spans repositories.

Workspace owns each project's source-code workspace: Spring Boot project generation, files, and revisions. Builds and local/preview execution are later responsibilities. Core owns project and user metadata. The separate Python/FastAPI Agentic service will use Workspace APIs to inspect and modify code. Temporal will orchestrate long-running flows such as project initialization.

This repository is currently only an application scaffold. Implement the requested layer or behavior when needed; do not add speculative APIs, persistence, build execution, or Temporal infrastructure ahead of a feature.

## Shared Core conventions

- Use Java 21 and the existing standalone Spring Boot/Gradle build. Keep Workspace code under `dev.chirag45.breeze.workspace`.
- Prefer constructor injection, thin controllers, service-level transaction boundaries, and typed enums or value types where useful.
- Generate BreezeBuild-owned IDs and accepted `X-Request-ID` correlation IDs as UUIDv7. Replace missing or invalid inbound request IDs with UUIDv7; Clerk IDs remain external strings.
- For future browser-facing APIs, validate Clerk session JWTs before protected work and derive the Clerk user ID from the verified `sub` claim. Core alone provisions local users; Workspace must not duplicate that flow. Check project-level access within Workspace.
- Follow Core's `code`/`message`/`errorCode`/`data` API response shape and propagate `X-Request-ID` once Workspace exposes HTTP APIs.
- Use `Instant` for persisted timestamps and PostgreSQL `timestamptz`, UUID primary keys, Flyway migrations, and database constraints for integrity. Validate mapped schema instead of relying on Hibernate to mutate it.
- Test PostgreSQL-specific behavior against PostgreSQL. Add service and API tests with the corresponding feature.

Do not copy Core's user-provisioning, profile-sync, or outbox code into Workspace. Temporal integration belongs with the first long-running workflow that needs it.
