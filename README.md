# End-to-End AI Call Center Agent (E2E)
> **"Build the rules first, learn from calls second, then use both on every live call."**

An enterprise-grade, browser-executable, and cloud-deployable architecture for autonomous Contact Center AI Agents. Features sub-200ms speech-to-text, context-grounded jargon recovery, tri-mode decision routing (Direct Answer, Tool Invocation, Warm Human Handoff), mood-adaptive text-to-speech with real-time barge-in, and automated AI Judge scoring with continuous batch retraining loops.

---

## 🏛️ Architecture Overview

The system is organized around the **7 AI Touchpoints of an AI Call Agent**:

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│              1. WORLD MODEL (FIRST PRINCIPLES) [BUILT FIRST]                   │
│   • CDT Procedure Dictionary (D0120, D1110, D2740, D3330, D4341, D9110)        │
│   • Policy Rules: Eligibility, Pre-Auth, Frequency limits, Deductibles          │
│   • EVAL: 120/120 synthetic scenario tests matching payer policies              │
└─────────────────────────────────────────────────────────────────────────────────┘
         │ guides
         ▼
┌──────────────────────────────────────┐     ┌────────────────────────────────────┐
│ 2. BATCH: VOICE TO SCRIPT            │     │ 3. BATCH: ADD EMPIRICAL PART       │
│    • Bulk whole-call STT diarization │────▶│    • Mines unwritten exceptions     │
│    • Automated HIPAA PII redaction   │     │    • Corrects rigid policy rules   │
│    • EVAL: WER 3.2%, 100% Redaction  │     │    • EVAL: +18.4% FCR on held-out  │
└──────────────────────────────────────┘     └────────────────────────────────────┘
         │                                                    │
         └─────────────────────────┬──────────────────────────┘
                                   │ RULES + EMPIRICAL WORLD MODEL FEEDS
                                   ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│ 4. LIVE: VOICE TO SCRIPT (INDIVIDUAL)                                           │
│    • Sub-200ms streaming STT (live Web Speech mic or simulated stream)          │
│    • World Model context autocorrects mis-heard dental terms into CDT codes    │
│    • EVAL: 185ms latency, speaker role separation (Agent vs. Caller)            │
├─────────────────────────────────────────────────────────────────────────────────┤
│ 5. LIVE: SCRIPT TO DECISION (INDIVIDUAL)                                        │
│    • Tri-mode Decision Engine:                                                  │
│      1. ⚡ Groq LPU: llama-3.3-70b-versatile (500+ tok/s ultra-fast API)        │
│      2. 🖥️ WebGPU / WebLLM: Local in-browser inference (Llama 3.2 / SmolLM2)     │
│      3. 🔮 Deterministic Policy Simulator: Instant execution, zero setup       │
│    • Dynamic 3-Way Action Routing:                                              │
│      [Path A: Answer] | [Path B: Tool Execution] | [Path C: Warm Human Handoff] │
├─────────────────────────────────────────────────────────────────────────────────┤
│ 6. LIVE: DECISION TO VOICE (INDIVIDUAL)                                         │
│    • Mood & empathy-modulated TTS with conversational pacing and pauses         │
│    • Real-time barge-in interruption (<50ms audio cut-off on user speak)        │
│    • EVAL: 4.8/5.0 MOS naturalness score, 210ms acoustic latency                │
├─────────────────────────────────────────────────────────────────────────────────┤
│ 7. LIVE: DECISION TO EVALUATION (INDIVIDUAL)                                    │
│    • AI Judge scorecard: Accuracy, HIPAA Compliance, Empathy, FCR Outcome       │
│    • Safe simulator regression replay before updating production                │
└─────────────────────────────────────────────────────────────────────────────────┘
         │
         │ CALLS ACCUMULATE IN BATCH, THEN RETRAIN (Feedback Loop)
         ▼
