# <div align="center"> Creating-EKS-Cluster </div>

![image](https://github.com/user-attachments/assets/df6ce78b-ce8f-4741-be22-abf5a66d8228)

**EKS Cluster**: Amazon Elastic Kubernetes Service (Amazon EKS) is a managed service that eliminates the need to install, operate, and maintain your own Kubernetes control plane on Amazon Web Services (AWS).
Kubernetes is an open-source system that automates the management, scaling, and deployment of containerized applications.

## Step 1 : Log in to your AWS account.

![image](https://github.com/user-attachments/assets/a49b0435-07bc-4549-858e-86c803898294)

## Step 2 : In the search bar, type “EKS” and press Enter.

![image](https://github.com/user-attachments/assets/0f5c393b-05c5-494a-9cee-9591aae4c208)

## Step 3: Now Click on “Clusters”

![image](https://github.com/user-attachments/assets/ffeb3653-a052-43d5-85e2-53becf5e5067)

## Step 4: Click the ‘Create cluster’ button. After clicking, you’ll see the following screen.
Simply fill in the details according to your requirements. As an example, I’ve provided the cluster name as ‘my-eks-cluster’ and click on ‘Next’

![image](https://github.com/user-attachments/assets/33145209-466a-4d29-9403-88b329388265)

## Step 5: After clicking the ‘Next’ button, the following screen will appear. Here, you need to select your required options such as VPC, Subnets, cluster IP address family, and cluster endpoint access according to your needs and click on ‘Next” button.
For reference, you can take a look at the screenshot image below.”

![image](https://github.com/user-attachments/assets/1649306b-7499-42da-8380-525ac557103e)

## Step 6: After clicking the ‘Next’ button, the following screen will appear. Here, you have the option to either ignore or set up login options.
Since I currently don’t have any specific requirements, I’m skipping this step and clicking on the ‘Next’ button. For reference, you can take a look at the screenshot image below.

![image](https://github.com/user-attachments/assets/6d7dd531-4f6a-47be-9293-886207fa3bda)

![image](https://github.com/user-attachments/assets/26bb2b8c-7d13-4dba-b7ad-412213e65ab9)

## Step 7: After click “next” following screen will appear for “Configure selected add-ons settings” choose according to your requiremnt as of now i am setting defaults everything.

![image](https://github.com/user-attachments/assets/8fff669a-ac7e-4472-a436-5587351d0ab5)

## Step 8: Now, simply click ‘Next’ and the following screen will appear for review. Check to ensure everything is correct.
If any changes are needed, you can modify them here after selecting the desired options. For now, I’m proceeding by clicking ‘Create’.

![image](https://github.com/user-attachments/assets/63c72c81-5a06-4220-b5d0-5889fd16fcf9)

## Step 9: After clicking the ‘Create’ button, you’ll see the following screen, and it will take approximately 10 to 20 minutes to create the cluster.

![image](https://github.com/user-attachments/assets/cdfc0cd7-563b-4e8d-a7cb-8fcaad548777)

**Now, the second phase involves creating a node group. Please note that you cannot create the node group before creating the cluster.**

## Step 10: After your cluster is ready, simply click on the ‘Compute’ tab.

![image](https://github.com/user-attachments/assets/0b8e390c-0560-4189-b5a4-f8974819376c)

## Step 11: Now, scroll down and select the ‘Add Node Group’ option.”

![image](https://github.com/user-attachments/assets/407463f2-acd9-4503-ab73-a64075456aac)

## Step 12: After selecting the ‘Node Group’ the following screen will appear. Here, you should provide a name for the node group and specify the Node IAM policy.
I’ve already provided the name as ‘my-node-group’ and the IAM policy as ‘my-eks-node-group-policy’ After completing this step, simply click on the ‘Next’ button

![image](https://github.com/user-attachments/assets/6ca873bd-160c-49dd-8601-43767114de92)

## Step 13: After clicking ‘Next’ the following screen will appear, and you should choose the options according to your requirements. I’ve already made selections, as shown in the image below, for your reference.

![image](https://github.com/user-attachments/assets/9bc85c0d-9896-4ab6-bbc9-a01281549131)

## Step 14: Now click on “Next” following screen will appear.

![image](https://github.com/user-attachments/assets/365747d2-dece-4bbb-9a59-1a9ecd7395d6)

## Step 15: Now, click ‘Next’ It will display a review interface. If there’s anything you’d like to change, you can make adjustments.
If you’re satisfied with the settings, click the ‘Create’ button to proceed and create the node group. For reference, you can view a snapshot of the review screen below

![image](https://github.com/user-attachments/assets/7462badf-290e-4ca6-9faf-5fee8757bd51)

Simply click ‘Create,’ and you’re all set. The node group will take a few minutes to become operational. Once it’s up and running, you’re ready to use it.
You’ve successfully created the cluster and node group. Now, if you’re wondering how to access your EKS cluster, don’t worry; it’s quite straightforward.

## Steps:
1.Open Your Terminal: If you’re using macOS or Linux, open your terminal. If you’re a Windows user, open your command prompt (CMD).<br>
2.Install Necessary Tools: Install the necessary tools such as AWS CLI and kubectl.<br>
3.Configure AWS: Configure your AWS credentials.<br>
4.After Configuring AWS Credentials: Once you’ve configured your AWS credentials, proceed with the following command.<br>

```
aws eks update-kubeconfig --name <my-eks-cluster-name>
```
