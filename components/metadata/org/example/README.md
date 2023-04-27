# example org commonAnnotations

A Kustomize component defining common annotations useful for tagging and identifying Kubernetes resources.

## Purpose

This component provides example commonAnnotations that can be applied to Kubernetes resources. Common annotations help enable additional monitoring, cost control, and resource management.

## Usage

This component is intended as an example and template. Users should copy this file and modify all values based on their environment and needs rather than directly using this component.

To apply common annotations to resources:

1. Create the commonAnnotations component

```
apiVersion: kustomize.config.k8s.io/v1alpha1  # <-- Component notation
kind: Component
commonAnnotations:
  team: example
  department: ops
  suite: platform
  customer: internal
```

2. Reference the component in your Kustomize overlay or config under the components key. For example:

```
apiVersion: kustomize.config.k8s.io/v1alpha1
kind: Component
namePrefix: example-env-
components:
- commonAnnotations
resources:
- deployment.yaml
- service.yaml
```

## Details

The included commonAnnotations configure resources with metadata as follows:

- team: example  (modify/ remove)
- department: rnd  (modify/remove)
- suite: platform  (modify/remove)
- customer: internal  (modify/remove)

These values are examples only. They should be overridden by the environment actually utilizing this component.

## Support

Feel free to contact us for any issues or questions regarding this component. We're happy to help you utilize it as a starting point for your Kubernetes projects!
