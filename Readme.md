# 🚀 DevOps Intern Assignment – NGINX Reverse Proxy + Docker

This project demonstrates routing two backend services (Golang and Python Flask) through an NGINX reverse proxy using Docker Compose. Each service is containerized with its own Dockerfile, and health checks ensure readiness before traffic routing. NGINX logs all incoming requests with timestamps and path info.

---

## ⚙️ Setup Instructions

• Clone the repository:
```bash
git clone https://github.com/UtkarshKayasth/devops-nginx-reverse-proxy.git
cd devops-nginx-reverse-proxy


• Build and start all services:
```bash
docker-compose up --build

• Test endpoints:

• http://localhost:8080/service1/ping

• http://localhost:8080/service1/hello

• http://localhost:8080/service2/ping

• http://localhost:8080/service2/hello

🔀 How Routing Works:
NGINX listens on port 8080 and routes requests to backend services based on path prefix:

| URL Prefix    | Routed To          |
| ------------- | ------------------ |
| `/service1/*` | Golang (port 8001) |
| `/service2/*` | Flask (port 8002)  |

Examples:
• /service1/hello → returns Go response
• /service2/hello → returns Flask response


🩺 Health Checks:
Docker Compose ensures both services are healthy before NGINX starts. Each service exposes a /ping endpoint.

Example healthcheck used:
healthcheck:
  test: ["CMD-SHELL", "curl -f http://127.0.0.1:8002/ping || exit 1"]
  interval: 10s
  timeout: 3s
  retries: 3
  start_period: 5s

🪵 Logging Clarity:
NGINX logs all incoming requests to its access log with timestamps and request paths.

Example from:
```bash
docker logs nginx_proxy

172.18.0.1 - [24/Jun/2025:21:08:02 +0000] "GET /service1/ping HTTP/1.1" 200
172.18.0.1 - [24/Jun/2025:21:08:06 +0000] "GET /service2/hello HTTP/1.1" 200

🧱 Clean & Modular Docker Setup
• Each service has its own Dockerfile:

• service_1/Dockerfile (Golang)

• service_2/Dockerfile (Python + Flask)

• nginx/Dockerfile (for reverse proxy)

• Docker Compose manages service orchestration and health checks.
• NGINX depends on healthy status of backend services using depends_on.

🏅 Bonus Points Implemented
• ✅ Health checks using /ping
• ✅ NGINX logs all requests (timestamp + path)
• ✅ Clean modular Docker setup
• ✅ Uses bridge networking (no host networking used)
• ✅ All services run via a single docker-compose up --build command




