# End-to-End AI Call Center Agent (Toy Example)

> **"Build the rules first, learn from calls second, then use both on every live call."**

A single-file HTML frontend application implementing the complete 7-step process from the architecture diagram:
1. **World Model (First Principles)**: Encodes dental insurance CDT procedure codes and eligibility rules.
2. **Batch: Voice to Script**: Bulk speech-to-text diarization with automated HIPAA PII redaction.
3. **Batch: Add Empirical Part**: Learns real-world call patterns to adapt rigid policy rules.
4. **Live: Voice to Script**: Live speech recognition with context-guided phonetic jargon correction.
5. **Live: Script to Decision**: Real-time decision routing (Answer, Tool, Human) powered by **Groq LPU**, in-browser **WebGPU / WebLLM**, or a built-in simulator.
6. **Live: Decision to Voice**: Mood-adaptive speech synthesis (TTS) with real-time barge-in interruption.
7. **Live: Decision to Evaluation**: AI Judge scoring with automated continuous batch retraining feedback.

---

## 🚀 How to Run

Zero build step or dependencies:

1. Double-click **`index.html`** in any browser (Chrome or Edge recommended).
2. Choose an engine:
   * **Deterministic Simulator**: Pre-loaded for instant execution without setup or keys.
   * **Groq LPU (Optional)**: Click the gear icon to add an API key for fast LPU inference.
   * **WebGPU / WebLLM (Optional)**: Runs a local lightweight model inside your browser GPU.
3. Click **"Run 7-Step Pipeline"** to watch the simulated end-to-end flow.

---

## 📄 License
MIT
