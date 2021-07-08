### Kubernetes sandbox
#### Yet another local Kubernetes
![alt text](https://github.com/spender0/kubernetes-sandbox/raw/master/kubernetes-sandbox.jpg)
 
#### Motivation
For ones who need to understand Kubernetes's complex architecture.

Such tools as minikube or kubeadm encapsulates the complexity.
As a result you get working kubernates without understanding how the things are done.

It is just well-commented code. I believe that well-commented code examples are much better than tons of instructions.

#### Features:
* SSL certificates and requirements with using old good openssl tool
* Fully automated and dockerized, only docker and docker-compose required
* All settings are transparent, you can fully control the cluster
* Bootstrap tokens are enabled and used  https://kubernetes.io/docs/reference/access-authn-authz/bootstrap-tokens
* OpenID Connect Tokens configured using Keycloak https://kubernetes.io/docs/reference/access-authn-authz/authentication/#openid-connect-tokens

#### Requirements:
* Docker https://docs.docker.com/install/
* Docker-compose https://docs.docker.com/compose/install/
* Git https://git-scm.com/downloads

#### Run:

```
git clone https://github.com/spender0/kubernetes-sandbox.git

cd kubernetes-sandbox

docker-compose up -d
```

Install it https://kubernetes.io/docs/tasks/tools/install-kubectl/

and then run:

```
export KUBECONFIG=conf/admin-local.conf

kubectl -n kube-system get pods
``` 

Aslo, you can test OpenID Connect Tokens with Keycloak and precreated k8s-user1 with read-only permissions in k8s:

```
./generate-kubeconfig-with-keycloak-token.sh

export KUBECONFIG=conf/k8s-user1-kubeconfig.conf

#this should be allowed
kubectl get ns

#this should be declined:
kubectl create ns test
```

#### Stop:
```
docker-compose down
```

#### Remove completely:
```
docker-compose down

git clean -f -d
```

#### References
Based on: https://kubernetes.io/docs/reference/

Docker images: https://console.cloud.google.com/gcr/images/google-containers/GLOBAL
