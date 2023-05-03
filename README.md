# kustomize-bases

[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](code_of_conduct.md)

A repository of shared Kustomize bases, components, and examples.

## Purpose

This repo contains reusable Kustomize resources which can simplify deploying common Kubernetes infrastructure components. The resources have been designed to be flexible and patched/ overridden based on environment needs.

## Contents

- [components/](components/)
Components that can be used to inject additional functionality into your configuration.

- [examples/](examples/)
Examples of how you might use the bases in this repository in your own projects.

- [resources/namespace](resources/namespace/)
Provides a base for building a namespace.

- [resources/network](resources/network/)
Bases for k8s network resources like Ingress and Services.

- [resources/workload](resources/network/)
Bases for k8s workload resources like Deployments, Jobs, and StatefulSets

## Usage

Import the bases/components you need into your own Kustomize configs and overlays, patching any UNDEFINED values as described in the respective READMEs.

For example, to setup a namespace that limits resource usage and enable Docker Hub access in a namespace called example-ns:

```
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
bases:
- https://github.com/OpenGov/kustomize-bases//resources/namespace?ref=v1.2.3
- https://github.com/OpenGov/kustomize-bases//resources/external-secret/docker-hub?ref=v1.2.3
namespace: example-ns
resources:
- deployment.yaml
- service.yaml
```

## Support

Feel free to contact us for any issues or questions regarding these shared Kustomize resources. We're happy to help you get started utilizing them for your Kubernetes projects!

However, we do not provide direct support for using resources from this repo. Resources are designed as templates to be customized based on your unique environment and needs. You assume all risks and liability that may result from using these configurations. More details can be found in the [LICENSE](LICENSE) file.

## License

This project is licensed under the Apache 2.0 License - see the [LICENSE](LICENSE) file for details

## Proprietary Information

Resources in this repository are designed to simplify deploying common, open source Kubernetes components. Do not commit any proprietary technology, credentials, or other sensitive artifacts.
