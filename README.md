# k8s-hello-minikube

Prerequisites:
- Mac OSX - https://www.apple.com/mac/
- Homebrew installation - https://brew.sh/
- Docker for Mac - https://www.docker.com/docker-mac

Commands:
- brew cask install minikube
- curl -LO https://storage.googleapis.com/minikube/releases/latest/docker-machine-driver-hyperkit && chmod +x docker-machine-driver-hyperkit && sudo mv docker-machine-driver-hyperkit /usr/local/bin/ && sudo chown root:wheel /usr/local/bin/docker-machine-driver-hyperkit && sudo chmod u+s /usr/local/bin/docker-machine-driver-hyperkit
- minikube start --vm-driver=hyperkit
- brew install kubernetes-cli
- kubectl config use-context minikube
- eval $(minikube docker-env)
- docker build -t hello-node:v1 .
- kubectl run hello-node --image=hello-node:v1 --port=8080 --image-pull-policy=Never
- kubectl expose deployment hello-node --type=LoadBalancer
- minikube service hello-node
- sed -i '' 's/Hello World V1!/Hello World V2!/g' server.js
- docker build -t hello-node:v2 .
- kubectl set image deployment/hello-node hello-node=hello-node:v2
- minikube service hello-node

Clean up:
- kubectl delete service hello-node
- kubectl delete deployment hello-node
- docker rmi hello-node:v1 hello-node:v2 -f
- minikube stop
- eval $(minikube docker-env -u)
- minikube delete

More info: https://kubernetes.io/docs/tutorials/hello-minikube/#create-a-deployment
