# Nginx CI/CD Pipeline with GitHub Webhooks 🚀

A professional static website served by **Nginx**, featuring a complete CI/CD pipeline for automated deployments triggered by `git push`.

---

## 📊 Repository Status & Stats
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![GitHub Issues](https://img.shields.io/github/issues/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment/issues)
[![GitHub Stars](https://img.shields.io/github/stars/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment/stargazers)
[![Last Commit](https://img.shields.io/github/last-commit/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment/commits/main)

---

## 🧰 Technologies Used
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)](https://nginx.org/)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)
[![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)](https://git-scm.com/)

---

## 📋 Table of Contents
1. [ℹ️ About The Project](#ℹ️-about-the-project)
2. [🛠️ Tech Stack](#🛠️-tech-stack)
3. [🔄 Deployment Workflows](#🔄-deployment-workflows)  
   - [A. Manual Deployment](#a-manual-deployment)  
   - [B. Automated CI/CD Deployment](#b-automated-cicd-deployment)  
4. [🚀 Initial Server Setup](#🚀-initial-server-setup)
5. [📄 License](#📄-license)

---

## ℹ️ About The Project

This repository demonstrates a **complete workflow** for deploying a static website to a live **Nginx server**.  

It showcases two methods of deployment:  
- A **manual pull** method from the server.  
- A **fully automated CI/CD pipeline** using GitHub Webhooks.  

The automated system uses a **GitHub Webhook** to send a signal to a custom **Python/Flask** listener running on the server.  
This listener executes a shell script to pull the latest changes, updating the website automatically within seconds after a `git push`.  

---

## 🛠️ Tech Stack

- **Web Server:** Nginx  
- **Operating System:** Ubuntu (on WSL or Linux server)  
- **Version Control:** Git & GitHub  
- **Automation:** GitHub Webhooks  
- **Webhook Listener:** Python with Flask  
- **Tunneling Service (local dev):** ngrok  
- **Frontend:** HTML & CSS  

---

## 🔄 Deployment Workflows

This project supports two deployment methods:

### A. Manual Deployment
After pushing changes to GitHub, SSH into the server and pull the latest version.

```bash
# On the server
cd /var/www/html
sudo git pull origin main

```

### B. Automated CI/CD Deployment

A **hands-off** approach: simply `git push` and the live site updates automatically.

#### How It Works
1.  Developer runs `git push`.
2.  GitHub sends a webhook notification to a public URL.
3.  `ngrok` tunnels this notification to the **Flask listener** on the server.
4.  Flask receives the signal and executes `deploy.sh`.
5.  The script runs `sudo git pull` to update the website files.

---
## 🚀 Initial Server Setup

### 1. Prerequisites
- Linux server with **Nginx** and **Git** installed.
- Python 3 + `pip` (for the automated workflow).

### 2. Clone the Repository
Clone the project into the Nginx web root:
```bash
# Navigate to the web server directory
cd /var/www

```
Clone the repo
```
sudo git clone [https://github.com/OmKadane/nginx-deployment.git](https://github.com/OmKadane/nginx-deployment.git)

```
Replace existing html folder with project
```
sudo rm -rf /var/www/html
sudo mv /var/www/nginx-deployment /var/www/html

```
### 3. Configure Nginx

Create a server block inside `/etc/nginx/sites-available/`:

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

```
Then restart Nginx:

```bash
sudo systemctl restart nginx

```

## ⚙️ Server-Side Scripts

The following scripts are not part of the website's repository but are placed on the server to handle the automated deployment.

<details>
<summary>Click to view <code>deploy.sh</code></summary>

This script is executed by the Python listener and is responsible for updating the website files.

```bash
#!/bin/bash
# Navigate to the website directory
cd /var/www/html
# Discard any local changes to prevent conflicts
sudo git reset --hard
# Pull the latest changes from the main branch
sudo git pull origin main

```
</details>  
<details>  
<summary>Click to view <code>webhook.py</code></summary>  

This Python Flask script runs on the server, listens for incoming webhook notifications from GitHub, and triggers the `deploy.sh` script.  

```python
import subprocess
from flask import Flask, request

app = Flask(__name__)

@app.route('/deploy', methods=['POST'])
def deploy():
    # This runs our deployment script
    subprocess.run(['/var/www/deploy.sh'])
    print("Deployment script executed.")
    return 'Deployment successful!', 200

if __name__ == '__main__':
    # The listener will run on port 9000
    app.run(host='0.0.0.0', port=9000)

```
---
### 📄 License  
Distributed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

