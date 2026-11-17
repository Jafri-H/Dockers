# **Docker vs. Containers**

Docker is a company and a platform that provides tools to build, package, distribute, and run containers. **Containers** are an operating-system-level virtualization technology; Docker is one way to use them.

## **Provisioning Methods**

1. Physical servers (bare metal)
2. Virtual machines (hardware virtualization)
3. Containers (OS-level virtualization)

## **Challenges Before Widespread Container Adoption**

1. **Slow provisioning:** Setting up servers and software environments could take significant time.
2. **Dependency conflicts:** Different applications or versions could require incompatible libraries or configurations.
3. **Migration challenges:** Software might behave differently across development, testing, and production environments.

## **How Container Technology Works**

- **Virtualization** allows hardware resources to be shared among virtual machines, each normally running its own guest OS and kernel.
- **Containers** isolate applications and their user-space dependencies while sharing the host OS kernel.
- Multiple application versions can run on the same host with reduced dependency conflicts.
- Containers can have isolated filesystems, processes, and networking (including virtual network interfaces and IP addresses, depending on configuration).
- Containers package application dependencies, but they still rely on the host kernel and available hardware resources.
- A Linux container cannot directly run a Windows kernel, or vice versa; a compatible VM or other compatibility layer is required.

## **Advantages of Container Technology**

1. **Faster deployment:** Prebuilt container images reduce repeated installation work.
2. **On-demand provisioning:** Containers can be created and removed quickly.
3. **Multiple environments:** Different applications and versions can run side by side.
4. **Software portability:** Container images can be transferred between compatible environments.
5. **Efficient resource use:** Containers generally have less overhead than separate full virtual machines.

## **Why Virtualization Is Still Important**

Virtual machines are not obsolete. They generally provide stronger isolation boundaries and can run different guest kernels. Cloud providers such as AWS offer virtual machines; organizations can run containers inside those VMs to improve application deployment and resource utilization.

Containers work on both **physical servers** and **virtual machines**, as long as a compatible OS kernel and container runtime are available.

## **Virtual Machine Architecture**

```text
+----------------+  +----------------+  +----------------+
| Application    |  | Application    |  | Application    |
| Guest OS       |  | Guest OS       |  | Guest OS       |
| Guest Kernel   |  | Guest Kernel   |  | Guest Kernel   |
| VM 1           |  | VM 2           |  | VM 3           |
+----------------+  +----------------+  +----------------+
+--------------------------------------------------------+
| Hypervisor                                             |
+--------------------------------------------------------+
| Physical Hardware                                      |
+--------------------------------------------------------+
```

*Note: This shows a Type 1 hypervisor. Other virtualization architectures also exist.*

## **Container Architecture**

```text
+----------------+  +----------------+  +----------------+
| Application    |  | Application    |  | Application    |
| Dependencies   |  | Dependencies   |  | Dependencies   |
| Container 1    |  | Container 2    |  | Container 3    |
+----------------+  +----------------+  +----------------+
+--------------------------------------------------------+
| Container Runtime                                      |
+--------------------------------------------------------+
| Host OS and Shared Kernel                              |
+--------------------------------------------------------+
| Physical Hardware or Virtual Machine                   |
+--------------------------------------------------------+
```

## **Application Example: Apache**

- **Direct installation:** Apache runs as a process on the host OS and uses host-installed dependencies.
- **Container installation:** Apache runs in an isolated container environment, sharing the host kernel while using its packaged dependencies and separately configured networking.

Both approaches use the host kernel. Containers help reduce application dependency conflicts, but they do not eliminate all resource or security risks.

## **Kernel and Resource Requests**

### **Virtual Machines**

```text
VM 1: Application -> Guest Kernel --+
                                    +-> Hypervisor -> Hardware
VM 2: Application -> Guest Kernel --+
```

Each VM normally has its own kernel. The hypervisor manages virtualized hardware resources.

### **Containers**

```text
Container 1: Application --+
Container 2: Application --+-> Shared Host Kernel -> Hardware
Container 3: Application --+
```

All Linux containers running directly on the same Linux host share its kernel. Kernel features such as namespaces and cgroups help provide isolation and resource control.

## **Key Takeaway**

**Virtual machines virtualize hardware and normally run separate guest operating systems. Containers isolate applications while sharing the host OS kernel. Docker provides tools to build, distribute, and run containers.**
