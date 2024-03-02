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
