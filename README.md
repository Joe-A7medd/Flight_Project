#  Real-Time Flight Tracking System (Flight Radar 2024)

A **modern real-time flight tracking pipeline** built with a full data engineering stack.  
It simulates live flight data — generated, streamed, processed, stored, and visualized — all in one system.

---

## Project Overview

This project demonstrates how **streaming data pipelines** work in real-world scenarios.  
Fake flight data is produced in real time, passed through **Kafka**, processed using **Spark**, stored in **PostgreSQL**, and finally visualized through a **Streamlit dashboard**.

---

##  Tech Stack

| Component | Purpose |
|------------|----------|
|  **Python (Faker)** | Generate synthetic flight data |
|  **Apache Kafka** | Real-time message streaming |
|  **Apache Spark (Structured Streaming)** | Data processing and transformation |
|  **PostgreSQL** | Store processed flight information |
|  **Streamlit** | Display live dashboard and flight map |
|  **Docker Compose** | Manage all services in containers |

---

##  System Architecture


![Image](https://github.com/user-attachments/assets/4e66ca91-20d4-4e38-8923-6f4afc181f68)

---

##  Getting Started

### 1. Launch the Environment
```bash
docker-compose up -d
