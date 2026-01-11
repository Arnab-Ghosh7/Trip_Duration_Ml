# NYC Taxi Trip Duration Prediction

![Python](https://img.shields.io/badge/Python-3.7%2B-blue?logo=python&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![DVC](https://img.shields.io/badge/DVC-945DD6?logo=dvc&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?logo=amazon-aws&logoColor=white)

A Machine Learning project design to predict the total duration of taxi trips in New York City. This repository contains the complete pipeline from data processing to model serving.

## Project Overview

## Project Overview



### Key Features

*   **Data Version Control (DVC)**: Manages data and model pipelines, ensuring reproducibility.
*   **Modular Codebase**: Organized source code for features, models, and data processing.
*   **Automated Workflow**: `Makefile` support for common tasks like setup, training, and linting.
*   **API Serving**: `FastAPI` application to serve model predictions.
*   **Containerization & Deployment**: Docker support and Kubernetes configurations (Seldon Core) for scalable deployment.

## Directory Structure

```text
├── .dvc/               # DVC configuration
├── .github/            # GitHub workflows/actions
├── data/               # Data directory (raw, processed)
├── docs/               # Project documentation
├── notebooks/          # Jupyter notebooks for experimentation
├── src/                # Source code
│   ├── data/           # Data generation scripts
│   ├── features/       # Feature engineering scripts
│   ├── models/         # Model training and prediction scripts
│   └── visualization/  # Visualization scripts
├── models.dvc          # DVC file for models
├── dvc.yaml            # DVC pipeline definition
├── params.yaml         # Training parameters
├── service.py          # FastAPI application entry point
├── requirements.txt    # Python dependencies
├── Dockerfile          # Docker configuration
├── Makefile            # Automation commands
└── README.md           # Project documentation
```

## Prerequisites

*   Python 3.7+
*   Pip
*   Docker (optional, for containerization)
*   Minikube/Kubernetes (optional, for deployment)

## Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Arnab-Ghosh7/Trip_Duration_Ml
    cd Trip_Duration_Ml
    ```

2.  **Create a virtual environment (Recommended):**
    ```bash
    # Using venv
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install dependencies:**
    ```bash
    make requirements
    # OR
    pip install -r requirements.txt
    ```

## Usage

### 1. Data Pipeline & Training
The project uses DVC to manage the pipeline defined in `dvc.yaml`.

*   **Run the entire pipeline (build features, train model):**
    ```bash
    dvc repro
    ```
    This command checks dependencies and runs necessary stages defined in `dvc.yaml`.

*   **Train manually (if needed):**
    ```bash
    python src/models/train_model.py data/processed/
    ```

### 2. Running the API
Start the FastAPI server to make predictions.

```bash
python service.py
# OR
uvicorn service.py:app --host 0.0.0.0 --port 8080
```
The API will be available at `http://localhost:8080`.

### 3. API Endpoints

*   **GET /**: Health check. Returns "Working fine".
*   **POST /predict**: Make a prediction.

**Request Body Example:**
```json
{
  "vendor_id": 2,
  "pickup_datetime": 1451616000,
  "passenger_count": 1,
  "pickup_longitude": -73.9817,
  "pickup_latitude": 40.7213,
  "dropoff_longitude": -73.9388,
  "dropoff_latitude": 40.7694,
  "store_and_fwd_flag": 0
}
```

## Deployment

The project includes configurations for deploying with **Seldon Core** on Kubernetes.

1.  **Build Docker Image:**
    ```bash
    docker build -t trip-duration:v1 .
    ```

2.  **Deploy to Kubernetes:**
    ```bash
    kubectl apply -f seldon_deployment.yaml
    ```

## Development Commands

Use the `Makefile` for common development tasks:

*   `make requirements`: Install dependencies.
*   `make clean`: Remove compiled Python files.
*   `make lint`: Run flake8 linting.
*   `make sync_data_to_s3`: Sync data to S3 bucket.
*   `make sync_data_from_s3`: Download data from S3 bucket.


## License

MIT License


## Author

**Arnab Ghosh**
