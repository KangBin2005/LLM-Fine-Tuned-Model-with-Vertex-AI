# 🧠 LLM Fine-Tuned Model with Vertex AI

## 📖 About This Project

This project was developed for the **IT3386 - AI Services in Analytics** assignment, focusing on building, configuring, and evaluating a Large Language Model (LLM) using Google Cloud Vertex AI. 

The repository demonstrates how **Supervised Fine-Tuning (SFT)** can transform a general-purpose LLM into a domain-specific AI assistant capable of providing structured, accurate, and context-aware responses for **Financial Literacy & Budgeting** tailored for young adults and students in Singapore.

---

## 🎯 Key Project Tasks Completed

* **Data Engineering:** Curated a custom `JSONL` training dataset consisting of 10 structured financial advisor prompt-response pairs (focusing on concepts like the 50/30/20 rule, emergency funds, and DBS NAV Planner tools).
* **Cloud Infrastructure Automation:** Built data pipelines to programmatically connect with Google Cloud, initializing secure access via a Service Account and handling data transfers to Google Cloud Storage (GCS) buckets.
* **Supervised Fine-Tuning (SFT):** Specialized a `gemini-2.5-flash-lite` base model on Vertex AI and systematically conducted hyperparameter tuning to find the optimal configuration (**4 epochs**).
* **Full-Stack Evaluation UI:** Developed a side-by-side benchmarking dashboard using Gradio to compare the fine-tuned model against the native base Gemini API across seen data, unseen data, and out-of-scope safety queries.
* **Advanced RAG Companion Pathway:** Engineered an alternative Retrieval-Augmented Generation (RAG) system utilizing **ChromaDB** and the `text-embedding-004` embedding model to ground generation in external knowledge documents.
* **Resource Cost-Cleanup:** Implemented strict programmatic teardown workflows to cleanly undeploy endpoints, delete cloud models, and clear buckets to prevent unnecessary cloud resource overhead.

---

## 💻 Tech Stack
* **Core Language:** Python
* **Cloud Ecosystem:** Google Cloud Platform (GCP Vertex AI, Google Cloud Storage)
* **LLM Foundations:** Gemini 2.5 Flash Lite
* **Vector Knowledge Base:** ChromaDB, `text-embedding-004`
* **Interface & Tooling:** Jupyter Notebooks, Gradio UI

---

## 📁 Repository Structure

```text
├── 244423Q_new data prep v2.ipynb
│   └── Data preparation, JSONL validation, GCS bucket automation, and cloud cleanup logic.
│
├── 244423Q_Model Finetuning template v2-edit.ipynb
│   └── SFT model training pipeline, Gradio comparison UI, and ChromaDB RAG implementation.
│
├── data/
│   ├── budgeting_dataset.jsonl
│   │   └── The custom-curated SFT training corpus containing targeted domain examples.
│   │
│   └── budgetting101.pdf
│       └── External knowledge document utilized as the context source for the RAG pipeline.
│
├── IT3386_244423Q_AIA_Assignment_Report.docx
│   └── Full evaluation, training analysis, project limitations, and discussion report.
│
└── README.md
    └── This file.
```

## 🚀 Quick Setup & Runtime Snippets
📦 Prerequisites
Install the required Google Cloud, generation, and vector DB libraries:
```bash
conda install -c conda-forge google-cloud-aiplatform google-cloud-storage
pip install -U google-genai gradio chromadb
```

## 🔐 Authentication Setup
```python
# Pass service account token to your notebook environment
%env GOOGLE_APPLICATION_CREDENTIALS=sa-244423q.json
```

## Vertex AI Fine-Tuning Launcher
```python
from vertexai.preview.tuning import sft

tuned_model = sft.train(
    source_model="gemini-2.5-flash-lite",
    train_dataset="gs://gcp-pj-vertex-244423q-881e-3386-aip/budgeting_dataset.jsonl",
    epochs=4,
    learning_rate_multiplier=1.0,
    tuned_model_display_name="financial-literacy-assistant"
)
```

## Programmatic Cloud Cleanup
```python
# Clean up endpoints to avoid resource charges
endpoint.undeploy_all()
endpoint.delete()
model.delete()
```

