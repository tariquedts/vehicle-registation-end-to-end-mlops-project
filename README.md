
# Vehicle Registration Rrediction and MLOps Pipeline 🚗📊🚀

This repository contains a complete end-to-end Machine Learning pipeline for a **Vehicle Registration Prediction**, integrated with **MongoDB**, **AWS**, and **CI/CD using GitHub Actions and Docker**. It includes data ingestion, validation, transformation, model training, evaluation, deployment, and a web-based prediction app hosted on an EC2 instance.

---

## 📁 Project Structure

```bash
├── src/                      # Source code directory
├── notebook/                 # Jupyter notebooks (EDA, MongoDB, etc.)
├── entity/                   # Config and artifact entity classes
├── components/               # Data pipeline components
├── configuration/            # Config modules (MongoDB, AWS)
├── aws_storage/              # AWS S3 interactions
├── templates/                # HTML templates for frontend
├── static/                   # Static files (CSS, JS, etc.)
├── app.py                    # Flask app for inference
├── demo.py                   # Main script for testing
├── requirements.txt          # Python dependencies
├── pyproject.toml            # Project metadata and build system
├── setup.py                  # For installing local modules
├── .github/workflows/        # GitHub Actions workflows (CI/CD)
├── Dockerfile                # Docker build configuration
├── .dockerignore             # Docker ignore rules
├── .gitignore                # Git ignore rules
└── README.md                 # Project documentation
````

---

## 🔧 Setup Instructions

### 1. Initial Project Setup

* Run `template.py` to initialize folder structure.
* Configure `setup.py` and `pyproject.toml` to enable local module imports.
* Refer to `crashcourse.txt` for details on packaging setup.

### 2. Virtual Environment & Dependencies

```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
pip install -r requirements.txt
pip list  # Confirm installed packages
```

---

## 📦 MongoDB Integration (MongoDB Atlas)

1. Create a MongoDB Atlas account and a new project.
2. Deploy an M0 cluster and create DB user credentials.
3. Add IP address `0.0.0.0/0` under **Network Access**.
4. Copy connection string from "Connect > Drivers > Python".
5. Create `notebook/mongoDB_demo.ipynb` to push sample data.
6. Verify data on MongoDB Atlas under **Browse Collections**.

---

## 🧾 Logging & Exception Handling

* `logger.py` and `exception.py` modules are created and tested using `demo.py`.
* EDA and Feature Engineering notebooks are included in the `notebook/` folder.

---

## 📥 Data Ingestion Module

* Define constants and configuration in:

  * `constants/__init__.py`
  * `configuration/mongo_db_connections.py`
  * `data_access/proj1_data.py`
  * `entity/config_entity.py` and `artifact_entity.py`
  * `components/data_ingestion.py`
* Run `demo.py` to test data ingestion after setting MongoDB URL.

> 🧠 Set MongoDB URL as Environment Variable:

```bash
# Bash
export MONGODB_URL="your-mongodb-url"
# PowerShell
$env:MONGODB_URL="your-mongodb-url"
```

---

## ✅ Data Validation, Transformation, and Training

* Define data schema in `config/schema.yaml`.
* Implement:

  * `components/data_validation.py`
  * `components/data_transformation.py`
  * `components/model_trainer.py`
* Add logic to `utils/main_utils.py` and `entity/estimator.py`.

---

## ☁️ AWS Configuration (for Model Evaluation & Deployment)

* Create IAM User with `AdministratorAccess`.
* Create AWS S3 bucket: `my-model-mlopsproj`.
* Store credentials in environment variables:

```bash
export AWS_ACCESS_KEY_ID="..."
export AWS_SECRET_ACCESS_KEY="..."
```

* Update `constants/__init__.py` with:

```python
MODEL_EVALUATION_CHANGED_THRESHOLD_SCORE = 0.02
MODEL_BUCKET_NAME = "my-model-mlopsproj"
MODEL_PUSHER_S3_KEY = "model-registry"
```

* Add `src/aws_storage/` and `entity/s3_estimator.py` for S3 operations.

---

## 📊 Model Evaluation & Pushing

* Implement Model Evaluation and Pusher components.
* Connect trained model to S3 bucket for versioning and retrieval.

---

## 🌐 Web App for Prediction

* Build Flask API in `app.py`
* Add routes for `/training` and prediction
* Setup frontend using `templates/` and `static/` directories.

---

## 🚀 CI/CD Deployment Pipeline

### 1. Docker & GitHub Actions

* Create Dockerfile and `.dockerignore`.
* Add GitHub Actions workflow in `.github/workflows/aws.yaml`.

### 2. AWS ECR & EC2

* Create IAM user (`usvisa-user`) and download credentials.
* Create ECR repository: `vehicleproj`.
* Launch EC2 instance (Ubuntu, t2.medium, 30GB).
* Install Docker:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```

### 3. Connect EC2 to GitHub as Runner

* Go to GitHub > Settings > Actions > Runners
* Follow steps to register EC2 as a self-hosted runner.

### 4. Add GitHub Secrets

| Secret Key               | Value (From AWS)           |
| ------------------------ | -------------------------- |
| AWS\_ACCESS\_KEY\_ID     | `<your-access-key-id>`     |
| AWS\_SECRET\_ACCESS\_KEY | `<your-secret-access-key>` |
| AWS\_DEFAULT\_REGION     | `us-east-1`                |
| ECR\_REPO                | `vehicleproj`              |

---

## 🌐 Launching the App on EC2

1. Add rule to Security Group to allow TCP on port `5080`.
2. Access the app at:

```
http://<ec2-public-ip>:5080
```

---

## 🧠 Features Summary

* ✅ Modular, production-grade MLOps pipeline
* ✅ MongoDB Atlas for NoSQL data storage
* ✅ AWS S3 for model storage/versioning
* ✅ Docker & GitHub Actions CI/CD setup
* ✅ EC2 hosting for web app with live inference
* ✅ Fully reproducible environment with proper version control

---

## 📌 TODOs

* [ ] Add unit tests
* [ ] Implement monitoring tools (e.g., Prometheus/Grafana)
* [ ] Setup model registry (e.g., MLflow)
* [ ] Add streamlit/Gradio alternative interface

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!
Feel free to open a pull request or raise an issue.

---

## 📄 License

This project is licensed under the MIT License.
See the [LICENSE](LICENSE) file for more details.

```

---

Let me know if you'd like to customize it further — e.g., add badges, code examples, or Docker usage guide.
```
