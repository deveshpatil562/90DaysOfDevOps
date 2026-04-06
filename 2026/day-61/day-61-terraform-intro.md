# 🚀 DevOps Lab Guide — Introduction to Terraform & Your First AWS Infrastructure

## 🧠 Concept First (Mentor Notes)

### 🔹 What is Infrastructure as Code (IaC)?
Infrastructure as Code means managing and provisioning infrastructure (servers, networks, storage, etc.) using code instead of manual processes. Instead of clicking in the AWS console, you define everything in files and let tools like Terraform create it for you.

👉 Why it matters:
- Consistency across environments
- Version control (just like application code)
- Faster and repeatable deployments
- Reduced human errors

---

### 🔹 Problems Solved by IaC
Manual AWS console work leads to:
- Configuration drift (prod ≠ dev)
- No tracking of changes
- Time-consuming setups

IaC solves this by:
- Making infra reproducible
- Tracking changes via Git
- Automating deployments

---

### 🔹 Terraform vs Other Tools

| Tool            | Type          | Key Difference |
|-----------------|--------------|---------------|
| Terraform       | Declarative  | Multi-cloud, simple syntax |
| CloudFormation  | Declarative  | AWS-only |
| Ansible         | Procedural   | Config management, not infra-first |
| Pulumi          | Imperative   | Uses programming languages |

---

### 🔹 Declarative & Cloud-Agnostic

- Declarative = You define "WHAT" you want, not "HOW"
- Cloud-agnostic = Works with AWS, Azure, GCP, etc.

---

## ⚙️ Task 1: Install Terraform & Configure AWS

### Step 1: Install Terraform

[ brew tap hashicorp/tap ]
[ brew install hashicorp/tap/terraform ]

OR

[ sudo apt update && sudo apt install terraform ]

OR

[ choco install terraform ]

### Verify Installation

[ terraform -version ]

---

### Step 2: Configure AWS CLI

[ aws configure ]

Enter:
- Access Key
- Secret Key
- Region: ap-south-1
- Output: json

### Verify

[ aws sts get-caller-identity ]

---

## 📦 Task 2: Create First Terraform Project

### Step 1: Create Directory

[ mkdir terraform-basics && cd terraform-basics ]

---

### Step 2: Create main.tf

[ 
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "my_bucket" {
  bucket = "terraweek-yourname-2026"
}
]

---

### Step 3: Terraform Lifecycle

[ terraform init ]
[ terraform plan ]
[ terraform apply ]

Type: yes

---

### 🔍 Verification

- Go to AWS S3 Console
- Check bucket created

📸 Screenshot Placeholder:

<img width="1903" height="770" alt="task3 2" src="https://github.com/user-attachments/assets/14c60b64-fca2-45a8-9863-a0ada1823c07" />


<img width="845" height="830" alt="task3 1" src="https://github.com/user-attachments/assets/c7b1467a-c77f-4f6f-997d-8b1fae8bff4a" />


---

### ❓ Questions & Answers

Q: What did terraform init download?
A: It downloaded AWS provider plugins required to interact with AWS APIs.

Q: What is .terraform directory?
A: It stores provider binaries and metadata.

---

## 💻 Task 3: Add EC2 Instance

### Update main.tf

[ 
resource "aws_instance" "my_instance" {
  ami           = "ami-0f5ee92e2d63afc18"
  instance_type = "t2.micro"

  tags = {
    Name = "TerraWeek-Day1"
  }
}
]

---

### Apply Changes

[ terraform plan ]
[ terraform apply ]

---

### 🔍 Verification

- Go to EC2 Dashboard
- Check instance is running

📸 Screenshot Placeholder:

<img width="767" height="788" alt="task4 1" src="https://github.com/user-attachments/assets/80a4022e-0328-4421-8d10-fb4816320aa6" />

<img width="1915" height="712" alt="task4 2" src="https://github.com/user-attachments/assets/3cabcc2e-55ea-486a-b96a-bbc888c3c4f9" />


---

### ❓ Questions & Answers

Q: How Terraform knows S3 exists?
A: Terraform uses the state file (terraform.tfstate) to track created resources.

---

## 📊 Task 4: Understand State File

### Commands

[ terraform show ]
[ terraform state list ]
[ terraform state show aws_s3_bucket.my_bucket ]
[ terraform state show aws_instance.my_instance ]

---

### ❓ Questions & Answers

Q: What does state file store?
A: Resource IDs, configurations, metadata, dependencies.

Q: Why not edit manually?
A: It can corrupt infrastructure tracking.

Q: Why not commit to Git?
A: It may contain sensitive data like resource IDs and secrets.

---

## 🔄 Task 5: Modify Infrastructure

### Update Tag

[ Name = "TerraWeek-Modified" ]

---

### Plan Again

[ terraform plan ]

---

### Symbols Meaning

- + → Create
- ~ → Modify
- - → Destroy

👉 This is an in-place update.

---

### Apply Changes

[ terraform apply ]

---

### 🔍 Verification

- Check updated tag in EC2 console

📸 Screenshot Placeholder:

<img width="1590" height="791" alt="task6" src="https://github.com/user-attachments/assets/8b032d9d-24cc-40b6-a31a-88554b8d1ecd" />

<img width="1918" height="526" alt="task6 2" src="https://github.com/user-attachments/assets/5af7a6a7-0430-4484-87cc-bd323cd388fd" />



---

## 💣 Task 6: Destroy Infrastructure

[ terraform destroy ]

Type: yes

---

### 🔍 Verification

- S3 bucket deleted
- EC2 instance terminated


---

## 🧾 Terraform Commands Summary

| Command            | Purpose |
|------------------|--------|
| terraform init   | Initialize project |
| terraform plan   | Preview changes |
| terraform apply  | Apply changes |
| terraform destroy| Delete resources |
| terraform show   | Show state |
| terraform state list | List resources |

---

## 📌 Final Notes (Mentor Tips)

- Always run:
  [ terraform fmt ]
  [ terraform validate ]

- Add to .gitignore:
  [ *.tfstate ]
  [ *.tfstate.backup ]
  [ .terraform/ ]

---

## 🏁 Conclusion

You just:
✔ Installed Terraform  
✔ Connected AWS  
✔ Created S3 + EC2 using code  
✔ Understood state management  
✔ Modified and destroyed infra  

👉 This is the foundation of real-world DevOps.

---

## 🔥 Interview Style Questions

Q: What is Terraform state?
A: It is a JSON file that tracks infrastructure resources created by Terraform.

Q: Difference between plan and apply?
A: Plan shows changes, apply executes them.

Q: What happens if state file is lost?
A: Terraform loses track of resources → can recreate duplicates or fail.

Q: Why Terraform is powerful?
A: Automation + versioning + multi-cloud support.

---

## 📢 LinkedIn Post Idea

"Started my Terraform journey 🚀  
Created S3 bucket & EC2 instance using code and destroyed it in seconds.  
Infrastructure as Code finally makes sense!"

#DevOps #Terraform #AWS #IaC #90DaysOfDevOps
