# End-to-End AI Call Center Agent (Toy Example)

> **Toy demonstration prototype:** "Build the rules first, learn from calls second, then use both on every live call."

This repository is a lightweight, frontend-only toy example demonstrating the 7 touchpoints of an AI Call Center Agent in a single web page. It uses in-browser Web Speech, WebLLM/WebGPU, Groq LPU (optional), or a built-in deterministic simulator.

---

## 🎮 What This Is

* A **self-contained toy simulator** for exploring conversational AI contact center concepts.
* Demonstrates the **7 Touchpoints** lifecycle:
  1. **World Model (First Principles)**: Basic CDT dental codes and eligibility rules.
  2. **Batch: Voice to Script**: Simulated bulk transcript ingestion and sample PII redaction.
  3. **Batch: Add Empirical Part**: Toy rule-adaptation based on common caller phrasing.
  4. **Live: Voice to Script**: Microphone input via Web Speech API with context-guided correction.
  5. **Live: Script to Decision**: Decision routing (Direct Answer, Mock Tool, or Mock Escalation) via Groq, WebLLM, or the built-in simulator.
  6. **Live: Decision to Voice**: Speech synthesis (Web Speech TTS) with barge-in test button.
  7. **Live: Decision to Evaluation**: Toy AI Judge score card and retraining loop demonstration.

---

## 🚀 How to Run

No build step, dependencies, or backend required:

1. Double-click **`index.html`** (or `callcenter_ai_touchpoints_studio.html`) to open it in Chrome or Edge.
2. Select an engine:
   * **Deterministic Simulator**: Works immediately with zero setup or API keys.
   * **Groq LPU (Optional)**: Click the gear icon to provide a Groq key for fast LLM inference.
   * **WebGPU / WebLLM (Optional)**: Runs a local lightweight model in your browser if WebGPU is supported.
3. Click **"Run 7-Step Pipeline"** to watch the simulated flow end-to-end.

---

## 📋 Included Files

* **`index.html` / `callcenter_ai_touchpoints_studio.html`**: The main toy touchpoints studio.
* **`callcenter_ai_voice_agents.html`**: Toy visual graph simulator for sample call scenarios.
* **`callcenter_macro_graph_studio.html`**: Visual prototype for contact center flow graphs.

---

## 📄 License
MIT / Apache 2.0.
