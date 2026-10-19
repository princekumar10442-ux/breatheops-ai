# 🌿 BreatheOps AI
### A Multi-Agent Air-Quality Event Investigation and Advisory System

BreatheOps AI is a domain-specific Agentic AI Proof of Concept (PoC) designed to investigate unusual air-quality events using historical pollution data, weather information, anomaly detection, and multi-agent collaboration.

The system processes air-quality measurements, identifies unusual pollutant readings, compares observations across monitoring stations, and generates an evidence-based advisory for human review.

**Domain:** Environmental Monitoring & Smart Cities  
**Project Type:** Agentic AI Proof of Concept — FAAI CA-3  
**Team Members:** Prince Kumar and Ishan Sharma  
**Institution:** Symbiosis Institute of Technology, Pune

---

## 📌 Problem Statement

Air-quality monitoring systems collect large volumes of pollutant and meteorological data from multiple monitoring stations. Manually identifying unusual pollution events, validating sensor readings, comparing stations, and preparing actionable reports can be time-consuming.

BreatheOps AI aims to streamline this process through a coordinated workflow of specialized AI agents that analyze data, detect anomalies, investigate contextual information, and validate the generated advisory.

## 🎯 Project Objectives

- Process and analyze multi-station air-quality data.
- Identify unusual pollutant readings using statistical and machine-learning techniques.
- Compare pollution trends across monitoring stations.
- Explore the relationship between pollutant levels and meteorological conditions.
- Generate clear, evidence-based advisory reports.
- Validate findings before presenting recommendations for human review.
- Demonstrate how agent orchestration can improve a domain-specific analytical workflow.

## ✨ Key Features

- **Data Processing:** Upload air-quality datasets, filter records, inspect missing values, and prepare data for analysis.
- **Interactive Visual Analytics:** Explore pollutant trends, station comparisons, distributions, correlations, and weather-related patterns.
- **Anomaly Detection:** Compare a rolling robust-baseline method with Isolation Forest.
- **Multi-Station Investigation:** Examine whether unusual readings are isolated or appear across multiple monitoring stations.
- **Agent Collaboration:** Coordinate planning, data validation, anomaly detection, contextual investigation, and advisory generation.
- **Critic and Safety Validation:** Check evidence consistency, data sufficiency, uncertainty, and unsupported claims.
- **Advisory Generation:** Produce a structured draft explaining the detected event and possible next steps.
- **Report Export:** Export investigation findings when supported by the implemented application.

## 🧠 Multi-Agent Architecture

BreatheOps AI uses specialized agents, each responsible for a particular stage of the investigation.

| Agent | Responsibility |
|---|---|
| Planner Agent | Breaks the investigation request into tasks and coordinates the workflow. |
| Data Quality Agent | Checks missing values, duplicates, and data consistency. |
| Spike Detection Agent | Identifies unusual pollutant readings using configured detection methods. |
| Multi-Station Context Agent | Compares observations across stations and examines weather context. |
| Response Planning Agent | Drafts an advisory based on detected events and supporting evidence. |
| Critic and Safety Agent | Validates the output and flags uncertainty or unsupported conclusions. |

### Workflow

1. The user uploads a dataset and selects the station, pollutant, and investigation period.
2. The Planner Agent creates the investigation plan.
3. The Data Quality Agent checks the input data.
4. The Detection Agent identifies candidate anomalies.
5. The Context Agent compares station readings and available weather variables.
6. The Response Planning Agent prepares an evidence-based advisory.
7. The Critic and Safety Agent checks the findings before the final output is presented for human review.

The agents can be implemented as Python functions coordinated by an orchestration workflow. A separate large language model for every agent is not required.

## 📊 Dataset

**Primary dataset:** Beijing Multi-Site Air Quality Data

Source: [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/501/beijing+multi+site+air+quality+data)

The dataset contains historical air-quality and meteorological observations from multiple monitoring stations in Beijing.

| Attribute | Description |
|---|---|
| Time period | March 2013 – February 2017 |
| Monitoring stations | 12 |
| Approximate records | 420,768 hourly observations |
| Pollutants | PM2.5, PM10, SO₂, NO₂, CO, O₃ |
| Weather variables | Temperature, pressure, dew point, rainfall, wind speed, wind direction |

The dataset contains missing values, which makes data-quality checks an important part of the workflow.

**Note:** The application should verify the uploaded file's actual columns and record count instead of assuming that every uploaded dataset has the same structure.

## 🔍 Anomaly Detection Methods

### 1. Rolling Robust Baseline

This method compares observations against a station's recent historical behaviour using a rolling median and median absolute deviation (MAD).

It helps identify unusually large deviations while being less sensitive to extreme observations than a simple mean-and-standard-deviation baseline.

### 2. Isolation Forest

Isolation Forest is an unsupervised machine-learning algorithm that identifies observations that are unusual relative to the wider data distribution.

It can analyze multiple pollutant and weather features after suitable preprocessing.

### Model Comparison

