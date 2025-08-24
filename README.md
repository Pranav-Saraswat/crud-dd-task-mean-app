# MEAN CRUD App: Setup, Containerization & Deployment

## Project Overview

A full-stack MEAN (MongoDB, Express, Angular, Node.js) CRUD application, containerized and deployed using Docker Compose, with automated CI/CD via GitHub Actions.

---
### Setup
```bash
git clone https://github.com/Pranav-Saraswat/crud-dd-task-mean-app.git
cd crud-dd-task-mean-app
```

### Build Images

```bash
# Backend
docker build -t pranavs24/mean-backend ./backend

# Frontend
docker build -t pranavs24/mean-frontend ./frontend
```

### Push Images

```bash
docker login
docker push pranavs24/mean-backend
docker push pranavs24/mean-frontend
```

---

## Deployment

1. **Set up Ubuntu VM** 
2. **Install Docker & Docker Compose**
	 ```bash
	 sudo apt update
	 sudo apt install docker.io docker-compose -y
	 ```

3. **Clone Repository on VM**
	 ```bash
	 git clone https://github.com/Pranav-Saraswat/crud-dd-task-mean-app.git
	 cd crud-dd-task-mean-app
	 ```

4. **Edit `docker-compose.yml`**  

```yaml
version: "3.9"

services:
  mongo:
    image: mongo:6
    container_name: mongo
    restart: unless-stopped
    ports:
      - "27017:27017"
    volumes:
      - /app/mongo_data:/data/db

  backend:
    image: docker.io/pranavs24/mean-backend:latest
    container_name: backend
    restart: unless-stopped
    ports:
      - "8080:8080"
    environment:
      - NODE_ENV=production
      - MONGO_URL=mongodb://mongo:27017/dd_db
    depends_on:
      - mongo

  frontend:
    image: docker.io/pranavs24/mean-frontend:latest
    container_name: frontend
    restart: unless-stopped
    ports:
      - "80:80"
    depends_on:
      - backend

volumes:
  mongo_data:
```

5. **Start the Application**
	 ```bash
	 docker-compose up -d
	 ```

---




## Accessing the Application

- Open your VM’s public IP in a browser: `http://74.226.208.219/`
- The app is available on port 80.

---

### Screenshots

Below are screenshots demonstrating the application's features:

#### Home Page
![Home](screenshots/home.png)

#### Add Tutorial
![Add Tutorial](screenshots/add.png)

#### Add Success
![Add Success](screenshots/add_sucess.png)

#### Edit Tutorial
![Edit Tutorial](screenshots/edit.png)

#### Home After Add
![Home After Add](screenshots/home_after_add.png)

#### Home After Delete
![Home After Delete](screenshots/home_after_delete.png)

