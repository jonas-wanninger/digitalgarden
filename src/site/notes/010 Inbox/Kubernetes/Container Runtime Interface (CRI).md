---
{"dg-publish":true,"permalink":"/010-inbox/kubernetes/container-runtime-interface-cri/","tags":["container"],"noteIcon":""}
---


# Container Runtime Interface (CRI)

Abstraction Layer that basically provides plug-and-play capabilities for swapping out [[000 Zettelkasten/Container Runtime (CR)\|Container Runtime]] without effecting other parts of the system.

## Kubernetes 

In Kubernetes the CRI sits between the [[000 Zettelkasten/kubelet\|kubelet]] and the Container Runtime. Separating the CR from the kubelet Making it therefore possible to [[000 Zettelkasten/Kubernetes Container Runtimes\|use different Container Runtimes in Kubernetes]].


<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">




==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
kubelet ^oP7akGTk

kubelet ^rOLZo0s4

dockershim ^XJQKCI28

Docker ^s3545C8L

containerd ^ftQsKEaS

Container ^zi6FrqqP

containerd ^cQrTzBlS

Container ^F7llq2rs

CRI Plugin ^nDltTqml

CRI ^5K3T32Bh

CRI ^LISmCo30

[[010 Inbox/containerd\|containerd]] ^V0Dj2ocS



</div></div>


## Security

CRI also ensures that the container runtime does not have direct access to the host system, improving security and isolation.