The two methods can be compared using:

- Number of anomalies detected.
- Agreement between their flagged observations.
- Differences in the events identified.
- Manual inspection of representative flagged records.
- Precision, recall, F1-score, or other metrics only when suitable labelled evaluation data is available.

Neither method proves that a pollution incident occurred. Detected anomalies are candidates for further investigation.

## 🖥️ Application Pages

The Streamlit application is organized around the following workflow.

### Page 1 — Data Processing

- Upload a CSV or supported ZIP dataset.
- Inspect dataset dimensions and available columns.
- Check missing values and data quality.
- Filter records by date, station, or pollutant where supported.
- Compare basic station statistics.
- Download processed data where supported.

### Page 2 — Visual Analytics

- Plot pollutant concentrations over time.
- Compare monitoring stations.
- Inspect pollutant distributions.
- Explore feature correlations.
- Visualize meteorological variables and their relationships with pollution levels.

### Page 3 — Agent Investigation

- Configure an investigation.
- Run the agent workflow.
- Review detected anomalies and contextual evidence.
- Inspect the generated advisory and validation findings.

### Page 4 — Reports and Evaluation

- Review investigation results.
- Compare detection methods.
- Inspect validation status.
- Export reports where implemented.

*The exact pages and controls depend on the files included in the current application version.*

## 🛠️ Technology Stack

- **Programming Language:** Python
- **User Interface:** Streamlit
- **Data Processing:** Pandas, NumPy
- **Data Visualization:** Plotly
- **Machine Learning:** Scikit-learn
- **Agent Orchestration:** Python-based workflow coordination
- **Dataset Source:** UCI Machine Learning Repository
- **Development Tools:** VS Code / Codex

Optional integrations such as LangChain, LangGraph, or Ollama can be added if required by the implementation. Paid API access is not necessary for a rule-based or mock-model PoC.

## ⚙️ Installation and Setup

### Prerequisites

- Python 3.10 or a compatible version supported by the project's dependencies.
- Git.
- A terminal or code editor such as VS Code.

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/breatheops-ai.git
cd breatheops-ai
```

Replace `YOUR-USERNAME` with your GitHub username.

### 2. Create a virtual environment

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the application

```bash
streamlit run app.py
```

Open the local URL printed in the terminal, usually `http://localhost:8501`.

If the project uses different entry-point or dependency filenames, adjust these commands to match the repository.

## 🧪 Testing and Evaluation

The PoC can be evaluated using the following checks:

- Verify missing-value and duplicate-record handling.
- Confirm that station and date filters return the expected records.
- Compare anomaly flags from both detection methods.
- Inspect whether contextual findings match the underlying data.
- Test the Critic Agent with inconsistent or insufficient evidence.
- Confirm that advisories do not claim an unverified pollution source.
- Verify that report exports contain the selected investigation details.

Because the dataset does not supply definitive incident labels, unsupervised anomaly detection results must not automatically be presented as verified accuracy measurements.

## ⚠️ Limitations

- The current PoC uses historical data rather than a verified live monitoring feed.
- Missing observations may affect the reliability of the analysis.
- Detection results depend on preprocessing, thresholds, and model settings.
- Correlation between weather, pollution, and station readings does not establish causation.
- Possible pollution sources cannot be confirmed from these measurements alone.
- Generated advisories require human review and are not substitutes for official public-health warnings.

## 🚀 Future Scope

- Integrate live air-quality monitoring APIs.
- Add an interactive geographical map of monitoring stations.
- Improve anomaly detection through domain-specific calibration.
- Evaluate detection methods using independently reviewed incident labels.
- Add explainable AI visualizations for individual anomalies.
- Support additional cities and environmental datasets.
- Introduce scheduled monitoring and notification workflows.
- Deploy the application to a cloud platform.

## 🌍 Expected Impact

BreatheOps AI demonstrates how a coordinated analytical workflow can help environmental monitoring teams investigate unusual readings more systematically.

By combining data-quality checks, anomaly detection, contextual comparisons, and output validation, the project aims to make air-quality event triage more transparent and easier to review.

## 👥 Team

- **Prince Kumar** — B.Tech, Artificial Intelligence and Machine Learning
- **Ishan Sharma** — B.Tech, Artificial Intelligence and Machine Learning

**Institution:** Symbiosis Institute of Technology, Pune

## 📚 References

1. UCI Machine Learning Repository — [Beijing Multi-Site Air Quality Data](https://archive.ics.uci.edu/dataset/501/beijing+multi+site+air+quality+data)
2. Scikit-learn Documentation — [Isolation Forest](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.IsolationForest.html)
3. Streamlit Documentation — [Build data applications](https://docs.streamlit.io/)
4. Pandas Documentation — [Data analysis tools](https://pandas.pydata.org/docs/)
5. Plotly Python Documentation — [Interactive visualizations](https://plotly.com/python/)

---

*BreatheOps AI — Detect with evidence. Investigate with context. Respond with care.*
