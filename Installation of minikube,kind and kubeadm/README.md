# Installation-of-minikube-kind-and-kubeadm
## MINIKUBE INSTALLATION

![image](https://github.com/user-attachments/assets/0a1a68ec-a8cb-4bbf-aa75-6702cd5314ce)

## Step 1: Update the package
```
sudo apt update -y  
```
## Step 2:  Install and configure Docker
```
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER && newgrp docker
```
## Step 3: These commands are used to download, make executable, and move the Minikube binary to a directory in your system's PATH
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube
sudo mv minikube /usr/local/bin/
```
## Step 4: Download and convert the GPG key
```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```
## Step 5: Add the Kubernetes APT repository
```
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
## Step 6: Again update the package
```
sudo apt-get update
```
## Step 7: To install the kubectl package
```
sudo apt-get install kubectl
```
## Step 8: To start a Minikube Kubernetes cluster using Docker as the virtualization driver
```
minikube start --driver=docker
```
## Step 9: To list the nodes in a Kubernetes cluster
```
kubectl get nodes 
```
## Successfully created Minikube Cluster

![Screenshot 2024-09-12 222219](https://github.com/user-attachments/assets/1e912ab8-bf58-41e5-b222-64d46406238d)


## KIND INSTALLATION

<img src="https://miro.medium.com/v2/resize:fit:985/1*nzCO38pyKTeYN2Z-Ydh29A.png" width="200" height="130"/>

## Step 1: Update the package
```
sudo apt update -y  
```
## Step 2:  Install Docker
```
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```
## Step 3: This command is used to download the kind binary
```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.18.0/kind-linux-amd64 
```
## Step 4: This command is used to change the permissions of the kind file to make it executable
```
chmod +x ./kind
```
## Step 5: This command is used to move the kind binary to a directory that is included in your system’s PATH
```
sudo mv ./kind /usr/local/bin/
```
## Step 6: This command is used to create a local Kubernetes cluster using Kind
```
kind create cluster
```
## Successfully created Kind Cluster

![image](https://github.com/user-attachments/assets/dcf09fca-134a-4037-bc33-79b0d8c616fc)

## KUBEADM INSTALLATION
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQB42T870ZRRrTvho1YOkwYSaSZO9pwWZDnSQ&s" width="150" height="130"/>

## Step 1: This command disables all swap space immediately
```
sudo swapoff -a
```
## Step 2: This command modifies the /etc/fstab file to ensure that swap space is not re-enabled automatically on the next system boot
```
sudo sed -i '/ swap / s/^/#/' /etc/fstab
```
## Step 3: These commands configure the Linux kernel for Kubernetes by loading necessary modules and setting network parameters to enable proper packet filtering and IP forwarding for container networking.
```
sudo modprobe overlay
sudo modprobe br_netfilter
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1
EOF
sudo sysctl --system
```
## Step 4: These commands update the package list, install Docker, and ensure the Docker service is enabled and started on the system.
```
sudo apt-get update
sudo apt-get install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
```
## Step 5: These commands install Kubernetes tools by adding the necessary repository, importing the GPG key, updating the package list, and installing kubelet, kubeadm, and kubectl, while preventing them from being upgraded.
```
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```
## Step 6: Update the package
```
sudo apt-get update
```
## Step 7: This command installs essential packages to enable APT to handle HTTPS sources and manage certificates, along with the curl utility for transferring data.
```
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
```
## Step 8: This command creates a directory for APT keyrings and imports the Kubernetes APT repository GPG key, saving it in the specified keyring format for secure package management.
```
sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```
## Step 9: This command adds the Kubernetes APT repository to the system's sources list, specifying the GPG key for package verification.
```
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
## Step 10: These commands update the package list, install kubelet, kubeadm, and kubectl, and prevent these packages from being automatically upgraded.
```
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```
## Step 11: This command enables the kubelet service to start at boot and immediately starts the service.
```
sudo systemctl enable --now kubelet
```
## Step 12: This command initializes a Kubernetes cluster with kubeadm, setting the pod network CIDR to 192.168.0.0/16 for network configuration.
```
  sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```
## Step 13: These commands create a directory for Kubernetes configuration, copy the admin configuration file to the user's kube directory, and change the ownership to the current user for access.
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
## Step 14: This command deploys the Calico network plugin for Kubernetes by applying its manifest file from the provided URL.
```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```
## Step 15: This command generates a join command for adding worker nodes to the Kubernetes cluster, displaying the necessary token and parameters.
```
kubeadm token create --print-join-command
```
## Step 16: This command allows a worker node to join a Kubernetes cluster, specifying the master node's IP, the token for authentication, and the CA certificate hash for secure communication.
```
sudo kubeadm join <master-node-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```
## Step 17: This command lists all nodes in the Kubernetes cluster along with their status and roles.
```
kubectl get nodes
```
**Successfully created Kubeadm Cluster**

![image](https://github.com/user-attachments/assets/221b02d2-0d9d-4701-9505-bcb358eca8ec)
