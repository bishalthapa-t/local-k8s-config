## Order of installation 

#### argo-cd

```
kubectl -n argocd apply -f argocd 
```

Change the argocd-server service type to LoadBalancer and start port forwarding
```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Command to reterieve argocd password:
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

Install [argocd](https://argo-cd.readthedocs.io/en/stable/cli_installation) command
```
brew install argocd
```

> To add github repository that is reachable with ssh private key
```
argocd repo add git@github.com:bishalthapa-t/local-k8s-config.git --ssh-private-key-path ~/.ssh/id_ed25519
```

#### argo-rollout

```
kubectl -n argo-rollout apply -f argo-rollout
```

