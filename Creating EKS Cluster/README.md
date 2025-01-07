# Creating an EKS Cluster on AWS

Amazon Elastic Kubernetes Service (EKS) is a managed service that simplifies the setup, operation, and scaling of Kubernetes clusters. EKS allows you to run Kubernetes workloads on AWS without the need to manage your own Kubernetes control plane.

This guide walks you through the steps of creating an EKS cluster, setting up node groups, and accessing the cluster using the necessary AWS tools.

## Prerequisites

- An active **AWS account**.
- IAM permissions to create and manage EKS clusters and related resources.
- Installed **AWS CLI** and **kubectl** on your local machine.
- Configured AWS CLI with your credentials using the command: `aws configure`.

---

## Step 1: Log in to Your AWS Account

1. Navigate to the [AWS Management Console](https://aws.amazon.com/console/).
2. Sign in using your AWS credentials.

![image](https://github.com/user-attachments/assets/0e72b6ea-05f9-496e-aa62-2b07f46f2492)

---

## Step 2: Search for "EKS"

1. In the AWS Management Console search bar, type `EKS` and press Enter.
2. Select **Elastic Kubernetes Service (EKS)** from the results.

![image](https://github.com/user-attachments/assets/a64a359a-9918-42a0-9d4d-d4d4f507ad09)

---

## Step 3: Click on "Clusters"

1. From the left sidebar, select **Clusters**.

![image](https://github.com/user-attachments/assets/65289c01-686f-4418-8ac1-bab7a1af0087)

---

## Step 4: Create a Cluster

1. Click on the **Create cluster** button.
2. Fill in the required cluster details, such as the **Cluster name**. For example, name the cluster `my-eks-cluster`.
3. Click **Next**.

![image](https://github.com/user-attachments/assets/5104ffcf-210d-4da2-9420-e0d247a9bf60)

---

## Step 5: Configure Cluster Settings

1. Choose your VPC, Subnets, Cluster IP Address Family, and Cluster Endpoint Access according to your requirements.
2. Once you've made your selections, click **Next**.

![image](https://github.com/user-attachments/assets/df83dccd-f564-4bd4-8a9e-373a8ee6c793)

---

## Step 6: Set Up Logging Options

1. This step allows you to configure the login options. You can either skip this step or configure it based on your requirements.
2. Once done, click **Next**.

![image](https://github.com/user-attachments/assets/135e461a-94a3-4d05-a335-1964d9b79b4a)
![image](https://github.com/user-attachments/assets/3dfa1cde-d2f2-4bc7-8f01-f255a1bd11b4)

---

## Step 7: Configure Add-Ons

1. In the **Configure selected add-ons settings** section, set up any necessary add-ons as per your requirements. For now, you can proceed with the default settings.
2. Click **Next**.

![image](https://github.com/user-attachments/assets/9ce7bb05-768f-4500-aa30-20bae38b3bd9)

---

## Step 8: Review Cluster Configuration

1. Review your cluster configuration to ensure everything is set up as needed.
2. If everything looks good, click **Create** to proceed.

![image](https://github.com/user-attachments/assets/e373bfad-4012-46d5-a38c-254dc65c051e)

---

## Step 9: Wait for Cluster Creation

1. After clicking **Create**, it will take approximately **10 to 20 minutes** to create your cluster.
2. Once the cluster is created, you’ll see a confirmation message.

![image](https://github.com/user-attachments/assets/9752d1cc-0bbd-49eb-bf5e-bc64e93c84c9)

---

## Step 10: Create a Node Group

1. After your cluster is created, go to the **Compute** tab.
2. Click **Add Node Group** to start creating the node group for your EKS cluster.

![image](https://github.com/user-attachments/assets/ad432c73-c312-4fb3-ab88-f1ca8818a3c6)

---

## Step 11: Configure Node Group

1. Under **Node Group details**, provide a name for your node group (e.g., `my-node-group`).
2. Choose the **Node IAM policy** for your group (e.g., `my-eks-node-group-policy`).
3. Click **Next**.

![image](https://github.com/user-attachments/assets/116ce2c8-8ff7-41b4-8579-24d65496504d)

---

## Step 12: Choose Node Group Options

1. On the next screen, select the desired configuration for your node group, such as instance types, desired node count, and scaling options.
2. After making your selections, click **Next**.

![image](https://github.com/user-attachments/assets/a191bd66-ef74-4e29-b66d-48719e3ce757)

---

## Step 13: Review Node Group Configuration

1. Review the node group settings and ensure everything is correct.
2. If satisfied, click **Create** to create the node group.

![image](https://github.com/user-attachments/assets/9b1318c5-d1f3-4193-8bbb-47159978b65a)

---

## Step 14: Wait for Node Group Creation

1. The node group will take a few minutes to become operational.
2. Once the node group is ready, you’ll see the status change to **Active**.

---

## Step 15: Access Your EKS Cluster

1. **Open your terminal**:
   - On **macOS/Linux**, open your terminal.
   - On **Windows**, open **Command Prompt** or **PowerShell**.

2. **Install the necessary tools**:
   - Ensure you have **AWS CLI** and **kubectl** installed.
   - If not, install them using the official AWS and Kubernetes documentation.

3. **Configure your AWS credentials** using the command:
   ```bash
   aws configure
   ```

4. **Update your kubeconfig** for your EKS cluster:
   ```bash
   aws eks update-kubeconfig --name my-eks-cluster
   ```

5. Now you can use `kubectl` to interact with your cluster. Verify your connection by running:
   ```bash
   kubectl get svc
   ```

---

## Conclusion

You’ve successfully created an EKS cluster and node group. You can now deploy and manage your containerized applications on Kubernetes using Amazon EKS.

For further resources and documentation, visit the [AWS EKS Documentation](https://docs.aws.amazon.com/eks/latest/userguide/).
