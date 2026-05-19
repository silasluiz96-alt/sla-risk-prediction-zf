# 🤖 SLA Risk Prediction — IT Ticket Management (ZF Automotive)

> **100% original project** — independently designed and developed by Silas Luiz Bom Fim
> Applied AI for IT service management in an automotive manufacturing environment.

---

## 📌 Overview

This project develops a **hybrid AI model** combining Decision Trees and LSTM Neural Networks to predict SLA breach risk in IT ticket management at **ZF Automotive Brasil** (Limeira unit).

The entire solution — from problem definition to data architecture and model implementation — was **conceived and built independently**, using a synthetic sandbox dataset modeled after real operational patterns to protect corporate confidentiality.

---

## 🎯 Problem Statement

The IT support team at ZF Automotive operates reactively, processing tickets by arrival order and nominal SLA priority. This generates three critical bottlenecks:

| Bottleneck | Description |
|---|---|
| **Triage Blindspot** | Tickets that appear simple at opening but carry hidden technical complexity |
| **Accumulation Inertia** | Backlog from previous days creates "operational fatigue" invisible to simple statistics |
| **Capacity Waste** | High responsiveness to low-priority (P4) tickets reduces senior specialist availability for critical incidents |

**Business goal:** Shift from reactive to **predictive IT management**, anticipating SLA breaches before they occur.

---

## 🏗️ Solution Architecture

A hybrid two-model approach:

```
Ticket Opens → Decision Tree (immediate triage) → LSTM (weekly risk forecast) → Action Plan
```

### 🌳 Decision Tree — "The Gatekeeper"
- **Role:** Immediate triage at ticket opening
- **Output:** Decision rules (IF complexity ≥ 3 AND no knowledge base → Senior escalation)
- **Result:** 97.3% triage accuracy

### 🧠 LSTM Neural Network — "The Manager"
- **Role:** Weekly SLA risk forecasting based on workload history
- **Output:** Risk probability for the next operational period
- **Result:** 84.2% accuracy after 50 training epochs
- **Key insight:** Learns temporal dependencies — yesterday's backlog affects today's risk

---

## 📊 Dataset — Sandbox Environment

> ⚠️ **Important:** All data in this project is **synthetic**, generated to replicate the statistical patterns of real ZF Automotive operational data without exposing any confidential corporate information.

**Coverage:** H2 2025 (July 1 – December 31, 2025)
**Size:** 184 daily records

| Feature | Type | Description |
|---|---|---|
| `Data` | Temporal | Date — essential for LSTM temporal dependency learning |
| `Vol_P1` to `Vol_P4` | Integer | Ticket volume by SLA priority level (P1 = critical, P4 = low) |
| `Complexidade_Cat` | Categorical | Technical complexity scale (1 = simple, 4 = out of scope) |
| `Tempo_Ocioso_Min` | Continuous | Minutes from ticket opening to first analyst action (responsiveness target) |
| `Tempo_Atuacao_Min` | Continuous | Effective working time on the ticket |
| `BC_pronta` | Binary | Knowledge base solution already available (1 = yes) |
| `BC_possivel` | Binary | Knowledge base solution could be created (1 = yes) |
| `Risco_SLA` | Binary | **Target variable** — SLA breach risk (1: Risk / 0: Normal) |

---

## 📈 Results

### Model Performance

| Model | Metric | Value |
|---|---|---|
| Decision Tree | Triage Accuracy | **97.3%** |
| LSTM Neural Network | Predictive Accuracy | **84.2%** |

### Business Impact — Hybrid Strategy Simulation

| Scenario | Days at Risk (Semester) | Change |
|---|---|---|
| Without AI — baseline | 23 days | — |
| Knowledge Base + Automation | 9 days | **−60.9%** |

> The combined strategy of structured knowledge bases + process automation reduced SLA breach risk days from **23 to 9** in a single semester — a **60.9% improvement** in operational reliability.

---

## 🔄 Business Logic — Triage Decision Engine

```python
def definir_plano(row):
    if row['BC pronta'] == 1:
        return 'Suggest Solution (Ready KB)'     # Reduces resolution time
    elif row['BC possivel'] == 1:
        return 'Action: Create Documentation'    # Backlog for knowledge capture
    elif row['Complexidade_Cat'] >= 3:
        return 'Senior Analysis Required'        # New complex cases
    else:
        return 'Normal Flow'
```

---

## 🛠️ Tech Stack

```python
pandas · numpy · matplotlib        # Data handling & visualization
scikit-learn                       # Decision Tree, preprocessing
tensorflow / keras                 # LSTM Neural Network
imbalanced-learn                   # Class balancing
```

---

## 🚀 How to Run

1. Open the notebook in **Google Colab** (recommended)
2. Upload the sandbox CSV file when prompted
3. Run all cells sequentially

```bash
# If running locally
pip install pandas numpy matplotlib scikit-learn tensorflow imbalanced-learn
```

---

## 💡 Future Work

- Integration with **RPA tools** for autonomous resolution of P4 tickets
- Real-time dashboard powered by LSTM for dynamic staffing during predicted peak periods
- Expansion of the knowledge base to push risk days below 9 per semester

---

## 👤 Author

**Silas Luiz Bom Fim**
Data Engineer · ML & AI Developer · UFABC

- 💼 [LinkedIn](https://www.linkedin.com/in/silas-luiz-bom-fim-96a448176)
- 🐙 [GitHub](https://github.com/silasluiz96-alt)
- 📧 silas.luiz.96@gmail.com
