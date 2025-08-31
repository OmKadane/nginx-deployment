# Nginx Deployment 🚀

A professional static website designed to be served by an Nginx web server, with a deployment workflow powered by Git.

---

### Repository Status & Stats
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![GitHub Issues](https://img.shields.io/github/issues/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment/issues)
[![GitHub Stars](https://img.shields.io/github/stars/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment/network)
[![Repo Size](https://img.shields.io/github/repo-size/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment)
[![Last Commit](https://img.shields.io/github/last-commit/OmKadane/nginx-deployment)](https://github.com/OmKadane/nginx-deployment/commits/main)

### Technologies Used
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)](https://nginx.org/)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)
[![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)](https://git-scm.com/)

---

## 📋 Table of Contents

1.  [About The Project](#ℹ️-about-the-project)
2.  [Built With](#🛠️-built-with)
3.  [Getting Started](#🚀-getting-started)
    * [Prerequisites](#prerequisites)
    * [Deployment](#deployment)
4.  [Features](#✨-features)
5.  [License](#📄-license)

---

## ℹ️ About The Project

This repository contains the source code for a clean, modern, and responsive static website. The primary purpose of this project is to demonstrate a powerful and efficient workflow for web development and deployment using **Nginx** as the web server and **Git** for version control and content synchronization.

This setup is ideal for portfolios, landing pages, and documentation sites where speed, security, and simplicity are top priorities.



---

## 🛠️ Built With

This project was built using fundamental web technologies and server software:

* **HTML5**
* **CSS3**
* **Nginx** (for serving the site)
* **Ubuntu** (as the server environment)
* **Git** (for version control and deployment)

---

## 🚀 Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

Make sure you have the following software installed on your server (or WSL environment):

* **Nginx:** [Installation Guide](https://nginx.org/en/docs/install.html)
* **Git:** [Installation Guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

### Deployment

1.  **Navigate to your web root directory.** On our Ubuntu server setup, this is `/var/www/html`.
2.  **Clone the repository** directly into your web root folder.
    ```sh
    sudo git clone [https://github.com/](https://github.com/)OmKadane/nginx-deployment /var/www/html
    ```
3.  **Configure Nginx** by creating a server block that points to `/var/www/html` as the root.
4.  **Restart Nginx** to apply the configuration.
    ```sh
    sudo systemctl restart nginx
    ```
5.  Visit your server's IP address or `http://localhost` in a browser to see the live site. To update the site, simply `git pull` the latest changes from this repository.

---

## ✨ Features

* **Clean & Modern Design:** A professional layout suitable for any project.
* **Responsive:** Looks great on desktops, tablets, and mobile devices.
* **Optimized for Nginx:** Built to be served quickly and efficiently.
* **Git-Powered Deployment:** Easily update the live site by pushing changes to this repository.

---

## 📄 License

Distributed under the MIT License. See [LICENSE]`LICENSE` file for more information.