### - Install K8S cluster [Minikube](https://minikube.sigs.k8s.io/docs/start/)
### - Use minikube cluster 
```
kubectl config use-context minikube
```
### - Point your terminal’s docker-cli to the Docker Engine inside [minikube](https://minikube.sigs.k8s.io/docs/commands/docker-env) (Useful for building docker images directly inside minikube)

```
 eval $(minikube docker-env)
 ```
        
Build the docker image the same terminal and to verify if the image is build inside minikube image registry 

```yaml
minikube image ls --format table
```

The image build should start with `docker.io/library/${new-image}`

### Install [istio](https://istio.io/latest/docs/setup/getting-started/)
After installing `istioctl` run the following to instal istion in the minikube cluster
```
istioctl install
```


### - To enable terminal in [web terminal](https://argo-cd.readthedocs.io/en/stable/operator-manual/web_based_terminal/#enabling-the-terminal) in argorollout

Edit configmap `kubectl edit configmap argocd-cm -n argocd` and add 
```
data:
 exec.enabled: "true"
```

Patch the argocd-server Role `kubectl edit roles.rbac.authorization.k8s.io -n argocd argocd-server`
```
  resources:
  - pods/exec
```

### For DNS routing use `nginx` in the host and `/etc/hosts` (MacOS)
Example: [Mapping Hostnames with Ports](https://www.baeldung.com/linux/mapping-hostnames-ports)

