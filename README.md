# CI/CD Pipeline using GitHub Actions, Docker Image, AWS ECS & ECR  (Fargate)

**End-to-end, production-style container deployment built from scratch**

**THE PROJECT THAT SHOWS MY WORK IS PRIVATE, RECRUITERS PLEASE REQUEST ACCESS**

━━━━━━━━━━━━━━━━━━━━━━
## 🧭 Project Summary
━━━━━━━━━━━━━━━━━━━━━━

This repository represents **hands-on cloud engineering experience** building a complete **CI/CD pipeline from zero**, starting from an empty GitHub repository and ending with a live, publicly accessible application running on **Amazon ECS Fargate**.

All work was performed using:
- Terminal-based workflows
- Real IAM users and roles
- Docker containerization
- GitHub Actions CI
- Secure, keyless authentication (OIDC)

No EC2 instances, no SSH access, no static AWS credentials, and no manual deployments were used.

━━━━━━━━━━━━━━━━━━━━━━
## 🧱 Chronological Execution (Exactly as Performed)
━━━━━━━━━━━━━━━━━━━━━━

This section documents **what was done, in the exact order it was done**, reflecting real-world cloud engineering work.

━━━━━━━━━━━━━━━━━━━━━━
## 1️⃣ Source Control Initialization (GitHub First)
━━━━━━━━━━━━━━━━━━━━━━

- Created a new **GitHub repository** with no pre-initialized files
- Cloned the empty repository locally using terminal:

