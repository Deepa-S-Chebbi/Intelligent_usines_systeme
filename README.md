Predictive Maintenance

Predictive maintenance platform integrating ML/DL, Data Mining (KNIME), and Microservices Architecture for anomaly detection and Remaining Useful Life (RUL) prediction of industrial equipment.

🎯 Overview

This platform combines 3 academic modules into a complete solution:

ML & DL: RUL prediction models (LSTM, XGBoost) and anomaly detection (Isolation Forest, Autoencoders)
Data Mining: Exploratory analysis using KNIME Analytics Platform
Microservices Architecture: Distributed system using Spring Boot, FastAPI, Docker, and Kubernetes

Dashboard interface
Anomaly detection functionality
Real-time RUL predictions
Service orchestration
🏗️ System Architecture
Data Flow
IIoT Ingestion → Preprocessing → Feature Extraction
                                      ↓
                    Anomaly Detection + RUL Prediction
                                      ↓
                    Maintenance Orchestrator
                                      ↓
                       Factory Dashboard (React + GIS)
7 Microservices
IIoT-Ingestion (Spring Boot): Collects data from PLC/SCADA systems through OPC UA, Modbus, and MQTT
Preprocessing (FastAPI): Data cleaning, normalization, and validation
Feature-Extraction (FastAPI): Calculates time-domain and frequency-domain features
Anomaly-Detection (FastAPI + ML): Real-time anomaly detection using Isolation Forest and Autoencoders
RUL-Prediction (FastAPI + ML): Estimates Remaining Useful Life using LSTM and XGBoost
Maintenance-Orchestrator (Spring Boot): Optimizes and schedules maintenance interventions
Factory-Dashboard (React + FastAPI): Real-time interface with GIS-based visualizations
Infrastructure
Messaging: Apache Kafka (Zookeeper)
Databases: PostgreSQL (TimescaleDB), InfluxDB, MinIO (S3-compatible)
Cache: Redis
Monitoring: Prometheus, Grafana (optional)
Tools: Kafka UI, pgAdmin, OPC UA Simulator (optional)
📊 Dataset

NASA C-MAPSS (Commercial Modular Aero-Propulsion System Simulation)

21 sensors
3 engine operating settings
4 degradation scenarios
CSV format
🚀 Installation and Setup
Prerequisites
Docker & Docker Compose (version 3.8+)
Git
8 GB RAM minimum (16 GB recommended)
Available ports: 3000, 4840, 5050, 5432, 6379, 8080–8091, 9000–9001, 9092–9093
Installation
1. Clone the Repository
git clone https://github.com/Kazaz-Mohammed/usines_intelligentes.git
cd usines_intelligentes
2. Configure Environment Variables
# Copy the example environment file
cp env.example .env

# Edit .env with your values (optional, default values are available)
# POSTGRES_DB=predictive_maintenance
# POSTGRES_USER=pmuser
# POSTGRES_PASSWORD=pmpassword
# MINIO_ROOT_USER=minioadmin
# MINIO_ROOT_PASSWORD=minioadmin
# INFLUXDB_TOKEN=pm-token-change-in-production
3. Initialize the Infrastructure
# Windows PowerShell
.\scripts\init-kafka-topics.ps1
.\scripts\init-minio-buckets.ps1

