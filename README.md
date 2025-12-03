.

🌟 Agentic AI for Early Sepsis Detection in ICU (MIMIC-IV)
Multimodal • Fuzzy Logic • GA Optimization • LLM Reasoning
🚑 Overview

Early detection of sepsis is a life-critical problem — every hour of delay significantly increases mortality.
Traditional methods depend on late-stage organ dysfunction (Sepsis-3 criteria), causing delays of 6–12 hours.

This project builds a multimodal, interpretable, agentic AI system for early ICU sepsis risk detection, using a 10,000-stay subset of the MIMIC-IV dataset.

The system integrates:

📊 Time-series Vitals

🧪 Laboratory Trends

🧬 Fuzzy Logic Risk Scoring

🧬 GA Optimization (optimized thresholds)

🧠 LLM Agent (clinical reasoning + action suggestions)

📝 Clinical Notes (discharge & radiology text)

Unlike black-box ML models, this pipeline provides:
✔ Numerical predictions,
✔ Clinically interpretable fuzzy risk, and
✔ Human-like reasoning.

⭐ Project Highlights
🔷 1. Multimodal Data Fusion

Combines vitals, labs, demographics, diagnoses, and clinical text from MIMIC-IV.

🔷 2. GA-Optimized Fuzzy Logic

A transparent fuzzy risk score capturing soft abnormality in HR, BP, RR, SpO₂.

Genetic Algorithm tunes:

High HR threshold

Low SBP threshold

for maximal predictive value.

🔷 3. Agentic LLM Clinical Reasoning

A Gemini-based agent generates:

Clinical interpretations

Risk assessments

Recommended next actions

This forms a closed loop: Perceive → Reason → Suggest.

🔷 4. ICU-Ready Interpretability

Doctors can understand WHY the model gives a risk score.

🔷 5. Fully Reproducible Kaggle Notebook

End-to-end pipeline:

Load subset files

Feature engineering

Fuzzy scoring

GA optimization

LLM agent

🧠 Architecture
            ┌─────────────────────────────┐
            │        Raw MIMIC-IV         │
            │ Vitals | Labs | Notes | ICD │
            └─────────────────────────────┘
                          │
                          ▼
     ┌────────────────────────────────────────┐
     │     Preprocessing & Feature Fusion     │
     │  (HR/SBP/RR/Temp/SpO2 + Labs + Demo)   │
     └────────────────────────────────────────┘
                          │
                          ▼
     ┌────────────────────────────────────────┐
     │       Fuzzy Logic Risk Scoring         │
     │ (Soft abnormality: high HR, low SBP…)  │
     └────────────────────────────────────────┘
                          │
                          ▼
     ┌────────────────────────────────────────┐
     │     Genetic Algorithm Optimization     │
     │ (Tune HR/SBP fuzzy thresholds)         │
     └────────────────────────────────────────┘
                          │
                          ▼
     ┌────────────────────────────────────────┐
     │        LLM Agentic Reasoning           │
     │  “Explain risk + suggest next action”  │
     └────────────────────────────────────────┘
                          │
                          ▼
     ┌────────────────────────────────────────┐
     │      Early Sepsis Risk Prediction      │
     └────────────────────────────────────────┘

📂 Dataset Used

10k ICU-stay subset derived from MIMIC-IV using BigQuery:

icustay_subset.csv

chartevents_filtered.csv (vitals)

labevents_filtered.csv (labs)

patients_subset.csv

admissions_subset.csv

diagnoses_withstayids.csv

discharge_notes_clean.csv

radiology_notes_clean.csv

🔬 Fuzzy Logic Model
Input Variables:

HR_mean

SBP_mean

RR_mean

SpO₂_mean

Membership Functions:

High HR

Low SBP

High RR

Low SpO₂

Aggregation:

Additive inference:

Risk = HR_high + SBP_low + RR_high + SpO2_low

Defuzzification:

Soft defuzzification using:

fuzzy_score = tanh(aggregated_risk)


Returns a clean 0–1 risk score.

🧬 Genetic Algorithm (GA) Optimization

Optimizes fuzzy cutpoints:

HR_high_cut

SBP_low_cut

Uses AUROC as fitness.
Final optimized parameters example:

Best GA parameters: [118.36, 51.25]

🤖 LLM Agent Component

Given:

vitals summary

lab summary

fuzzy_score

clinical notes (optional)

LLM generates:

Clinical interpretation

Risk narrative

Suggested actions

Example output:

“The patient shows moderate tachycardia and low SBP. Recommend fluid assessment and lactate re-check.”

This forms an agentic AI loop.

💻 How to Run (Kaggle)

Upload your MIMIC subset files to /kaggle/input

Open the provided notebook

Run sequentially:

Load data

Preprocess

Fuzzy Logic

GA Optimization

LLM Agent

Get final risk score + explanation

📊 Outputs

fuzzy_score (0–1)

GA-optimized thresholds

LLM-generated explanation

Risk assessment summary

✨ Key Contributions

✔ Novel agentic architecture
✔ Combined fuzzy logic + GA + LLM
✔ Transparent early-warning scoring
✔ Real-world clinical interpretability
✔ Multimodal MIMIC-IV fusion
✔ Fully reproducible pipeline

🚀 Future Work

Add proper Sepsis-3 label extraction

Integrate real-time streaming vitals

Train transformer-based note embeddings

Expand fuzzy rules / more membership functions

Build bedside decision-support dashboard

❤️ Acknowledgements

This project uses data from the MIMIC-IV database (MIT-PhysioNet).
Ensure proper credentialing & CITI training before use.

📘 License

For academic and research use under MIMIC-IV dataset restrictions.
