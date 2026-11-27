# Docker Keywords and Concepts

This file is an index of Docker terminology, Dockerfile instructions, CLI operations, Compose configuration, and container operations. Docker is a platform and tooling ecosystem, not a programming language. The Dockerfile instruction list below covers common instructions and is not a complete replacement for a version-specific reference.

Behavior can vary by Docker Engine, Docker Desktop, builder, operating system, and Compose implementation. Check the target environment before relying on a version-specific option.

For the course outline and broader review, see [README.md](README.md) and [Docker summary](docker-summary.md).

## Container and image vocabulary

- **Container** - an isolated runtime process with configured files, environment, network, and resource access.
- **Container image** - layered template used to create containers.
- **Container instance** - a running or stopped container created from an image.
- **Image layer** - filesystem changes produced during an image build.
- **Writable container layer** - temporary writable layer associated with a container.
- **Image tag** - human-readable reference that can be reassigned to image content.
- **Image digest** - content-addressed identifier for a specific image manifest or artifact.
- **Image ID** - local identifier for an image object.
- **Registry** - service that stores and distributes images.
- **Repository** - named collection of related image references in a registry.
- **Base image** - starting image used by a Dockerfile stage.
- **Parent image** - image from which another image or stage is derived.
- **Multi-platform image** - image reference that can resolve to platform-specific image manifests.
- **OCI image format** - open container image packaging format supported by many runtimes and registries.
- **Container runtime** - component that creates and manages container processes.
- **Containerization** - packaging and running application processes using container isolation.
- **Virtual machine (VM)** - virtualized hardware environment that runs a guest operating-system kernel.
- **Container isolation** - process, filesystem, network, and resource boundaries provided by the host kernel and runtime.
- **Container lifecycle** - creation, start, stop, restart, and removal states for a container.
- **Exit code** - numeric status returned when the primary container process finishes.
- **Container ID** - identifier assigned to a created container.
- **Image pull** - retrieving image content from a registry.
- **Image push** - uploading image content to a registry.
- **Image provenance** - information describing how and from what inputs an image was built.
- **Software bill of materials (SBOM)** - inventory of software components included in an artifact.

## Docker architecture and endpoints

- **Docker Engine** - Docker's container management technology, including the daemon, API, and CLI.
- **Docker daemon** - background service that manages Docker resources.
- **dockerd** - Docker daemon process name.
- **Docker CLI** - command-line client for sending requests to a Docker endpoint.
- **Docker Engine API** - API used to manage Docker Engine resources.
- **Docker context** - configuration selecting a Docker endpoint and related connection information.
- **Docker Desktop** - desktop application that provides an integrated Docker environment on supported systems.
- **Docker host** - machine or managed environment where Docker workloads run.
- **Remote daemon** - Docker daemon accessed over a configured endpoint rather than the local default.
- **BuildKit** - modern Docker build engine and feature set.
- **Buildx** - Docker CLI plugin that provides advanced BuildKit build workflows.
- **Builder instance** - configured build environment used by Buildx.
- **Container backend** - runtime environment provided by Engine or Desktop.

## Dockerfile instructions

Dockerfile instruction names are conventionally written in uppercase, though instruction parsing is case-insensitive in the documented syntax. Instruction behavior can depend on Dockerfile frontend and builder version.

- **FROM** - select a base image or start a new build stage.
- **RUN** - execute build-time commands and record resulting filesystem changes.
- **CMD** - provide the default command or arguments used when a container starts.
- **ENTRYPOINT** - define the primary executable for a container.
- **COPY** - copy files from a build context or stage into an image.
- **ADD** - copy files with additional supported source handling; use COPY for ordinary local copies.
- **WORKDIR** - set the working directory for subsequent instructions and runtime defaults.
- **ENV** - define environment variables stored in image configuration.
- **ARG** - define build-time values that can be set when building.
- **EXPOSE** - document an intended container port; it does not publish the port to the host.
- **USER** - set the user and optionally group for later build steps or runtime.
- **VOLUME** - declare a mount point associated with persistent or external storage.
- **LABEL** - add metadata to an image.
- **HEALTHCHECK** - define a command for reporting container health.
- **STOPSIGNAL** - set the signal sent to stop the container's main process.
- **SHELL** - configure the shell used by shell-form instructions.
- **ONBUILD** - configure a trigger instruction for child builds.
- **Dockerfile parser directive** - special leading comment that can select syntax or influence parsing.
- **Build stage** - a named or numbered stage in a multi-stage Dockerfile.
- **Build target** - selected stage used as the final build output.
- **Exec form** - JSON-array form of commands that can start the executable directly.
- **Shell form** - command form interpreted through a shell.
- **Entrypoint arguments** - runtime arguments provided to the image's primary executable.
- **Build argument** - value provided while a build stage runs; not safe storage for secrets.
- **Runtime environment variable** - value supplied to the container process at runtime.
- **Dockerfile instruction cache** - reusable result from an earlier build instruction when inputs are unchanged.

