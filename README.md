# OCI Generative AI Chatbot Deployment

This repository demonstrates a practical chatbot deployment on Oracle Cloud Infrastructure (OCI) as part of the Oracle Cloud Infrastructure Generative AI Professional course. The course is designed for Software Developers, Machine Learning/AI Engineers, and Generative AI Professionals, covering topics such as pretrained foundational models, summarization, embeddings, Dedicated AI Clusters, and the OCI Generative AI security architecture.

## Course Overview

In this course, I learned how to enhance the chatbot's conversational abilities by integrating memory and implementing Retrieval-Augmented Generation (RAG) with LangChain. Additionally, I gained experience in deploying the chatbot on an OCI compute instance.

### The skills that i learned

1. **Fundamentals of Large Language Models (LLMs):**
   - LLM Basics
   - LLM Architectures
   - Prompt Engineering
   - Fine-tuning Techniques
   - Fundamentals of Code Models
   - Multi-modal LLMs and Language Agents

2. **OCI Generative AI Deep Dive:**
   - Pretrained Foundational Models (Generation, Summarization, Embedding)
   - Flexible Fine-tuning (including T-Few technique)
   - Model Inference
   - Dedicated AI Clusters
   - Generative AI Security Architecture

3. **Building a Conversational Chatbot with OCI Generative AI:**
   - Understanding Retrieval-Augmented Generation (RAG)
   - Vector Databases and Semantic Search
   - Building a Chatbot using the LangChain Framework (Prompts, Models, Memory, Chains)
   - Tracing and Evaluating the Chatbot
   - Deploying the Chatbot on OCI

# OCI Generative AI Chatbot Deployment

This repository demonstrates a practical chatbot deployment on Oracle Cloud Infrastructure (OCI) as part of the Oracle Cloud Infrastructure Generative AI Professional course. The course is designed for Software Developers, Machine Learning/AI Engineers, and Generative AI Professionals. It covers key topics such as pretrained foundational models, summarization, embeddings, Dedicated AI Clusters, and the OCI Generative AI security architecture.

## Course Overview

In this course, I learned how to enhance a chatbot’s conversational abilities by integrating memory and implementing Retrieval-Augmented Generation (RAG) with LangChain. Additionally, the course covered deploying the chatbot on an OCI compute instance.

## Skills You Will Learn

1. **Fundamentals of Large Language Models (LLMs):**
   - LLM basics
   - LLM architectures
   - Prompt engineering
   - Fine-tuning techniques
   - Fundamentals of code models
   - Multi-modal LLMs and Language Agents

2. **OCI Generative AI Deep Dive:**
   - Pretrained foundational models (generation, summarization, embedding)
   - Flexible fine-tuning (including T-Few technique)
   - Model inference
   - Dedicated AI Clusters
   - Generative AI security architecture

3. **Building a Conversational Chatbot with OCI Generative AI:**
   - Understanding RAG
   - Vector databases and semantic search
   - Building a chatbot using the LangChain framework (prompts, models, memory, chains)
   - Tracing and evaluating the chatbot
   - Deploying the chatbot on OCI

## Repository Overview

This repository contains various files for learning and certification purposes. However, the primary files needed for deploying the conversational chatbot are:

### Key Files

- **`demo-ou-chatbot-chroma-final-v1.py`:**  
  This script creates a vector store using the Chroma library, suitable for document retrieval tasks in natural language processing.

  **Key Features:**
  1. **Importing Libraries:** Includes `OCIGenAIEmbeddings`, `RecursiveCharacterTextSplitter`, and `Chroma` for essential tasks.
  2. **Loading and Splitting Documents:** Loads PDF documents from the `./pdf-docs` directory and splits them into manageable text chunks.
  3. **Setting Up OCI Generative AI Embeddings:** Uses a `LoadProperties` class to retrieve configuration settings and set up `OCIGenAIEmbeddings`.
  4. **Processing and Storing Documents in Batches:** Handles batch processing due to the embedding model's limit of 96 documents at a time.
  5. **Persisting the Vector Store:** Automatically saves data in Chroma 0.4.x and later.

- **`demo-chroma-create-v1.py`:**  
  A demonstration for creating a Chroma vector store using LangChain and OCI Generative AI embeddings.

  **Key Features:**
  1. **Importing Modules:** Includes libraries for PDF loading, text splitting, embedding generation, and vector storage.
  2. **Loading and Splitting Documents:** Loads and splits documents into 2,500-character chunks with a 100-character overlap.
  3. **Setting Up OCI Generative AI Embeddings:** Configures embeddings using model settings retrieved by `LoadProperties`.
  4. **Batch Processing:** Efficiently processes large datasets by splitting them into smaller batches.
  5. **Persisting the Vector Store:** Automatically saves the vector store for future retrieval and analysis.

- **`LoadProperties.py`:**  
  A utility class that loads configuration settings from a `config.txt` file (in JSON format) and provides access to these settings throughout the application.

## Step-by-Step Guide

In this guide, I will walk through the process of building and deploying an OCI Generative AI chatbot.

### 1. Setting up the OCI Environment

- Create a VM instance with the following configuration:
  - **Image:** Canonical Ubuntu 22.04
  - **Shape:** `VM.Standard.E4.Flex`
  - **Virtual Machine Specs:** 1 OCPU, 64 GB memory, 2 Gbps network bandwidth
- Download the SSH key and save it as `ubuntu-vm-priv.key`.

### 2. Connecting to the VM

- Open Windows PowerShell and connect via SSH:
  ```bash
  
  ssh -i ubuntu-vm-priv.key ubuntu@<VM_IP_Address>
  ```
- Upgrade Ubuntu packages:
   ```bash
   sudo apt update && sudo apt upgrade
   ```
- Install Python and Virtual Environment:
  ```bash
   sudo apt update && sudo apt upgrade
   ```
### 3. Setting Up the Project
- Create a virtual environment and activate it:
  ```bash
  virtualenv ouenv
   source ouenv/bin/activate
  ```
- Install dependencies from requirements.txt (copy the files from your local machine to the VM first):
  ```bash
    pip install -r requirements.txt
  ```
### 4. Setting Up Network Configuration:
- Set up the firewall to open port 8501:
```bash
sudo iptables -I INPUT 6 -m state --state NEW -p tcp --dport 8501 -j ACCEPT
 ```
### 5.Indexing Documents and Running the Chatbot
- Index the documents:
```bash
python3 demo-chroma-create-v1.py
```
- Start the chroma server:
```bash
chroma run --host localhost --port 8000 --path ./chroma.sqlite3
```
- Run the Streamlit Application:
```bash

streamlit run demo-ou-chatbot-chroma-final-v1.py --server.port 8501
```








