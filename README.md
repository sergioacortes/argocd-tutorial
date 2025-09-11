# argocd-tutorial

## Install argocd custom resource definition

1.- helm install argocd -n argocd argo/argo-cd
2.- kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
3.- kubectl port-forward service/argocd-server -n argocd 8081:443


https://github.com/sergioacortes/argocd-tutorial.git

# ArgoCD UI access
kubectl port-forward service/argocd-server -n argocd 8081:443 --address="0.0.0.0"


# helm package
helm pull oci://ghcr.io/sergioacortes/charts/dockerwalkthrough:0.4.0-rev.1