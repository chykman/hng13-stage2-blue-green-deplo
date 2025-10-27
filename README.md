Here’s a reworked version of your Blue-Green Deployment README — it keeps the same meaning but with a refreshed tone, slightly different phrasing, and smoother structure:

---

# 🟦🟩 Blue-Green Deployment with Nginx Automatic Failover

This project showcases a **Blue-Green deployment model** using **Nginx load balancing and health-aware failover** to achieve zero downtime during service disruptions or version switches.

---

## 🌐 Project Summary

* Two identical Node.js application instances — **Blue (primary)** and **Green (standby)** — run as separate containers.
* **Nginx** acts as a smart traffic router, directing all incoming requests to the Blue instance by default.
* If Blue becomes unresponsive or returns errors (timeouts or 5xx codes), Nginx **instantly reroutes** the request to the Green service without users noticing any interruption.
* All client headers and responses are preserved during the switch, ensuring a consistent experience.
* Failover occurs **seamlessly within a single request cycle**.

---

## 🐳 How to Run

### 1️⃣ Start the Stack

Run all containers using Docker Compose:

```bash
docker compose up -d
```

### 2️⃣ Verify Containers

Check that all services are active:

```bash
docker ps
```

### 3️⃣ Test the Active Service

By default, Nginx sends traffic to **Blue**:

```bash
curl -i http://localhost:8080/version
```

### 4️⃣ Simulate a Failure (Trigger Failover)

Cause Blue to throw errors:

```bash
curl -X POST http://localhost:8081/chaos/start?mode=error
```

### 5️⃣ Observe Auto-Failover

Send a request again through Nginx — it will automatically route to Green:

```bash
curl -i http://localhost:8080/version
```

### 6️⃣ Recover the Blue Service

Restore Blue to a healthy state:

```bash
curl -X POST http://localhost:8081/chaos/stop
```

---

## 🧑‍💻 Project Info

* **Author:** Chike Okoro
* **Goal:** Demonstrate **resilient Blue-Green deployments** with **Nginx-based automatic failover** for high availability and zero downtime updates.
* **Tech Stack:** Node.js, Nginx, Docker, Docker Compose

---
