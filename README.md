# argocd-tutorial

## Install argocd custom resource definition

* helm repo add argo https://argoproj.github.io/argo-helm
* kubectl create namespace argocd
* helm install argocd -n argocd argo/argo-cd
* kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
* kubectl port-forward service/argocd-server -n argocd 8091:443
* kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/kind/deploy.yaml


## Create private docker registry credentials on kubernetes cluster

The configuration to pull images from private container registry is made through kubernates. You can find how to pull images from private registry on the official kubernetes documentation.

* [How to pull image from private registry](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)
* [Configure through service account](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#add-imagepullsecrets-to-a-service-account)

The following code shows how to create a definition file with the private registry credentials
```
kubectl create secret docker-registry ghcr-credentials --docker-server=ghcr.io --docker-username=sergioacortes --docker-password=<your-password> --docker-email=sergioacortes@msn.com --namespace=dev --dry-run=client -o yaml > ghcr-credentials.yaml
```


## Github tutorial
https://github.com/sergioacortes/argocd-tutorial.git

# ArgoCD UI access
kubectl port-forward service/argocd-server -n argocd 8081:443 --address="0.0.0.0"


# helm - private registry 

To add a helm private registry repository you have to create an argo repository defintion file

```
apiVersion: v1
kind: Secret
metadata:
  name: oci-helm-repository
  namespace: argocd
  labels:
    argocd.argoproj.io/secret-type: repository
stringData:
  name: oci-helm-repository
  url: ghcr.io/sergioacortes/charts
  enableOCI: "true"
  type: helm
  username: "sergioacortes"
  password: "<PAT>"
  ForceHttpBasicAuth: "true"
```

## Manually pull image from a private oci registry

Helm login 
```
echo "PAT" | helm registry login ghcr.io --username <user-name> --password-stdin
```

Helm pull
```
helm pull oci://ghcr.io/sergioacortes/charts/dockerwalkthrough:0.4.0-rev.1
```
