<img width="900" height="569" alt="image" src="https://github.com/user-attachments/assets/2348b437-4d98-4370-aec5-3cb659c4ec99" />





# GitHub-Action-tf_CICD

This repository demonstrates how to set up a **CI/CD pipeline with GitHub Actions** for deploying infrastructure using **Terraform** on AWS.

---

## ⚙️ Setup Instructions

### 1. Create Repository
- Create a new repository named **`GitHub-Action-tf_CICD`**.
- Inside the repository, add the following structure:
  - `.github/workflows/test.yml`
  - `main.tf`
  - `provider.tf`

---

## 📂 Repository Structure

```
GitHub-Action-tf_CICD/
│
├── .github/
│   └── workflows/
│       └── test.yml        # GitHub Actions workflow file
│
├── main.tf                 # Terraform configuration file
├── provider.tf             # Terraform provider configuration
```

---



### 2. Configure GitHub Secrets
Go to:
- **Settings → Secrets and variables → Actions → New repository secret**

Add the following secrets:

- `AWS_ACCESS_KEY_ID`  = KJHWDGHKCJIGJJOIHENCK
 

  <img width="994" height="531" alt="Screenshot 2025-11-24 131236" src="https://github.com/user-attachments/assets/a1dd39d2-5145-40a9-8b72-1da4fd139b24" />


- `AWS_SECRET_ACCESS_KEY`  
  ```
  jlwtawSzy6QwKXTm8mmX8fkYY5pthYO7hgBxubaY
  ```

  <img width="1003" height="519" alt="Screenshot 2025-11-24 131504" src="https://github.com/user-attachments/assets/e5571abe-589f-45eb-a7b5-f69ec6a59a98" />


These secrets will be used by Terraform to authenticate with AWS.

---

<img width="1411" height="295" alt="Screenshot 2025-11-24 131530" src="https://github.com/user-attachments/assets/8c7b367d-4efc-403b-b4af-2d89c66ad7a6" />


### 3. GitHub Action Workflow

The workflow file `.github/workflows/test.yml` defines the CI/CD pipeline:

```yaml

name: Terraform Deploy

on:
  # push:
   #  branches: [ main ]
  workflow_dispatch:   # ✅ Manual trigger only


jobs:
  terraform:
    runs-on: ubuntu-latest

    env:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      AWS_DEFAULT_REGION: us-east-1 # change if needed

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3

      - name: Terraform Init
        run: terraform init

      - name: Terraform Validate
        run: terraform validate

      - name: Terraform Plan
        run: terraform plan -out=tfplan

      - name: Terraform Apply
        run: terraform apply -auto-approve tfplan
---
````



### 4. Run Workflow
- Navigate to the **Actions** tab in GitHub.
- Select **Terraform Deploy** workflow.
- Click **Run workflow**.
- Terraform will automatically create resources in AWS.


<img width="1878" height="835" alt="Screenshot 2025-11-24 133818" src="https://github.com/user-attachments/assets/cf064ef6-ab27-4145-b78e-5268684685a8" />

<img width="750" height="701" alt="Screenshot 2025-11-24 133528" src="https://github.com/user-attachments/assets/3b8fe1a4-7d2b-4c63-8420-0bd1a848a30f" />

<img width="686" height="765" alt="Screenshot 2025-11-24 133616" src="https://github.com/user-attachments/assets/65329a3a-22b3-48ab-b0a9-de76b751da69" />

<img width="589" height="702" alt="Screenshot 2025-11-24 133636" src="https://github.com/user-attachments/assets/7ffacea2-566e-43d5-8628-7a51330bcf0f" />



---

## ✅ Notes
- Ensure your `main.tf` and `provider.tf` files are correctly configured for the AWS resources you want to deploy.
- Secrets must be kept private and never hardcoded in files.
- This setup uses **manual workflow dispatch**; you can extend it to run on `push` or `pull_request`.

  <img width="1865" height="869" alt="Screenshot 2025-11-24 140006" src="https://github.com/user-attachments/assets/4ed4c064-64b9-49cd-ad4b-b386f9b077a6" />


---

## 🚀 Outcome
Once the workflow runs successfully:
- Terraform initializes.
- Plans the infrastructure changes.
- Applies the configuration.
- AWS resources are automatically created.

---

## 📌 Next Steps
- Add resource definitions in `main.tf` (e.g., EC2, S3, VPC).
- Extend workflows for testing, linting, and multi-environment deployments.
```
```
<img width="1673" height="256" alt="Screenshot 2025-11-24 133847" src="https://github.com/user-attachments/assets/fe7febb5-cadf-443f-9a25-9a76a5987af8" />


<img width="1672" height="313" alt="Screenshot 2025-11-24 133912" src="https://github.com/user-attachments/assets/c74b6bba-af0c-440b-bb40-4cd872310c8d" />




```
---

Would you like me to also **fill in sample Terraform code** for `main.tf` and `provider.tf` (like deploying an EC2 instance or S3 bucket), so your workflow creates actual AWS resources immediately?
