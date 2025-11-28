# MEAN Stack CRUD Application – Dockerized + CI/CD (GitHub Actions)

This project is a fully containerized **MEAN Stack CRUD application** that uses:

* **MongoDB** — Database
* **Express + Node.js** — Backend API
* **Angular** — Frontend UI
* **Nginx** — Reverse Proxy
* **Docker & Docker Compose** — Deployment
* **GitHub Actions** — CI/CD pipeline
* **Docker Hub** — Container registry

Everything runs locally using **Docker Desktop as the VM**.

---

## 🗂️ Project Structure

```
.
├── docker-compose.yml
├── nginx.conf
├── my_readme.md
│
├── backend/
│   ├── Dockerfile
│   ├── package.json
│   └── app/
│       ├── config/db.config.js
│       ├── controllers/
│       ├── models/
│       └── routes/
│
└── frontend/
    ├── Dockerfile
    ├── angular.json
    └── src/
```

---

## 🚀 How to Run the Project (Deployment on Docker Desktop)

Make sure Docker Desktop is running.

### **Start all services**

```
docker compose up --build
```

### **Stop everything**

```
docker compose down
```

### **After CI/CD pushes new images → pull & redeploy**

```
docker compose pull
docker compose up -d
```

Then open the app:

👉 [http://localhost](http://localhost)

---

## 🧱 Service Breakdown

### **1. Frontend (Angular + Nginx)**

* Angular is built using Node
* Served through Nginx
* Calls backend using `/api/...`
* Runs on **port 80**

### **2. Backend (Node + Express)**

* Exposes REST API for CRUD operations
* Connects to MongoDB inside Docker network
* Connection string:

```
mongodb://root:example@mongo:27017/mean-db?authSource=admin
```

### **3. MongoDB**

* Official Mongo image
* Persistent storage via Docker volume
* Credentials:

  * Username: root
  * Password: example

### **4. Nginx Reverse Proxy**

Routes:

* `/` → Angular frontend
* `/api/*` → Backend container

Makes entire app accessible on a single port.

---

## 🐳 CI/CD Pipeline (GitHub Actions)

Pipeline file is located at:

```
.github/workflows/docker-build.yml
```

### **What the pipeline does**

* Runs automatically on each push to `main`
* Builds backend Docker image
* Builds frontend Docker image
* Logs into Docker Hub
* Pushes both images to your Docker Hub account

### **Images pushed**

* `your-dockerhub-username/mean-backend:latest`
* `your-dockerhub-username/mean-frontend:latest`

This completes the CI/CD requirement.

---

## 🧪 Testing the Application

Open:

👉 [http://localhost](http://localhost)

From the UI you can:

* Add a tutorial
* Edit a tutorial
* Delete a tutorial
* View tutorial details

All operations work through the Express API with MongoDB storage.

---

## 📸 Screenshots Required (for Submission)

Your professor will expect these:

1. **Docker Desktop dashboard**

   * mongo
   * backend
   * frontend
   * nginx

2. **Web UI working** (`http://localhost`)

3. **GitHub Actions pipeline (green successful run)**

4. **Docker Hub repository pages**

   * mean-frontend
   * mean-backend

5. **Terminal screenshot of:**

```
docker compose up
```

6. **Project structure screenshot in VS Code**

7. **nginx.conf screenshot**

This completes documentation proof.

---

## 🧩 Architecture Diagram (Simple)

```
         ┌────────────┐
         │  Angular    │
         │  Frontend   │
         └──────┬──────┘
                │  (localhost:80)
        ┌───────▼────────┐
        │     Nginx       │
        └───────┬────────┘
                │ /api/*
        ┌───────▼─────────┐
        │   Backend API    │
        │  (Express/Node)  │
        └───────┬─────────┘
                │
        ┌───────▼─────────┐
        │    MongoDB       │
        └──────────────────┘
```

---

## 🏁 Conclusion

This project demonstrates complete understanding of:

* MEAN Stack architecture
* Docker containerization
* Multi-service orchestration using Docker Compose
* MongoDB integration
* Nginx reverse proxy setup
* Automated CI/CD using GitHub Actions
* Deployment using Docker Desktop as a Linux VM substitute


# END OF README
