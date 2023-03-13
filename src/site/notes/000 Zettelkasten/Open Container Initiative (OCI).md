---
{"dg-publish":true,"permalink":"/000-zettelkasten/open-container-initiative-oci/","tags":["container"],"noteIcon":""}
---


# Open Container Initiative

is an open governed [[CNCF\|CNCF]] project which provides a common standard for

- Container Formats 
    - Image Specification (image-spec)
- Container Runtimes
    - Runtime Specification (runtime-spec)
    - Outlines how to run a “filesystem bundle” that is unpacked on disk
        - See also: [[000 Zettelkasten/OCI Compliant Container Runtimes\|OCI Compliant Container Runtimes]]
- Distribution Specification (distribution-spec)

Docker donated [[000 Zettelkasten/runC\|runC]] to the OCI.
## How These Components Play Together

>
> ```mermaid
> graph TB
> 
>  A[Some OCI implementation] -->|downloads | B[OCI Runtime Bundle] --> | will be run by | C[OCI Runtime]
> ```