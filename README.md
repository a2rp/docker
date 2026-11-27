# Docker: Practical Learning Notes

These personal learning notes provide a structured path for learning Docker, from container fundamentals to building images, running multi-service applications, managing persistent data, and securing container workloads.

The course focuses on Docker Engine, Docker Desktop, Dockerfiles, BuildKit, and Docker Compose. Exact behavior may vary by Docker version, operating system, builder, and runtime configuration. Future examples should state their prerequisites and the commands or platform they target.

## Learning outcomes

By following the roadmap, you will learn to:

- Explain containers, images, registries, and how Docker differs from virtual machines.
- Build reproducible images with clear Dockerfiles, limited contexts, cache-aware layers, and multi-stage builds.
- Run containers with deliberate commands, ports, health checks, resource limits, and restart behavior.
- Persist data and connect services using volumes, bind mounts, networks, and Compose.
- Troubleshoot builds and running workloads using logs, inspection, and process access.
- Protect host and application data by applying least privilege and container security practices.
- Publish and automate images while considering tags, platforms, provenance, and dependency updates.
- Operate containerized applications with documented monitoring, backup, upgrade, and cleanup procedures.

## Prerequisites

You should be comfortable using a terminal and editing text files. Basic knowledge of Linux commands, networking, environment variables, and application development is useful. The course introduces container-specific concepts as needed.

You need a Docker-compatible environment for hands-on examples. Docker Engine is commonly used on Linux; Docker Desktop provides a managed desktop environment for supported operating systems. Installation and networking details differ by platform. Check the target version and platform before running an example.

## Quick guides

- [Docker summary](docker-summary.md)
- [Docker keywords and concepts](docker-keywords.md)

## How to use these notes

1. Read the roadmap in order. Image and container concepts come before networking, storage, Compose, and operations.
2. Use the lesson for explanations, Q&A for review and edge cases, and the example for a practical task.
3. Treat image builds and container starts as separate steps. An image is a build artifact; a container is a runtime instance created from an image.
4. Review the build context before copying files into an image. Exclude credentials, local state, and unnecessary files.
5. Identify which data is temporary and which must persist before deleting or recreating containers.
6. Use the summary for broad review and the keywords file for a quick terminology lookup.

## Security and data safety

The Docker daemon and its API can control containers, images, networks, volumes, and host mounts. Grant access only to trusted users. A bind mount can expose host files to a container, and a highly privileged container can affect the host. Prefer least privilege, non-root application users, minimal capabilities, and narrowly scoped mounts.

Do not put credentials in Dockerfiles, build arguments, image layers, source files, or public examples. Use appropriate runtime secret mechanisms. Review image sources, base image updates, published ports, mounted paths, and persistent volumes before deploying or cleaning up.

## Docker platform scope

Docker uses client and server components to build and manage containers. On Linux, containers use host-kernel isolation mechanisms. Docker Desktop adds a managed environment for running Linux containers on supported desktop systems. Containers share a kernel and are not equivalent to independent virtual machines.

Docker Compose describes a multi-container application using services, networks, volumes, and related configuration. Compose is useful for local development and other supported workflows, but its behavior and deployment target should be stated clearly.

## Course roadmap

