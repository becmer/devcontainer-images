# Becmer's Development Container Images

This repository contains a set of **dev container images** which are Docker images built
with [dev container features](https://github.com/devcontainers/features).

## JetBrains Runtime

Docker Hub: [becmer/jbr](https://hub.docker.com/r/becmer/jbr)

These images are based
on [mcr.microsoft.com/devcontainers/java](https://github.com/devcontainers/images/tree/main/src/java), but comes
with [JetBrains Runtime](https://github.com/JetBrains/JetBrainsRuntime) instead.

| JBR Release                                                                                               | Image Tags                                | OS Variants |
|-----------------------------------------------------------------------------------------------------------|-------------------------------------------|-------------|
| [**21.0.5b631.28**](https://github.com/JetBrains/JetBrainsRuntime/releases/tag/jbr-release-21.0.5b631.28) | `21.0.5b631.28`, `21.0.5`, `21`, `latest` | `bookworm`  |
| [17.0.11b1312.2](https://github.com/JetBrains/JetBrainsRuntime/releases/tag/jbr-release-17.0.11b1312.2)   | `17.0.11b1312.2`, `17.0.11`, `17`         | `bookworm`  |
