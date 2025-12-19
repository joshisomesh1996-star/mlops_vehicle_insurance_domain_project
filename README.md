# 🚗 Vehicle Data MLOps Project

An **end-to-end MLOps pipeline** demonstrating best practices in **data ingestion, validation, transformation, model training, evaluation, deployment, and CI/CD**, powered by **MongoDB Atlas, AWS (S3, EC2, ECR), Docker, and GitHub Actions**.

---

## 📌 Project Overview

This project covers the **complete lifecycle of a Machine Learning system**, including:

* Modular project structure
* MongoDB-based data ingestion
* Robust logging & exception handling
* Data validation using schema checks
* Feature engineering & model training
* Model versioning with AWS S3
* CI/CD pipeline with GitHub Actions
* Dockerized deployment on AWS EC2
* Prediction & training APIs using Flask

---

## 🏗️ Project Structure

```bash
├── src
│   ├── components
│   ├── configuration
│   ├── constants
│   ├── data_access
│   ├── entity
│   ├── aws_storage
│   ├── utils
│   └── pipeline
│
├── notebook
│   ├── mongoDB_demo.ipynb
│   └── eda_feature_engineering.ipynb
│
├── static
├── templates
├── app.py
├── demo.py
├── requirements.txt
├── setup.py
├── pyproject.toml
├── Dockerfile
├── .dockerignore
├── .github/workflows/aws.yaml
└── README.md
```

---

## ⚙️ Environment Setup

### 1️⃣ Create Project Template

```bash
python template.py
```

### 2️⃣ Configure Local Package Imports

* Implement:

  * `setup.py`
  * `pyproject.toml`
* Refer: **crashcourse.txt**

---

### 3️⃣ Virtual Environment Setup (Conda)

```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
pip install -r requirements.txt
```

Verify installation:

```bash
pip list
```

---

## 🍃 MongoDB Atlas Setup

1. Create MongoDB Atlas account
2. Create a **new project**
3. Deploy **M0 free cluster**
4. Create DB user (username & password)
5. Add IP access:

   ```
   0.0.0.0/0
   ```
6. Get connection string:

   * Driver: Python
   * Version: 3.6+
7. Replace password & save connection string

---

### 📓 Notebook Setup

```bash
mkdir notebook
```

* Add dataset to `notebook/`
* Create `mongoDB_demo.ipynb`
* Select kernel: **vehicle**
* Push dataset to MongoDB
* Verify data in **Atlas → Browse Collections**

---

## 🧾 Logging & Exception Handling

* Implement:

  * `logger.py`
  * `exception.py`
* Test via:

```bash
python demo.py
```

---

## 📥 Data Ingestion Workflow

### Key Steps

1. Define constants in `constants/__init__.py`
2. MongoDB connection:

   ```
   configuration/mongo_db_connections.py
   ```
3. Data access logic:

   ```
   data_access/proj1_data.py
   ```
4. Convert MongoDB records → Pandas DataFrame
5. Define entities:

   * `DataIngestionConfig`
   * `DataIngestionArtifact`
6. Implement:

   ```
   components/data_ingestion.py
   ```
7. Trigger via training pipeline

---

### 🔐 MongoDB Environment Variable

#### Bash

```bash
export MONGODB_URL="mongodb+srv://<username>:<password>..."
echo $MONGODB_URL
```

#### PowerShell

```powershell
$env:MONGODB_URL="mongodb+srv://<username>:<password>..."
echo $env:MONGODB_URL
```

📌 Add `artifact/` to `.gitignore`

---

## ✅ Data Validation

* Define dataset schema in:

  ```
  config/schema.yaml
  ```
* Implement validation logic using:

  ```
  utils/main_utils.py
  ```
* Validate:

  * Column names
  * Data types
  * Missing values

---

## 🔄 Data Transformation

* Feature engineering
* Encoding, scaling
* Define estimator config in:

  ```
  entity/estimator.py
  ```
* Implement component logic in:

  ```
  components/data_transformation.py
  ```

---

## 🤖 Model Trainer

* Train ML model
* Save trained artifacts
* Define model trainer class in:

  ```
  entity/estimator.py
  ```

---

## ☁️ AWS Setup (Model Registry)

### IAM & Credentials

* Region: **us-east-1**
* Create IAM user with **AdministratorAccess**
* Generate access keys
* Set environment variables

```bash
export AWS_ACCESS_KEY_ID="..."
export AWS_SECRET_ACCESS_KEY="..."
```

---

### S3 Configuration

* Bucket Name:

  ```
  my-model-mlopsproj
  ```
* Required constants:

```python
MODEL_EVALUATION_CHANGED_THRESHOLD_SCORE = 0.02
MODEL_BUCKET_NAME = "my-model-mlopsproj"
MODEL_PUSHER_S3_KEY = "model-registry"
```

* Implement:

  * `configuration/aws_connection.py`
  * `aws_storage/`
  * `entity/s3_estimator.py`

---

## 📊 Model Evaluation & Model Pusher

* Compare new vs old model
* Push best model to S3
* Maintain model versioning

---

## 🔮 Prediction Pipeline

* Create prediction pipeline structure
* Implement:

  ```
  app.py
  ```
* Add:

  * `static/`
  * `template/`

---

## 🐳 Docker & CI/CD

### Docker Setup

* `Dockerfile`
* `.dockerignore`

---

### GitHub Actions

```bash
.github/workflows/aws.yaml
```

---

### AWS ECR

* Repository:

  ```
  vehicleproj
  ```

---

### EC2 Deployment

* Instance: **Ubuntu 24.04**
* Type: **t2.medium**
* Install Docker:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```

---

### Self-Hosted GitHub Runner

* Connect EC2 as GitHub Runner
* Runner state: **Idle**

---

### GitHub Secrets

Add:

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_DEFAULT_REGION
ECR_REPO
```

---

## 🌐 Application Access

* Open port **5080**
* Visit:

```
http://<EC2_PUBLIC_IP>:5080
```

### Routes

* `/` → App UI
* `/training` → Model training trigger

---

## 🚀 Final Outcome

✔ Fully automated ML pipeline
✔ Cloud-native deployment
✔ CI/CD enabled
✔ Scalable & production-ready

---

## ⭐ If you like this project

Give it a ⭐ on GitHub and feel free to fork, modify, and extend it!

---
