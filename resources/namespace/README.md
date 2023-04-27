# namespace

A Kustomize base containing a LimitRange and Namespace resource.

## Purpose

This base provides a LimitRange resource which enforces quotas on compute resources (CPU, memory, storage) for namespaces using this base. It also includes a Namespace resource with an undefined name, allowing the base to be used to generate namespaces with custom names.
It helps ensure resources are used sustainably and prevents overcommitting across namespaces.

## Usage

Import this Kustomize base into an overlay or standalone Kustomize config to apply quota limits and generate namespaces. Any UNDEFINED values should be patched via the overlay.

For example:

```
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
bases:
- https://github.com/OpenGov/kustomize-bases/tree/vX.Y.Z/resources/limit-range
resources:
- namespace.yaml
```

## Details

The included resources configure quotas and namespaces as follows:

- LimitRange
- Name: cpu-mem-limit-range
- Namespace: UNDEFINED (Deployment namespace, patch via overlay)
- CPU request/limit: 100m/1
- Memory request/limit: 128Mi/256Mi
- Storage limit: 10Gi
- Namespace
- Name: UNDEFINED (patch via overlay)

No hardcoded limit values or namespace names are present in this base. Those values should be patched based on the needs of the environment utilizing this Kustomize base.

## Support

Feel free to contact us for any issues or questions regarding this Kustomize base. We're happy to help you utilize it for your Kubernetes projects!
