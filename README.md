# kubernetes_lab_gitops

How to bootstrap K8s cluster.

1) Get Helm installed
2) Add the repos to helm list
```
helm repo add fluxcd https://charts.fluxcd.io
```
3) install Flux using helm. https://hub.helm.sh/charts/fluxcd/flux
```
4) kubectl create secret generic flux-git-auth --namespace flux --from-literal=GIT_AUTHUSER=<username> --from-literal=GIT_AUTHKEY=<token>
```
ex for using HTTPS:
```
helm upgrade -i flux fluxcd/flux \
--set git.url='https://$(GIT_AUTHUSER):$(GIT_AUTHKEY)@github.com/dilerous/kubernetes_lab_gitops
--set env.secretName=flux-git-auth \
--namespace flux
--set additionalArgs={--sync-garbage-collection}
```
5) Install Flux operator
```
kubectl apply -f https://raw.githubusercontent.com/fluxcd/helm-operator/1.2.0/deploy/crds.yaml

helm upgrade -i helm-operator fluxcd/helm-operator --wait \
--namespace flux \
--set helm.versions=v3
```
Temporary: How to install metallb
https://davidstamen.com/deploying-tkg-on-vsphere/
