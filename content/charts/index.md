---
title: "charts"
date: 2024-08-11T15:38:15+09:00
lastmod: 2024-08-11T15:35:33+09:00
slug: ""
description: "Index page for helm chart repoistory"
keywords: []
tags: ["helm", "chart"]
showAdvertisement: false
---

## Summary

Helm chart repository hosted on [younsl.github.io](https://github.com/younsl/younsl.github.io).

## Usage

Add the helm chart repository with the name `younsl`.

```bash
helm version  # If you don't have helm installed, install first
helm repo add younsl https://younsl.github.io
helm repo update
```

Search all helm charts in the `younsl` chart repository.

```bash
helm search repo younsl
```

The `helm search repo` command checks the status of the charts based on the `index.yaml` file in the helm chart repository.

The `index.yaml` file contains the metadata of the repository and is used for chart search and installation. Check [index file](https://github.com/younsl/younsl.github.io/blob/main/static/index.yaml) directly.

## Available charts

| Chart name | Status | Chart version |
| ---------- | ------ | ------------- |
| [**actions-runner**][actions-runner] | Active | 0.1.3 |
| [**argocd-apps**][argocd-apps] | Active | 1.6.1 |
| [**backup-utils**][backup-utils] | Active | 0.3.2 |
| [**karpenter-nodepool**][karpenter-nodepool] | Active | 0.1.1 |
| [**rbac**][rbac] | Active | 0.2.0 |

[actions-runner]: https://github.com/younsl/younsl.github.io/tree/main/content/charts/actions-runner
[argocd-apps]: https://github.com/younsl/younsl.github.io/tree/main/content/charts/argocd-apps
[backup-utils]: https://github.com/younsl/younsl.github.io/tree/main/content/charts/backup-utils
[karpenter-nodepool]: https://github.com/younsl/younsl.github.io/tree/main/content/charts/karpenter-nodepool
[rbac]: https://github.com/younsl/younsl.github.io/tree/main/content/charts/rbac
