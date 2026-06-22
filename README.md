# loan-risk-mlops

\# Loan Risk Prediction — MLOps Pipeline



A production-grade MLOps pipeline for predicting loan default risk using the Home Credit Default Risk dataset.



\## Architecture

Dataset (DVC) → Preprocessing → Training (LightGBM) → Evaluation



↓               ↓                ↓                   ↓



DVC Track      params.yaml      MLflow Track       metrics.json



↓



FastAPI REST API



↓



Docker Container



↓



GitHub Actions CI/CD



↓



Prometheus Metrics + Evidently Drift



↓



Trivy Security Scan



\## Tech Stack



| Component | Tool |

|-----------|------|

| Version Control | Git + GitHub |

| Data Versioning | DVC |

| Experiment Tracking | MLflow |

| ML Model | LightGBM |

| API | FastAPI |

| Containerization | Docker |

| CI/CD | GitHub Actions |

| Monitoring | Prometheus + Grafana |

| Drift Detection | Evidently AI |

| Security | Trivy |



\## Project Structure

loan-risk-mlops/



├── data/               # DVC-tracked data



├── models/             # Trained model artifacts



├── src/



│   ├── preprocess.py   # Data preprocessing



│   ├── train.py        # Model training + MLflow logging



│   ├── evaluate.py     # Model evaluation



│   └── app.py          # FastAPI prediction service



├── tests/              # Unit tests



├── reports/            # Metrics, drift report, compliance



├── monitoring/         # Prometheus config



├── .github/workflows/  # CI/CD pipeline



├── dvc.yaml            # DVC pipeline stages



├── params.yaml         # Hyperparameters



├── Dockerfile          # Container definition



└── docker-compose.yml  # Multi-service deployment



\## Quick Start



\### 1. Clone and install

```bash

git clone https://github.com/impanarn/loan-risk-mlops.git

cd loan-risk-mlops

pip install -r requirements.txt

```



\### 2. Run the ML pipeline

```bash

dvc repro

```



\### 3. Start the API

```bash

docker-compose up -d

```



\### 4. Test the API

GET  http://localhost:8000/health



POST http://localhost:8000/predict



GET  http://localhost:8000/metrics



GET  http://localhost:8000/docs



\## Model Performance



| Metric | Value |

|--------|-------|

| AUC | 0.7557 |

| Accuracy | 0.7083 |

| F1 Score | 0.2687 |

| Precision | 0.1685 |

| Recall | 0.6638 |



> High recall (0.66) is prioritized to minimize missed loan defaults.



\## CI/CD Pipeline



GitHub Actions workflow (`.github/workflows/ci.yml`) runs on every push:

1\. \*\*Lint\*\* — flake8 code quality check

2\. \*\*Test\*\* — pytest unit tests

3\. \*\*Build\*\* — Docker image build

4\. \*\*Push\*\* — DockerHub deployment (main branch only)



\## Monitoring



\- \*\*Prometheus\*\* scrapes `/metrics` endpoint every 15 seconds

\- \*\*Grafana\*\* dashboard at `http://localhost:3000`

\- \*\*Evidently AI\*\* drift report in `reports/drift\_report.html`



\## Security



\- Trivy scan: 58 vulnerabilities (5 CRITICAL in base OS packages)

\- No application-level vulnerabilities detected

\- Secrets managed via GitHub Secrets

\- `.env` excluded from version control



\## Dataset



\[Home Credit Default Risk](https://www.kaggle.com/c/home-credit-default-risk) — `application\_train.csv`

\- 307,511 applicants, 122 features

\- Binary target: loan default (1) or repaid (0)

\- Class imbalance: 91.9% / 8.1% handled via `scale\_pos\_weight`

