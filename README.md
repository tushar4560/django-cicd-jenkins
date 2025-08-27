
# 🐳 Django CI/CD Pipeline with Jenkins & Docker

📌 This project demonstrates a Complete CI/CD workflow for a Django Notes App using Jenkins, Docker, and Ubuntu servers. It automates the process of building, testing, and deploying containerized applications — ideal for learning or implementing modern DevOps pipelines.


# 🏗 Architecture



Component	Description
Server Setup	Two Ubuntu servers (AWS / on‑prem) — one acts as Jenkins Master, the other as Jenkins Slave
Master Node	Runs Jenkins, Java, and exposes required ports (21, 80, 8080)
Slave Node	Runs Java, Docker, allows same ports, connected securely via SSH keys
Code Source	Hosted on GitHub and pulled during the pipeline
Deployment	Managed with Docker Compose on the target server


## Lessons Learned

What did you learn while building this project? What challenges did you face and how did you overcome them?


## 🏗 Architecture

- **Server Setup** – Two Ubuntu servers (AWS / on‑prem) — one acts as **Jenkins Master**, the other as **Jenkins Slave**  
- **Master Node** – Runs Jenkins and Java, exposes required ports **21, 80, 8080**  
- **Slave Node** – Runs Java and Docker, allows same ports, connected securely via **SSH keys**  
- **Code Source** – Hosted on **GitHub** and pulled during the pipeline  
- **Deployment** – Managed with **Docker Compose** on the target server  

<img width="1024" height="1536" alt="Image" src="https://github.com/user-attachments/assets/8596772b-e185-4d25-ab7f-1b3f0aa62156" />

## 🔄 CI/CD Pipeline Flow

- **Clone Code** – Pulls the latest code from GitHub  
- **Build Image** – Creates a Docker image for the Django app  
- **Run Tests** – Executes Django unit tests in an isolated container  
- **Auto‑cleanup** – Deletes dangling (untagged) Docker images to keep the environment clean  
- **Deploy** – Uses Docker Compose to run the application on the server

## 📌 Prerequisites

- Two **Ubuntu** servers (Master & Slave)  
- **Jenkins** installed on Master  
- **Java** installed on both nodes  
- **Docker** & **Docker Compose** installed on Slave  
- Open ports: **21, 80, 8080**  
- **SSH key exchange** from Master to Slave  

---

## 🎯 Benefits

- ✅ Fully automated **build → test → deploy** process  
- ✅ **Clean, reproducible** environments  
- ✅ Clear **separation of orchestration and execution**  
- ✅ Ideal for **DevOps learning** and **production setups**  



## Diagram

<img width="1024" height="1536" alt="Image" src="https://github.com/user-attachments/assets/8596772b-e185-4d25-ab7f-1b3f0aa62156" />

