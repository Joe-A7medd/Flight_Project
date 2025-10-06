#  Flight Radar 2024 - Real-Time Flight Tracking Pipeline

This project demonstrates a **real-time flight tracking system** built with a modern data engineering stack.  
It simulates flight data generation, real-time streaming, transformation, storage, and visualization — all containerized with Docker.

---

##  Tools & Technologies

- **Python (Faker)** → Generates fake flight events (Producer)  
- **Apache Kafka** → Streams flight data in real time  
- **Apache Spark (Structured Streaming)** → Processes and transforms streaming data  
- **PostgreSQL** → Stores flight information  
- **Streamlit** → Visualizes flight data on an interactive dashboard  
- **Docker Compose** → Manages all services in containers  

---

## How to Run

1. **Start all containers**
   ```bash
   docker-compose up -d
   ```

2. **Check running services**
   ```bash
   docker ps
   ```

3. **Run the data producer**
   - Open `script/producer.ipynb` in **Anaconda** or **Jupyter Notebook**
   - Execute the cells to generate flight data and publish to Kafka topic `flights`

4. **Monitor Kafka**
   - Go to [http://localhost:8090](http://localhost:8090)  
   - Verify messages are streaming to the `flights` topic

5. **Access PostgreSQL**
   - Open **pgAdmin** → [http://localhost:8085](http://localhost:8085)  
   - Login:
     - Email: `admin@admin.com`  
     - Password: `admin`  

6. **Add a new connection**
   - Server Name: `postgres_general`  
   - Host: `postgres`  
   - Port: `5432`  
   - Username: `admin`  
   - Password: `admin`

7. **Create the database**
   ```sql
   CREATE DATABASE flights_project;
   ```

8. **Create the flights table**
   ```sql
   CREATE TABLE flights (
       flight_id VARCHAR PRIMARY KEY,
       origin TEXT,
       destination TEXT,
       status TEXT,
       departure_time BIGINT,
       arrival_time BIGINT
   );
   ```

9. **Run Spark Streaming**
   - Open the Spark notebook from the `scripts` folder  
   - In Jupyter: [http://localhost:8888](http://localhost:8888)  
   - Install PostgreSQL driver:
     ```bash
     pip install psycopg2-binary
     ```
   - Run the notebook to stream data into PostgreSQL

10. **Launch Streamlit Dashboard**
    ```bash
    streamlit run app.py
    ```
    Then open [http://localhost:8501](http://localhost:8501)  
    Explore **live flight data**, map, and flight status updates.

---

##  Data Flow

```
[ Python Producer (Faker) ]
           ↓
     Kafka Topic: flights
           ↓
   Spark Structured Streaming
           ↓
        PostgreSQL
           ↓
     Streamlit Dashboard
```

---

##  Example Flight Event

```json
{
  "flight_id": "FL2453",
  "origin": [33.9416, -118.4085],
  "destination": [51.4700, -0.4543],
  "status": "Delayed",
  "departure_time": 1695638400,
  "arrival_time": 1695645600
}
```

---

##  Clean Up

To stop all containers and remove volumes:

```bash
docker-compose down -v
```

---

##  Project Info

- **Kafka Topic:** `flights`  
- **Database:** `flights_project`  
- **pgAdmin:** [http://localhost:8085](http://localhost:8085)  
- **Kafka UI:** [http://localhost:8090](http://localhost:8090)  
- **Dashboard:** [http://localhost:8501](http://localhost:8501)  

---

![Image](https://github.com/user-attachments/assets/4e66ca91-20d4-4e38-8923-6f4afc181f68)

##  Project Screenshots

---

###  Kafka UI  

![Kafka UI](https://github.com/user-attachments/assets/3bed8961-cc24-46ce-860e-788b15ab4310)  
> **Image Description:** Kafka UI displaying the real-time messages being streamed into the `flights` topic.  
> *(This confirms that the flight producer is successfully sending live data to Kafka.)*


---

###  PostgreSQL (pgAdmin)  
![PostgreSQL](https://github.com/user-attachments/assets/b5787fa0-5968-4d88-a6b4-4f19f0762d01)  
> **Image Description:** PostgreSQL database `flights_project` displaying the stored flight records in the `flights` table.  
> *(This shows that Spark successfully processed and inserted the data.)*

---

###  Streamlit Dashboard  

![Streamlit Dashboard - Map View](https://github.com/user-attachments/assets/b50ea0f8-b237-48c9-965f-abc50b6b2a4b)  
> **Image Description:** Streamlit dashboard displaying the live flight map, showing each flight’s location and status in real time.  
> *(Visual representation of the active flights streamed through the pipeline.)*

![Streamlit Dashboard - Table View](https://github.com/user-attachments/assets/6389eb5a-65e4-42aa-bc46-0050bc4df510)  
> **Image Description:** Streamlit dashboard showing tabular data of all flights including their origins, destinations, and statuses.  
> *(Demonstrates the structured view of processed data inside the visualization layer.)*

###  Docker Setup  

![Docker Compose Overview](https://github.com/user-attachments/assets/6bd320b4-0a24-41f3-89bd-64bd883632bc)  
> **Image Description:** Overview of Docker Compose environment showing all active containers — Kafka, Spark, PostgreSQL, and Streamlit — working together.  

![Running Containers](https://github.com/user-attachments/assets/3e60d7b2-4fa6-4cea-be74-f94e73ca4cd0)  
> **Image Description:** Docker Desktop showing running containers for each service in the Flight Radar 2024 pipeline.  
> *(Demonstrates that all components are successfully deployed and running in containers.)*
