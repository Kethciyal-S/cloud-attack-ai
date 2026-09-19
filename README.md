# Attacking Cloud Infrastructure and Detecting with AI

## Overview

An AI-powered framework that simulates cloud attacks on AWS and detects them using machine learning. This project combines offensive security (attack simulation) with defensive AI (threat detection) in a real AWS cloud environment.

## Project Structure

- **ai/** — AI model + detection
  - train_model.py — Model training script
  - detect.py — Attack detection script
  - model.pkl — Trained model (excluded)
  - cicids2017.csv — Dataset (excluded)
- **attack/** — Attack simulation
  - stratus.exe — Stratus Red Team (excluded)
- **docs/** — Documentation
  - screenshots/ — 6 demo screenshots
- **terraform/** — Infrastructure as Code
- **.gitignore** — Excluded files list
- **README.md** — Project documentation

## Technologies Used

- **AWS**: S3, IAM, EC2, CloudTrail
- **Python 3.11**: scikit-learn, pandas, numpy
- **Machine Learning**: Random Forest Classifier
- **Attack Simulation**: Stratus Red Team
- **Infrastructure**: Terraform
- **Version Control**: Git, GitHub

## Setup Instructions

### 1. Clone the Repository

git clone https://github.com/kethciyal-S/cloud-attack-ai.git
cd cloud-attack-ai

### 2. Install Dependencies

pip install scikit-learn pandas numpy

### 3. Download Dataset

Download the CICIDS2017 dataset from Kaggle:
https://www.kaggle.com/datasets/ericanacletoribeiro/cicids2017-cleaned-and-preprocessed

Rename the file to cicids2017.csv and place it in the ai/ folder.

### 4. Train Model

cd ai
python train_model.py

### 5. Run Detection

python detect.py

## Project Workflow

### Part 1: Setup
- AWS account configured with IAM user
- Python 3.11 environment with virtual environment
- AI model trained on CICIDS2017 dataset

### Part 2: Vulnerable Cloud Build
- S3 bucket with public read access (intentional)
- IAM role with overly permissive policies (intentional)
- Security group with open SSH/HTTP rules (intentional)
- CloudTrail enabled for logging

### Part 3: Attack Simulation
- Stratus Red Team installed
- Attack technique: aws.credential-access.ec2-steal-instance-credentials
- Successfully stole EC2 instance credentials
- Captured attack logs via CloudTrail

### Part 4: AI Detection
- Detection script analyzes CloudTrail logs
- AI model identifies anomalous events
- Real-time alerts triggered

### Part 5: Cleanup
- All AWS resources deleted (cost + security)
- Access keys deactivated
- Code uploaded to GitHub

## Results

| Metric | Value |
|--------|-------|
| Model Accuracy | 99.45% |
| Total Events Analyzed | 30 |
| Attacks Detected | 3 |
| Normal Events | 27 |
| Detection Rate | 10.0% |

## MITRE ATT&CK Mapping

- **Tactic**: Credential Access
- **Technique**: T1552.005 - Unsecured Credentials: Cloud Instance Metadata API

## Screenshots

### 1. Vulnerable S3 Bucket
![S3 Bucket](docs/screenshots/01_s3_bucket_deleted.png)

### 2. Weak IAM Role
![IAM Role](docs/screenshots/02_iam_weak_role.png)

### 3. Open Security Group
![Security Group](docs/screenshots/03_security_group_open.png)

### 4. CloudTrail Attack Events
![CloudTrail](docs/screenshots/04_cloudtrail_events.png)

### 5. Stratus Attack Execution
![Stratus Attack](docs/screenshots/05_stratus_attack.png)

### 6. AI Detection Output
![AI Detection](docs/screenshots/06_ai_detection.png)

## Security Notes

⚠️ **This project is for educational purposes only.**

- All attacks were performed on own AWS account
- Vulnerable resources were intentionally created
- All resources were cleaned up after demo
- Never use these techniques on systems you don't own

## Author

**[Kethciyal-S]**

## License

MIT License

## Acknowledgments

- DataDog for Stratus Red Team
- CICIDS2017 dataset creators
- AWS documentation
