# django-docker-deploy

A portfolio project to deploy a **Django** app using **Docker**, with PostgreSQL, Redis, and Nginx.  
Designed for real-world deployment on cloud servers like **DigitalOcean**, **Hetzner**, or **AWS**.

---

## 🔧 Technologies Used

- **Django** – main backend framework  
- **PostgreSQL** – relational database  
- **Redis** – caching layer  
- **Gunicorn** – WSGI HTTP server  
- **Nginx** – reverse proxy  
- **Docker & Docker Compose** – containerization and orchestration  
- **UFW + Fail2Ban** – basic server security  

---

## 📁 Project Structure

- `docker-compose.yml` – service definitions  
- `nginx/nginx.conf` – Nginx reverse proxy settings  
- `web/Dockerfile` – image definition for Django app  
- `web/requirements.txt` – Python dependencies  
- `web/` – Django source code structure  
- `docs.pdf` – 📄 deployment & security documentation  

---

## 🐳 Services (Docker Compose)

| Service  | Role             | Notes                     |
|----------|------------------|---------------------------|
| `web`    | Django app       | Exposed at `:8000`        |
| `db`     | PostgreSQL       | Internal only             |
| `redis`  | Redis cache      | Internal only             |
| `nginx`  | Reverse proxy    | Exposed at `:80`          |

---

## 🔐 Security Practices

Basic hardening for Ubuntu 22.04+:

- Enable UFW and open only necessary ports (22, 80, 443)  
- Use **Fail2Ban** to block brute-force attacks  
- Disable root SSH login  
- Change default SSH port  
- Use SSH keys instead of passwords  
- Use HTTPS with **Let’s Encrypt + Certbot**

---

## 🚀 Deployment Guide

1. SSH into your cloud server:

    ```bash
    ssh your_user@your_server_ip
    ```

2. Install Docker:

    ```bash
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh
    ```

3. Transfer files to the server:

    ```bash
    scp -r ./project_folder your_user@your_server_ip:/home/your_user/
    ```

4. Run the app:

    ```bash
    cd project_folder
    docker-compose up --build -d
    ```

5. Visit your app:

    http://your_server_ip

---

## ✅ Requirements (web/requirements.txt)

```txt
Django>=4.0
gunicorn
psycopg2-binary
redis
