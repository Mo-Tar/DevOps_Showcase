# 🚀 Azure DevOps Showcase

![CI/CD Pipeline](https://github.com/YOUR_USERNAME/azure-devops-showcase/actions/workflows/ci-cd.yml/badge.svg)
![Terraform](https://img.shields.io/badge/IaC-Terraform-7B42BC?logo=terraform)
![Docker](https://img.shields.io/badge/Container-Docker-2496ED?logo=docker)
![Azure](https://img.shields.io/badge/Cloud-Azure-0078D4?logo=microsoftazure)
![Python](https://img.shields.io/badge/App-Python%20Flask-3776AB?logo=python)

A fully automated cloud-native web application deployed on **Microsoft Azure**, built to demonstrate core Junior DevOps competencies:
Infrastructure as Code, containerization, and a complete CI/CD pipeline — all from a single `git push`.

---

## 🌐 Live Demo

# In Progress

---

## 🏗️ Architecture Overview

```
Developer (git push)
        │
        ▼
┌──────────────────┐
│   GitHub Actions │  ← CI/CD Engine
│                  │
│  1. 🧪 Test      │  pytest runs on every push
│  2. 🐳 Build     │  Docker image built & pushed
│  3. 🚀 Deploy    │  Azure App Service updated
└──────────────────┘
        │
        ▼
┌─────────────────────────────────────┐
│            Microsoft Azure          │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  Azure Container Registry   │    │  ← Docker image stored here
│  └─────────────────────────────┘    │
│              │                      │
│              ▼                      │
│  ┌─────────────────────────────┐    │
│  │   Azure App Service (Linux) │    │  ← App runs here (live URL)
│  └─────────────────────────────┘    │
│                                     │
│  All provisioned with Terraform ✅  │
└─────────────────────────────────────┘
```

---

## 🧰 Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Application** | Python + Flask | Lightweight web app |
| **Containerization** | Docker | Consistent, portable builds |
| **CI/CD** | GitHub Actions | Automated test → build → deploy |
| **Infrastructure** | Terraform | Azure resources as code (IaC) |
| **Container Registry** | Azure Container Registry (ACR) | Stores Docker images |
| **Hosting** | Azure App Service | Runs the live container |
| **Testing** | pytest | Automated unit testing |
| **Secrets** | GitHub Encrypted Secrets | Secure credential management |

---

## 🔄 CI/CD Pipeline

Every `git push` to `main` triggers a **3-stage automated pipeline**:

```
┌─────────────┐     ✅ pass     ┌──────────────────┐     ✅ pass     ┌──────────────────┐
│  1. 🧪 TEST │ ─────────────► │  2. 🐳 BUILD     │ ─────────────► │  3. 🚀 DEPLOY    │
│             │                │                  │                │                  │
│  pytest     │                │  docker build    │                │  Azure App       │
│  unit tests │                │  docker push     │                │  Service pulls   │
│             │                │  → to Azure ACR  │                │  new image       │
└─────────────┘                └──────────────────┘                └──────────────────┘
     ❌ fail = pipeline stops here, nothing broken in production
```

> **Key principle:** If tests fail, the pipeline stops. Broken code never reaches production.

---

## 🏗️ Infrastructure as Code (Terraform)

All Azure resources are defined in code — **no manual portal clicking**. Running `terraform apply` provisions everything from scratch:

```hcl
# Terraform creates all of this automatically:
✅ Azure Resource Group
✅ Azure Container Registry (ACR)
✅ Azure App Service Plan (Linux, B1)
✅ Azure Linux Web App (Docker-based)
```

To destroy all resources cleanly:
```bash
terraform destroy
```

---

## 📁 Project Structure

```
azure-devops-showcase/
├── app/
│   ├── app.py              # Flask application
│   ├── requirements.txt    # Python dependencies
│   └── test_app.py         # pytest unit tests
├── terraform/
│   ├── main.tf             # Azure resource definitions
│   ├── variables.tf        # Configurable values
│   └── outputs.tf          # Output values (e.g. app URL)
├── Dockerfile              # Container build instructions
├── .dockerignore
├── .gitignore
├── README.md
└── .github/
    └── workflows/
        └── ci-cd.yml       # GitHub Actions pipeline
```

---

## 🚀 Run It Locally

### Prerequisites
- Python 3.11+
- Docker Desktop
- Git

### Option A: Run with Python
```bash
git clone https://github.com/YOUR_USERNAME/azure-devops-showcase.git
cd azure-devops-showcase
pip install -r app/requirements.txt
python app/app.py
# Visit http://localhost:8000
```

### Option B: Run with Docker
```bash
docker build -t azure-devops-showcase:local .
docker run -p 8000:8000 azure-devops-showcase:local
# Visit http://localhost:8000
```

### Run Tests
```bash
pytest app/test_app.py -v
```

---

## ☁️ Deploy Your Own Copy

### 1. Azure Setup
```bash
az login
az group create --name rg-devops-showcase --location canadacentral
az acr create --resource-group rg-devops-showcase \
              --name acrdevopsshowcase \
              --sku Basic --admin-enabled true
```

### 2. Terraform
```bash
cd terraform
terraform init
terraform plan
terraform apply
```

### 3. GitHub Secrets
Add these to your repo under **Settings → Secrets → Actions**:

| Secret | Description |
|---|---|
| `ACR_NAME` | Your Azure Container Registry name |
| `ACR_USERNAME` | ACR admin username |
| `ACR_PASSWORD` | ACR admin password |
| `AZURE_WEBAPP_NAME` | Your App Service name |

### 4. Push & Watch It Deploy
```bash
git push origin main
# Go to GitHub → Actions tab → Watch the pipeline run 🎉
```

---

## 📡 API Endpoints

| Endpoint | Method | Description |
|---|---|---|
| `/` | GET | Homepage — welcome message |
| `/health` | GET | Health check — returns `{"status": "healthy"}` |

---

## 🌟 What I Learned

- Provisioning cloud infrastructure using **Terraform** instead of manual portal setup
- Containerizing applications with **Docker** for environment consistency
- Building multi-stage **CI/CD pipelines** with GitHub Actions
- Securely managing credentials with **GitHub Encrypted Secrets**
- Deploying containers to **Azure App Service** via Azure Container Registry
- Writing **automated unit tests** with pytest as a pipeline gate

---

## 🔮 Future Improvements

- [ ] Add Trivy container vulnerability scanning in the pipeline (DevSecOps)
- [ ] Store Terraform state remotely in Azure Blob Storage
- [ ] Add a `dev` branch deploying to a staging environment
- [ ] Integrate Azure Application Insights for monitoring & observability
- [ ] Add Dependabot for automated dependency updates

---

## 👤 Author

**Muhammad Tararr**
📍 Calgary, AB
🔗 [LinkedIn](https://linkedin.com/in/YOUR_LINKEDIN)
🐙 [GitHub](https://github.com/YOUR_USERNAME)

---

## 📄 License

MIT License — feel free to fork and build on this!
