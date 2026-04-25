# Climate-Framing-Affect: A Multi-Stage Framework for Analyzing Climate Change Discourse

This repository contains the annotated datasets, model training notebooks, and reproducibility materials for the paper titled:

> **"The Narrative Coping Deficit: Computational Diagnosis of Climate Framing-Affect Coupling"**

---

## 📂 Repository Structure

```
climate-framing-affect/
│
├── dataset/
│   ├── stage1_public_discourse_sdg13_dimension.xlsx
│   └── stage2_public_discourse_eco_emotion.xlsx
│
├── codes/
│   ├── BERT/
│   │   ├── Stage 1 - SDG Dimension Classification/
│   │   └── Stage 2 - Eco-Emotion Classification/
│   └── BERTopic/
│       └── SDG13 Topic Modeling/
│
├── prompt/
│   ├── prompt_stage1_sdg_dimension/
│   └── prompt_stage2_eco_emotion/
│
├── results/
│   ├── figures/
│   ├── tables/
│   └── topic_outputs/
│
├── requirements.txt
├── LICENSE
└── CITATION.cff
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

Labeled datasets are available in the `/dataset` folder, with one file per classification stage:

| File | Stage | Description |
|---|---|---|
| `stage1_public_discourse_sdg13_dimension.xlsx` | Stage 1 | Public-discourse documents annotated for three SDG 13 sub-target dimensions (multi-label, binary per dimension) |
| `stage2_public_discourse_eco_emotion.xlsx` | Stage 2 | Subset of Stage 1 documents additionally annotated with one eco-emotion label per document (multi-class) |

Each file contains preprocessed text data drawn from institutional news sources and public social media discourse. The **raw corpora** are not redistributed due to platform terms of service and publisher copyright; please contact the corresponding author for access requests.

---

## 🧠 Model Training Notebooks

The `/codes` folder contains all notebooks for fine-tuning BERT and running the BERTopic pipeline, organized by approach and stage:

- Use notebooks in `codes/BERT/Stage 1` or `codes/BERT/Stage 2` for supervised classification training and evaluation
- Use the notebook in `codes/BERTopic` for the unsupervised topic modeling pipeline
- Fine-tuning configurations (batch size, learning rate, epochs) follow the best-performing setups reported in the paper

| # | Notebook | Stage | Input | Main Outputs |
|---|---|---|---|---|
| 01 | `Stage 1 - Institutional News` | Stage 1 — Multi-label BERT | Institutional news annotated dataset | Fine-tuned classifier, classification report, predictions |
| 02 | `Stage 1 - Public Discourse` | Stage 1 — Multi-label BERT | `stage1_public_discourse_sdg13_dimension.xlsx` | Fine-tuned classifier, classification report, predictions |
| 03 | `Stage 2 - Public Discourse` | Stage 2 — Multi-class BERT | `stage2_public_discourse_eco_emotion.xlsx` | Fine-tuned eco-emotion classifier, classification report |
| 04 | `BERTopic SDG13` | Topic Modeling | Pre-cleaned corpora per SDG 13 sub-target | Topic info, distributions, coherence scores, HTML visualizations |

---

## 🔁 Reproducibility

- Data splits were stratified with a fixed random seed (`set_seed(43)` for BERT notebooks; `random_state=42` for UMAP/HDBSCAN inside BERTopic)
- The supervised models were trained using the Hugging Face Transformers library with `bert-base-uncased`
- For reproducibility, set environment seeds across Python, NumPy, and PyTorch as shown in the notebooks
- BERTopic involves a stochastic UMAP step; minor variation across hardware is expected and does not affect the substantive findings
- A CUDA-enabled GPU is strongly recommended for Notebooks 02–04; Notebook 04 (BERTopic) can also run on CPU at slower speed

To install dependencies and run locally:

```bash
git clone https://github.com/anjawm/climate-framing-affect.git
cd climate-framing-affect
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

---

## 🤖 Pre-trained Models

Fine-tuned BERT classifiers will be uploaded to the Hugging Face Hub upon manuscript acceptance. Links will be added here after publication.

<!--
- Stage 1 (multi-label SDG dimension): https://huggingface.co/<your-username>/<model-name>
- Stage 2 (multi-class eco-emotion): https://huggingface.co/<your-username>/<model-name>
-->

---

## 🔗 Links

- 📄 **[Paper (Coming Soon)](https://)**
- 📁 **[GitHub Repository](https://github.com/anjawm/climate-framing-affect)**


---

## ⚖️ License

- **Code** (notebooks and scripts): [MIT License](LICENSE)
- **Annotated data** (`dataset/`): [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)

---

## 📬 Contact

For questions about the code or annotated data, please open a [GitHub issue](../../issues) or contact the corresponding author indicated in the manuscript.

---

## 🙏 Acknowledgements

We acknowledge the developers of [BERTopic](https://github.com/MaartenGr/BERTopic) and [Hugging Face Transformers](https://github.com/huggingface/transformers), on which this analysis depends.
