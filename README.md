# AI-Smart-Water-Leak-Detectio
AI and IoT-powered dashboard that predicts water pipeline leaks from sensor data, visualizes leak-prone zones on a GIS map, and answers questions via an integrated AI assistant.


<div align="center">

![Smart Water Leak Detection Banner](https://github.com/atharva1727/AI-Smart-Water-Leak-Detectio/blob/main/banner%20(2).png)

<br/>

# 💧 Smart Water Leak Detection & Monitoring Dashboard

### AI & IoT-Powered Leak Prediction, GIS Mapping, and Real-Time Monitoring

**Tech:** Python 3.10+ · Streamlit · scikit-learn · Groq (LLaMA) &nbsp;|&nbsp; **License:** MIT &nbsp;|&nbsp; **Status:** Active

*A Machine Learning powered dashboard that predicts pipeline leaks from sensor data, visualizes leak-prone zones on an interactive map, and answers natural-language questions about the system via an AI assistant.*

</div>

---

## 📖 Project Overview

The **Smart Water Leak Detection System** combines **Machine Learning** with an **interactive Streamlit dashboard** to detect and monitor water leakages across pipeline networks. It works with IoT-style sensor readings — pressure, flow rate, vibration, temperature, and RPM — to classify whether a pipeline segment is leaking, and layers this with **location-aware GIS data** (zone, block, pipe) so leaks can be traced to a physical spot on a map.

The system is built around two core components:

* **ML Models (Jupyter Notebook)** — training and evaluation of four classification models (`water_leak_detection.ipynb`)
* **Interactive Dashboard (Streamlit App)** — real-time prediction, simulation, mapping, and reporting (`app.py`)

An integrated **AI Assistant**, powered by Groq's LLaMA models, lets users ask natural-language questions about leak trends and maintenance, and can generate plots on demand.

---

## ✨ Key Features

| Feature | Description |
|:---|:---|
| 🔍 **Leak Prediction** | Detects leakage for individual pipeline inputs using trained ML models (Random Forest, Decision Tree, Logistic Regression, SVM) |
| 🎛️ **What-if Analysis** | Simulate different sensor values with sliders and instantly see how predictions change |
| 🗺️ **Zone Map & Geo Analysis** | Interactive GIS map showing leak locations, active/dead pipes, and zone-wise analytics |
| 📂 **Batch Prediction** | Upload a CSV dataset for bulk leak detection with downloadable results |
| 📊 **Analytics & Insights** | Feature importance, model comparisons, and system-wide insights |
| 🤖 **AI Assistant** | Groq-powered LLaMA assistant answers questions on leak trends and maintenance, and generates plots dynamically |
| ℹ️ **About Page** | Quick overview of the system for new users |

---

## ⚙️ System Architecture

![Architecture Diagram](https://github.com/atharva1727/AI-Smart-Water-Leak-Detectio/blob/main/architecture%20(1).png)

The pipeline flows from raw data to actionable insight in five stages:

### 📡 Data Sources
Sensor readings (pressure, flow rate, vibration, temperature, RPM), GIS location data (zone/block/pipe with latitude-longitude), and historical leak logs feed into the system. Secrets such as the Groq API key are kept in a `.env` file, never hard-coded.

### 🧹 Data Preprocessing
Pandas and NumPy handle cleaning and feature engineering, with `imbalanced-learn` used to address class imbalance between leak and non-leak samples before training.

### 🧠 Machine Learning Models
Four classifiers are trained and compared in `water_leak_detection.ipynb`, then exported with `joblib` for use in the live app:
- **Random Forest** — 0.98 accuracy (best performing)
- **Decision Tree** — 0.91 accuracy
- **SVM** — 0.90 accuracy
- **Logistic Regression** — 0.89 accuracy

### 🖥️ Streamlit Application
`app.py` loads all four trained models and routes user interaction through a sidebar-driven interface, keeping model inference and UI logic in one lightweight app.

### 🧩 Feature Modules
Each sidebar option — Predict Leakage, What-if Analysis, Zone Map & Geo Analysis, Batch Prediction, Analytics & Insights, and AI Assistant — is a self-contained view built on top of the shared models and data.

---

## 🛠️ Tech Stack

![Tech Stack](https://github.com/atharva1727/AI-Smart-Water-Leak-Detectio/blob/main/techstack%20(1).png)

### Core Framework

```
Python 3.10+          — Primary language
Streamlit             — Interactive web dashboard
python-dotenv         — Environment variable management (.env)
```

### Machine Learning

```
scikit-learn          — Random Forest, Decision Tree, Logistic Regression, SVM
imbalanced-learn      — Class balancing for leak/no-leak data
joblib                — Model serialization (.pkl files)
```

### Visualization & Mapping

```
Plotly                — Interactive charts and comparisons
Folium                — GIS leak-location mapping
streamlit-folium      — Embedding Folium maps in Streamlit
```

### Data Handling

```
Pandas                — Data wrangling and CSV handling
NumPy                 — Numerical computation
```

### AI Assistant

```
Groq API              — LLaMA model access for natural-language Q&A
```

---

## 🔄 How It Works — Detailed Walkthrough

```
Sensor Reading / CSV Upload
       │
       ▼
┌─────────────────────────────────┐
│   Data Preprocessing             │
│   Clean → Engineer Features      │
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│   ML Model Inference             │
│   RF / DT / LR / SVM             │
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│   Streamlit Dashboard            │
│   Predict → Visualize → Map      │
└────────────────┬────────────────┘
                 │
                 ▼
       ✅  Leak Flagged / Cleared
       (Plotted on GIS map + logged for analytics)
```

**Step-by-step:**

1. **Input** — A user enters pipeline sensor values manually, adjusts what-if sliders, or uploads a CSV for batch prediction
2. **Preprocessing** — Inputs are validated and formatted to match the feature set the models were trained on
3. **Prediction** — The selected model (or all four, for comparison) classifies the input as leak or no-leak
4. **Visualization** — Results are plotted on the GIS zone map and summarized in the analytics view
5. **AI Assistant** — Users can ask the Groq-powered assistant follow-up questions about trends or request custom plots

---

## 📁 Project Structure

```
Smart-Water-Leak-Detection/
│
├── app.py                                      # Streamlit dashboard — main entry point
├── water_leak_detection.ipynb                  # Model training & evaluation notebook
├── requirements.txt                            # Python dependencies
├── .env.example                                # Environment variable template
├── .gitignore
├── README.md
│
├── models/
│   ├── random_forest_model.pkl                 # Best performing model (0.98 acc)
│   ├── decision_tree_model.pkl
│   ├── logistic_regression_model.pkl
│   └── svm_model.pkl
│
├── data/
│   ├── location_aware_gis_leakage_dataset.csv  # Training dataset (sensor + GIS)
│   └── testing.csv                             # Sample data for testing
│
└── assets/
    ├── banner.png
    ├── architecture.png
    └── techstack.png
```

---

## ⚡ Quick Start

### Prerequisites

```bash
Python 3.10 or higher
pip (Python package manager)
A Groq API key (for the AI Assistant feature)
```

### Installation

```bash
# 1. Clone the repository (replace with your own repo path once uploaded)
git clone Smart-Water-Leak-Detection
cd Smart-Water-Leak-Detection

# 2. Create & activate a virtual environment
python -m venv venv
source venv/bin/activate          # Linux / macOS
# venv\Scripts\activate           # Windows

# 3. Install all dependencies
pip install -r requirements.txt

# 4. Set up environment variables
cp .env.example .env
# Edit .env and add your GROQ_API_KEY and AI_MODEL

# 5. Run the dashboard
streamlit run app.py
```

The app will open in your browser at:

```
http://localhost:8501
```

### Retraining the Models (Optional)

```bash
jupyter notebook water_leak_detection.ipynb
```

This regenerates the `.pkl` model files used by the dashboard.

### Requirements File

```txt
streamlit
pandas
numpy
scikit-learn
joblib
plotly
folium
streamlit-folium
groq
imbalanced-learn
python-dotenv
```

---

## 🧭 How to Use

**Navigate using the Sidebar Menu:**

- **Predict Leakage** — Input pipeline parameters and get an instant prediction
- **What-if Analysis** — Adjust sliders to simulate different sensor conditions
- **Zone Map & Geo Analysis** — Visualize leaks on an interactive map by zone, block, and pipe
- **Batch Prediction** — Upload a CSV for bulk leak detection with downloadable results
- **Analytics & Insights** — Explore feature importance and compare model performance
- **AI Assistant** — Ask questions about leak trends and request generated plots

**Dataset Requirements** (for Batch Prediction & AI Assistant):

```
Pressure, Flow_Rate, Temperature, Vibration, RPM, Operational_Hours,
Latitude, Longitude, Zone, Block, Pipe, Location_Code, Leakage_Flag (optional)
```

---

## 📊 Model Performance

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  Model                           Accuracy
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  Random Forest                   0.98  ✅ Best performing
  Decision Tree                   0.91
  SVM                             0.90
  Logistic Regression             0.89
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 🏆 Project Highlights

- ✅ **Four-model comparison** — Random Forest, Decision Tree, Logistic Regression, and SVM benchmarked side by side
- ✅ **Location-aware detection** — leak predictions tied to real zone/block/pipe GIS coordinates
- ✅ **Interactive simulation** — what-if sliders let users explore sensor conditions without live hardware
- ✅ **Batch processing** — bulk CSV predictions with downloadable results for reporting
- ✅ **Conversational insights** — Groq LLaMA assistant turns raw predictions into plain-language answers and plots
- ✅ **Single-file dashboard** — the entire frontend runs from one Streamlit app, easy to deploy and extend
- ✅ **Secure by design** — API keys and secrets isolated in `.env`, excluded from version control

---

## 🔒 Security Note

API keys and credentials (such as the Groq API key) must be stored in **environment variables** using a `.env` file. Never hard-code secrets into source files. Always keep `.env`, virtual environment folders, and cache directories out of version control.

```bash
# .gitignore — always include these
__pycache__/
*.pyc
.venv/
venv/
.env
.streamlit/
.vscode/
.idea/
```

---

## 🔮 Future Enhancements

- [ ] **Live Sensor Integration** — connect directly to real IoT sensor streams instead of static CSV input
- [ ] **Alerting System** — automated email/SMS/Slack alerts when a leak is predicted
- [ ] **Model Retraining Pipeline** — scheduled retraining as new leak data becomes available
- [ ] **Cloud Deployment** — host the dashboard on Streamlit Community Cloud, AWS, or Docker
- [ ] **Mobile-Friendly View** — responsive layout for field technicians
- [ ] **Historical Trend Dashboard** — long-term leak frequency and maintenance-cost tracking
- [ ] **Multi-language AI Assistant** — support for regional languages in the chat assistant

---

## 📄 License

This project is licensed under the **MIT License**. See the LICENSE file included in the repository for full details.

---

<div align="center">

⭐ **If you found this useful, consider starring the repo!**

*"Catching leaks before they become losses — one sensor reading at a time."* 💧

</div>
