# Machine Learning Quick Revision Guide

# 1. What is Machine Learning?

Machine Learning (ML) is a branch of AI where systems learn patterns from data instead of being explicitly programmed.

```text
Traditional Programming:
Rules + Data → Output

Machine Learning:
Data + Answers → Model
```

---

# 2. What is a Model?

A model is a trained mathematical system that learns patterns from data and makes predictions.

Examples:
- Spam detection
- Face recognition
- Recommendation systems
- Chatbots

---

# 3. Types of Machine Learning

| Type | Description |
|---|---|
| Supervised Learning | Learns from labeled data |
| Unsupervised Learning | Finds hidden patterns |
| Reinforcement Learning | Learns using rewards |
| Self-Supervised Learning | Learns from raw data |

---

# 4. ML Workflow

```text
Problem → Data → Training → Evaluation → Deployment → Monitoring
```

---

# 5. Steps to Create a Model

## Step 1 — Define Problem

Examples:
- Fraud detection
- Price prediction
- Spam classification

---

## Step 2 — Collect Data

Sources:
- Databases
- APIs
- Sensors
- Logs
- Websites

---

## Step 3 — Clean Data

Tasks:
- Remove duplicates
- Handle missing values
- Normalize values
- Remove invalid records

---

## Step 4 — Feature Engineering

Convert raw data into meaningful numerical features.

Example:

```text
Date → Day, Month, Weekend
```

---

## Step 5 — Split Dataset

Typical split:

```text
70% Training
15% Validation
15% Testing
```

---

## Step 6 — Choose Algorithm

| Problem | Algorithm |
|---|---|
| Prediction | Linear Regression |
| Classification | Logistic Regression |
| Images | CNN |
| NLP | Transformers |

---

## Step 7 — Train Model

Training Loop:

```text
Input → Prediction → Error → Update Weights → Repeat
```

Gradient Descent:

```math
w_new = w_old - η ∂L/∂w
```

Where:
- `L` = Loss
- `w` = Weight
- `η` = Learning Rate

---

## Step 8 — Evaluate Model

Metrics:
- Accuracy
- Precision
- Recall
- F1 Score
- RMSE

---

## Step 9 — Deploy Model

Deployment Targets:
- APIs
- Websites
- Mobile Apps
- Cloud Servers

---

## Step 10 — Monitor Model

Monitor:
- Accuracy
- Latency
- Failures
- Drift

---

## Step 11 — Retrain Model

Models are retrained using fresh data.

---

# 6. Important ML Terms

| Term | Meaning |
|---|---|
| Dataset | Collection of data |
| Feature | Input variable |
| Label | Correct output |
| Training | Learning process |
| Inference | Making predictions |
| Epoch | One full pass through data |
| Batch | Small chunk of data |
| Loss Function | Measures prediction error |
| Optimizer | Improves learning |

---

# 7. Overfitting vs Underfitting

| Problem | Meaning |
|---|---|
| Overfitting | Memorizes training data |
| Underfitting | Too simple to learn patterns |

---

# 8. Data Drift

When real-world data changes over time.

Examples:
- New fraud methods
- Changing customer behavior

---

# 9. ML Model Lifecycle

```text
Problem Definition
        ↓
Data Collection
        ↓
Data Cleaning
        ↓
Feature Engineering
        ↓
Model Selection
        ↓        
Training
        ↓
Model Evaluation
        ↓
Hyper parameter
        ↓
Validation
        ↓
Testing
        ↓
Deployment
        ↓
Monitoring
        ↓
Retraining
```

---

# 10. Neural Network Basics

A neural network contains:
- Input Layer
- Hidden Layers
- Output Layer

Training includes:
- Forward Propagation
- Loss Calculation
- Backpropagation

---

# 11. Deep Learning

Deep Learning uses large neural networks.

Applications:
- Computer Vision
- NLP
- Speech Recognition
- Autonomous Vehicles

---

# 12. Transformers

Transformers are advanced deep learning architectures used in:
- ChatGPT
- Gemini
- Claude
- Translation systems

Advantages:
- Parallel processing
- Better context understanding
- Large-scale learning

---

# 13. Real-Time Prediction Flow

