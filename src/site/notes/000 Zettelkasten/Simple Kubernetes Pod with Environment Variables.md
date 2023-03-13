---
{"dg-publish":true,"permalink":"/000-zettelkasten/simple-kubernetes-pod-with-environment-variables/","tags":["type/code-snippet, topic/kubernetes"],"noteIcon":""}
---


# Simple Kubernetes Pod with Environment Variables

Useful for testing the value of enviornment variables.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: envar-demo
  labels:
    purpose: demonstrate-envars
spec:
  containers:
  - name: envar-demo-container
    image: gcr.io/google-samples/node-hello:1.0
    env:
    - name: DEMO_GREETING
      value: "Hello from the environment"
    - name: DEMO_FAREWELL
      value: "Such a sweet sorrow"
```

source: [kubernetes.io](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container)
## See Also

- [[Kubernetes YAML Snippets\|Kubernetes YAML Snippets]]