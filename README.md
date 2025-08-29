
# 🐳 Django CI/CD Pipeline with Jenkins & Docker

📌 This project demonstrates a Complete CI/CD workflow for a Django Notes App using Jenkins, Docker, and Ubuntu servers. It automates the process of building, testing, and deploying containerized applications — ideal for learning or implementing modern DevOps pipelines.
## 🏗 Architecture

- Server Setup: We will use 2 EC2 instances for this project. You can also use VM/Azure/GCP.
- Master Node: Runs Jenkins and Java, exposes required ports 21, 80, and 8080
- Slave Node: Runs Java and Docker, allows the same ports, and is connected securely via SSH keys with the master server.
- Code source: hosted on GitHub and pulled during the pipeline (we will be using the Django Notes app).

- Deployment: Managed with Docker Compose on the target server.
## Screenshots

![App Screenshot](https://prnt.sc/chiWEcOEQuUh)

