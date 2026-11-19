## 1. Container Host / Docker Host

A **Docker host** is a physical or virtual machine that runs the Docker Engine and hosts containers.

## 2. Container Client / Docker Client

The **Docker client** (`docker` CLI) sends commands to the Docker daemon, which manages images and containers. The client can run on the host itself or connect to a remote Docker host. In simple words, Docker client is the command-line tool or visual interface we use to talk to Docker and give it instructions.

- **Local connection:** Commonly uses the Unix socket `unix:///var/run/docker.sock` on Linux.
- **Remote connection:** Can use SSH or a secured TCP connection. **Do not expose an unsecured Docker TCP socket.**

### Docker Editions

- **Docker Community Edition (Docker CE):** The community-focused Docker Engine distribution.
- **Docker Enterprise Edition (Docker EE):** A historical enterprise offering. The Docker enterprise product landscape has changed; **Docker EE is not simply the current paid edition of Docker CE**.

## 3. Container Images

A **container image** is a read-only, layered package containing an application, its dependencies, and the filesystem content required to run it.

**Images do not include a complete operating-system kernel.** Linux containers share the host's Linux kernel, although images may contain user-space tools and libraries from a Linux distribution.

### Types of Images

1. **Prebuilt images:** Images published by a community, vendor, or organization and ready to pull and use.
2. **Custom images:** Images built for specific application requirements, typically using a `Dockerfile`.

## 4. Image Registry Server

A **container registry** stores and distributes container images in a centralized location.

### Types of Registries

1. **Public registries:** Accessible to the public, although some images may require authentication or have access restrictions.
   - Docker Hub: `docker.io`
   - Red Hat Registry: `registry.redhat.io`
   - Red Hat Quay: `quay.io`
   - GitHub Container Registry: `ghcr.io`
2. **Private registries:** Restricted registries used by companies or teams to store internal images.

## 5. Container

A **container** is a runnable instance of an image. Multiple containers can be created from the **same image** and run simultaneously.

Containers typically have isolated processes, filesystem views, and networking. **A unique IP address, network interface, or user identity is not guaranteed for every container**; isolation depends on its configuration.

## 6. Namespaces

**Linux namespaces** isolate what a container's processes can see, such as process IDs, network interfaces, mount points, hostnames, and user IDs.

Examples include **PID, network, mount, UTS, IPC, and user namespaces**. Namespaces provide isolation; they are not simply names or identities assigned to containers.

## 7. Control Groups (cgroups)

**Linux cgroups** track, control, and limit resource usage for groups of processes, including **CPU, memory, and I/O**.

They help prevent a container from consuming excessive host resources when appropriate limits are configured.

## 8. Container Runtime

A **container runtime** helps create, start, stop, and manage containers.

- **containerd:** A container runtime that manages container lifecycle operations.
- **CRI-O:** A container runtime designed for Kubernetes through the Container Runtime Interface (CRI).
- **runc:** A lower-level OCI runtime commonly used to create and run containers.

**Correction:** A container runtime is not necessarily a *plugin*. Docker Engine commonly uses `containerd` and `runc`; CRI-O is primarily used in Kubernetes environments.

## Trivy

**Trivy** is a security scanner used to find vulnerabilities and certain misconfigurations or secrets in container images, filesystems, repositories, and other supported targets.

Example — scan a container image:

```bash
trivy image nginx:latest
```

> **Key concept:** Images are packaged templates; containers are running instances. Namespaces provide isolation, while cgroups manage resource consumption.