## Build context and optimization

- **Build context** - set of files and named inputs available to a Docker build.
- **Default context** - primary filesystem or remote source passed to a build command.
- **Named context** - additional named source made available to a build.
- **.dockerignore** - patterns that exclude files from the default build context.
- **Dockerfile-specific ignore file** - ignore file associated with a particular Dockerfile where supported.
- **Build cache** - reusable results from prior build steps.
- **Cache invalidation** - conditions that require a build step to run again.
- **Layer cache** - reuse of image build layers where instruction inputs match.
- **Build secret** - secret supplied to a build step through a secret mechanism rather than embedded in an image.
- **SSH mount** - temporary build access to an SSH agent or key source where supported.
- **Multi-stage build** - Dockerfile workflow with multiple stages, often separating build and runtime dependencies.
- **BuildKit frontend** - component that interprets Dockerfile syntax for the builder.
- **Build target platform** - operating-system and architecture combination for an image output.
- **Cross-platform build** - build workflow that targets a platform different from the build host.
- **Buildx** - CLI interface to BuildKit features including multi-platform builds.
- **Build metadata** - information recorded about a build and its inputs.
- **Reproducible build** - build designed to produce the same output from controlled inputs.
- **Build provenance** - record of source, parameters, builder, and other information used to create an artifact.

## Runtime commands and options

- **docker build** - build an image from a Dockerfile and context.
- **docker buildx build** - build using Buildx and BuildKit.
- **docker run** - create and start a new container from an image.
- **docker create** - create a container without starting it.
- **docker start** - start a stopped container.
- **docker stop** - request that a running container stop.
- **docker restart** - restart a container.
- **docker rm** - remove a container.
- **docker ps** - list running containers; an option can include stopped containers.
- **docker images** - list local images.
- **docker pull** - retrieve an image from a registry.
- **docker push** - publish an image to a registry.
- **docker logs** - view a container's captured output.
- **docker exec** - run a command in a running container.
- **docker inspect** - display structured information about a Docker resource.
- **docker stats** - display selected resource-usage information.
- **docker tag** - create another image reference to image content.
- **docker login** - authenticate to a registry.
- **docker logout** - remove local registry credentials.
- **docker volume** - manage Docker volumes.
- **docker network** - manage Docker networks.
- **docker context** - manage Docker endpoint contexts.
- **docker system df** - summarize Docker disk usage.
- **docker system prune** - remove selected unused resources; review scope before using.
- **Detached mode** - run a container in the background from the CLI.
- **Interactive mode** - attach input and terminal behavior to a container process.
- **Port publishing (-p)** - map a host port or interface to a container port.
- **Environment option (-e)** - provide a runtime environment variable.
- **Mount option (--mount)** - configure a volume, bind mount, or supported mount type.
- **Restart policy** - configure container restart behavior after process exit.
- **Resource limit** - constraint on CPU, memory, processes, or other resources.
- **Health status** - health-check result reported for a container.
- **Restart policy versus health check** - restart policy responds to process lifecycle; a health check reports status.

## Docker Compose model and keys

Compose configuration describes a multi-container application. Supported fields and exact behavior depend on the Compose specification and implementation version.

