# argocd-tutorial


https://github.com/sergioacortes/argocd-tutorial.git

# ArgoCD UI access
kubectl port-forward service/argocd-server -n argocd 8081:443 --address="0.0.0.0"


# helm package
helm pull oci://ghcr.io/sergioacortes/charts/dockerwalkthrough:0.4.0-rev.1