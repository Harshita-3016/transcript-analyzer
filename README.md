# Transcript Analyzer

A web-based tool that analyzes supervisor call transcripts and generates structured performance insights using a rubric-driven evaluation system powered by Ollama.

---

## ⚙️ Setup Instructions

Follow these steps to run the project locally:

### 1. Install Ollama
Download and install Ollama from: https://ollama.com

### 2. Pull the Model
```bash
ollama pull llama3.2
```
### 3. Start Ollama Server
```
ollama serve
```
### 4. Run the Application
Open the project folder
Open index.html in your browser
(or use Live Server in VS Code)

🤖 Model Used

Model: llama3.2

Why this model?

Fast and lightweight for local execution
Good reasoning capability for structured analysis
Reliable in generating JSON outputs with proper prompt constraints
Suitable for real-time frontend integration

🏗️ Architecture Overview

This is a frontend-driven application using a local LLM backend:

Frontend (HTML, CSS, JavaScript):
Accepts transcript input from the user
Sends request to Ollama API
Displays structured JSON output
Backend (Ollama):
Runs locally at http://localhost:11434
Processes prompts using the LLM
Returns structured evaluation
🔄 Flow:

User Input → Frontend → Ollama API → Model → JSON Output → UI Display

Ollama acts as the inference engine, so no separate backend server is required.

🧠 Design Challenges & Approach
1. Ensuring Structured JSON Output

Challenge:
LLMs often return inconsistent or incomplete JSON.

Approach:

Enforced strict output schema in the prompt
Restricted values for key fields:
signal: positive / negative / neutral
confidence: low / medium / high
systemOrPersonal: system / personal
Added strict rules:
“Return ONLY valid JSON”
“Do NOT leave fields empty”
2. Handling the 6 vs 7 Scoring Boundary

Challenge:
Correctly distinguishing between:

Score 6 → Executes tasks reliably
Score 7 → Identifies problems independently

Approach:

Added explicit scoring rules in the prompt
Reinforced boundary condition:
“Do NOT assign 7+ without strong evidence of independent problem identification”
Included examples to guide model behavior
3. Mapping Unstructured Transcripts to Structured Insights

Challenge:
Supervisor conversations are informal and inconsistent.

Approach:

Extracted:
Direct quotes (evidence)
Behavioral signals
KPI impact
Mapped outputs to fixed dimensions:
execution
systems_building
kpi_impact
change_management

What I Would Improve With More Time
1. Side-by-Side View

Display transcript and analysis together for better usability and comparison.

2. Editable Output

Allow users to review and edit generated insights before finalizing.

3. Multi-Transcript Dashboard

Enable comparison across multiple fellows to identify patterns and trends.

4. Enhanced Error Handling

Show detailed error messages (e.g., model not running, API issues) instead of generic alerts.

5. Prompt Versioning

Allow switching between prompt versions to test and improve model performance over time.