| No. | Lesson | Q&A | Example |
|---:|---|---|---|
| 001 | [Containers, images, and virtual machines](lessons/001-containers-images-and-virtual-machines.md) | [Open Q&A](qnas/001-containers-images-and-virtual-machines.md) | [Open example](examples/001-containers-images-and-virtual-machines.md) |
| 002 | [Docker architecture: client, daemon, and builder](lessons/002-docker-architecture-client-daemon-and-builder.md) | [Open Q&A](qnas/002-docker-architecture-client-daemon-and-builder.md) | [Open example](examples/002-docker-architecture-client-daemon-and-builder.md) |
| 003 | [Docker Engine, Docker Desktop, and installation choices](lessons/003-docker-engine-docker-desktop-and-installation-choices.md) | [Open Q&A](qnas/003-docker-engine-docker-desktop-and-installation-choices.md) | [Open example](examples/003-docker-engine-docker-desktop-and-installation-choices.md) |
| 004 | [Registries, repositories, image names, and tags](lessons/004-registries-repositories-image-names-and-tags.md) | [Open Q&A](qnas/004-registries-repositories-image-names-and-tags.md) | [Open example](examples/004-registries-repositories-image-names-and-tags.md) |
| 005 | [Running containers and lifecycle commands](lessons/005-running-containers-and-lifecycle-commands.md) | [Open Q&A](qnas/005-running-containers-and-lifecycle-commands.md) | [Open example](examples/005-running-containers-and-lifecycle-commands.md) |
| 006 | [Dockerfile foundations and common instructions](lessons/006-dockerfile-foundations-and-common-instructions.md) | [Open Q&A](qnas/006-dockerfile-foundations-and-common-instructions.md) | [Open example](examples/006-dockerfile-foundations-and-common-instructions.md) |
| 007 | [Build context, .dockerignore, and file selection](lessons/007-build-context-dockerignore-and-file-selection.md) | [Open Q&A](qnas/007-build-context-dockerignore-and-file-selection.md) | [Open example](examples/007-build-context-dockerignore-and-file-selection.md) |
| 008 | [Image layers, cache, and BuildKit](lessons/008-image-layers-cache-and-buildkit.md) | [Open Q&A](qnas/008-image-layers-cache-and-buildkit.md) | [Open example](examples/008-image-layers-cache-and-buildkit.md) |
| 009 | [Multi-stage builds and smaller runtime images](lessons/009-multi-stage-builds-and-smaller-runtime-images.md) | [Open Q&A](qnas/009-multi-stage-builds-and-smaller-runtime-images.md) | [Open example](examples/009-multi-stage-builds-and-smaller-runtime-images.md) |
| 010 | [Build arguments, environment variables, and secrets](lessons/010-build-arguments-environment-variables-and-secrets.md) | [Open Q&A](qnas/010-build-arguments-environment-variables-and-secrets.md) | [Open example](examples/010-build-arguments-environment-variables-and-secrets.md) |
| 011 | [Container commands, entrypoints, and signals](lessons/011-container-commands-entrypoints-and-signals.md) | [Open Q&A](qnas/011-container-commands-entrypoints-and-signals.md) | [Open example](examples/011-container-commands-entrypoints-and-signals.md) |
| 012 | [Ports, health checks, and restart policies](lessons/012-ports-health-checks-and-restart-policies.md) | [Open Q&A](qnas/012-ports-health-checks-and-restart-policies.md) | [Open example](examples/012-ports-health-checks-and-restart-policies.md) |
| 013 | [Persistent data: volumes, bind mounts, and tmpfs](lessons/013-persistent-data-volumes-bind-mounts-and-tmpfs.md) | [Open Q&A](qnas/013-persistent-data-volumes-bind-mounts-and-tmpfs.md) | [Open example](examples/013-persistent-data-volumes-bind-mounts-and-tmpfs.md) |
| 014 | [Docker networks, DNS, and service discovery](lessons/014-docker-networks-dns-and-service-discovery.md) | [Open Q&A](qnas/014-docker-networks-dns-and-service-discovery.md) | [Open example](examples/014-docker-networks-dns-and-service-discovery.md) |
| 015 | [Docker Compose application model and file](lessons/015-docker-compose-application-model-and-file.md) | [Open Q&A](qnas/015-docker-compose-application-model-and-file.md) | [Open example](examples/015-docker-compose-application-model-and-file.md) |
| 016 | [Compose configuration, environments, and secrets](lessons/016-compose-configuration-environments-and-secrets.md) | [Open Q&A](qnas/016-compose-configuration-environments-and-secrets.md) | [Open example](examples/016-compose-configuration-environments-and-secrets.md) |
| 017 | [Compose startup order, health, and dependencies](lessons/017-compose-startup-order-health-and-dependencies.md) | [Open Q&A](qnas/017-compose-startup-order-health-and-dependencies.md) | [Open example](examples/017-compose-startup-order-health-and-dependencies.md) |
| 018 | [Local development workflows with Compose](lessons/018-local-development-workflows-with-compose.md) | [Open Q&A](qnas/018-local-development-workflows-with-compose.md) | [Open example](examples/018-local-development-workflows-with-compose.md) |
| 019 | [Databases and stateful containers](lessons/019-databases-and-stateful-containers.md) | [Open Q&A](qnas/019-databases-and-stateful-containers.md) | [Open example](examples/019-databases-and-stateful-containers.md) |
| 020 | [Logs, inspection, exec, and troubleshooting](lessons/020-logs-inspection-exec-and-troubleshooting.md) | [Open Q&A](qnas/020-logs-inspection-exec-and-troubleshooting.md) | [Open example](examples/020-logs-inspection-exec-and-troubleshooting.md) |
| 021 | [Storage usage, cleanup, and backup practices](lessons/021-storage-usage-cleanup-and-backup-practices.md) | [Open Q&A](qnas/021-storage-usage-cleanup-and-backup-practices.md) | [Open example](examples/021-storage-usage-cleanup-and-backup-practices.md) |
| 022 | [Docker contexts, remote engines, and Desktop integration](lessons/022-docker-contexts-remote-engines-and-desktop-integration.md) | [Open Q&A](qnas/022-docker-contexts-remote-engines-and-desktop-integration.md) | [Open example](examples/022-docker-contexts-remote-engines-and-desktop-integration.md) |
| 023 | [Docker daemon security and rootless mode](lessons/023-docker-daemon-security-and-rootless-mode.md) | [Open Q&A](qnas/023-docker-daemon-security-and-rootless-mode.md) | [Open example](examples/023-docker-daemon-security-and-rootless-mode.md) |
| 024 | [Container isolation: namespaces and cgroups](lessons/024-container-isolation-namespaces-and-cgroups.md) | [Open Q&A](qnas/024-container-isolation-namespaces-and-cgroups.md) | [Open example](examples/024-container-isolation-namespaces-and-cgroups.md) |
| 025 | [Linux capabilities, seccomp, and AppArmor](lessons/025-linux-capabilities-seccomp-and-apparmor.md) | [Open Q&A](qnas/025-linux-capabilities-seccomp-and-apparmor.md) | [Open example](examples/025-linux-capabilities-seccomp-and-apparmor.md) |
| 026 | [Non-root users, filesystem permissions, and hardening](lessons/026-non-root-users-filesystem-permissions-and-hardening.md) | [Open Q&A](qnas/026-non-root-users-filesystem-permissions-and-hardening.md) | [Open example](examples/026-non-root-users-filesystem-permissions-and-hardening.md) |
| 027 | [Container image trust, scanning, and supply chain](lessons/027-container-image-trust-scanning-and-supply-chain.md) | [Open Q&A](qnas/027-container-image-trust-scanning-and-supply-chain.md) | [Open example](examples/027-container-image-trust-scanning-and-supply-chain.md) |
| 028 | [Registry authentication and image publishing](lessons/028-registry-authentication-and-image-publishing.md) | [Open Q&A](qnas/028-registry-authentication-and-image-publishing.md) | [Open example](examples/028-registry-authentication-and-image-publishing.md) |
| 029 | [CI pipelines, Buildx, and multi-platform images](lessons/029-ci-pipelines-buildx-and-multi-platform-images.md) | [Open Q&A](qnas/029-ci-pipelines-buildx-and-multi-platform-images.md) | [Open example](examples/029-ci-pipelines-buildx-and-multi-platform-images.md) |
| 030 | [Orchestration concepts and Docker Swarm overview](lessons/030-orchestration-concepts-and-docker-swarm-overview.md) | [Open Q&A](qnas/030-orchestration-concepts-and-docker-swarm-overview.md) | [Open example](examples/030-orchestration-concepts-and-docker-swarm-overview.md) |
| 031 | [Production monitoring, updates, and operations](lessons/031-production-monitoring-updates-and-operations.md) | [Open Q&A](qnas/031-production-monitoring-updates-and-operations.md) | [Open example](examples/031-production-monitoring-updates-and-operations.md) |
| 032 | [Capstone: build and secure a multi-container application](lessons/032-capstone-build-and-secure-a-multi-container-application.md) | [Open Q&A](qnas/032-capstone-build-and-secure-a-multi-container-application.md) | [Open example](examples/032-capstone-build-and-secure-a-multi-container-application.md) |

## Repository structure

- README.md - course introduction, setup guidance, and linked roadmap.
- LICENSE - MIT license for this notes repository.
- docker-summary.md - topic-wide Docker review and container concepts.
- docker-keywords.md - Docker commands, configuration, and terminology.
- lessons/ - chapter explanations, to be written in future steps.
- qnas/ - chapter questions and answers, to be written in future steps.
- examples/ - practical chapter examples, to be written in future steps.

## Future chapter content

The lesson, Q&A, and example files are intentionally empty in this initial scaffold. Their detailed content will be written in future steps, one chapter at a time.

## License

This repository is licensed under the MIT License. See [LICENSE](LICENSE).
