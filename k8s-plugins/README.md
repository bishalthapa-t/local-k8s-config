## Order of installation 

#### 1) argo-cd

```
kubectl create namsepace argocd
kubectl -n argocd apply -f argocd 
```

- Change the argocd-server service type to LoadBalancer and start port forwarding
```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
- Command to reterieve argocd password:
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

- Install [argocd](https://argo-cd.readthedocs.io/en/stable/cli_installation) command
```
brew install argocd
```

- Login to argocd in command line
```
argopass=$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)
argocd login localhost:8080 --insecure --username=admin --password=$argopass
```

- Example to add github repository that is reachable with ssh private key
> Make sure to login to argcd in command line before executing this commmand
```
argocd repo add git@github.com:bishalthapa-t/local-k8s-config.git --ssh-private-key-path ~/.ssh/id_ed25519
```
> Argocd [doesn't support](https://github.com/argoproj/argo-cd/issues/1894) passpharase private ssh key.  Create new temporary ssh private key and integrate it with github and use it argocd. To verify if argocd can connect to private github repo run the command `argocd repo list`.


#### 2) [argo-rollout](https://argoproj.github.io/argo-rollouts/installation/)

```
kubectl create namsepace argo-rollouts
kubectl apply -n argo-rollouts -f argo-rollouts
```
