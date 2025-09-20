# Enterprise Cloud Architecture — Redesigned README

> A polished, user-friendly README for a microservices-based enterprise application for educational institutions (Spring Boot + React + multi-cloud ready).

---

## 🚀 Project Overview

**Enterprise Cloud Architecture** is a microservices demo app built for educational institutions.
It demonstrates modern microservices patterns (service separation, independent data stores, file/media service), local developer ergonomics, and deployment-ready configuration for cloud providers (AWS & GCP).

## Student Details 

* **Name** : Nipun Nishamaheeka
* **Student Registration Number** : 2301682067
* **Email Address** : nishamaheeka123@gmail.com

**Key services**

* **Course Service** — Spring Boot + MySQL (Port **8081**)
* **Student Service** — Spring Boot + MongoDB (Port **8082**)
* **Media Service** — Spring Boot (file uploads) (Port **8083**)
* **Frontend** — React + TypeScript (Vite + Material-UI) (Port **5173**)

**Demo video:** [Watch Project](https://drive.google.com/file/d/1zXF4KWs9aC6JhPt21ojF6yKspi7632G4/view?usp=sharing)

---

## 🧰 Technology Stack

* **Backend:** Spring Boot 3.5.5, Java 21, Maven
* **Frontend:** React 18, TypeScript, Vite, Material-UI
* **Datastores:** MySQL (relational), MongoDB (document)
* **Cloud:** Prepared configs for AWS & GCP
* **Build & Run:** Maven, npm/yarn, option to use Docker

---

## ⚙️ Prerequisites

Make sure you have the following installed:

* Java 21 (JDK 21)
* Node.js 18+
* Maven 3.8+
* MySQL server
* MongoDB
* (Optional) Docker & Docker Compose

---

## 📥 Clone repository

```bash
git clone https://github.com/nipunnishamaheeka/Enterprise-Cloud-Architecture.git
cd Enterprise-Cloud-Architecture
```

---

## 🗄️ Database Setup

### MySQL (Course Service)

```sql
CREATE DATABASE eca_courses;
CREATE USER 'eca_user'@'localhost' IDENTIFIED BY 'eca_password';
GRANT ALL PRIVILEGES ON eca_courses.* TO 'eca_user'@'localhost';
FLUSH PRIVILEGES;
```

Update `course-service/src/main/resources/application.properties` (or `application.yml`) with the DB credentials and URL if needed.

### MongoDB (Student Service)

Start MongoDB on a custom port (example: 16000):

```bash
mongod --port 16000 --dbpath /path/to/your/db
```

Update `student-service` Spring properties to point to the correct host/port.

---

## ▶️ Start Locally (Recommended developer flow)

### 1. Build backend services

```bash
# From repo root (build all modules)
mvn clean install -DskipTests
```

### 2. Start each backend in its own terminal

```bash
# Terminal 1 - Course Service
cd course-service
mvn spring-boot:run

# Terminal 2 - Student Service
cd ../student-service
mvn spring-boot:run

# Terminal 3 - Media Service
cd ../media-service
mvn spring-boot:run
```

### 3. Start frontend

```bash
# Terminal 4
cd frontend-app
npm install
npm run dev
```

### 4. Access endpoints

* Frontend: `http://localhost:5173`
* Course Service API: `http://localhost:8081`
* Student Service API: `http://localhost:8082`
* Media Service API: `http://localhost:8083`

---

## 🐳 Docker (optional)

You can containerize each service and run them with Docker Compose. *(Example docker-compose snippet — adapt as needed)*

```yaml
version: '3.8'
services:
  mysql:
    image: mysql:8
    environment:
      MYSQL_DATABASE: eca_courses
      MYSQL_USER: eca_user
      MYSQL_PASSWORD: eca_password
      MYSQL_ROOT_PASSWORD: root_password
    ports:
      - "3306:3306"
    volumes:
      - mysql-data:/var/lib/mysql

  mongo:
    image: mongo:6
    ports:
      - "16000:27017"
    volumes:
      - mongo-data:/data/db

  course-service:
    build: ./course-service
    ports:
      - "8081:8081"
    depends_on:
      - mysql

  student-service:
    build: ./student-service
    ports:
      - "8082:8082"
    depends_on:
      - mongo

  media-service:
    build: ./media-service
    ports:
      - "8083:8083"

volumes:
  mysql-data:
  mongo-data:
```

Run with:

```bash
docker compose up --build
```

---

## ☁️ Cloud & Deployment Notes

This repo includes deployment-ready configuration starters for **AWS** and **GCP**. Suggested deployment pathways:

* **Kubernetes (EKS / GKE):** Containerize services, create deployments + services, use PersistentVolumes for DBs or managed DB services (RDS / Cloud SQL).
* **Managed DBs:** Use AWS RDS (MySQL) and MongoDB Atlas (or GCP Cloud MongoDB / managed options).
* **CI/CD:** Use GitHub Actions to build images and push to ECR/GCR, then trigger k8s deployment updates.

> Tip: Keep environment-specific configuration outside of the JAR (use config server or environment variables / secrets manager).

---

## 🔧 Configuration & Environment Variables

Each service should accept configuration via environment variables. Example variables:

**Course Service**

```
SPRING_DATASOURCE_URL=jdbc:mysql://<host>:3306/eca_courses
SPRING_DATASOURCE_USERNAME=eca_user
SPRING_DATASOURCE_PASSWORD=eca_password
```

**Student Service**

```
SPRING_DATA_MONGODB_URI=mongodb://localhost:16000/eca_students
```

**Media Service**

```
MEDIA_STORAGE_PATH=/data/media
MAX_FILE_SIZE=10MB
```

**Frontend**

```
VITE_API_BASE_URL=http://localhost:8081
VITE_STUDENT_API=http://localhost:8082
VITE_MEDIA_API=http://localhost:8083
```

---

## 🧭 Project Structure

```
Enterprise-Cloud-Architecture/
├── course-service/          # Course management microservice (MySQL)
├── student-service/         # Student management microservice (MongoDB)
├── media-service/           # File/media service
├── frontend-app/            # React + TypeScript frontend
├── docker-compose.yml       # Optional local multi-container setup
├── pom.xml                  # Parent Maven configuration
└── README.md
```

---

## ✅ Features & Patterns Demonstrated

* Microservices separation of concerns
* Independent data stores per service (polyglot persistence)
* RESTful APIs & standard CRUD operations
* File uploads + static/media handling service
* Local development with Maven and Vite
* Dockerization and cloud deployment scaffolding

---

## 🧪 Tests

Add unit/integration tests per service (JUnit, Spring Boot Test). CI pipeline should run `mvn test` and frontend checks (`npm test` / `npm run build`).

---

## 🤝 Contributing

Contributions are welcome! Suggested workflow:

1. Fork the repo
2. Create a feature branch: `git checkout -b feat/your-feature`
3. Commit changes and open a PR to `main`
4. Provide clear changelog and test coverage

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file.

---

## 👤 Author

**Nipun Nishamaheeka**

* GitHub: [@nipunnishamaheeka](https://github.com/nipunnishamaheeka)

---

## 📝 Quick Start (one-minute copy-paste)

```bash
git clone https://github.com/nipunnishamaheeka/Enterprise-Cloud-Architecture.git
cd Enterprise-Cloud-Architecture
# Build all services
mvn clean install -DskipTests
# Start each service in separate terminals
cd course-service && mvn spring-boot:run
cd ../student-service && mvn spring-boot:run
cd ../media-service && mvn spring-boot:run
# Frontend
cd ../frontend-app
npm install && npm run dev
```

---