```text
User Input
    ↓
API Request
    ↓
ML Model
    ↓
Prediction
    ↓
Response Returned
```

---

# 14. Important Metrics

## Classification Metrics

| Metric | Meaning |
|---|---|
| Accuracy | Correct predictions |
| Precision | Correct positive predictions |
| Recall | Captures actual positives |
| F1 Score | Balance of precision & recall |

---

## Regression Metrics

| Metric | Meaning |
|---|---|
| MAE | Mean Absolute Error |
| RMSE | Root Mean Squared Error |

---

# 15. Popular ML Tools

| Category | Tools |
|---|---|
| Data Analysis | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| ML Libraries | Scikit-learn |
| Deep Learning | TensorFlow, PyTorch |
| Deployment | FastAPI, Flask |
| Containers | Docker |
| Cloud | AWS, GCP, Azure |
| Monitoring | Grafana, Prometheus |

---

# 16. Common Interview Questions

## What is Machine Learning?
Learning patterns from data.

## What is a model?
A trained mathematical representation of patterns.

## Difference between AI and ML?
ML is a subset of AI.

## What is overfitting?
Model memorizes training data.

## What is feature engineering?
Creating useful input variables.

## What is inference?
Using trained model for predictions.

## What is data drift?
Production data changes over time.

---

# 17. End-to-End ML Architecture

```text
Data Sources
     ↓
Data Pipeline
     ↓
Training Pipeline
     ↓
Model Registry
     ↓
Deployment
     ↓
Monitoring
     ↓
Retraining
```

---

# 18. Quick Revision Formulas

Gradient Descent:

```math
w = w - η ∂L/∂w
```

Linear Regression:

```math
y = mx + b
```

Accuracy:

```math
Accuracy = Correct Predictions / Total Predictions
```

---

# 19. Roles in Machine Learning

## Data Scientist
Focus:
- Data analysis
- Model building
- Feature engineering
- Business insights

---

## ML Engineer
Focus:
- Deployment
- APIs
- Scalability
- Infrastructure

---

## MLOps / Operations Engineer
Focus:
- Automation
- Monitoring
- CI/CD
- Infrastructure reliability

---

# 20. Data Scientist vs ML Engineer vs MLOps

| Aspect | Data Scientist | ML Engineer | MLOps / Operations Engineer |
|---|---|---|---|
| Main Focus | Analyze data & build models | Deploy ML systems | Automate & maintain ML infrastructure |
| Primary Goal | Find insights & predictions | Build scalable ML applications | Keep ML systems reliable |
| Works Mostly With | Data, statistics, experiments | APIs, backend systems, deployment | Cloud, automation, monitoring |
| Key Responsibility | Model creation | Model deployment | Model monitoring & retraining |
| Coding Level | Medium | High | High |
| Math/Statistics | Very High | Medium | Medium |
| Software Engineering | Medium | Very High | High |
| Infrastructure Knowledge | Low-Medium | High | Very High |
| Daily Tasks | Data analysis, visualization, training | APIs, optimization, scaling | CI/CD, pipelines, monitoring |
| Common Tools | Pandas, SQL, Scikit-learn | PyTorch, FastAPI, Docker | Kubernetes, MLflow, Airflow |
| Cloud Usage | Sometimes | Frequent | Extensive |
| Production Responsibility | Low | High | Very High |
| Focus Stage in Lifecycle | Training & experimentation | Deployment & serving | Automation & operations |
| Performance Concern | Accuracy | Speed & scalability | Reliability & uptime |
| Monitoring Responsibility | Limited | Moderate | Major responsibility |
| Best For People Who Like | Analysis & research | Coding & system design | DevOps & infrastructure |
| Example Work | Predict customer churn | Deploy recommendation API | Automate retraining pipelines |

---

# 21. One-Line Summary

## Data Scientist

```text
Builds and experiments with ML models
```

## ML Engineer

```text
Turns ML models into scalable production systems
```

## MLOps / Operations Engineer

```text
Automates, monitors, and maintains ML infrastructure
```

---

# 22. Final Summary

```text
Machine Learning =
Learning patterns from data to make predictions.
```

```text
Model =
Trained mathematical representation of learned patterns.
```

```text
ML Lifecycle =
Build → Deploy → Monitor → Improve
```
