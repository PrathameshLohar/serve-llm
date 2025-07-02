# 📘 LLaMA 2 Textbook QA Chatbot

This project demonstrates how to deploy a **fine-tuned LLaMA 2 7B model** for answering textbook-style questions using **Streamlit**. It is made to run seamlessly in environments like **Google Colab**, with a public URL provided via **Cloudflare Tunnel**.

---

## 🚀 Features

* Ask any question based on the contents of a textbook.
* Powered by **LLaMA 2 7B**, fine-tuned using the [QLoRA](https://arxiv.org/abs/2305.14314) method.
* Lightweight deployment using **4-bit quantization** via `bitsandbytes`.
* User-friendly interface built with **Streamlit**.
* Accessible on the web using **Cloudflare Tunnel**.

---

## 🧠 About the Model: `Prathamesh25/Llama-2-7b-chatbot-textbook`

This model is a **fine-tuned variant of Meta’s LLaMA 2 7B** for answering **educational and textbook-related questions**.
Key points:

* **Base Model**: `meta-llama/Llama-2-7b-hf`
* **Fine-tuning method**: [QLoRA](https://github.com/artidoro/qlora) for low-RAM training.
* **Training Dataset**: Custom textbook QA pairs in ChatML-style format.
* **Quantization**: Uses 4-bit quantization (`nf4`) for optimized inference on consumer GPUs.
* **Hosted on**: [Hugging Face Hub](https://huggingface.co/Prathamesh25/Llama-2-7b-chatbot-textbook)

---

## ☁️ About Cloudflare Tunnel

**Cloudflare Tunnel** is a secure way to expose localhost servers (like Streamlit running on port 8501) to the internet without exposing your IP or configuring a server.
Used here to make the Streamlit UI available in a notebook (e.g., Colab) via a public HTTPS URL.

Steps involved:

1. Download Cloudflare Tunnel binary.
2. Launch Streamlit app on localhost.
3. Run the tunnel command:

   ```bash
   ./cloudflared tunnel --url http://localhost:8501
   ```
4. A public link (e.g., `https://randomstring.trycloudflare.com`) is generated.

---

## 📦 Installation

Install required libraries:

```bash
!pip install -q streamlit pyngrok transformers bitsandbytes accelerate peft
```

---

## 📁 App Setup

Write the app code using:

```python
%%writefile app.py
# Streamlit code here...
```

It loads the tokenizer and 4-bit quantized model, takes user input, and generates responses.

---

## ▶️ Running the App in Colab

```bash
# Step 1: Install Cloudflare Tunnel binary
!wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 -O cloudflared
!chmod +x cloudflared

# Step 2: Launch Streamlit
!streamlit run app.py &> logs.txt &

# Step 3: Start Tunnel and get public link
!./cloudflared tunnel --url http://localhost:8501
```

Open the URL shown in output to access your chatbot.

---
## 🖼️ App Screenshot

Here’s a glimpse of the Streamlit UI in action:

![LLaMA 2 Textbook Chatbot Screenshot](assests\streamlit-demo-cloufare-app.png)


## 💬 Example Prompt

```
What is Newton's first law of motion?
```

---

## 📎 Notes

* `st.cache_resource` ensures model loads only once.
* `BitsAndBytesConfig` enables running large models in 4-bit on lower-end GPUs.
* Prompt format uses ChatML-style `[INST] ... [/INST]`.

---

## 👨‍💻 Author

**Prathamesh Lohar**
🔗 [Model on Hugging Face](https://huggingface.co/Prathamesh25/Llama-2-7b-chatbot-textbook)

---
