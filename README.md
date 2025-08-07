# 🚀 Provision a Docker Container using Terraform

This project demonstrates how to use **Terraform** with the **Docker provider** to provision and manage a local Docker container (NGINX) on a **Windows system**.

---

## 🧰 Tools Used

- [Terraform](https://developer.hashicorp.com/terraform)
- [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop)

---

## 📂 Project Structure

```
terraform-docker-demo/
├── main.tf                # Terraform configuration
├── README.md              # Project documentation
├── init_log.txt           # Log from terraform init
├── validate_log.txt       # Log from terraform validate
├── plan_log.txt           # Log from terraform plan
├── apply_log.txt          # Log from terraform apply
├── state_log.txt          # Log from terraform state list
├── destroy_log.txt        # Log from terraform destroy
```

---

## ✅ Prerequisites

- Docker Desktop installed and running
- Terminal/PowerShell run as **Administrator**
- Terraform installed and added to PATH

---

## 🔧 Terraform Configuration (`main.tf`)

```hcl
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0"
    }
  }
}

provider "docker" {
  host = "npipe:////./pipe/docker_engine"
}

resource "docker_image" "nginx_image" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx_container" {
  name  = "nginx_server"
  image = docker_image.nginx_image.image_id

  ports {
    internal = 80
    external = 8080
  }
}
```

---

## 🪜 Steps to Run

### 1. Initialize Terraform

```bash
terraform init > init_log.txt
```

### 2. Validate Configuration

```bash
terraform validate > validate_log.txt
```

### 3. Generate an Execution Plan

```bash
terraform plan > plan_log.txt
```

### 4. Apply the Configuration

```bash
terraform apply -auto-approve > apply_log.txt
```

✅ Visit [http://localhost:8080](http://localhost:8080) to see the NGINX welcome page.

### 5. View Terraform-managed Resources

```bash
terraform state list > state_log.txt
```

### 6. Destroy the Infrastructure

```bash
terraform destroy -auto-approve > destroy_log.txt
```

---

## 📦 Outcome

- A local NGINX Docker container is provisioned using Terraform.
- The infrastructure is fully managed via code (Infrastructure as Code).
- Terraform handles container lifecycle (create/update/destroy).

---

## 📚 References

- [Terraform Docker Provider Docs](https://registry.terraform.io/providers/kreuzwerker/docker/latest/docs)
- [Terraform CLI Docs](https://developer.hashicorp.com/terraform/docs/cli)

---

## 👤 Author

*Shravani Devarakonda*
