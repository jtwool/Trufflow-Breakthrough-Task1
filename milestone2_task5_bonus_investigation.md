## Milestone 2 – Task 5: Bonus Task Investigation

### Goal
The goal of this task is to think about **ways to improve or extend** our current Trufflow anomaly detection and service similarity system.  
We are not building new models — only exploring **ideas** that could make future versions smarter and faster.

---

### 1. Feature Ideas
We can add more advanced or detailed features to help the model understand patterns better:
- **Rolling Averages & Variance:** Track how each service’s performance changes over time (for example, sudden jumps in latency or request volume).
- **Transaction Frequency Patterns:** Measure how often services communicate, which can show unusual spikes.
- **Entropy or Diversity Scores:** Detect if a service suddenly starts interacting with new or unusual partners.
- **Temporal Windows:** Create features that capture daily or weekly changes in behavior.

**Why it helps:**  
These features can catch *hidden or time-based anomalies* that current static averages may miss.

---

### 2. Model Improvements
We can test stronger anomaly detection and clustering methods:
- **Isolation Forest:** A model made just for anomaly detection that isolates rare points efficiently.  
- **Autoencoder (Neural Network):** Learns to rebuild normal patterns; anything it can’t rebuild well is likely an anomaly.  
- **LSTM (Time-Series Deep Learning):** Good for detecting changes over time — can track trends across days or weeks.  
- **Graph Embeddings (Node2Vec / DeepWalk):** Learn similarity by looking at service-to-service connections, not just feature values.

**Why it helps:**  
These models understand *complex patterns* and *relationships* better than basic algorithms like Naive Bayes or KNN.

---

### 3. Service Relationship Insights
We can go beyond pairwise similarity and look at *whole network structures*:
- **Graph Analysis:** Represent all services as nodes connected by their interactions.  
- **Centrality Measures:** Identify “key” or “risky” services that many others depend on.  
- **Cluster Validation Metrics:** Use scores like *Davies–Bouldin Index* or *Calinski–Harabasz* to confirm if clusters are truly separate.

**Why it helps:**  
This would reveal *which services influence others most*, helping Trufflow detect not just isolated issues but also **chain reactions** across systems.

---

### Summary
For future work, we recommend:
- Adding more **behavior-based features**
- Trying **advanced models** like Isolation Forest or Autoencoders
- Exploring **graph-based relationships** for deeper service mapping  

These steps can make the Trufflow system more **accurate, flexible, and intelligent** for large-scale monitoring.
