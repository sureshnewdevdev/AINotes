# 🧠 Ollama – Installation and Python Integration Guide

Ollama is an open-source framework that allows you to **run AI models locally** on your own system (Windows, macOS, or Linux).  
It’s perfect for privacy, offline AI assistants, and integrating open models like **Mistral**, **LLaMA**, or **Phi** directly into your Python apps.

---

## 🪟 Windows Installation

1. Open **PowerShell** as Administrator.
2. Run:
   ```bash
   winget install Ollama.Ollama
   ```
3. Start the Ollama service:
   ```bash
   ollama serve
   ```
4. Verify installation:
   ```bash
   ollama --version
   ```

---

## 🍎 macOS Installation

1. Open **Terminal**.
2. Run:
   ```bash
   brew install ollama
   ```
3. Start the Ollama service:
   ```bash
   ollama serve
   ```
4. Test it:
   ```bash
   ollama run llama3
   ```

---

## 🐧 Linux Installation

1. Open Terminal.
2. Install Ollama:
   ```bash
   curl -fsSL https://ollama.com/install.sh | sh
   ```
3. Start Ollama service:
   ```bash
   ollama serve
   ```
4. Test it:
   ```bash
   ollama run mistral
   ```

---

## 🧩 Download a Sample Model

You can use **Mistral** (fast and small).

### Step 1 – Pull a Model
```bash
ollama pull mistral
```

### Step 2 – Run it Interactively
```bash
ollama run mistral
```

Sample output:
```
>>> What is AI?
AI stands for Artificial Intelligence, the simulation of human intelligence by machines.
```

---

## 🐍 Use Ollama from Python

Ollama runs a local API at:
```
http://localhost:11434
```

### ✅ Python Example

```python
import requests
import json

url = "http://localhost:11434/api/generate"

payload = {
    "model": "mistral",
    "prompt": "Explain AI in one short paragraph."
}

response = requests.post(url, json=payload, stream=True)

for line in response.iter_lines():
    if line:
        data = json.loads(line)
        print(data.get("response", ""), end="")
```

### 🟣 Expected Output
```
Artificial Intelligence is the branch of computer science focused on building systems
that can perform tasks that require human-like reasoning, learning, and perception.
```

---

## ⚙️ Troubleshooting Tips

| Issue | Fix |
|-------|-----|
| ❌ “Connection refused” | Start Ollama service → `ollama serve` |
| ❌ “Model not found” | Pull the model first → `ollama pull mistral` |
| ⚠️ “Out of memory” | Use smaller model like `phi3` |
| 🐢 Slow performance | Ensure you have a GPU or reduce quantization bits |

---

## ✅ Summary

| Step | Command | Purpose |
|------|----------|----------|
| Install Ollama | `winget install Ollama.Ollama` | Setup |
| Start service | `ollama serve` | Run locally |
| Pull model | `ollama pull mistral` | Download |
| Run model | `ollama run mistral` | Chat manually |
| Python connect | `requests.post("http://localhost:11434/api/generate")` | Automate |
