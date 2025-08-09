📚 SLM Stylized Story Generator: Controlled Narrative Generation for Children's Literature
Project Overview

This repository hosts a sophisticated project focused on fine-tuning a Small Language Model (SLM) to generate stylized children's stories. By leveraging the vast ajibawa-2023/Children-Stories-Collection dataset, this model is trained to recognize and implement specific narrative styles, such as 'Science,' 'Twist,' and 'Heartfelt,' using specialized prompt tokens.

The core technical innovation lies in efficiently processing a massive, multi-gigabyte dataset and implementing fine-grained stylistic control over the generated text.

✨ Key Features

Stylistic Control: Utilizes custom tokens ([SCIENCE], [TWIST], [HEARTFELT], etc.) to guide narrative style.

Efficient Data Processing: Handles a nearly 1 million-story dataset by serializing data into highly optimized binary formats (Apache Arrow/.bin).

Small Language Model (SLM) Optimization: Utilizes distilgpt2 for efficient fine-tuning and faster inference compared to larger models.

Hugging Face Ecosystem: Built entirely on the transformers and datasets libraries for seamless integration.

⚙️ Prerequisites

This project requires a Python environment (3.9+) and the following libraries:

code
Bash
download
content_copy
expand_less

pip install transformers datasets torch accelerate numpy
🚀 Getting Started
1. Data Processing and Serialization

The ajibawa-2023/Children-Stories-Collection dataset is too large to load entirely into memory. We must first tokenize and serialize it into a binary format.

The primary method involves converting the raw text dataset into a optimized binary format using the datasets library:

code
Bash
download
content_copy
expand_less
IGNORE_WHEN_COPYING_START
IGNORE_WHEN_COPYING_END
# Script to download, tokenize, and serialize the dataset
python scripts/prepare_data.py

Output: This process saves the tokenized dataset to the ./processed_stories_dataset directory in a memory-mapped format.

2. Fine-Tuning the SLM

The model is fine-tuned using the tokenized dataset. The style tokens are added to the tokenizer's vocabulary during initialization.

code
Bash
download
content_copy
expand_less
IGNORE_WHEN_COPYING_START
IGNORE_WHEN_COPYING_END
# Script to train the model on the preprocessed data
python scripts/train_slm.py

This script will:

Load distilgpt2.

Add custom style tokens to the tokenizer and resize the model's embeddings.

Train the model using the Hugging Face Trainer.

Output: The fine-tuned model and tokenizer will be saved to ./story-generator-final.

🤖 Usage: Generating Stylized Stories

Once the fine-tuning is complete, you can generate stories using the specialized pipeline.

Load the model:

code
Python
download
content_copy
expand_less
IGNORE_WHEN_COPYING_START
IGNORE_WHEN_COPYING_END
from transformers import pipeline

generator = pipeline(
    'text-generation', 
    model='./story-generator-final', 
    tokenizer='./story-generator-final'
)

Generate a Science Story:

code
Python
download
content_copy
expand_less
IGNORE_WHEN_COPYING_START
IGNORE_WHEN_COPYING_END
prompt_science = "[SCIENCE] Once upon a time, a curious owl named Professor Hoot discovered something amazing about gravity..."

output = generator(
    prompt_science, 
    max_length=200, 
    num_return_sequences=1, 
    do_sample=True, 
    top_p=0.9
)
print(output[0]['generated_text'])

Generate a Story with a Twist:

code
Python
download
content_copy
expand_less
IGNORE_WHEN_COPYING_START
IGNORE_WHEN_COPYING_END
prompt_twist = "[TWIST] The brave knight went on a quest to save the sleeping dragon, but when he reached the cave..."

output = generator(
    prompt_twist, 
    max_length=200, 
    num_return_sequences=1, 
    do_sample=True, 
    top_p=0.9
)
print(output[0]['generated_text'])
📂 Project Structure
code
Code
download
content_copy
expand_less
IGNORE_WHEN_COPYING_START
IGNORE_WHEN_COPYING_END
.
├── scripts/
│   ├── prepare_data.py        # Handles data serialization and style tokenization
│   └── train_slm.py           # Fine-tuning script for the SLM
├── processed_stories_dataset/ # Optimized, tokenized dataset files (Apache Arrow)
├── story-generator-final/     # Fine-tuned model and tokenizer weights
├── README.md                  # Project documentation (this file)
└── requirements.txt           # Python dependencies
🤝 Contribution

We welcome contributions! If you have suggestions for new style tokens, model architectures, or performance optimizations, please open an issue or submit a pull request.

📄 License

This project is licensed under the MIT License. See the LICENSE file for details.
