---
{"dg-publish":true,"permalink":"/000-zettelkasten/container-runtime-cr/","tags":["container"],"noteIcon":""}
---


# What is a Container Runtime

A Container runtime is a low-level tool responsible for creating and managing containers. 

- Interacts directly with the host operating system 
- Abstract away [[sys-calls\|sys-calls]]
- Manages the container's resources
    - CPU, memory, and networking

Container Runtimes are typically used by a [[010 Inbox/Container Engine\|Container Engine]].

## Examples for Container Runtimes 

- [[rkt\|rkt]]
- [[010 Inbox/containerd\|containerd]]
- [[]]

## See Also

- [[010 Inbox/Kubernetes/Container Runtime Interface (CRI)\|Container Runtime Interface (CRI)]]
- [[000 Zettelkasten/OCI Compliant Container Runtimes\|OCI Compliant Container Runtimes]]
- [[010 Inbox/Container Engine\|Container Engine]]
- [[000 Zettelkasten/Kubernetes Container Runtimes\|Kubernetes Container Runtimes]]