```bash
git clone https://github.com/<username>/ecs-app.git
cd ecs-app
Verified repository state (git status) showing an empty working tree

✔ GitHub established as the single source of truth
✔ All automation later triggered from Git events

━━━━━━━━━━━━━━━━━━━━━━

2️⃣ Application Creation (Terminal & Nano)
━━━━━━━━━━━━━━━━━━━━━━

Created the application directly from terminal using nano

Built a Python Flask web application exposing port 8000

bash
Copy code
nano app.py
Implemented application logic

Saved and exited nano (CTRL + O, ENTER, CTRL + X)

Created dependency file:

bash
Copy code
nano requirements.txt
✔ Application created manually (no scaffolding tools)
✔ Verified application runs locally before containerization

━━━━━━━━━━━━━━━━━━━━━━

3️⃣ Local Environment Validation
━━━━━━━━━━━━━━━━━━━━━━

Created and activated a Python virtual environment

Installed dependencies locally

Ran the application to confirm functionality

bash
Copy code
python app.py
✔ Confirmed application behavior before Docker usage
✔ Prevented shipping broken code into the pipeline

━━━━━━━━━━━━━━━━━━━━━━

4️⃣ Dockerization (From Scratch)
━━━━━━━━━━━━━━━━━━━━━━

Created a Dockerfile manually using nano

Defined base image, working directory, dependency installation, and runtime command

bash
Copy code
nano Dockerfile
Built Docker image locally:

bash
Copy code
docker build -t ecs-app .
Ran container locally and verified application response:

bash
Copy code
docker run -p 8000:8000 ecs-app
✔ Confirmed container behavior before cloud deployment
✔ Docker used as a build artifact, not a runtime tool

━━━━━━━━━━━━━━━━━━━━━━

5️⃣ Git Versioning (Human Action)
━━━━━━━━━━━━━━━━━━━━━━

Created .gitignore to exclude virtual environment

Staged all files manually

Configured Git identity

Committed and pushed code to GitHub

bash
Copy code
git add .
git commit -m "Initial Flask app and Docker setup"
git push origin main
✔ Human responsibility ends here
✔ Everything beyond this point is automated

━━━━━━━━━━━━━━━━━━━━━━

6️⃣ Human IAM Access (AWS Setup)
━━━━━━━━━━━━━━━━━━━━━━

Created a dedicated IAM user for cloud engineering tasks

Enabled console access

Attached permissions to allow infrastructure creation

✔ Root account not used for daily operations
✔ Human access separated from automation

━━━━━━━━━━━━━━━━━━━━━━

7️⃣ Amazon ECR (Container Registry)
━━━━━━━━━━━━━━━━━━━━━━

Created a private Amazon ECR repository

Enabled image scanning on push

Copied repository URI for CI and ECS usage

✔ CI pushes images
✔ ECS pulls images
✔ No manual Docker pushes in production

━━━━━━━━━━━━━━━━━━━━━━

8️⃣ IAM Roles & Trust Model
━━━━━━━━━━━━━━━━━━━━━━

Created and verified three distinct IAM roles, each with a single responsibility:

• ECS Service-Linked Role
AWSServiceRoleForECS

Enables ECS control plane operations

Required for cluster and service creation

• ECS Task Execution Role
ecsTaskExecutionRole

Allows tasks to pull images from ECR

Allows logging to CloudWatch

• CI Role (GitHub Actions via OIDC)
Trusted entity: GitHub Actions

Authentication via OpenID Connect (OIDC)

Permissions scoped to ECR image push

✔ No static AWS access keys
✔ All credentials are short-lived

━━━━━━━━━━━━━━━━━━━━━━

9️⃣ CI Pipeline Creation (GitHub Actions)
━━━━━━━━━━━━━━━━━━━━━━

Created workflow directory manually:

bash
Copy code
mkdir -p .github/workflows
nano .github/workflows/ci.yml
Defined CI workflow to:

Check out source code

Build Docker image

Authenticate to AWS using OIDC

Authenticate to ECR

Tag and push image to ECR

Committed and pushed workflow to GitHub

bash
Copy code
git add .github/workflows/ci.yml
git commit -m "Add CI workflow to build and push Docker image"
git push origin main
✔ CI triggered automatically on push
✔ Image published without human involvement

━━━━━━━━━━━━━━━━━━━━━━

🔄 Continuous Integration (CI)
━━━━━━━━━━━━━━━━━━━━━━

Executed by GitHub Actions on every push to main:

Source checkout

Docker build

OIDC-based AWS authentication

ECR login

Image tagging

Image push to ECR

✔ No SSH
✔ No secrets stored
✔ Fully automated

━━━━━━━━━━━━━━━━━━━━━━

🚀 Continuous Deployment (CD)
━━━━━━━━━━━━━━━━━━━━━━

Handled by Amazon ECS:

Created ECS Fargate cluster

Created task definition referencing ECR image

Created ECS service with:

Desired task count: 1

Public networking enabled

Security group allowing TCP 8000

ECS automatically:

Pulls the latest image

Runs the container

Restarts tasks on failure

✔ No EC2
✔ No server management

━━━━━━━━━━━━━━━━━━━━━━

🌍 Deployment Result
━━━━━━━━━━━━━━━━━━━━━━

Docker image built and pushed via CI

ECS service deployed container successfully

Application running continuously on Fargate

Public endpoint serving live traffic

━━━━━━━━━━━━━━━━━━━━━━

🔐 Security & Authentication Model
━━━━━━━━━━━━━━━━━━━━━━

Not Used
SSH access

Long-lived AWS keys

IAM users for CI

Manual Docker pushes

Used Instead
GitHub OpenID Connect (OIDC)

IAM role assumption

Short-lived credentials

Least-privilege access

✔ Matches enterprise security standards

━━━━━━━━━━━━━━━━━━━━━━

🎯 Why This Matters
━━━━━━━━━━━━━━━━━━━━━━

This repository demonstrates real cloud engineering experience with:

Terminal-driven development

Docker-based build pipelines

Secure CI/CD authentication

AWS IAM role design

ECS Fargate operations

Debugging real AWS errors

This is production-aligned work, not a lab or guided tutorial.

━━━━━━━━━━━━━━━━━━━━━━

👤 Author
━━━━━━━━━━━━━━━━━━━━━━

Joshua Agyapong
Cloud Engineering • CI/CD • AWS • Containers