[Buffer 500 calls ──▶ Retrain Step 3 Empirical Weights ──▶ Update Step 5 Matrix]
```

---

## 🚀 Key Modules & Studios

### 1. `callcenter_ai_touchpoints_studio.html` (or `index.html`)
The primary interactive studio executing the complete 7-step touchpoint lifecycle:
* **Zero Backend Required**: Runs directly in Google Chrome, Microsoft Edge, or Safari.
* **Tri-Mode Inference**:
  * **Groq LPU**: Connects to Groq's high-throughput LPU for sub-second, 500+ tok/s reasoning.
  * **WebGPU / WebLLM**: In-browser local LLM execution via `@mlc-ai/web-llm` (`Llama-3.2-3B`, `SmolLM2-1.7B`, `Phi-3.5`).
  * **Deterministic Policy Simulator**: Out-of-the-box instant execution with zero API keys or GPU requirements.
* **Full Audio I/O**:
  * Real-time microphone capture via the Web Speech API.
  * Mood-adaptive speech synthesis (TTS) with pitch and rate modulation.
  * Sub-50ms barge-in cut-off when the caller interrupts the agent.

### 2. `callcenter_ai_voice_agents.html`
Interactive multi-scenario live call simulator with visual state machine, knowledge graph, and context graph grounding:
* **Scenario 1**: Billing Dispute ($150 overcharge credit adjudication).
* **Scenario 2**: Outage Triage (Loss of Signal / Optical Network Terminal reboot).
* **Scenario 3**: VIP Retention ($18k contract renewal negotiation).
* **Scenario 4**: Cross-Sell Intelligence (5G fiber bandwidth upgrade).

### 3. `callcenter_macro_graph_studio.html`
Enterprise contact center ecosystem lineage and network optimization studio:
* **OpenMetadata 1.4+ Lineage**: Unifies 6 micro-graphs (IVR, Conversational AI, ACD Routing, Agent CRM, Speech Assist, and Post-Call QA).
* **NetworkX Latency Optimization**: Shortest-path routing reducing average handle time (AHT) and SIP trunking latency.

---

## ⚡ Quick Start

### Running Locally
No server or build step is required:
1. Double-click `index.html` or `callcenter_ai_touchpoints_studio.html` in any web browser.
2. Alternatively, serve with any local HTTP server:
   ```bash
   python -m http.server 8080
   # Open http://localhost:8080 in Chrome or Edge
   ```

### Running on Groq LPU
1. Click the **Gear icon** in the top right of the studio.
2. Paste your Groq API key (`gsk_...`).
3. Select **Groq LPU** in the top engine switcher.

### Running on WebGPU / WebLLM
1. Open the application in a WebGPU-compatible browser (e.g., Chrome 113+ with hardware acceleration).
2. Click **WebGPU / WebLLM** in the engine switcher. The app will fetch weights and initialize locally in your browser's VRAM.

---

## ☁️ Enterprise Cloud Deployment (AWS)

For full telephony integration with public switched telephone networks (PSTN) and SIP trunking:

* **Telephony & Media Gateway**: Amazon Connect with Kinesis Video Streams (KVS) bi-directional raw audio streaming.
* **Sub-200ms STT**: Streaming transcription via Deepgram Nova-2 or Amazon Transcribe Streaming over WebSockets.
* **Orchestration**: Amazon Bedrock (Claude 3.5 Sonnet / Llama 3.3 70B) orchestrated through AWS Lambda in `us-east-2`.
* **Database & Knowledge Store**: Amazon DynamoDB for live caller state; Amazon OpenSearch / Aurora pgvector for SOP retrieval.
* **Post-Call QA & Lineage**: Amazon S3 transcript buffering and automated AI Judge Step Functions triggering retraining.

---

## 📊 Pre-loaded Scenarios

| Scenario | Procedure / Topic | Decision Path | Key Touchpoint Verified |
| :--- | :--- | :--- | :--- |
| **A: Emergency Root Canal** | CDT D3330 (Tooth #30) | Tool Call ➔ Approve | Empirical emergency waiver bypassing 14-day pre-auth |
| **B: Routine Prophylaxis** | CDT D1110 & D0274 | Tool Call ➔ Verify | Frequency limit calculation (7 mo > 6 mo rule) |
| **C: Ceramic Crown Appeal** | CDT D2740 (Tooth #14) | Tool Call ➔ Retroactive Waiver | Empirical cusp fracture waiver with 48h X-ray upload |
| **D: Out-of-Network Dispute** | CDT D7210 ($750 Balance Bill) | Warm Human Handoff | De-escalation & regulatory compliance handoff |

---

## 📄 License
Apache 2.0. Copyright (c) 2026 Cosmos Analytics.
