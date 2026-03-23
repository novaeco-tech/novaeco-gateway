# ⛩️ NovaEco Gateway

![Component ID](https://img.shields.io/badge/ID-GATEWAY-orange)
![Layer](https://img.shields.io/badge/Layer-Infrastructure-blue)
![Type](https://img.shields.io/badge/Type-Reverse_Proxy-green)

> **The Front Door of the Digital Commons.**
> A unified, multiplexed interface that routes public traffic to internal circular economy microservices (Balance, Policy, IoT Ingest).

## 📖 Overview

The **NovaEco API Gateway** is the single entry point for all external clients (Web Dashboards, Mobile Apps, and IoT Worker Nodes). It acts as a **Hybrid Server**, enforcing security and handling routing for both standard web traffic and high-throughput environmental telemetry agents.

* **Role:** Reverse Proxy, Orchestrator, Health Aggregator, and Security Perimeter.
* **Protocol:** Multiplexed HTTP/1.1 (REST) & HTTP/2 (gRPC).
* **Ports:**
    * `443/8000`: Public HTTP Ingress (REST / Proxy).
    * `50051`: Internal Management Interface (gRPC).
* **Auth:** Validates Bearer Tokens via the internal `novaeco-auth` verifier before routing.

---

## ⚠️ Architectural Migration Notice (V2)

**This repository is part of the NovaEco v2 Polyrepo Architecture.**
Active development and migration from the legacy v1 prototype into this dedicated infrastructure component is scheduled for **Q2/Q3 2026**. 

---

## 🌟 Key Capabilities (Target Architecture)

### 1. Protocol Multiplexing
Accepts both REST/JSON payloads for Web Clients (e.g., Municipal Dashboards) and gRPC frames for high-throughput worker nodes (e.g., IoT environmental sensors) over a unified ingress point.

### 2. Zero-Trust Context Injection
Validates identities externally and propagates trusted `x-user-id` and `x-user-role` headers to the internal service mesh. This prevents downstream domain enablers (like `novaeco-balance` or `novaeco-policy`) from having to parse raw JWTs, ensuring strict isolation of concerns.

### 3. Dynamic Payload Compression
To minimize data transfer energy and bandwidth costs (aligning with Green Software principles), the Gateway intercepts all REST API responses. If the payload exceeds 1KB, the Gateway compresses the data (GZIP/Brotli) on the fly before routing it to the public internet.

### 4. RBAC & Policy Enforcement
Acts as the Policy Enforcement Point (PEP) for the ecosystem. The Gateway intercepts requests and rejects them (`403 Forbidden`) if the user or worker node lacks the required Role-Based Access Control (RBAC) permissions to mutate environmental ledger states.

---

## 🤝 Contributing

We welcome contributors to help build the open-source infrastructure for the circular economy. 

Please see the central [**NovaEco Organization README**](https://github.com/novaeco-tech) for our overall contribution guidelines, Code of Conduct, and ecosystem roadmap.

## 📄 License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for details.
