# registry-docker-hub

A Kustomize base to configure imagePullSecrets referencing the Docker Hub registry credentials.  This base is hosted remotely at  <https://github.com/OpenGov/kustomize-bases/tree/vX.Y.Z/resources/external-secret-store/aws>

## Purpose

This base enables Kubernetes pods to access the Docker Hub registry (index.docker.io) for pulling container images without hardcoded credentials. It creates an ExternalSecret resource to dynamically generate and manage the registry's authentication token.

## Usage

Import this Kustomize base into an overlay or standalone Kustomize config to make the Docker Hub credentials available to pods as imagePullSecrets. Then, patch any deployments using this base to incorporate the generated imagePullSecret.

For example:

```
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
bases:
- https://github.com/OpenGov/kustomize-bases/tree/vX.Y.Z/resources/external-secret-store/aws
resources:
- deployment.yaml
- service.yaml
```

Be sure to specify the SemVer tag (vX.Y.Z) for the version of this remote base you want to use.  Any UNDEFINED values should be patched via the overlay Kustomize config.

This will generate a Docker Hub imagePullSecret which must be manually added to deployment resources for pods to utilize it.

## Details

The included ExternalSecret resource configures the Docker Hub registry credentials as follows:

- Name: registry-docker-hub
- Namespace: UNDEFINED (Deployment namespace, patch via overlay)
- Stored externally in a secret-store of kind ClusterSecretStore
- Template to generate the Secret contains Docker config JSON with Docker Hub credentials
- Creation Policy set to "Owner" to allow pruning of unused/unreferenced secrets

No hardcoded credentials are stored in this remote Kustomize base. The credentials are managed externally by the External Secrets Operator and refreshed automatically according to the spec.refreshInterval.

## Support

Feel free to contact us for any issues or questions regarding this remote Kustomize base. We're happy to help you utilize it for your Kubernetes projects!
