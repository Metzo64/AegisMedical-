# 🛡️ AegisRL: Adaptive Reinforcement Learning for Hospital EHR Access Control

<div align="center">

[![Python](https://img.shields.io/badge/Python-3.10%20%7C%203.14-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/API-FastAPI-009688.svg?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Database](https://img.shields.io/badge/Database-Supabase%20PostgreSQL-3ECF8E.svg?logo=supabase&logoColor=white)](https://supabase.com/)
[![Algorithm](https://img.shields.io/badge/RL-Tabular%20Q--Learning-FF6F00.svg)](https://en.wikipedia.org/wiki/Q-learning)
[![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)](LICENSE)

**Intelligent, context-aware cybersecurity access control that replaces static RBAC with adaptive AI decision-making**

[Features](#-key-features) • [Demo](#-live-demo) • [Installation](#-quick-start) • [Documentation](#-documentation) • [Performance](#-verified-performance)

</div>

---

## 📖 Overview

**AegisRL** is an advanced, production-ready **Adaptive Reinforcement Learning** system designed to revolutionize Electronic Health Record (EHR) access control in hospital environments. By replacing rigid Role-Based Access Control (RBAC) with an intelligent Q-Learning agent, AegisRL dynamically evaluates multi-dimensional context to make real-time security decisions that balance **patient safety** with **zero-trust cybersecurity**.

### The Problem with Traditional RBAC

Traditional hospital security systems face a critical dilemma:

- **Too Restrictive**: Emergency physicians can't access off-department records during Code Blue situations, risking patient lives
- **Too Permissive**: Stolen credentials or insider threats can exfiltrate thousands of records without detection
- **Context-Blind**: Static rules ignore critical signals like access time, location, query frequency, and emergency status

### The AegisRL Solution

AegisRL introduces **context-aware, adaptive decision-making** powered by Reinforcement Learning:

```
📊 Traditional RBAC:           🤖 AegisRL:
   ├─ Doctor? → ALLOW             ├─ Doctor + Emergency + Internal → ALLOW
   └─ Other? → DENY               ├─ Doctor + Off-Hours + External → CHALLENGE
                                  ├─ Staff + VIP Record + Mismatch → RESTRICT
                                  └─ Burst Queries + External → DENY
```

---

## ✨ Key Features

### 🧠 **Intelligent Decision Engine**
- **1,152-State Observation Space**: Analyzes 7 contextual dimensions (role, department, sensitivity, time, location, frequency, emergency)
- **4-Action Policy**: `ALLOW`, `DENY`, `CHALLENGE` (step-up MFA), `RESTRICT` (masked view)
- **Tabular Q-Learning**: Provably convergent, mathematically explainable, sub-millisecond inference

### 🎯 **Real-World Attack Defense**
Protects against 5 critical threat scenarios:
- ✅ **Stolen Credentials**: External IP + off-hours access
- ✅ **Insider Misuse**: VIP/celebrity record snooping
- ✅ **Mass Data Scraping**: Burst query detection (>20/min)
- ✅ **Cross-Department Abuse**: Unauthorized unit access
- ✅ **Emergency Overrides**: Life-safety priority without compromise

### 🚀 **Production-Ready Architecture**
- **FastAPI Backend**: RESTful API with automatic OpenAPI documentation
- **Supabase PostgreSQL**: 7-table schema with full audit logging
- **Interactive Frontend**: Glassmorphic UI with real-time simulation, Chart.js analytics, and HTML5 Canvas network visualization
- **Offline Training**: Complete model training/evaluation pipeline with Plotly convergence charts

---

## 🏆 Verified Performance

*Evaluated on 5,000 independent test requests across realistic hospital scenarios:*

<div align="center">

| Metric | Target | **Achieved** | Impact |
|:-------|:------:|:------------:|:-------|
| **Attack Blocking Rate** | > 90% | **99.37%** ✅ | Stopped 1,733 of 1,744 malicious attempts |
| **Legitimate Access Rate** | > 95% | **99.79%** ✅ | 3,249 of 3,256 legitimate requests granted |
| **False Denial Rate** | < 5% | **0.21%** ✅ | Minimal clinical workflow disruption |
| **Emergency Denial Rate** | < 1% | **0.13%** ✅ | Life-safety priority preserved |
| **Unauthorized Access Rate** | < 5% | **0.63%** ✅ | Only 11 attacks slipped through |
| **Decision Latency** | < 5 ms | **0.018 ms** ✅ | 18.4 microseconds average |

</div>

### 📊 Scenario Performance Breakdown

```
NORMAL ACCESS (2,484 requests)
  └─ ALLOW: 96.1%  |  Optimal for routine clinical workflow

EMERGENCY ACCESS (772 requests)
  └─ ALLOW: 99.7%  |  Trauma/ER priority override

STOLEN CREDENTIAL (604 attacks)
  └─ DENY/CHALLENGE: 98.5%  |  External threat neutralization

INSIDER MISUSE (594 attacks)
  └─ DENY/RESTRICT: 96.6%  |  VIP record protection

MASS SCRAPING (546 attacks)
  └─ DENY: 90.3%  |  Automated bot blocking
```

---

## 🎥 Live Demo

### Interactive Web Application

```bash
# Start the server
python -m uvicorn main:app --reload --host 127.0.0.1 --port 8000
```

**Then open your browser:**
- 🌐 **Web Dashboard**: http://127.0.0.1:8000
- 📚 **API Documentation**: http://127.0.0.1:8000/docs

### Features Available:
1. **Hospital Staff Dashboard**: Real-time KPIs and access stream
2. **Patient Records Browser**: Search, filter, and clinical record viewer
3. **RL Decision Engine**: Interactive access evaluation with Q-score visualization
4. **Cyber Attack Simulator**: HTML5 Canvas network visualization
5. **Access History**: Complete audit trail with PostgreSQL correlation
6. **Security Analytics**: Chart.js decision distributions

---

## 🚀 Quick Start

### Prerequisites

- Python 3.10 or higher
- pip package manager
- (Optional) Supabase account for live database integration

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Metzo64/AegisMedical-.git
cd AegisMedical-
```

2. **Install dependencies**
```bash
pip install -r requirements.txt
```

3. **Configure environment variables**
```bash
# Copy the example environment file
cp .env.example .env

# Edit .env with your credentials (optional - system works offline)
# SUPABASE_URL=https://your-project-id.supabase.co
# SUPABASE_KEY=your-supabase-key
# PORT=8000
```

4. **Train the RL agent** (optional - pre-trained model included)
```bash
python train.py --episodes 35000
```

5. **Evaluate the model** (optional - results included)
```bash
python evaluate.py --samples 5000
```

6. **Run tests**
```bash
python test_pipeline.py
python test_integration.py
```

7. **Start the web application**
```bash
python -m uvicorn main:app --reload --host 127.0.0.1 --port 8000
```

---

## 🔬 Technical Deep Dive

### State Space Representation

The agent observes a 7-dimensional discrete context vector:

```python
Observation = (
    Role,              # DOCTOR | NURSE | STAFF | RESEARCHER (4 values)
    DeptMatch,         # MATCH | MISMATCH (2 values)
    Sensitivity,       # LOW | MEDIUM | HIGH | CRITICAL_VIP (4 values)
    RequestTime,       # NORMAL_HOURS | OFF_HOURS (2 values)
    Location,          # INTERNAL | VPN_OFFSITE | EXTERNAL_UNKNOWN (3 values)
    Frequency,         # NORMAL | ELEVATED | BURST_HIGH (3 values)
    IsEmergency        # NO | YES (2 values)
)

# Total State Space: 4 × 2 × 4 × 2 × 3 × 3 × 2 = 1,152 states
```

### Q-Learning Algorithm

The agent learns optimal policies using **Temporal-Difference (TD) control**:

```
Q(s, a) ← Q(s, a) + α · [r + γ · max Q(s', a') - Q(s, a)]
                            a'
where:
  α = 0.10  (learning rate)
  γ = 0.90  (discount factor)
  r = reward from clinical-security tradeoff matrix
```

### Reward Engineering

Multi-objective reward function balancing patient safety and security:

- **Emergency Override**: `+20.0` for immediate access, `-35.0` for denial
- **Legitimate Access**: `+12.0` for frictionless workflow
- **Attack Defense**: `+18.0` for blocking stolen credentials
- **Insider Detection**: `+15.0` for VIP record protection
- **Clinical Friction**: `-18.0` for false denials

---

## 📁 Project Structure

```
AegisMedical-/
├── 📄 README.md                          # You are here
├── 📄 requirements.txt                    # Python dependencies
├── 📄 .env.example                        # Environment template
├── 📄 .gitignore                          # Git exclusions
│
├── 🧠 Core RL System
│   ├── agent.py                          # Tabular Q-Learning Agent
│   ├── env.py                            # Hospital Access Control Environment
│   ├── train.py                          # Training pipeline with convergence charts
│   ├── evaluate.py                       # Benchmark evaluation script
│   └── config.py                         # Hyperparameters and constants
│
├── 🌐 Backend API
│   ├── main.py                           # FastAPI application with 12+ endpoints
│   └── db.py                             # Supabase PostgreSQL client
│
├── 🎨 Frontend Application
│   └── static/
│       ├── index.html                    # Main SPA entry point
│       ├── css/
│       │   ├── style.css                 # Design system & themes
│       │   └── components.css            # UI components
│       └── js/
│           ├── app.js                    # Core application logic
│           ├── dashboard.js              # KPI dashboard
│           ├── patients.js               # Patient records browser
│           ├── simulator.js              # Cyber attack simulator
│           ├── access.js                 # RL decision engine UI
│           └── history.js                # Audit trail viewer
│
├── 📊 Models & Results
│   └── models/
│       ├── q_table.json                  # Trained Q-Table (1,152×4)
│       ├── agent_metadata.json           # Training hyperparameters
│       ├── training_curves.html          # Plotly convergence chart
│       ├── evaluation_chart.html         # Plotly scenario breakdown
│       └── evaluation_results.json       # Performance metrics
│
├── 📖 Documentation
│   └── project_documentation/
│       ├── AegisRL_Technical_Dossier.md  # Complete academic documentation
│       ├── AegisRL_Project_Facts.md      # Key facts and Q&A
│       ├── AegisRL_Results.csv           # Evaluation data export
│       └── AegisRL_Technical_Dossier.pdf # PDF report
│
└── 🧪 Testing & Utilities
    ├── test_pipeline.py                  # Unit tests
    ├── test_integration.py               # Integration tests
    ├── audit_all_phases.py               # Security audit script
    ├── inspect_schema.py                 # Database schema inspector
    └── generate_dossier_pdf.py           # PDF generation utility
```

---

## 🔌 API Reference

### Core Endpoints

#### `POST /predict` - Real-time Access Decision

```http
POST /predict HTTP/1.1
Content-Type: application/json

{
  "user_id": "DR-ER-CHIEF",
  "patient_id": "PAT-TRAUMA-9",
  "record_id": "REC-5510",
  "role": "DOCTOR",
  "department_match": false,
  "record_sensitivity": "HIGH",
  "request_time": "OFF_HOURS",
  "location": "INTERNAL_HOSPITAL",
  "request_frequency": "ELEVATED",
  "emergency_status": true
}
```

**Response:**
```json
{
  "status": "success",
  "action": "ALLOW",
  "action_description": "Grant immediate full access to requested patient record.",
  "q_values": {
    "ALLOW": 20.0,
    "DENY": -35.0,
    "CHALLENGE": -10.0,
    "RESTRICT": -5.0
  },
  "explanation": "Selected 'ALLOW' (Q-Score: 20.00). Context: Emergency override active...",
  "decision_time_ms": 0.1598,
  "request_id": "REQ-1727602000123",
  "timestamp": "2026-11-15T09:32:00.123456Z",
  "logged_to_supabase": false
}
```

#### Other Endpoints

- `GET /health` - System health check
- `GET /db/test` - Database connection test
- `GET /schema` - Dynamic table schema inspection
- `GET /simulate?scenario=STOLEN_CREDENTIAL` - Synthetic request evaluation
- `GET /metrics` - Evaluation benchmarks
- `GET /api/users` - User list
- `GET /api/patients` - Patient search
- `GET /api/history` - Access audit trail
- `GET /api/stats` - System statistics

---

## 🗄️ Database Schema

### Supabase PostgreSQL (7 Tables)

| Table | Primary Key | Purpose | Rows |
|:------|:------------|:--------|-----:|
| **users** | user_id | Hospital staff and their roles | 100 |
| **patients** | patient_id | Patient demographics | 1,000 |
| **medical_records** | record_id | Clinical documents with sensitivity | 3,548 |
| **departments** | department_id | Hospital organizational units | 5 |
| **access_requests** | request_id | Every access request telemetry | 10,000+ |
| **rl_decisions** | decision_id | Agent decisions with Q-values | Growing |
| **audit_logs** | audit_id | Immutable compliance audit trail | Growing |

**Graceful Offline Mode**: System operates fully without database connection using intelligent mock fallback.

---

## 🎓 Academic Context

### Viva Questions & Answers

<details>
<summary><b>Q: Why Reinforcement Learning over standard RBAC?</b></summary>
<br>

RBAC is **static and binary**: a doctor either has access or does not. If an attacker steals credentials, RBAC blindly grants access. If a trauma physician needs off-department records during Code Blue, RBAC denies access.

**RL is adaptive**: it evaluates multi-dimensional context (time, location, query velocity, emergency override) and balances clinical care with zero-trust defense. The agent learns through 35,000 episodes to optimize the tradeoff between security and patient safety.

</details>

<details>
<summary><b>Q: What is the State Space and why Tabular Q-Learning?</b></summary>
<br>

The state space comprises 7 discrete features:
- User Role (4 values) × Department Match (2) × Record Sensitivity (4) × Request Time (2) × Location (3) × Frequency (3) × Emergency Status (2) = **1,152 total states**

With 1,152 states, **Tabular Q-Learning is optimal**:
- ✅ Guaranteed mathematical convergence (Bellman optimality)
- ✅ Sub-0.02 ms inference (18 microseconds)
- ✅ Zero GPU requirements
- ✅ 100% explainable for medical audits
- ✅ No "black box" neural network opacity

</details>

<details>
<summary><b>Q: What is the Bellman Update Rule?</b></summary>
<br>

```
Q(s, a) ← Q(s, a) + α · [r + γ · max Q(s', a') - Q(s, a)]
                              a'

where:
  α = 0.10  (learning rate)
  γ = 0.90  (discount factor)  
  r = calculated reward
```

This **temporal-difference (TD) learning** equation updates the agent's value estimate based on the immediate reward `r` and the discounted maximum future value from the next state `s'`.

</details>

<details>
<summary><b>Q: How do you prevent the agent from "cheating"?</b></summary>
<br>

**Strict observation-metadata separation**:
- The agent receives **only observable telemetry**: role, dept_match, sensitivity, time, location, frequency, emergency
- It **never sees** `is_legitimate` or `scenario_name` labels
- Ground truth is used **exclusively** by the environment's reward calculator

This mirrors real-world deployment: the agent cannot know attack labels in advance—it must learn from contextual patterns and reward feedback.

</details>

<details>
<summary><b>Q: What happens when the agent makes the wrong decision?</b></summary>
<br>

The **reward function provides corrective feedback**:
- Denying emergency access: **-35.0 penalty** (strongest negative signal)
- Allowing stolen credential: **-30.0 penalty**
- Allowing insider VIP snooping: **-22.0 penalty**

Through 35,000 episodes, the agent learns to **avoid catastrophic mistakes** while maximizing cumulative reward (+71,363 final score).

</details>

---

## 🧪 Testing & Validation

### Automated Test Suites

```bash
# Unit tests (7 tests)
python test_pipeline.py

# Integration tests (8 tests)  
python test_integration.py

# Security audit (15 checks)
python audit_all_phases.py
```

### Test Coverage

✅ State-index bijection correctness  
✅ Observation-metadata separation  
✅ Reward function sanity checks  
✅ Q-table serialization/deserialization  
✅ FastAPI endpoint validation  
✅ Database schema introspection  
✅ Frontend API integration  
✅ Training convergence verification  

---

## 🌟 Why AegisRL?

### Comparison with Alternatives

| Feature | Static RBAC | ABAC Rules | AegisRL |
|:--------|:-----------:|:----------:|:-------:|
| **Context-Aware** | ❌ | ⚠️ Partial | ✅ Full |
| **Adaptive Learning** | ❌ | ❌ | ✅ |
| **Emergency Override** | ❌ | ⚠️ Manual | ✅ Automatic |
| **Insider Detection** | ❌ | ⚠️ Limited | ✅ Advanced |
| **Sub-ms Latency** | ✅ | ⚠️ Slow | ✅ |
| **Mathematical Proof** | N/A | N/A | ✅ Bellman |
| **Explainability** | ✅ Simple | ⚠️ Complex | ✅ Q-scores |

### Baseline Performance Comparison

Tested on 5,000 identical requests:

| Policy | Attack Block | Legit Access | False Deny | Emergency Deny | Cumulative R |
|:-------|:------------:|:------------:|:----------:|:--------------:|:------------:|
| **Random Policy** | 61.44% | 73.61% | 26.39% | 27.95% | -11,361 |
| **Static RBAC** | 94.54% | 75.02% | 24.98% | **53.56%** ⚠️ | +36,480 |
| **AegisRL** | **99.37%** | **99.79%** | **0.21%** | **0.13%** | **+71,363** |

⚠️ **Critical Finding**: Static RBAC causes a **53.56% emergency denial rate** because trauma consults cross departmental boundaries, which violates static unit-role rules. AegisRL learns to prioritize life-safety without sacrificing perimeter defense.

---

## 📚 Documentation

- **[Technical Dossier](project_documentation/AegisRL_Technical_Dossier.md)**: Complete academic documentation (30+ pages)
- **[Project Facts](project_documentation/AegisRL_Project_Facts.md)**: Quick reference and key statistics
- **[API Documentation](http://127.0.0.1:8000/docs)**: Interactive Swagger UI (when server running)
- **[Evaluation Results](models/evaluation_results.json)**: Full benchmark metrics
- **[Training Curves](models/training_curves.html)**: Interactive Plotly convergence visualization
- **[Evaluation Charts](models/evaluation_chart.html)**: Interactive scenario breakdown

---

## 🛠️ Technology Stack

| Component | Technology |
|:----------|:-----------|
| **Language** | Python 3.14 |
| **Backend Framework** | FastAPI 0.115+ with Uvicorn ASGI |
| **Database** | Supabase PostgreSQL (PostgREST) |
| **RL Algorithm** | Tabular Q-Learning (NumPy) |
| **Data Visualization** | Plotly 5.24+, Chart.js |
| **Frontend** | Vanilla JavaScript ES6+, HTML5 Canvas |
| **Styling** | Modern CSS3 with Design Tokens, Glassmorphism |
| **PDF Generation** | ReportLab 4.2+ |
| **Testing** | Python unittest |

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Sutton & Barto** for foundational RL theory (Reinforcement Learning: An Introduction)
- **NIST** for RBAC standardization (Ferraiolo et al.)
- **Supabase** for the excellent PostgreSQL platform
- **FastAPI** for the high-performance async framework
- **Plotly** for beautiful interactive visualizations

---

## 📞 Contact & Support

- **GitHub**: [@Metzo64](https://github.com/Metzo64)
- **Repository**: [AegisMedical-](https://github.com/Metzo64/AegisMedical-)
- **Issues**: [Report a Bug](https://github.com/Metzo64/AegisMedical-/issues)

---

## 🎯 Future Enhancements

- [ ] Deep Q-Networks (DQN) for continuous state spaces
- [ ] Multi-agent coordination for distributed hospital networks
- [ ] FHIR/HL7 integration for real EHR systems
- [ ] Federated learning across multiple hospitals
- [ ] Real-time anomaly detection dashboards
- [ ] Mobile application for clinicians
- [ ] Integration with existing IAM systems (Okta, Azure AD)

---

<div align="center">

**⭐ If you find AegisRL useful, please star this repository! ⭐**

Made with ❤️ for safer healthcare systems

[Back to Top](#-aegisrl-adaptive-reinforcement-learning-for-hospital-ehr-access-control)

</div>
