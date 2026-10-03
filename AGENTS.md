# Breeze Workspace Agent Guide

`breeze-workspace` is a standalone Spring Boot service and Git repository. Keep its Gradle build, tests, configuration, and deployment independent of other BreezeBuild services. Define and verify cross-service API contracts when a feature spans repositories.

Workspace owns each project's source-code workspace: Spring Boot project generation, files, and revisions. Builds and local/preview execution are later responsibilities. Core owns project and user metadata. The separate Python/FastAPI Agentic service will use Workspace APIs to inspect and modify code. Temporal will orchestrate long-running flows such as project initialization.

This repository is currently only an application scaffold. Implement the requested layer or behavior when needed; do not add speculative APIs, persistence, build execution, or Temporal infrastructure ahead of a feature.
