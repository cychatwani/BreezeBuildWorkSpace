# Breeze Workspace

Breeze Workspace is a standalone Spring Boot service for BreezeBuild. It has its own Git repository, Gradle build, tests, configuration, and deployment. The Core Platform, web app, and future Python/FastAPI agent runtime live in separate repositories.

This repository currently contains only the generated application scaffold. Service APIs and cross-service contracts will be defined alongside the features that need them.

## Build

Use Java 21, then run:

```powershell
.\gradlew.bat classes
```

The generated `contextLoads` test currently requires database configuration. Configure the Workspace database when the first persistence feature is implemented, then run `.\gradlew.bat test`.
