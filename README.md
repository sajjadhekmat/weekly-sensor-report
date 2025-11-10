# 🏗️ Structural Health Monitoring — Automated Weekly Report (n8n + OpenRouter)

This project automates the generation of a **weekly structural health report**  
using **ThingSpeak IoT sensor data**, processed and analyzed through **n8n** and an **LLM model** (OpenRouter / OpenAI).  
It combines IoT data retrieval, preprocessing, AI-based analytics, and automatic reporting — all in one automated workflow.

---

## 🔁 Workflow Overview

**Automation Flow:**
1. **Cron Trigger** – Runs automatically every Monday at 08:00 (Europe/Paris time).
2. **HTTP Request** – Fetches the last 7 days of data from the ThingSpeak API.
3. **Code Nodes** – Clean and organize JSON, then compute weekly statistics (min, max, average).
4. **Basic LLM Chain (OpenRouter / OpenAI)** – Uses an AI model (e.g., GPT-4.1-mini) to generate a detailed, structured technical report.
5. **Email Node (Gmail)** – Sends the final report automatically to the engineering or research team.

---

## 🧠 Project Goal

This workflow is designed for **structural health monitoring (SHM)** of small structures equipped with **low-cost IoT sensors**.  
The goal is to:
- Automate weekly data analysis.
- Detect potential drifts or anomalies.
- Correlate temperature with inclination (X/Y).
- Produce professional reports for engineers or researchers.

---

## 🧩 Repository Structure

```
├── workflow/
│   └── weekly_sensor_workflow.json     # Exported n8n workflow
├── docs/
│   ├── architecture.png                # System diagram or workflow screenshot
│   └── data_flow.md                    # Step-by-step data transformation description
├── examples/
│   └── sample_output_report.md         # Example AI-generated weekly report
└── README.md
```

---

## ⚙️ Requirements

Before running this project, ensure you have:

- [n8n](https://n8n.io) (v1.50+ recommended)
- **ThingSpeak Channel Read API Key**  
  (for accessing the IoT data)
- **OpenRouter or OpenAI API Key**  
  (for AI report generation)
- **Gmail or SMTP credentials**  
  (for sending reports by email)

---

## 🚀 Setup Instructions

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/yourusername/weekly-sensor-monitoring.git
cd weekly-sensor-monitoring
```

### 2️⃣ Open n8n
- Launch n8n via your browser or local instance.
- Go to **Workflows → Import from File**.
- Select the file:  
  `workflow/weekly_sensor_workflow.json`

### 3️⃣ Configure Credentials
- Open the imported workflow.
- Add credentials for:
  - **OpenRouter/OpenAI API key**
  - **Gmail (or SMTP)** for email
- Update the **ThingSpeak Channel API Key** in the *HTTP Request* node (if needed).

### 4️⃣ Test the Workflow
- Click **Execute Workflow** to test it manually.
- Verify that:
  - Data is retrieved correctly.
  - The LLM generates a readable technical report.
  - The email is received successfully.

### 5️⃣ Enable Weekly Scheduling
- Open the **Cron Node**.
- Set to trigger automatically every week (e.g., Monday 08:00).
- Save and enable the workflow.

---

## 📊 Data Flow Summary

| Step | Node Name | Function |
|------|------------|-----------|
| 1 | **Cron Schedule** | Triggers the workflow weekly |
| 2 | **HTTP Request** | Fetches 7 days of sensor data (Temperature, Inclination X/Y) |
| 3 | **Code (Clean JSON)** | Cleans data and removes nulls or invalid readings |
| 4 | **Code (Calculate Stats)** | Calculates min, max, and average for each variable |
| 5 | **Basic LLM Chain** | Sends processed JSON to AI for report generation |
| 6 | **OpenAI/OpenRouter Model** | Generates a markdown-formatted technical report |
| 7 | **Email Node** | Sends report to defined recipient(s) automatically |

---

## 🔒 Security Notes

- Never commit API keys or passwords in your workflow exports.
- Use **n8n Credentials Manager** to securely store:
  - OpenRouter/OpenAI API keys  
  - ThingSpeak tokens  
  - Gmail/SMTP credentials
- Check that `.gitignore` excludes files like `credentials.json`.

---

## 📸 Example Output

**Generated AI Report Example:**

```markdown
### 1) Summary
- **Period Analyzed:** From 2025-11-04T00:07:24Z to 2025-11-05T14:52:06Z (approximately 1.6 days due to limited data provided).
- **Typical Temperature Range:** 14.5°C to 20.5°C.
- **Typical Inclination Ranges:**
  - Inclination X: approx. 0.8° to 1.18°.
  - Inclination Y: approx. 0.59° to 0.70°.
- **Key Conclusions:**
  - Temperature data shows a gradual variation over the scanning period, typical for environmental changes.
  - Inclination measurements reveal smooth variations with temperature, indicating expected structural thermal response without abrupt anomalies.
  - No sensor malfunction or abrupt data gaps detected, suggesting reliable sensor performance.

```

---

## 👷 Author

**Sajjad Hekmat**  
Data Scientist/PhD Researcher@UniLisboa
Automation with n8n + IoT + LLMs  
📧 [sajjad.hekmat1995@gmail.com](mailto:sajjad.hekmat1995@gmail.com)

---

## 🧾 License
This project is released under the **MIT License**.  
You are free to use, modify, and distribute it with attribution.

---

## ⭐ Acknowledgements
- [ThingSpeak IoT Platform](https://thingspeak.mathworks.com)
- [n8n.io](https://n8n.io)
- [OpenRouter API](https://openrouter.ai)
- [OpenAI API](https://openai.com)

---

📘 *If this project helps you automate your sensor analysis, please star the repo and share it!*
