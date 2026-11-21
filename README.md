# End-to-End AI Call Center Agent — Cellular Carrier (Toy Example)

> **"Build the rules first, learn from calls second, then use both on every live call."**

A single-file HTML frontend application demonstrating the complete 7-step process from the architecture diagram for a **Cell Phone / Mobile Carrier Call Center** (eSIM activation, 5G data deprioritization, international roaming waivers, CPNI privacy, and anti-SIM swap hijacking protection).

### The 7 Touchpoints:
1. **World Model (First Principles)**: Encodes cellular network logic: SIM/eSIM, EID, IMEI, 5G priority buckets, and FCC CPNI authentication rules.
2. **Batch: Voice to Script**: Bulk speech-to-text diarization with automated CPNI PIN and account redaction.
3. **Batch: Add Empirical Part**: Learns real-world caller patterns (e.g. mapping "SOS only" to unprovisioned eSIM, courtesy roaming bill shock waivers).
4. **Live: Voice to Script**: Streaming speech recognition with telecom jargon autocorrection ("easy sim" ➔ eSIM over-the-air push).
5. **Live: Script to Decision**: Real-time decision routing (Answer, Network Tool, or Fraud Escalation) on **Groq LPU**, in-browser **WebGPU / WebLLM**, or the deterministic simulator.
6. **Live: Decision to Voice**: Mood-adaptive speech synthesis (TTS) with sub-50ms barge-in interruption.
7. **Live: Decision to Evaluation**: AI Judge scoring with automated continuous batch retraining feedback.

---

## 🚀 How to Run

Zero build step or dependencies:

1. Double-click **`index.html`** in any web browser (Chrome or Edge recommended).
2. Choose an engine:
   * **Deterministic Simulator**: Pre-loaded for instant execution without setup or keys.
   * **Groq LPU (Optional)**: Click the gear icon to add an API key for fast LPU inference.
   * **WebGPU / WebLLM (Optional)**: Runs a local lightweight model inside your browser GPU.
3. Click **"Run 7-Step Pipeline"** to watch the simulated end-to-end flow.

---

## 📱 Pre-loaded Cellular Scenarios

* **Scenario A: Sudden "SOS Only" & eSIM Activation Failure (iPhone 16 Pro)** — Remote over-the-air profile push to EID.
* **Scenario B: International Roaming Bill Shock & Courtesy Credit ($120)** — Empirical waiver with TravelPass enrollment.
* **Scenario C: 5G Priority Data Deprioritization & Hotspot Top-Up** — Congestion deprioritization explanation and complimentary speed boost.
* **Scenario D: Urgent SIM-Swap Attack & Fraud Security Handoff** — Emergency rogue SIM revocation, port-out lock, and warm transfer to Carrier Fraud Bureau.

---

## 📄 License
MIT
