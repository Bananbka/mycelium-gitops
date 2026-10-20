# mycelium-gitops

Desired state of the clone-factory deployment on minikube; Argo CD applies it.

```
bootstrap/root.yaml        App of Apps, the only object applied by hand
argocd-apps/clone-factory.yaml Application for the chart (auto-sync)
charts/clone-factory/          Helm chart from lab 4
  values-minikube.yaml         image tags and cluster-specific values
```

Release flow: edit the image tag in `charts/clone-factory/values-minikube.yaml`,
commit, push. Argo CD syncs. Credentials are never in Git: the chart reads an
existing Secret `clone-factory-secret` created once with `kubectl create secret`.
