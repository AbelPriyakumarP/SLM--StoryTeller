## 📚 SLM Stylized Story Generator: Controlled Narrative Generation for Children's Literature
---

## Project Overview

This repository hosts a sophisticated project focused on fine-tuning a Small Language Model (SLM) to generate stylized children's stories. By leveraging the vast **`ajibawa-2023/Children-Stories-Collection`** dataset, this model is trained to recognize and implement specific narrative styles, such as 'Science,' 'Twist,' and 'Heartfelt,' using specialized prompt tokens.

The core technical innovation lies in efficiently processing a massive, multi-gigabyte dataset and implementing fine-grained stylistic control over the generated text.

---

## ✨ Key Features

*   **Stylistic Control:** Utilizes custom tokens (`[SCIENCE]`, `[TWIST]`, `[HEARTFELT]`, etc.) to guide narrative style.
*   **Efficient Data Processing:** Handles a nearly 1 million-story dataset by serializing data into highly optimized binary formats (Apache Arrow/`.bin`).
*   **Small Language Model (SLM) Optimization:** Utilizes `distilgpt2` for efficient fine-tuning and faster inference compared to larger models.
*   **Hugging Face Ecosystem:** Built entirely on the `transformers` and `datasets` libraries for seamless integration.

---

## ⚙️ Prerequisites

This project requires a Python environment (3.9+) and the following libraries. You can install them via pip:

```bash
pip install transformers datasets torch accelerate numpy
```

## 🚀 Getting Started

# Step 1: Data Processing and Serialization
The ajibawa-2023/Children-Stories-Collection dataset is too large to load entirely into memory. The following script will tokenize the dataset and serialize it into an efficient binary format.

# Script to download, tokenize, and serialize the dataset
python scripts/prepare_data.py
Output: This process saves the tokenized dataset to the ./processed_stories_dataset directory in a memory-mapped format, ready for training.

# Step 2: Fine-Tuning the SLM
The model is fine-tuned using the pre-processed data. The style tokens are automatically added to the tokenizer's vocabulary during initialization.

# Script to train the model on the preprocessed data
python scripts/train_slm.py
Output: The fine-tuned model and tokenizer will be saved to the ./story-generator-final directory.
---

# 🤖 Usage: Generating Stylized Stories
Once the model is trained, you can easily generate stories using the specialized pipeline.

Load the Generator Pipeline
from transformers import pipeline

generator = pipeline(
    'text-generation', 
    model='./story-generator-final', 
    tokenizer='./story-generator-final'
)
---

# 🤝 Contribution
We welcome contributions! If you have suggestions for new style tokens, model architectures, or performance optimizations, please open an issue or submit a pull request.
