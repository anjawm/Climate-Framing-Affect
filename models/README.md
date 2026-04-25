# Models

This folder is intentionally kept (mostly) empty in the repository because trained BERT checkpoints are too large to commit directly to GitHub.

## Where the fine-tuned models will live

Once the manuscript is accepted, the fine-tuned BERT classifiers will be uploaded to the [Hugging Face Hub](https://huggingface.co/) and linked from here.

| Stage | Task | Hugging Face link |
|---|---|---|
| Stage 1 — Institutional News | Multi-label classification (3 SDG 13 dimensions) | *to be added on acceptance* |
| Stage 1 — Public Discourse | Multi-label classification (3 SDG 13 dimensions) | *to be added on acceptance* |
| Stage 2 — Public Discourse | Multi-class classification (eco-emotion) | *to be added on acceptance* |

Once published, you will be able to load each model in two lines:

```python
from transformers import AutoModelForSequenceClassification, AutoTokenizer
tokenizer = AutoTokenizer.from_pretrained("<your-username>/<model-name>")
model     = AutoModelForSequenceClassification.from_pretrained("<your-username>/<model-name>")
```

## If you want to reproduce training locally

The notebooks in `notebooks/` (specifically 02, 03, and 04) contain the full fine-tuning pipeline. They will save checkpoints to this folder by default; those checkpoint files are listed in `.gitignore` and will not be committed.
