# 🤖 Complete Guide to Installing and Using Ollama with Python (Small Model Setup)

This guide walks you through **installing Ollama**, setting up a **small AI model (phi3)**, writing a **Python program** to call the model, and organizing your project folder structure.

---

## 🧩 1️⃣ Folder Setup and Project Structure

Before you start, create a folder to organize everything neatly.

### 📂 Folder Structure
```
OllamaProject/
│
├── app/
│   └── ollama_call.py         # Python script to call Ollama API
│
├── docs/
│   └── Ollama_Notes.md        # Notes or documentation (this file)
│
└── requirements.txt           # Python dependencies
```

### 🪄 Steps to Create Folders (Windows PowerShell)
```bash
mkdir OllamaProject
cd OllamaProject
mkdir app, docs
New-Item requirements.txt
```

You’ll now have a clean workspace for your Ollama demo.

---

## ⚙️ 2️⃣ Install Ollama

### 🪟 **Windows Installation**
1. Open **PowerShell** as Administrator.
2. Run:
   ```bash
   winget install Ollama.Ollama
   ```
3. Start Ollama background service:
   ```bash
   ollama serve
   ```
4. Confirm installation:
   ```bash
   ollama --version
   ```

---

### 🍎 **macOS Installation**
1. Open **Terminal**.
2. Install using Homebrew:
   ```bash
   brew install ollama
   ```
3. Start the Ollama service:
   ```bash
   ollama serve
   ```

---

### 🐧 **Linux Installation**
1. Open terminal and run:
   ```bash
   curl -fsSL https://ollama.com/install.sh | sh
   ```
2. Start the Ollama service:
   ```bash
   ollama serve
   ```

---

## 🧠 3️⃣ Pull a Small and Fast Model

We’ll use **phi3** — a lightweight (2.2 GB) model perfect for local testing.

### 🪄 Download Model
```bash
ollama pull phi3
```

You’ll see something like:
```
pulling manifest
pulling 2.2GB model...
done
```

### 🧪 Test It in Terminal
```bash
ollama run phi3
```

Type your question:
```
>>> What is AI?
AI is the ability of machines to simulate human thinking and learning.
```
Press **Ctrl + C** to exit chat.

---

## 🐍 4️⃣ Python Setup

You can now interact with the local model using Python.

### Step 1 — Create a Virtual Environment (Optional but Recommended)
```bash
cd OllamaProject
python -m venv .venv
.venv\Scripts\activate       # Windows
source .venv/bin/activate      # macOS/Linux
```

### Step 2 — Install Required Libraries
In your virtual environment, run:
```bash
pip install requests
```

### Step 3 — Update `requirements.txt`
Add this line:
```
requests
```

---

## 💻 5️⃣ Python Program to Call Ollama API

Create this file inside the **app/** folder → `ollama_call.py`

```python
import requests
import json

# Ollama API endpoint (local host)
url = "http://localhost:11434/api/generate"

# Prepare request payload
payload = {
    "model": "phi3",
    "prompt": "Explain Artificial Intelligence in 3 short lines."
}

# Make POST request
response = requests.post(url, json=payload, stream=True)

# Stream and print response
for line in response.iter_lines():
    if line:
        data = json.loads(line)
        print(data.get("response", ""), end="")
```

### ▶️ Run the Script
From your terminal:
```bash
cd OllamaProject/app
python ollama_call.py
```

### ✅ Expected Output
```
Artificial Intelligence means machines can think.
They learn from data and experience.
It powers tools like chatbots and automation.
```

---

## 🧩 6️⃣ How Ollama Works (Architecture)

```
User Prompt
     ↓
Python Script (requests.post)
     ↓
Local API → http://localhost:11434
     ↓
Ollama Engine (runs phi3 model)
     ↓
Response streamed back to terminal
```

---

## 🧠 7️⃣ Troubleshooting

| Problem | Solution |
|----------|-----------|
| ❌ `Connection Refused` | Start Ollama service → `ollama serve` |
| ❌ `Model not found` | Download it → `ollama pull phi3` |
| 🐢 Slow or laggy | Use `tinyllama` (~1.1 GB) instead |
| 💥 Memory issues | Avoid big models like `llama3:70b` |

---

## 🔍 8️⃣ Useful Small Models

| Model | Size | Description | Command |
|--------|------|-------------|----------|
| **phi3** | ~2.2 GB | Fast, small, educational | `ollama pull phi3` |
| **tinyllama** | ~1.1 GB | Tiny, ultra-fast | `ollama pull tinyllama` |
| **gemma:2b** | ~2.5 GB | Balanced, multilingual | `ollama pull gemma:2b` |

🟢 *Start small, upgrade later once you’re confident!*

---

## 🧾 9️⃣ Summary of Commands

| Step | Command | Purpose |
|------|----------|----------|
| Install Ollama | `winget install Ollama.Ollama` | Setup Ollama |
| Start Service | `ollama serve` | Run locally |
| Pull Model | `ollama pull phi3` | Download small model |
| Test Run | `ollama run phi3` | Chat manually |
| Python Call | `python app/ollama_call.py` | Automate with Python |

---

## 🧭 🔟 Conclusion

🎯 You have successfully:
- Installed **Ollama** on your system  
- Downloaded a **small AI model (phi3)** for quick testing  
- Created a **Python script** that sends a prompt and receives a live response  
- Organized your project into a professional folder layout  

💡 **You now have your own private, offline AI assistant running locally on your computer!**

If you want to go deeper, try:
- Replacing `"phi3"` with `"mistral"` for better quality responses.
- Integrating Ollama with LangChain for multi-step workflows.
- Deploying your Ollama setup inside Docker for reproducible environments.

---

🧠 **End of Document**  
*(Created by ItTechGenie AI Tutor – Local AI Setup Guide)*
