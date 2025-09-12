# argocd-tutorial

## Install argocd custom resource definition

* helm repo add argo https://argoproj.github.io/argo-helm
* kubectl create namespace argocd
* helm install argocd -n argocd argo/argo-cd
* kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
* kubectl port-forward service/argocd-server -n argocd 8081:443
* kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/kind/deploy.yaml

## Github tutorial
https://github.com/sergioacortes/argocd-tutorial.git

# ArgoCD UI access
kubectl port-forward service/argocd-server -n argocd 8081:443 --address="0.0.0.0"


# helm package
helm pull oci://ghcr.io/sergioacortes/charts/dockerwalkthrough:0.4.0-rev.1