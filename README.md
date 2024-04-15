# ArgoCDExample
## Install ArgoCD with repository
1. Prepare repository of the application in github:
created service.yaml, deployment.yaml files
2. install argoCD from the [internet](https://argo-cd.readthedocs.io/en/stable/getting_started/).
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
```
free -h # check free mem space on WSL
kubectl get svc -n argocd # get services running in argocd namespace
kubectl port-forward -n argocd svc/argocd-server 8080:443 # forward ports locally
```
3. Login as default user admin. The password in secrets argocd-initial-admin-secret
```
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
echo TXZhOGRIaWI3WTVnLXlyRg== | base64 --decode
```
## Configure ArgoCD
1. create application.yaml and make sure that it corresponds to [documentation](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)
2. create namespace 'myapp' in k8s
3. ArgoCD doesn't know anything about our repository so to apply configuration do:
```
kubectl apply -f application.yaml
```
4. See synced project in 127.0.0.1:8080 you can find it.

## Test automatic sync
change deployment.yaml