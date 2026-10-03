# Breeze Workspace

Breeze Workspace is a standalone Spring Boot service for BreezeBuild, with its own Git repository and Gradle build. The Core Platform, web app, and future Python/FastAPI Agentic service live in separate repositories.

Workspace owns the source-code workspace for each BreezeBuild project. It will generate Spring Boot projects and manage their files and revisions. Builds and local/preview execution come later. Core owns project and user metadata; the Agentic service will use Workspace APIs to inspect and modify code. Long-running flows such as project initialization will be orchestrated with Temporal.

This repository currently contains only the generated application scaffold. APIs, contracts, and orchestration will be introduced with the features that need them.

## Build

Use Java 21, then run:

```powershell
.\gradlew.bat classes
```

The generated `contextLoads` test currently requires database configuration. Configure the Workspace database when the first persistence feature is implemented, then run `.\gradlew.bat test`.
