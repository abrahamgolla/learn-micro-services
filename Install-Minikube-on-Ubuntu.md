## Step 1

### 1. Install Kubectl

curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl


### 2. Make the kubectl binary executable.
sudo chmod +x ./kubectl

### 3. Move the binary in to your PATH.
sudo mv ./kubectl /usr/local/bin/kubectl

### 4. Test to ensure the version you installed is up-to-date:
kubectl version

### 5. sudo curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && sudo chmod +x minikube
  
### 6. Here’s an easy way to add the Minikube executable to your path:
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/

### 7. Confirm Installation
minikube start --vm-driver=none

### 8. minikube status

### 9. To Stop
minikube stop

### 10. To delete
minikube delete

## To set Proxy
https://minikube.sigs.k8s.io/docs/reference/networking/proxy/

## To Completely Remove minikube
sudo minikube stop; sudo minikube delete &&
docker stop $(docker ps -aq) &&
docker system prune -f --volumes &&
sudo rm -rf ~/.kube ~/.minikube &&
sudo rm -rf /usr/local/bin/localkube /usr/local/bin/minikube &&
sudo systemctl stop '*kubelet*.mount' &&
sudo systemctl stop localkube.service &&
sudo systemctl disable localkube.service &&
sudo rm -rf /etc/kubernetes/
