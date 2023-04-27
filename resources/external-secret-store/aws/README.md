# secret-store

A Kustomize base containing a SecretStore and ServiceAccount for external secrets.

## Purpose

This base provides the SecretStore and ServiceAccount resources needed to enable the External Secrets Operator in a Kubernetes cluster. The SecretStore defines AWS Secrets Manager as the backend for managing secrets externally, with authentication via a service account.

## Usage

Import this Kustomize base into an overlay or standalone Kustomize config to set up the infrastructure for external secrets. Any UNDEFINED values should be patched via the overlay.

For example:

```
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
bases:
- https://github.com/OpenGov/kustomize-bases/tree/vX.Y.Z/resources/secret-store
resources:
- deployment.yaml
- service.yaml
```

## Details

The included resources configure external secrets as follows:

- SecretStore
- Name: secret-store
- Namespace: UNDEFINED (Deployment namespace, patch via overlay)
- Provider: AWS Secrets Manager
- Region: UNDEFINED (patch via overlay)
- ServiceAccount: secret-store  (used by Secrets Manager to call Secrets API)

No hardcoded AWS region or credentials are present in this base. Those values should be patched based on the environment utilizing this Kustomize base.

## Support

Feel free to contact us for any issues or questions regarding this Kustomize base. We're happy to help you utilize it for your Kubernetes projects!
