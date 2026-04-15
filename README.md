# FastAPI DevOps Assignment

## Project Overview

This project is a simple FastAPI application where users can be added and fetched using APIs.
The goal of this assignment was to:

* Dockerize the application
* Run it using docker-compose
* Ensure data persistence without a database
* Create a Jenkins pipeline for deployment
* Set up monitoring using Prometheus and Grafana

---

## API Endpoints

* `GET /` → Returns a hello message
* `GET /users` → Returns list of users
* `POST /users` → Adds a new user

Swagger UI:

```
http://localhost:8000/docs
```

---

## Running the Application

```bash
docker compose up --build
```

To stop:

```bash
docker compose down
```

---

## Data Persistence

User data is stored in a `users.json` file.

I used Docker volume mapping:

```
./app/data:/app/app/data
```

### How I verified persistence:

1. Added a user using `/docs`
2. Stopped the container
3. Started it again
4. Checked `/users` → data was still there

---

## Jenkins Pipeline

I created a Jenkins pipeline to automate deployment.

### What it does:

* Pulls code from GitHub
* Stops existing containers
* Builds the Docker image
* Runs the application using docker-compose
* Performs a basic health check

---

## Monitoring

I used:

* Prometheus
* Grafana
* Blackbox Exporter

Since I couldn’t modify the application code, I used blackbox exporter to monitor the API externally.

---

## Monitoring URLs

* Prometheus → http://localhost:9090
* Grafana → http://localhost:3000

Grafana login:

```
admin / admin
```

---

## Metrics Used

* `probe_success` → checks if app is up
* `probe_duration_seconds` → response time
* uptime and failure count using Prometheus queries

---

## Notes

* No database is used, only JSON file
* Data persists even after container restart
* Everything runs using Docker containers

---

## Author

Niraj Vishwakarma