- **Compose file** - YAML configuration describing services and related resources.
- **Compose project** - group of resources created and managed from a Compose application model.
- **services** - top-level mapping of application components to their container configuration.
- **image** - image reference used to start a service.
- **build** - build configuration for a service image.
- **command** - command or arguments that override an image default.
- **entrypoint** - executable override for a service.
- **environment** - runtime environment variables.
- **env_file** - file supplying environment variable values.
- **ports** - host-to-container port mappings.
- **expose** - ports made available to other services without host publishing in common Compose use.
- **volumes** - persistent volumes or host paths mounted into a service.
- **networks** - networks a service joins.
- **depends_on** - dependency or start-order relationship; not a readiness guarantee by itself.
- **healthcheck** - health test configuration for a service container.
- **restart** - service restart behavior.
- **profiles** - groups of optional services selected for a workflow.
- **secrets** - sensitive configuration supplied through supported Compose secret handling.
- **configs** - non-secret configuration supplied to services.
- **container_name** - explicit container name; can affect scaling and project flexibility.
- **working_dir** - runtime working directory for a service.
- **read_only** - option to make a container root filesystem read-only where supported.
- **docker compose up** - create or update and start application services.
- **docker compose down** - stop and remove Compose-managed containers and networks; named volumes may be retained or removed depending on options.
- **docker compose logs** - view logs from Compose services.
- **docker compose exec** - run a command in a running Compose service container.
- **docker compose config** - render and validate the resolved Compose configuration.
- **Compose dependency readiness** - application-level check that a dependency can serve requests, beyond merely starting first.

## Storage and networking

- **Docker volume** - storage managed by Docker outside a container's writable layer.
- **Named volume** - volume referenced by a stable explicit name.
- **Anonymous volume** - volume created without an explicit stable name.
- **Bind mount** - mapping between a host path and a container path.
- **tmpfs mount** - temporary memory-backed mount on supported systems.
- **Volume driver** - component that provides storage behavior for Docker volumes.
- **Bridge network** - virtual network for containers on a Docker host.
- **User-defined bridge** - bridge network with configurable membership and service discovery.
- **Host network** - network mode that shares host networking behavior where supported.
- **Overlay network** - network spanning multiple Docker hosts in supported configurations.
- **Container DNS** - name resolution between containers on a network.
- **Published port** - host interface and port forwarded to a container port.
- **Container port** - port on which a process listens inside a container network namespace.
- **Network alias** - additional DNS name for a container endpoint on a Docker network.
- **Network namespace** - Linux isolation of network interfaces, routes, and related state.

## Security and isolation

- **Docker daemon attack surface** - host-control capability created by access to the Docker daemon.
- **Rootless mode** - mode in which the daemon and containers run without host root privileges, subject to prerequisites.
- **User namespace** - kernel isolation and ID mapping for users inside a container.
- **Non-root user** - application identity with limited container permissions.
- **Linux capability** - fine-grained privilege that can be granted or removed from a process.
- **Privileged container** - container with expanded host device and capability access.
- **Seccomp** - Linux system-call filtering mechanism.
- **AppArmor** - Linux mandatory access control system using profiles.
- **SELinux** - Linux mandatory access control system using labels and policy.
- **Read-only root filesystem** - runtime restriction that prevents writes to the container root filesystem.
- **Secret management** - controlled delivery of credentials or sensitive configuration to workloads.
- **Image scanning** - analysis of an image for known vulnerabilities or policy issues.
- **Trusted base image** - base image selected from a reviewed source and maintained according to update policy.
- **Least privilege** - limiting daemon, container, and process access to required authority.
- **Host mount risk** - possibility that a container can read or modify host files through a bind mount.

## Operations and deployment

- **Logging driver** - mechanism Docker uses to collect or forward container output.
- **Log rotation** - retention policy limiting accumulated log data.
- **Image cleanup** - removal of unneeded local image references or layers.
- **Volume cleanup** - removal of unused volume data; may permanently delete application state.
- **Container cleanup** - removal of stopped or unused containers.
- **Orchestrator** - system that schedules workloads across machines and manages health or desired state.
- **Docker Swarm** - Docker's native clustering and orchestration mode.
- **Kubernetes** - container orchestration platform with a different object model and control plane.
- **CI pipeline** - automated process for building, checking, and publishing software artifacts.
- **Multi-platform manifest** - registry object that maps a single image reference to platform-specific images.
- **Rollback** - returning a deployment to a known previous image or configuration.
- **Image update policy** - process for rebuilding and deploying images when base images or dependencies change.
