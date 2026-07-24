# Climate-Framing-Affect: A Multi-Stage Framework for Analyzing Climate Change Discourse

This repository contains the annotated datasets, model training notebooks, and reproducibility materials for the paper titled:

> **"Where Climate-Action Discourse Diverges: Governance Registers and Expressed Eco-Emotion Across Communicative Arenas"**

---

## 📂 Repository Structure

```
Climate-Framing-Affect/
│
├── data/
│   ├── stage1_institutional_news_sdg_13_dimension.xlsx
│   ├── stage1_public_discourse_sdg13_dimension.xlsx
│   └── stage2_public_discourse_eco_emotion.xlsx
│
├── notebooks/
│   ├── multilabel_stage1_institutional_news.ipynb
│   ├── multilabel_stage1_public_discourse.ipynb
│   ├── multiclass_stage2_public_discourse.ipynb
│   └── bertopic_sdg13.ipynb
│
├── models/
│   └── README.md
│
├── .gitignore
├── CITATION.cff
├── LICENSE
├── README.md
└── requirements.txt
```

---

## 📘 Project Overview

This project introduces a multi-stage computational framework to analyze how climate change is:

- **Framed** (Stage 1: SDG 13 Sub-Target Dimension Classification — mapping discourse to Climate Resilience, Policy Integration, and Education & Awareness)
- **Felt** (Stage 2: Eco-Emotion Classification — identifying affective responses embedded in climate discourse)
- **Structured** (Topic Modeling: unsupervised BERTopic analysis across institutional news and public discourse arenas)

Two complementary modeling approaches were applied across these tasks:

- **Supervised BERT fine-tuning** (`bert-base-uncased`) for Stage 1 (multi-label) and Stage 2 (multi-class) classification
- **Unsupervised BERTopic** for latent topic discovery across the three SDG 13 sub-targets

---

## 📁 Dataset

Labeled datasets are available in the `/data` folder, organized by analysis stage and discourse arena:

| File | Stage | Description |
|---|---|---|
| `stage1_institutional_news_sdg_13_dimension.xlsx` | Stage 1 | Institutional-news documents annotated for three SDG 13 sub-target dimensions (multi-label, binary per dimension) |
| `stage1_public_discourse_sdg13_dimension.xlsx` | Stage 1 | Public-discourse documents annotated for three SDG 13 sub-target dimensions (multi-label, binary per dimension) |
| `stage2_public_discourse_eco_emotion.xlsx` | Stage 2 | Subset of Stage 1 public-discourse documents additionally annotated with one eco-emotion label per document (multi-class) |

Each file contains preprocessed text data drawn from institutional news sources and public social media discourse. The **raw corpora** are not redistributed due to platform terms of service and publisher copyright; please contact the corresponding author for access requests.

---

## 🧠 Model Training Notebooks

The `/notebooks` folder contains all notebooks for fine-tuning BERT and running the BERTopic pipeline:

- `multilabel_stage1_*.ipynb` — supervised multi-label BERT classification for Stage 1 (SDG 13 sub-target dimensions), one notebook per discourse arena
- `multiclass_stage2_public_discourse.ipynb` — supervised multi-class BERT classification for Stage 2 (eco-emotion)
- `bertopic_sdg13.ipynb` — unsupervised BERTopic pipeline for latent topic discovery
- Fine-tuning configurations (batch size, learning rate, epochs) follow the best-performing setups reported in the paper

| # | Notebook | Stage | Input | Main Outputs |
|---|---|---|---|---|
| 01 | `multilabel_stage1_institutional_news.ipynb` | Stage 1 — Multi-label BERT | `stage1_institutional_news_sdg_13_dimension.xlsx` | Fine-tuned classifier, classification report, predictions |
| 02 | `multilabel_stage1_public_discourse.ipynb` | Stage 1 — Multi-label BERT | `stage1_public_discourse_sdg13_dimension.xlsx` | Fine-tuned classifier, classification report, predictions |
| 03 | `multiclass_stage2_public_discourse.ipynb` | Stage 2 — Multi-class BERT | `stage2_public_discourse_eco_emotion.xlsx` | Fine-tuned eco-emotion classifier, classification report |
| 04 | `bertopic_sdg13.ipynb` | Topic Modeling | Pre-cleaned corpora per SDG 13 sub-target | Topic info, distributions, coherence scores, HTML visualizations |

---

## 🤖 Models

The `/models` folder is reserved for fine-tuned model weights and related artifacts. Fine-tuned BERT classifiers will be uploaded to the Hugging Face Hub upon manuscript acceptance; links will be added below after publication.

<!--
- Stage 1 (multi-label SDG dimension): https://huggingface.co/<your-username>/<model-name>
- Stage 2 (multi-class eco-emotion): https://huggingface.co/<your-username>/<model-name>
-->

---

## 🔁 Reproducibility

- Data splits were stratified with a fixed random seed (`set_seed(43)` for BERT notebooks; `random_state=42` for UMAP/HDBSCAN inside BERTopic)
- The supervised models were trained using the Hugging Face Transformers library with `bert-base-uncased`
- For reproducibility, set environment seeds across Python, NumPy, and PyTorch as shown in the notebooks
- BERTopic involves a stochastic UMAP step; minor variation across hardware is expected and does not affect the substantive findings
- A CUDA-enabled GPU is strongly recommended for the supervised classification notebooks; `bertopic_sdg13.ipynb` can also run on CPU at slower speed

To install dependencies and run locally:

```bash
git clone https://github.com/anjawm/Climate-Framing-Affect.git
cd Climate-Framing-Affect
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

---

## 🔗 Links

- 📄 **[Paper (On Publication Process)](https://)**
- 📁 **[GitHub Repository](https://github.com/anjawm/Climate-Framing-Affect)**

---

## ⚖️ License

- **Code** (notebooks and scripts): [MIT License](LICENSE)
- **Annotated data** (`data/`): [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)

---

## 📬 Contact

For questions about the code or annotated data, please open a [GitHub issue](../../issues) or contact the corresponding author indicated in the manuscript.

---

## 🙏 Acknowledgements

We acknowledge the developers of [BERTopic](https://github.com/MaartenGr/BERTopic) and [Hugging Face Transformers](https://github.com/huggingface/transformers), on which this analysis depends.
