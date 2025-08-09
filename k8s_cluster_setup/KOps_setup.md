# 🚀 Kubernetes Production Cluster Setup Using KOps

KOps (Kubernetes Operations) is a production-ready tool for creating, managing, and maintaining Kubernetes clusters—primarily on AWS. It automates infrastructure provisioning, DNS integration, state storage, and node lifecycle management.

### 🧰 1️⃣ Prerequisites

Before creating the cluster, ensure the following are ready:

### Domain

- A registered domain (e.g., `devops-prod.xyz` via GoDaddy)
- This domain will be used for Kubernetes DNS integration

### EC2 Bootstrap Instance (for running KOps commands only)

| Property       | Value                              |
| -------------- | ---------------------------------- |
| Name           | `kOps`                             |
| Type           | `t2.micro`                         |
| OS             | Ubuntu 24.04 LTS                   |
| Key Pair       | `kops-keypair`                     |
| Security Group | `KOps-SG` (allow SSH from your IP) |
| Storage        | 8 GB                               |

![kops-kp](../Images/KOPs-kp.png)

![kops-sg](../Images/KOPs-sg.png)

![Kops_ec2](../Images/kops_ec2.png)

This instance **is not** part of the Kubernetes cluster.

### AWS Resources Needed

- S3 bucket to store KOps state
- IAM user for AWS CLI
- Route53 hosted zone for Kubernetes DNS

### 🆔 2️⃣ Create IAM User

- **Name:** `kops-admin`
- **Permission:** `AdministratorAccess`

Generate access keys → save the CSV (for AWS CLI use).

![kops-admin](../Images/kopsadmin.png)

![accesskey](../Images/accesskey.png)

### 🖥️ 3️⃣ Configure the EC2 Bootstrap Instance

**SSH into the EC2 instance:**

```bash
sudo -i
apt update && apt upgrade -y
```

![ec2_update](../Images/ec2_update.png)

**Install AWS CLI**

```bash
snap install aws-cli --classic
aws configure
```

![aws-cli_install](../Images/aws-cli_install.png)

Use the access keys from `kops-admin`.

**Generate SSH Keys**

```bash
ssh-keygen
ls ~/.ssh/
```

![generate_ssh-keys](../Images/generate_ssh-keys.png)

### ⚙️ 4️⃣ Install KOps

```bash
curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x kops
sudo mv kops /usr/local/bin/kops
```

Verify:

```bash
kops version
```

![install_kops](../Images/install_kops.png)

### ⚙️ 5️⃣ Install kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```

![install_kubectl](../Images/install_kubectl.png)

### 🪣 6️⃣ Create S3 Bucket for KOps State Store

- **Bucket Name:** `kops-state-0730`
- **Type:** General Purpose

![alt text](../Images/s3.png)

This bucket stores the cluster configuration and must remain available.

### 🌐 7️⃣ Create Route53 Hosted Zone

- **Hosted Zone Name:** `kubernetes.devops-prod.xyz`

This creates **4 NS records** → copy these.

![hostedzones](../Images/route53_hostedzone.png)

#### Add NS Records to GoDaddy

- Go to DNS settings
- Add **4 NS records**

  - **Name:** `kubernetes`
  - **Value:** NS values from Route53

This allows KOps to manage Kubernetes DNS entries in Route53.

![Domain_mapping](../Images/domain.png)

### 🏗️ 8️⃣ Create Kubernetes Cluster (KOps Command)

Verify SSH public key:

```bash
ls ~/.ssh/
```

Run cluster creation:

```bash
kops create cluster \
--name=kubernetes.devops-prod.xyz \
--state=s3://kops-state-0730 \
--zones=us-east-1a,us-east-1b \
--node-count=2 \
--node-size=t3.small \
--control-plane-size=t3.medium \
--dns-zone=kubernetes.devops-prod.xyz \
--node-volume-size=12 \
--control-plane-volume-size=12 \
--ssh-public-key ~/.ssh/id_ed25519.pub
```

![create_cluster](../Images/create_cluster.png)

### ▶️ 9️⃣ Build the Cluster

```bash
kops update cluster \
--name=kubernetes.devops-prod.xyz \
--state=s3://kops-state-0730 \
--yes \
--admin
```

![start_cluster](../Images/start_cluster.png)

_(Use your correct name + bucket values.)_

### 🔍 🔟 Validate Cluster

```bash
kops validate cluster \
--name=kubernetes.devops-prod.xyz \
--state=s3://kops-state-0730
```

![validate_cluster](../Images/validate_cluster.png)

### What Happens After Creation

- A `.kube` directory is created (kubectl config stored here)
- Route53 automatically adds:

  - Public API server DNS record
  - Private API server DNS record

- Infrastructure created:

  - **1 Control Plane Node**
  - **2 Worker Nodes**
  - **Private VPC** (subnets, routing, NAT, etc.)

![alt text](../Images/cluster01.png)

![alt text](../Images/cluster02.png)

![alt text](../Images/cluster03.png)

![alt text](../Images/cluster04.png)

![alt text](../Images/cluster05.png)

![alt text](../Images/cluster06.png)

![alt text](../Images/cluster07.png)

![alt text](../Images/cluster08.png)

![alt text](../Images/cluster09.png)

### ❌ 1️⃣1️⃣ Delete Cluster

```bash
kops delete cluster \
--name=kubernetes.devops-prod.xyz \
--state=s3://kops-state-0730 \
--yes
```
