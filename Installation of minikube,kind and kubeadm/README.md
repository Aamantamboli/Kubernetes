# Installation of Minikube, KIND, and Kubeadm

This guide provides step-by-step instructions for installing **Minikube**, **KIND**, and **Kubeadm** on a Linux system. These tools are useful for setting up Kubernetes clusters locally and on virtualized environments.

---

## MINIKUBE INSTALLATION

Minikube is a tool that runs a single-node Kubernetes cluster locally on your machine, primarily used for development and testing purposes.

![image](https://github.com/user-attachments/assets/7367c720-d6d3-4a6e-904b-2469f2fea24d)

### Step 1: Update the package
```bash
sudo apt update -y  
```

### Step 2: Install and configure Docker
```bash
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER && newgrp docker
```

### Step 3: Download, make executable, and move Minikube binary
```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube
sudo mv minikube /usr/local/bin/
```

### Step 4: Download and convert the GPG key
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

### Step 5: Add the Kubernetes APT repository
```bash
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

### Step 6: Update the package list again
```bash
sudo apt-get update
```

### Step 7: Install kubectl
```bash
sudo apt-get install kubectl
```

### Step 8: Start Minikube Kubernetes cluster using Docker as the driver
```bash
minikube start --driver=docker
```

### Step 9: List the nodes in the Kubernetes cluster
```bash
kubectl get nodes 
```

#### Successfully created Minikube Cluster

![image](https://github.com/user-attachments/assets/d4b48e26-1f30-4c53-9206-8d841e0ce81b)

---

## KIND INSTALLATION

KIND (Kubernetes IN Docker) is a tool for running Kubernetes clusters in Docker containers, making it easy to spin up clusters quickly.

<img src="https://github.com/user-attachments/assets/e927f95a-23d6-432e-8837-6ff63ecbd635" width="200" height="130"/>

### Step 1: Update the package
```bash
sudo apt update -y  
```

### Step 2: Install Docker
```bash
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```

### Step 3: Download the KIND binary
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.18.0/kind-linux-amd64 
```

### Step 4: Make the KIND binary executable
```bash
chmod +x ./kind
```

### Step 5: Move the KIND binary to a directory included in your system’s PATH
```bash
sudo mv ./kind /usr/local/bin/
```

### Step 6: Create a local Kubernetes cluster using KIND
```bash
kind create cluster
```

#### Successfully created KIND Cluster

![image](https://github.com/user-attachments/assets/061e6d7f-f9f5-4935-8ec4-7a68063d8bf5)

---

## KUBEADM INSTALLATION

Kubeadm is a tool that helps you set up a Kubernetes cluster on your own infrastructure. It’s more hands-on and offers greater flexibility compared to Minikube and KIND.

![image](https://github.com/user-attachments/assets/b853e56f-2574-44f8-bf3b-e11f5af51d34)

### Step 1: Disable swap space
```bash
sudo swapoff -a
```

### Step 2: Modify `/etc/fstab` to prevent swap space re-enabling on the next boot
```bash
sudo sed -i '/ swap / s/^/#/' /etc/fstab
```

### Step 3: Configure the Linux kernel for Kubernetes
```bash
sudo modprobe overlay
sudo modprobe br_netfilter
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1
EOF
sudo sysctl --system
```

### Step 4: Install Docker
```bash
sudo apt-get update
sudo apt-get install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
```

### Step 5: Install Kubernetes tools (kubelet, kubeadm, kubectl)
```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

### Step 6: Update the package list
```bash
sudo apt-get update
```

### Step 7: Install essential packages for HTTPS handling
```bash
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
```

### Step 8: Import the Kubernetes APT GPG key
```bash
sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

### Step 9: Add the Kubernetes APT repository
```bash
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

### Step 10: Install kubelet, kubeadm, kubectl
```bash
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

### Step 11: Enable and start the kubelet service
```bash
sudo systemctl enable --now kubelet
```

### Step 12: Initialize the Kubernetes cluster using kubeadm
```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

### Step 13: Set up kubeconfig
```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### Step 14: Deploy Calico network plugin for Kubernetes
```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

### Step 15: Generate join command for worker nodes
```bash
kubeadm token create --print-join-command
```

### Step 16: Join worker node to the cluster
```bash
sudo kubeadm join <master-node-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

### Step 17: List all nodes in the Kubernetes cluster
```bash
kubectl get nodes
```

#### Successfully created Kubeadm Cluster

![image](https://github.com/user-attachments/assets/ec67f11b-96e0-4f69-b339-a3d6612e9b54)

---

## Conclusion

You have successfully installed **Minikube**, **KIND**, and **Kubeadm** on your system. Each of these tools is suitable for different use cases:

- **Minikube**: Ideal for local Kubernetes clusters and testing.
- **KIND**: Perfect for testing Kubernetes clusters in Docker containers.
- **Kubeadm**: Best for setting up Kubernetes clusters on physical or virtual machines.

For more details on each tool, refer to their official documentation:
- [Minikube](https://minikube.sigs.k8s.io/docs/)
- [KIND](https://kind.sigs.k8s.io/)
- [Kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/)
