# 🚀 Task 1: CI/CD Pipeline using Azure

## 📌 Project Overview

This project implements an **automated CI/CD pipeline using Azure DevOps** for a Blazor web application named **AzureWebApp**. The objective is to automate the **build, integration, and deployment** process so that code changes are delivered **quickly, reliably, and consistently**.

The application is developed using **ASP.NET Core Blazor**, managed with **Git**, and deployed automatically to **Azure App Service** through **Azure Pipelines**. This project demonstrates practical **DevOps concepts** used in cloud-based enterprise applications.

---

## 🛠️ Tools Used

* **Visual Studio Code** – Development IDE
* **Blazor Web App (ASP.NET Core)** – Web application framework
* **Git** – Version control
* **Azure DevOps** – Repository and CI/CD pipeline management
* **Azure Pipelines** – Automated build and release pipeline
* **Azure App Service** – Hosting and deployment
* **Azure Container Registry (ACR)** – Container image storage (if containerized)

---

## 🔄 Project Flow

### Development and Structure

* **Program.cs** – Entry point of the application; configures the builder, services, and middlewares.
* **App.razor** – Root component that manages routing and layout.
* **Components Folder** – Implements core functionalities and pages using Razor components.
* **_Imports.razor** – Shared namespaces across pages.
* **wwwroot Folder** – Stores static files like HTML, CSS, JavaScript, images, fonts, and videos.
* **appsettings.json** – Configuration file for environment settings and database connection strings.

### CI/CD Flow

1. Developer pushes code to **Azure DevOps Repository**.
2. **Azure Pipeline** fetches the code from Azure Repo and start running pipeline from the YAML Script.
3. Dependencies are restored, and the application is built.
4. (Optional) Docker container image is pushed to **Azure Container Registry (ACR)**.
5. Application is deployed to **Azure App Service** automatically.
6. Pipeline execution is monitored via **Azure DevOps Dashboard**.

This flow ensures **continuous integration, automated deployment, and reduced manual intervention**.

---
🔄 Application Flow
Program.cs → App.razor → Routes → Home Page

## ✅ Conclusion

This task successfully demonstrates a complete **Azure-based CI/CD pipeline**. It highlights how automation improves deployment speed, reliability, and consistency while reducing manual effort.

The project provides strong hands-on experience with **Azure DevOps**, **Azure App Service**, and modern **DevOps workflows**.

---

👤 **Author**: Sameen Afzal
