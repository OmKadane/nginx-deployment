# Nginx CI/CD Pipeline with GitHub Webhooks 🚀

A professional static website served by Nginx, featuring a complete CI/CD pipeline for automated deployments triggered by `git push`.

---

### Repository Status & Stats
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![GitHub Issues](https://img.shields.io/github/issues/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment/issues)
[![GitHub Stars](https://img.shields.io/github/stars/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment/stargazers)
[![Last Commit](https://img.shields.io/github/last-commit/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment/commits/main)

### Technologies Used
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)](https://nginx.org/)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)
[![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)](https://git-scm.com/)

---

## 📋 Table of Contents
1.  [About The Project](#ℹ️-about-the-project)
2.  [Tech Stack](#🛠️-tech-stack)
3.  [Deployment Workflows](#🔄-deployment-workflows)
    * [Workflow A: Manual Deployment](#a-manual-deployment)
    * [Workflow B: Automated CI/CD Deployment](#b-automated-cicd-deployment)
4.  [Initial Server Setup](#🚀-initial-server-setup)
5.  [License](#📄-license)

---

## ℹ️ About The Project

This repository demonstrates a complete workflow for deploying a static website to a live Nginx server. The project showcases two methods of deployment: a basic manual pull from the server and a fully automated CI/CD pipeline.

The automated system uses a **GitHub Webhook** to send a signal to a custom **Python/Flask** listener running on the server. This listener then executes a shell script to pull the latest changes, making the website update automatically seconds after a `git push`.



---

## 🛠️ Tech Stack

* **Web Server:** Nginx
* **Operating System:** Ubuntu (on Windows Subsystem for Linux)
* **Version Control:** Git & GitHub
* **Automation:** GitHub Webhooks
* **Webhook Listener:** Python with the Flask framework
* **Tunneling Service:** `ngrok` (for local development)
* **Frontend:** HTML & CSS

---

## 🔄 Deployment Workflows

This project supports two distinct deployment methods.

### A. Manual Deployment

This is the simplest method. After pushing changes to GitHub, you SSH into the server and manually run a script to pull the latest version of the code.

```bash
# On the server
cd /var/www/html
sudo git pull origin main

---
### B. Automated CI/CD Deployment

This is a fully automated "hands-off" process. A `git push` is all that's needed to update the live site.

**How It Works:**

1.  A developer runs `git push` from their local machine.
2.  GitHub sends a webhook notification to a public URL.
3.  `ngrok` securely tunnels this notification to the Python Flask listener running on the private server.
4.  The Flask script receives the signal and executes the `deploy.sh` script.
5.  The script runs `sudo git pull` to update the website files.

---

## 🚀 Initial Server Setup

To deploy this project, you first need to configure the server.

### 1. Prerequisites
* A Linux server with Nginx and Git installed.
* Python 3 and `pip` for the automated workflow.

---
### 2. Clone the Repository
Clone the project into the Nginx web root directory.
```bash
# Navigate to the web server directory
cd /var/www

# Clone the repo, then move it into place
sudo git clone [https://github.com/OmKadane/nginx-deployment.git](https://github.com/OmKadane/nginx-deployment.git)
sudo rm -rf /var/www/html
sudo mv /var/www/nginx-deployment /var/www/html

---
### 3. Configure Nginx
Create and enable a server block in `/etc/nginx/sites-available/` that points to `/var/www/html` as its root.

```nginx
server {
    listen 80;
    server_name your_domain_or_ip;

    root /var/www/html;
    index index.html;
    charset utf-8;

    location / {
        try_files $uri $uri/ =404;
    }
}

---
Finally, restart Nginx with `sudo systemctl restart nginx`.

*(For the full automated deployment setup, see the project scripts `deploy.sh` and `webhook.py`)*.

---
## 📄 License
Distributed under the MIT License. See [LICENSE](LICENSE) file for more information.
