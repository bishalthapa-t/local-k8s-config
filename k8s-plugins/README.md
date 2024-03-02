#### Order of installation 
• argo-cd

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

• argo-rollout

```
kubectl -n argo-rollout apply -f argo-rollout
```

