# Building a Generative AI Chatbot with Ollama API in Python

Generative AI has moved far beyond academic research — it is now an integral part of business automation, customer support, marketing content creation, data analysis, and product innovation.

In this article, we’ll walk through a **Python-based integration with Ollama’s API** to create a chatbot-like interaction, and we’ll explore the available modes and use cases.

---

## 1. What is Ollama?

Ollama is a **local large language model (LLM) serving tool** that lets you run models like **LLaMA, Mistral**, and others on your own machine **without sending data to the cloud**.

It exposes a **REST API** so you can integrate LLM capabilities into your Python, JavaScript, or backend applications.

---

## 2. Understanding the API Structure

The basic API endpoint for chatting is:

```bash
POST /api/chat
```
Where:

```model``` → The name of the model you want to use (e.g., ```llama2```, ```mistral```, ```gemma```, etc.).

```messages``` → A list of chat history messages in ```{ role, content }``` format.

```stream``` → Whether to stream the output in chunks or get it in one response.

## 3. The Example Code
Here’s a minimal Python script to interact with Ollama’s chat API:

```bash
import os
import requests

# 1. Load API configuration from environment variables
url = os.getenv('OLLAMA_BASE_URL') + '/api/chat'
model = os.getenv('OLLAMA_MODEL')

# 2. Prepare the conversation history
messages = [
    {
        "role": "user",
        "content": "Describe some of the business applications of Generative AI"
    }
]

# 3. Create the payload
payload = {
    "model": model,
    "messages": messages,
    "stream": False
}

# 4. Send the POST request
response = requests.post(url, json=payload)

# 5. Print the model's response
print(response.json())

```
## 4. Step-by-Step Explanation
Step 1 — Environment Variables

```bash
url = os.getenv('OLLAMA_BASE_URL') + '/api/chat'
model = os.getenv('OLLAMA_MODEL')
```

```OLLAMA_BASE_URL``` → The base address of your Ollama server (e.g., ```http://localhost:11434``` if running locally).

```OLLAMA_MODEL``` → The model you want to use (e.g., ```llama2:13b```, ```mistral:7b```).

Using environment variables keeps credentials/config out of code.

## Step 2 — Message Structure

```bash
messages = [
    {"role": "user", "content": "Describe some of the business applications of Generative AI"}
]
```

role can be:

```"system"``` → sets behavior and tone (e.g., “You are a helpful assistant”).

```"user"``` → human input.

```"assistant"``` → AI’s prior responses.

**Why this matters**: By keeping the history, the model can maintain context.

### Step 3 — Payload and Modes
```bash
payload = {
    "model": model,
    "messages": messages,
    "stream": False
} 
```


```model``` → Which LLM to use. Bigger models = more reasoning, smaller = faster.

```messages``` → The entire conversation history.

```stream:```

  - ```True``` → Response arrives token-by-token (good for live chat UIs).

  -  ```False``` → Response comes as one complete block (simpler but slower to display).


## Step 4 — Sending the Request

```bash
response = requests.post(url, json=payload)
```
Uses Python’s requests library to send a POST request.

API returns JSON with the AI’s generated text.

## Step 5 — Reading the Response
```bash
print(response.json())
```
A typical response looks like:

```bash
{
  "model": "llama2",
  "created_at": "2025-08-11T10:00:00Z",
  "message": {
    "role": "assistant",
    "content": "Generative AI can be applied in business for..."
  },
  "done": true
}
```
## 5. Modes in Ollama API
Ollama supports different interaction modes depending on the endpoint and parameters:

| **Mode**           | **Description**                          | **Use Case**                            |
| ------------------ | ---------------------------------------- | --------------------------------------- |
| `/api/chat`        | Structured chat with role-based messages | Customer support bots, tutoring systems |
| `/api/generate`    | Free-form text generation from a prompt  | Blog writing, product descriptions      |
| `/api/embeddings`  | Vector embedding generation for text     | Search, semantic similarity             |
| Streaming (`True`) | Streams tokens in real-time              | Live chat UIs, CLI assistants           |
| Batch (`False`)    | Returns full response at once            | API calls in backend processing         |


## 6. Real Business Applications of Generative AI
With Ollama or other LLMs, companies can:

**Automate Customer Support** → 24/7 answering FAQs.

**Generate Marketing Content** → Blog posts, social media captions.

**Summarize Documents** → Legal, medical, financial.

**Code Assistance** → Automated code generation & review.

**Product Research** → Idea generation, competitor analysis.

**Internal Knowledge Base Search** → Chat with company documents.
