<div align="center">

<img src="./Vigilant Mavericks DevSecOps Banner.png" alt="CI/CD Pipeline Integrity & Code Injection Monitoring Tool" width="100%">

<br>

# 🚨 CI/CD Pipeline Integrity & Code Injection Monitoring Tool

### AI-powered DevSecOps security for your build pipelines

**Detect malicious logic, code injections and integrity violations inside CI/CD pipelines, even when the code is obfuscated, novel or previously unseen.**

<br>

[![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)](https://vitejs.dev/)
[![JWT](https://img.shields.io/badge/Auth-JWT-000000?style=flat-square&logo=jsonwebtokens&logoColor=white)](https://jwt.io/)
[![WebSockets](https://img.shields.io/badge/Live_Logs-WebSockets-F7931E?style=flat-square)](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)

</div>

---

# 🎯 About the Project

This platform **executes user-defined pipeline steps securely**, scans them **before and during execution**, and **blocks malicious pipelines in real time**.

---

# 🧠 Why This Project Exists

Modern CI/CD pipelines are a prime attack surface. Attackers inject:

- Backdoors into build steps
- Cryptominers in CI scripts
- Reverse shells hidden in YAML
- Supply-chain attacks during build time

Traditional security tools **do not analyze pipeline execution logic**. This project is built to solve exactly that.

---

# ✨ Core Capabilities

### 🔍 Pipeline Integrity Monitoring

- Detects unauthorized changes in pipeline configuration
- Flags injected or tampered steps
- Maintains execution history and audit logs

### ⚙️ Pipeline Step Execution Engine

- Executes **custom user-defined pipeline steps**
- Supports **multi-step pipelines**
- Streams logs in real time via WebSockets
- Immediately stops execution on high-risk detection

### 🧬 AI-Based Malicious Logic Detection (PyGuard)

- Semantic analysis using sentence embeddings
- Detects **intent**, not just signatures
- Resistant to obfuscation and zero-day logic

### 🚫 Pre-Deployment Blocking

- Steps are scanned **before execution**
- Commands are re-scanned **during runtime**
- Malicious pipelines are blocked instantly

### 📊 Real-Time Dashboard

- Pipeline status (Running / Passed / Blocked)
- Step-by-step execution visibility
- Risk scores and severity classification
- Live log streaming

---

# 🧪 Attacks Detected Inside Steps

- ✅ Obfuscated reverse shells
- ✅ Base64 / hex encoded payloads
- ✅ Cryptominers in build commands
- ✅ `curl | bash` download attacks
- ✅ Logic bombs in conditionals
- ✅ Malicious Dockerfile instructions

---

# ⚙️ Pipeline Execution Flow

Each pipeline consists of **ordered execution steps** defined by the user.

### 🧩 Example Pipeline Configuration

```json
{
  "steps": [
    { "name": "Build", "cmd": "npm install && npm run build" },
    { "name": "Test", "cmd": "npm test" },
    { "name": "Dockerize", "cmd": "docker build -t app ." }
  ]
}
```

```text
 ┌──────────┐    ┌────────────┐    ┌──────────────┐    ┌───────────┐
 │ Define   │───▶│ Pre-scan   │───▶│ Execute step │───▶│ Runtime   │
 │ steps    │    │ every step │    │ (isolated)   │    │ re-scan   │
 └──────────┘    └─────┬──────┘    └──────────────┘    └─────┬─────┘
                       │                                     │
                 High risk?                            High risk?
                       ▼                                     ▼
                 ⛔ BLOCKED                             ⛔ BLOCKED
```

---

# 🏗️ High-Level Architecture

```text
┌───────────────┐      JWT       ┌─────────────────────────────┐
│ React Frontend│ ─────────────▶ │ Flask Backend               │
│ (Dashboard)   │                │ - Auth (JWT)                │
└───────────────┘                │ - Pipeline Engine           │
                                 │ - Step Executor             │
                                 │ - ML Scanner (PyGuard)      │
                                 │ - Rule Engine               │
                                 │ - WebSockets (Logs)         │
                                 └──────────────┬──────────────┘
                                                │
                                                ▼
                                  Secure Step-by-Step Execution
```

---

# 🛠️ Technology Stack

| Component | Technology |
|---|---|
| Backend | Python, Flask |
| Authentication | JWT |
| AI Detection | PyGuard (sentence embeddings) |
| Live Logs | WebSockets |
| Frontend | React (Vite) |
| Reports | Generated in `backend/reports/` |

---

# 📁 Project Structure

```text
ai-cicd-security-tool/
│
├── Assets/
│   └── banner.jpeg
│
├── backend/
│   ├── app.py
│   ├── auth/
│   ├── models/
│   ├── ci-integrity/
│   │   ├── train_embeddings.py
│   │   ├── expand_dataset.py
│   │   ├── embeddings/
│   │   └── malicious_samples/
│   ├── utils/
│   │   └── build_runner.py
│   └── reports/
│
├── frontendx/
│   ├── src/
│   ├── pages/
│   ├── components/
│   └── services/
│
└── README.md
```

---

# ⚙️ Setup

### 1. Backend

Create and activate the virtual environment, then start the server.

```bash
cd backend
.venv/Scripts/Activate
python app.py
```

### 2. Frontend

Install the Node modules.

```bash
cd frontendx
npm install
```

---

# 🧠 Model Training & Dataset Expansion

### Train the initial embeddings

```bash
cd backend/ci-integrity/
python train_embeddings.py
```

### Expand the malicious dataset

```bash
python expand_dataset.py
```

---

# 🚀 Running the Project

### Terminal 1: Backend

```bash
cd backend
.venv/Scripts/Activate
python app.py
```

### Terminal 2: Frontend

```bash
cd frontendx
npm run dev
```

Then open the dashboard:

```text
http://localhost:5173/
```

---

# 📌 Sample Pipeline Commands

A complete example pipeline that clones a repository, scans it with both scanners, and cleans up. These commands use Windows syntax.

| Step | Name | Command |
|---|---|---|
| 1 | Start | `echo === Step 1: Starting Secure Pipeline ===` |
| 2 | Clone repository | `git clone https://github.com/<username>/<repo>.git repo` |
| 3 | PyGuard scan | `python ci-integrity\pyguard_embedding.py repo --fail-on-high` |
| 4 | VMX scan | `python cicd-integrity-monitor-main\scanner\scanner\cli.py repo` |
| 5 | Remove repository | `rmdir /s /q repo` |
| 6 | End | `echo === ✅ All Scanners Completed ===` |

> **Tip:** On Linux/macOS, use forward slashes in paths and `rm -rf repo` instead of `rmdir /s /q repo`.

---

# 🔐 Security & Isolation

- JWT-based authentication
- User-specific pipeline isolation
- Secure API enforcement
- No cross-user pipeline visibility

> **Important:** This tool executes user-defined commands. Run it in an isolated environment (VM or container) and never expose it publicly without additional hardening.

---

# 🧪 Why This Tool Is Different

| Security Tool | Limitation |
|---|---|
| SAST | No execution logic |
| SCA | Ignores CI/CD scripts |
| Secrets Scanning | Misses intent |
| Policy Gates | Easily bypassed |
| **This Tool** | **Detects malicious steps** |

- ✅ Step-level security
- ✅ Runtime blocking
- ✅ AI-driven intent detection

---

<div align="center">

**Scan → Execute → Monitor → Block**

### 🚨 CI/CD Pipeline Integrity & Code Injection Monitoring Tool

</div>
Every command is inspected
Every build is verified before deployment