# Linux/Mac
chmod +x scripts/*.sh
./scripts/init-kafka-topics.sh
./scripts/init-minio-buckets.sh
4. Start All Services
# Start infrastructure and services
docker-compose up -d

# Check service status
docker-compose ps

# View logs
docker-compose logs -f
5. Start with Development Tools

To start additional development tools such as Kafka UI, pgAdmin, and the OPC UA Simulator:

docker-compose --profile tools up -d
🌐 Service Access
Dashboard Frontend: http://localhost:3000
Dashboard Backend API: http://localhost:8091
Kafka UI: http://localhost:8080 (if enabled with --profile tools)
pgAdmin: http://localhost:5050 (if enabled with --profile tools)
MinIO Console: http://localhost:9001 (minioadmin/minioadmin)
OPC UA Simulator: opc.tcp://localhost:4840 (if enabled)
API Services
IIoT-Ingestion: http://localhost:8081
Preprocessing: http://localhost:8082
Feature-Extraction: http://localhost:8083
Anomaly-Detection: http://localhost:8084
RUL-Prediction: http://localhost:8085
Maintenance-Orchestrator: http://localhost:8087
📁 Project Structure
usines_intelligentes/
├── services/                         # Microservices
│   ├── ingestion-iiot/               # Spring Boot service
│   ├── preprocessing/                # FastAPI service
│   ├── extraction-features/          # FastAPI service
│   ├── detection-anomalies/          # FastAPI + ML service
│   ├── prediction-rul/               # FastAPI + ML service
│   ├── orchestrateur-maintenance/    # Spring Boot service
│   └── dashboard-usine/              # React + FastAPI frontend/backend
├── ml_pipeline/                      # ML training pipeline
│   ├── ml_pipeline_tutorial.ipynb
│   └── saved_models/                 # Trained models
├── data-mining/                      # KNIME workflows
├── datasets/                         # NASA C-MAPSS dataset
├── video/                            # Demonstration video
│   └── demonstrationVideo.mp4
├── infrastructure/                   # Kubernetes configuration and scripts
├── scripts/                           # Utility scripts
├── docs/                             # Technical documentation
├── docker-compose.yml                # Docker Compose configuration
└── README.md                         # Project documentation
🔧 Usage
1. Start the Complete System
docker-compose up -d
2. Check Service Health
# Check all services
docker-compose ps

# Check individual services
curl http://localhost:8081/health
curl http://localhost:8082/health
curl http://localhost:8083/health
curl http://localhost:8084/health
curl http://localhost:8085/health
curl http://localhost:8087/health
curl http://localhost:8091/health
3. Train the ML Models

Refer to ml_pipeline/README.md for model training instructions.

4. Test with the OPC UA Simulator
# Start the OPC UA simulator
docker-compose --profile tools up -d opcua-simulator

# The IIoT-Ingestion service will connect automatically
5. Stop the System
docker-compose down

# Also remove volumes (⚠️ deletes stored data)
docker-compose down -v
🧪 Testing
# Unit tests (inside each service)
cd services/[service-name]

# Python
pytest

# Java
./mvnw test

# Integration tests
docker-compose up -d

# Execute test scripts
# available in the scripts/ directory
📊 Monitoring
Logs: docker-compose logs -f [service-name]
Metrics: Prometheus (if configured)
Visualization: Grafana (if configured)
Kafka Monitoring: Kafka UI at http://localhost:8080
🔒 Security
⚠️ Important: Change all default passwords before deploying to production
Use environment variables to manage secrets
Enable TLS/SSL for service-to-service communication
Configure JWT-based authentication
🛠️ Technologies
Backend
Java: Spring Boot 3.x, Eclipse Milo (OPC UA)
Python: FastAPI, PyTorch, scikit-learn, XGBoost
Machine Learning
Deep Learning: PyTorch, LSTM
Machine Learning: XGBoost, Isolation Forest
Anomaly Detection: Isolation Forest, Autoencoders
Data Mining: KNIME Analytics Platform
Messaging & Databases
Messaging: Apache Kafka
Databases: PostgreSQL, TimescaleDB, InfluxDB
Object Storage: MinIO
Caching: Redis
Frontend
React.js
Next.js
WebSockets
Plotly
Infrastructure & DevOps
Docker
Docker Compose
Kubernetes
Prometheus
Grafana
📝 Documentation
Microservices Architecture Documentation
ML Pipeline
Infrastructure
Scripts
🤝 Contribution

This project was developed as part of an academic project. For questions, suggestions, or contributions, please create an issue on the GitHub repository.
