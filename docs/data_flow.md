# Data Flow Overview

This document explains how data is processed step-by-step in the n8n workflow.

---

## 1️⃣ Fetch and Clean Data
**Node:** `HTTP Request` → `Code in JavaScript`

- Fetches the last 7 days of sensor data from ThingSpeak.
- Filters invalid entries and converts values to numeric form.
- Keeps only `timestamp`, `temperature`, `inclination_x`, and `inclination_y`.

---

## 2️⃣ Compute Statistics
**Node:** `Code in JavaScript1`

- Calculates minimum, maximum, and average values for:
  - Temperature
  - Inclination X
  - Inclination Y
- Output format:
  ```json
  {
    "stats": {
      "temperature": { "min": ..., "max": ..., "avg": ... },
      "inclinationX": { "min": ..., "max": ..., "avg": ... },
      "inclinationY": { "min": ..., "max": ..., "avg": ... }
    }
  }
  ```

---

## 3️⃣ Prepare Data for Report
**Node:** `Code in JavaScript2`

- Converts the cleaned data into a readable JSON string (`reportInput`).
- Keeps both the raw data and computed statistics ready for the LLM.

---

## 4️⃣ Generate Report
**Node:** `Basic LLM Chain` (connected to `OpenRouter Chat Model`)

- Passes structured prompt and the `reportInput` data to an LLM (e.g., `gpt-4.1-mini` or `llama-3.1-70b`).
- Produces a markdown-formatted weekly report.

---

## 5️⃣ Send Email
**Node:** `Gmail`

- Sends the generated report automatically every Monday at 08:00.

---

📊 **Summary**
The workflow turns raw ThingSpeak IoT data → cleans → analyzes → reports → emails.
