# 🚀 CI/CD DevOps Project README

## 📌 Project Overview

This repository contains **Task 1 (CI/CD Pipeline using Azure App Service)** and **Task 2 (Jenkins Remoting with Azure DevOps)**. The goal of this project is to demonstrate practical DevOps concepts including **application development, CI/CD pipelines, source control integration, and automation using Jenkins**.

---

# 🧩 Task 1: CI/CD Pipeline – Azure Blazor Web App

## 🔹 Explanation of DevOps Project

### 1️⃣ Development Environment Setup

* **VS Code** installed and configured (already completed).
* Created a **Blazor Web App** using **ASP.NET Core Framework**.
* Project name: **AzureWebApp**.
* Application initially runs on **localhost**.
* Objective: **Publish the application to Azure App Service**.

---

### 2️⃣ Project Structure Explanation

#### 🔹 Project File (.csproj)

* Contains **Target Framework** configuration.
* Includes C# settings such as:

  * `nullable`
  * `implicitUsings`

These settings improve code safety and reduce boilerplate code.

---

#### 🔹 Program.cs (Entry Point)

* Acts as the **main entry point** of the application.
* Creates and configures the **WebApplication Builder**.
* Registers services and HTTP pipeline configuration.
* Uses **middlewares**, which are built-in functions handling requests and responses.

---

#### 🔹 Connected Services

* No connected services currently.
* No database or third-party integrations configured.

---

#### 🔹 Dependencies

* The Blazor application depends on:

  * `Microsoft.AspNetCore.App`

---

#### 🔹 Properties Folder

* Contains **JSON configuration files**.
* Defines environment-specific settings and development requirements.

---

#### 🔹 wwwroot Folder (Static Files)

* Contains **static files**, which do not change dynamically:

  * HTML
  * CSS
  * JavaScript
  * Images
  * Fonts
  * Videos

---

#### 🔹 Components Folder

* Core functionality of the Blazor application is implemented here.
* **Layout**:

  * Uses **master layout concept**.
  * Avoids duplication of UI design.
  * Provides flexibility and consistency.
* **Pages**:

  * All application pages are defined here.
  * `.razor` files allow writing **HTML + C# code** together.

---

#### 🔹 _Imports.razor

* Contains **shared namespaces**.
* Automatically accessible across all pages.

---

#### 🔹 App.razor

* **Root component** of the application.
* Executes first when the application starts.
* Handles routing and layout rendering.

---

#### 🔹 appsettings.json

* Used to configure application settings.
* Database connections can be added here using **connection strings**.

---

### 🔄 Application Flow

```
Program.cs → App.razor → Routes → Home Page
```

* `Program.cs` calls the App component.
* `App.razor` loads routes.
* Routes render the Home page.

---

### 🚀 Deployment (Publishing)

After building the website:

* The application is **published to Azure App Service** using:

  * VS Code publish option
* Alternative deployment method:

  * Push code to **Git repository** and deploy from source control

---

# 🧩 Task 2: Jenkins Remoting Project (CI Pipeline)

## 🔹 Architecture Flow

```
Azure DevOps Repo → Jenkins → Build/Test → (Optional) Deploy
```

Jenkins Responsibilities:

* Pull code from Azure DevOps repository
* Trigger builds automatically
* Execute pipelines using **Jenkinsfile**

---

## 🔹 Prerequisites

Ensure the following are available:

1. Jenkins installed (Java 17 compatible)
2. Azure DevOps project
3. Azure Repos (Git)
4. Admin access to Jenkins
5. Azure DevOps **Personal Access Token (PAT)**

---

## 🔹 Step 1: Install Required Jenkins Plugins

### 📌 Why?

Jenkins requires plugins to authenticate and communicate with Azure DevOps.

### ✅ Required Plugins

* Azure DevOps Plugin
* Git Plugin
* Pipeline Plugin
* Credentials Binding Plugin

### 🔧 Installation Steps

1. Jenkins Dashboard → Manage Jenkins
2. Plugins → Available Plugins
3. Search and install:

   * Azure DevOps
   * Git
   * Pipeline
4. Restart Jenkins

---

## 🔹 Step 2: Create Azure DevOps Personal Access Token (PAT)

### 📌 Why?

PAT is used by Jenkins to securely access Azure Repos.

### 🔧 Steps to Create PAT

1. Open Azure DevOps
2. User Settings → Personal Access Tokens
3. Click **New Token**
4. Configure:

   * Name: `Jenkins-Integration`
   * Organization: Your organization
   * Scope: Code → Read (or Read & Write)
5. Click **Create**
6. Copy the token (shown only once)

---

## 🔹 Step 3: Add Azure DevOps Credentials in Jenkins

### 📌 Why?

Secure authentication between Jenkins and Azure DevOps.

### 🔧 Steps

1. Manage Jenkins → Credentials
2. Select **Global** → Add Credentials
3. Configure:

   * Kind: Username with password
   * Username: Azure DevOps email
   * Password: PAT token
   * ID: `azure-devops-creds`
4. Save

---

## 🔹 Step 4: Get Azure Repo Git URL

1. Azure DevOps → Repos
2. Click **Clone**
3. Copy HTTPS URL

Example:

```
https://dev.azure.com/organization/project/_git/repository
```

---

## 🔹 Step 5: Create Jenkins Pipeline Job

### 🔧 Steps

1. Jenkins Dashboard → New Item
2. Job Name: `AzureDevOps-CI`
3. Select **Pipeline**
4. Click OK

---

## 🔹 Step 6: Configure Source Code Management

### 📌 Why?

To connect Jenkins with Azure Repos.

### 🔧 Configuration

* Pipeline Definition: **Pipeline script from SCM**
* SCM: Git
* Repository URL: Azure Repo HTTPS URL
* Credentials: `azure-devops-creds`
* Branch: `*/main`
* Script Path: `Jenkinsfile`

---

## 🔹 Step 7: Jenkinsfile (Pipeline Script)

### 📌 Purpose

Defines CI/CD pipeline stages.

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'azure-devops-creds',
                    url: 'https://dev.azure.com/org/project/_git/repo'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
```

Commit and push this file to Azure Repo.

---

## 🔹 Step 8: Enable Auto Trigger (Optional)

### 📌 Why?

Automatically trigger Jenkins build on every code push.

### 🔧 Jenkins Side

1. Job → Configure
2. Build Triggers → Enable **Poll SCM**
3. Schedule:

```
H/5 * * * *
```

### 🔧 Azure DevOps Side (Webhooks)

1. Project Settings → Service Hooks
2. Add Web Hook
3. Trigger: Code Push
4. URL:

```
http://<jenkins-url>/azure-webhook/
```

---

## 🔹 Step 9: Run & Verify

1. Click **Build Now** in Jenkins
2. Check **Console Output**
3. Verify:

   * Repository cloned successfully
   * All pipeline stages executed
   * No authentication errors

---

## ✅ Conclusion

This project demonstrates a complete **DevOps CI/CD workflow** using:

* Azure Blazor Web App
* Azure App Service
* Azure DevOps Repos
* Jenkins Pipeline Automation

---

👤 **Author**: Sameen Afzal
