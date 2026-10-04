# Breeze Workspace

Breeze Workspace is a standalone Spring Boot service for BreezeBuild, with its own Git repository and Gradle build. The [Core Platform](https://github.com/cychatwani/BreezeBuildCore), [web app](https://github.com/cychatwani/BreezeBuildWeb), and [Python/FastAPI Agentic service](https://github.com/cychatwani/BreezeBuildAgentic) live in separate repositories.

Workspace owns the source-code workspace for each BreezeBuild project. It will generate Spring Boot projects and manage their files and revisions. Builds and local/preview execution come later. Core owns project and user metadata; the Agentic service will use Workspace APIs to inspect and modify code. Long-running flows such as project initialization will be orchestrated with Temporal.

This repository currently contains only the generated application scaffold. It does not yet expose project creation, file, or revision APIs. Core has begun sending project-initialization workflow starts to Temporal, but no worker or Workspace creation contract is implemented yet. A queued workflow is not an initialized Workspace.

## Build

Use Java 21, then run:

```powershell
.\gradlew.bat classes
```

The generated `contextLoads` test currently requires database configuration. Configure the Workspace database when the first persistence feature is implemented, then run `.\gradlew.bat test`.

## Collaboration

Make changes on feature branches and propose them through pull requests targeting
`main`. The `main` branch requires a PR. Keep the repository independent of Core
and Agentic, and leave merges for human review on GitHub.
