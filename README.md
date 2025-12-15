# Trufflow Application Value Insight Detection

### 👥 **Team Members**

| Name             | GitHub Handle | Contribution                                                             |
|------------------|---------------|--------------------------------------------------------------------------|
| Sindhuja Sarabu    | @sindhujas-dev | Data exploration, Feature Engineering, Overall Project Coordination            |
| Ashlee Boodram    | @    | Data collection, exploratory data analysis (EDA), dataset documentation  |
| Cynthia Korankye    | @CynthiaKorankye  | Data preprocessing, feature engineering, data validation                 |
| Saksham Kapoor    | @SakshamKapoor2911      | Model selection, feature engineering, hyperparameter tuning, Neuro-Symbolic AI Engine, Early Warning Detection System, Model training and optimization  |
| Pablo Moreno    | @pablomoreon10    | Model evaluation, performance analysis, results interpretation           |

---

## 🎯 **Project Highlights**

- Detected outstanding anomalies in app-to-app transactions using various supervised and unsupervised learning models to address unusual behavior. 
- Achieved 28x faster inference latency (0.8μs/sample), demonstrating production-ready, real-time processing of high-frequency transaction streams for Trufflow.
- Generated actionable service-behavior insights to inform business decisions for Trufflow and Trufflow’s stakeholders through clustering. 
- Prevented potential downtime by developing an Early Warning System using Logistic Regression that achieves 87.5% Recall, identifying anomalies 1 hour before they impact billing or reliability.
- Implemented a multi-stage anomaly detection framework to meet industry expections for real-time alerting and high-precision detection in production systems.

---

## 🏗️ **Project Overview**

**Describe:**

- This project is part of the Break Through Tech AI Studio Program, where students are given the opportunity to apply their machine learning skills to real-world, industry-sponsored problems in collaboration with companies in various industries. 
- Trufflow is the first software-value observability platform for data and AI, helping companies measure, manage, and maximize IT-business alignment and ROI. 
- The project objective was to identify insights relevant to AI and data product owners by analyzing Trufflow’s app-to-app transaction records. Our project’s scope included detecting outstanding anomalies and unusual behavior, service similarity analysis, clustering, and bonus early-warning and LLM-based insight tasks. 
- When critical apps in complex systems fail, true issues are often buried under hundreds of false alerts, causing alert fatigure. This project plans to cut the noise by advancing Trufflow’s platform toward detecting true anomalies with near-perfect precision.

---

## 📊 **Data Exploration**

**Datasets**
3 Datasets ~500M:
- **Daily Metric Summaries**: Aggregated daily metrics (14 total) containing value, data, and application identifiers
- **Monthly Metric Summaries**: Aggregated monthly metrics (14 total) containing value, data, and application identifiers.
- **App-to-App Transactions**: Records communication between applications including participating parties and timestamps.

**Data exploration and Preprocessing Approaches:**
- Aggregated over 7.2 million raw transaction rows into 1.54 million hourly windows
- Final feature set included 6 core metrics: Cost mean, Cost Sum, Data Mean, Data Sum, Request Count, and Error Rate

**Key Challenges and Assumptions:**
- Identified and addressed data leakage, future peeking, and global bias during early modeling stages

Please refer to the visualizations folder located in the repository to see images of visualizations. 

---

## 🧠 **Model Development**

**Models Used:**
- Naive Bayes
- KNN
- Logistic Regression
- K-Means Clustering
- XGBoost
- LightGBM

**Learning Paradigms:**
- Supervised classification for anomaly detection
- Unsupervised clustering for service similarity
- LLM-based insight detection for bonus tasks

**Feature Engineering**
- Lag features to capture seasonality
- Blast radius features using transaction graphs to assess service critically
- Business efficiency ratios (e.g. cost per request)

---

## 📈 **Results & Key Findings**

XGBoost achieved the strongest real-time anomaly detection performance with:
- 0.8 μs Latency
- PR-AUC = 0.44
- F1 = 0.048

Logistic Regression was the best model for an early warning system, where it was able to prioritize "pre-alerts" to prevent downtime before it happens. 
- 87.5% Recall (1-hr lookahead)
- 9.8M Samples per Second

K-Means clustering was the primary model giving top performance for service insights. It identified high-risk vs, steady-state services for better monitoring
- 8 distinct service groups

For analyst insights, the Neuro-Symbolic Engine we created transformed "Black Box" anomalies into "White Box" explanations
- ~0% Hallucination Target

Please refer to the visualizations folder located in the repository to see images of visualizations. 

---

## 🚀 **Next Steps**

- Continue refining early-warning detection and LLM-based insight generation with human-annotated examples
- Further validate production scalability and deployment readiness of real-time models. 

---

## 📝 **License**

This project is licensed under the Apache 2.0 license. 
See: https://opensource.org/licenses/Apache-2.0  

---

## 📄 **References**

Cite relevant papers, articles, or resources that supported your project.

---

## 🙏 **Acknowledgements**

Thank your Challenge Advisor, host company representatives, TA, and others who supported your project.

Thank you to J.T. and Sai, our Challenge Advisor and AI Studio Coach, who have been guiding and helping our team throughout this project. Their mentorship and thoughtful guidance helped shape our project’s success, and we couldn’t have done it without them! 
