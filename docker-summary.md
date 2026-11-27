# Docker Summary

A topic-wide review of Docker containers, images, builds, networking, storage, Compose, security, and operations. The README roadmap expands these concepts into lessons, Q&A, and practical examples.

Docker behavior can vary by Engine or Desktop version, operating system, builder, and runtime configuration. Confirm the target environment before using version-sensitive options.

## 1. Container model

A container is an isolated process with a configured filesystem, environment, resource limits, and network context. Containers on a Linux host share the host kernel. A virtual machine runs a separate guest operating system and kernel, so containers and virtual machines provide different isolation and overhead characteristics.

Containers help package an application with its runtime dependencies. They improve repeatability, but do not by themselves guarantee portability, security, or identical behavior. Host architecture, kernel features, mounted data, environment settings, network access, and external services still matter.

## 2. Docker architecture

Docker uses a client-server architecture:

- The Docker CLI sends requests to a Docker Engine API.
- The Docker daemon manages images, containers, networks, and volumes.
- A builder processes Dockerfiles and produces image artifacts.
- Docker Desktop provides an integrated environment on supported desktop platforms.
- A context selects which Docker endpoint the CLI uses.

The Docker CLI is not the daemon. A client can communicate with a local or remote daemon, and commands affect the endpoint selected by the current context. Check the context and target before removing resources or publishing images.

## 3. Images and containers

An image is a layered template used to create containers. A container is a runtime instance of an image with its own configuration and writable layer.

- Image layers are reused between images and builds where possible.
- A tag is a human-readable reference to an image; tags can be moved to identify a different image.
- A digest identifies image content in a content-addressed form.
- A container's writable layer is generally ephemeral and should not be treated as durable application storage.
- Named volumes, bind mounts, and external services provide other data lifecycles.

The image name typically includes a registry, namespace or organization, repository, and optional tag. Pulling by a mutable tag can retrieve different content at different times. Pinning by digest can make a deployment's image input more explicit, but updates then require deliberate digest changes.

## 4. Dockerfiles and builds

A Dockerfile describes how to build an image. Common instructions include:

- FROM - select a base image or build stage.
- WORKDIR - set the working directory for later instructions.
- COPY - copy files from the build context into an image.
- RUN - execute build-time commands.
- ENV - define environment variables in the image configuration.
- ARG - define build-time values.
- EXPOSE - document a port used by the application; it does not publish the port to the host.
- USER - select the user for later image operations or runtime.
- ENTRYPOINT - define the primary executable.
- CMD - provide a default command or arguments.

Each build instruction can affect image layers and cache reuse. Organize instructions so stable dependency inputs are processed before frequently changing application files. Use multi-stage builds to keep compilers and intermediate artifacts out of the final runtime image.

The build context is the set of files available to the builder. The path or URL passed to a build determines that context. COPY can only use files available in the context or an explicitly configured named context. A .dockerignore file excludes files from the default local context.

Exclude version-control data, local build outputs, credentials, private keys, production data, and other unnecessary files from the build context. A small context improves build performance and reduces the chance of accidentally packaging sensitive data.

## 5. Build cache and BuildKit

The builder can reuse cached results when an instruction and its relevant inputs have not changed. Cache behavior depends on instruction inputs, build arguments, source files, platform, and builder configuration.

BuildKit supports modern build workflows, including parallelizable stages, secret and SSH mounts, and improved output controls. Build secret mounts provide a way to expose credentials to a build step without baking them into an image layer. Build arguments and environment variables should not be used as secret storage because their values can be retained in build metadata or image configuration.

A cache hit is a performance optimization, not proof that an image contains the expected content. Rebuild deliberately when dependencies, base images, or security updates change.

## 6. Container runtime configuration

A container's runtime configuration determines its command, environment, user, working directory, ports, mounts, resource limits, capabilities, and restart behavior.

ENTRYPOINT and CMD work together. ENTRYPOINT identifies the main process, while CMD supplies defaults or a default command. Prefer exec-form commands when appropriate so the application receives operating-system signals directly. Shell-form behavior can affect signal delivery and process handling.

A container should usually run one primary application process and allow Docker or another supervisor to manage its lifecycle. If the application exits, the container exits unless another process keeps it running. Do not add a shell loop solely to keep a container alive.

## 7. Ports and health

A container port is not automatically reachable from the host or network. Port publishing maps a host port to a container port. Binding to a host interface determines which clients can connect. Exposing a port publicly can create a security boundary change.

A health check reports whether a configured command considers a container healthy. Health status is useful for diagnosis and orchestration, but a health check alone does not repair the application. Restart policies control actions after process exit and are distinct from health reporting.

Use health checks that test meaningful application readiness. Avoid checks that are too expensive, depend on unrelated services, or report healthy before initialization is complete.

## 8. Networks

Docker networks connect containers and, when configured, connect containers to external networks. A user-defined bridge network provides container-to-container connectivity and service-name discovery in common local workflows. Containers on the default bridge have different name-resolution behavior than those attached to user-defined networks.

Published ports connect a host interface to a container port. Internal container-to-container traffic can often use the container port directly without publishing it to the host.

Network design should consider:

- Which services need to communicate.
- Which ports must be reachable from outside the network.
- Whether DNS names remain stable across container recreation.
- How secrets and credentials are transferred.
- How host firewall and cloud firewall rules apply.
- Whether a network is intentionally isolated.

## 9. Persistent data

Choose storage according to ownership and lifetime:

- A named volume is managed by Docker and can persist independently of a container.
- An anonymous volume is created without a stable explicit name.
- A bind mount maps a host path into a container.
- A tmpfs mount stores temporary data in memory on supported hosts.
- An external database or object store has a lifecycle outside the container.

Recreating a container does not automatically migrate or back up its data. Volumes can outlive containers and continue consuming disk. Bind mounts expose host paths and can permit a container to modify host files. Review mount source and destination carefully.

Back up persistent data using application-aware procedures. A copy of a live database directory may not be a consistent backup. Test restore procedures and document which service owns the data.

## 10. Docker Compose

Docker Compose describes a multi-container application using a Compose file. The model can define services, networks, volumes, configuration, and secrets. The Compose CLI applies the model to create, update, inspect, and stop local resources.

A Compose service describes how a containerized application component should run. Multiple service replicas can be configured in supported modes, but this does not make local Compose equivalent to a full production orchestrator.

Key Compose concepts:

- Service - application component and its container configuration.
- Build - instructions or context for building a service image.
- Image - image reference for a service.
- Network - communication boundary between services.
- Volume - persistent or shared data attachment.
- Environment - runtime configuration values.
- Depends_on - startup and dependency relationship; it does not by itself prove that a dependency is ready.
- Health check - signal that can support readiness conditions.
- Profile - optional grouping of services for selected workflows.

Use health checks and retry logic when service readiness matters. Applications should tolerate temporary dependency failures even when Compose orders startup.

## 11. Registries and images

A registry stores and distributes container images. Repositories group images, and tags or digests identify references to image content. Authentication, access controls, retention, vulnerability scanning, and replication depend on the chosen registry.

Image publishing should include:

- A deliberate image name and version strategy.
- Review of the base image and dependency sources.
- Removal of credentials, temporary files, and build tools not needed at runtime.
- Vulnerability and license checks appropriate to the project.
- A clear plan for rebuilding when upstream images change.
- Access controls for private images.
- Image provenance or software bill of materials where the workflow supports it.

Avoid relying only on the latest tag for reproducible deployments. A mutable tag can point to different content over time.

## 12. Security

Container isolation is useful but not a complete security boundary. Docker daemon access is powerful because the daemon can start privileged containers, mount host paths, and control workloads. Restrict daemon access to trusted operators. On some Linux installations, membership in a Docker control group effectively grants broad host privileges.

Security controls include:

- Run application processes as non-root where practical.
- Use minimal base images and remove unnecessary packages.
- Drop Linux capabilities not needed by the workload.
- Avoid privileged containers unless a reviewed requirement exists.
- Use read-only filesystems where practical.
- Limit CPU, memory, process counts, and open files.
- Restrict host mounts and published ports.
- Keep images and the Engine updated.
- Review secrets, build context, registry trust, and dependency provenance.
- Use rootless mode, user namespace mapping, seccomp, AppArmor, or SELinux where appropriate and supported.

Root inside a container is not always equivalent to host root, but privileged mode, host namespaces, broad device access, or dangerous mounts can weaken that separation. Security depends on configuration and host controls.

## 13. Resource management and operations

Set CPU and memory constraints according to workload needs. Without appropriate limits, one container can compete heavily with other host workloads. Observe actual usage before tuning.

Docker logs usually contain the container process's stdout and stderr, depending on the logging configuration. Drivers, retention, rotation, and remote aggregation affect availability and disk usage. Monitor host disk capacity, image cache, build cache, container logs, and unused volumes.

Cleanup commands can remove images, containers, networks, and volumes. Review exactly what a cleanup operation targets before running it. Deleting an unused-looking volume can permanently delete application data.

## 14. Troubleshooting workflow

1. Confirm the active Docker context and endpoint.
2. Check whether the image build succeeded and which image reference was produced.
3. Inspect container state, exit code, command, environment, mounts, ports, and networks.
4. Read logs from the actual application process.
5. Confirm that the application listens on the expected address and container port.
6. Verify host port publishing, firewall rules, and container-network membership.
7. Check file ownership, mounted paths, permissions, and volume state.
8. Inspect CPU, memory, disk, and process limits.
9. Confirm that dependencies are ready and credentials are available without exposing them.
10. Recreate only the affected resources and preserve persistent data.
11. Record root cause, cleanup, and prevention steps.

## 15. Key mental models

- A Docker image is a build artifact; a container is an instance created from an image.
- Container writable layers are not a substitute for persistent storage.
- A Dockerfile's build context controls which local files the builder can access.
- Docker Compose describes an application model; it does not guarantee dependency readiness.
- EXPOSE documents a container port; port publishing creates host-to-container reachability.
- Health checks report status; they do not automatically correct a failed application.
- Access to the Docker daemon is a powerful administrative capability.
- A container shares a kernel with its host and is not a virtual machine.
- Tags are references; use digests when an exact image identity is required.
- Security, reproducibility, and cleanup must be designed into the workflow.
