# kustomize-bases

[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](code_of_conduct.md)

A repository of shared Kustomize bases, components, and examples.

## Purpose

This repo contains reusable Kustomize resources which can simplify deploying common Kubernetes infrastructure components. The resources have been designed to be flexible and patched/ overridden based on environment needs.

## Contents

- [namespace](resources/namespace/README.md)
Limits CPU, memory, and storage usage for namespaces.

- [external-secret-store](resources/external-secret-store/aws/README.md)
Sets up the infrastructure for externally managing secrets via AWS Secrets Manager.

- [registry-docker-hub](external-secret/registry-docker-hub/README.md)
Enables pods to access the Docker Hub registry through dynamically generated credentials.

- [example org commonAnnotations](components/metadata/org/example/README.md)
Defines common annotations useful for tagging and identifying resources. Intended as a template to be modified and overridden.

## Usage

Import the bases/components you need into your own Kustomize configs and overlays, patching any UNDEFINED values as described in the respective READMEs.

For example, to limit resource usage and enable Docker Hub access in a namespace called example-ns:

```
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
bases:
- https://github.com/OpenGov/kustomize-bases/tree/vX.Y.Z/limit-range
- https://github.com/OpenGov/kustomize-bases/tree/vX.Y.Z/registry-docker-hub
namespace: example-ns
resources:
- deployment.yaml
- service.yaml
```

## Support

Feel free to contact us for any issues or questions regarding these shared Kustomize resources. We're happy to help you get started utilizing them for your Kubernetes projects!

We do not provide long-term support for directly using resources from this repo without modification. Resources are designed as templates to be customized based on your unique environment and needs.

## License

This project is licensed under the Apache 2.0 License - see the LICENSE file for details

## Proprietary Information

Resources in this repository are designed to simplify deploying common, open source Kubernetes components. Do not commit any proprietary technology, credentials, or other sensitive artifacts.
