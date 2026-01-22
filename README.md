# RadJEPA

RadJEPA is a self-supervised vision encoder for chest X-ray images based on a **Joint Embedding Predictive Architecture (JEPA)**.  
The model learns visual representations by predicting latent features of masked image regions, without text supervision or pixel-level reconstruction.

RadJEPA is intended as a **general-purpose radiology image backbone** for downstream tasks.

## Overview

- **Model type:** Vision Transformer–based JEPA encoder  
- **Training:** Self-supervised latent prediction  
- **Input:** Chest X-ray images  

## Intended use

RadJEPA is released **for research purposes only** and is **not intended for clinical use**.

Typical downstream applications include:
- Multi-label classification
- Semantic segmentation using patch embeddings
- Image retrieval and clustering
- Report generation, with a language model to decode text


### Load RadJEPA

```python
from transformers import AutoModel
model = AutoModel.from_pretrained(
    "AIDElab-IITBombay/RadJEPA",
    trust_remote_code=True
)
print(model)
```

### Dependency note (timm)

If you encounter issues with newer versions of `timm`, install the known working version explicitly:

```bash
pip install timm==1.0.24
```

## Training details

### Training data

### Training procedure

#### Preprocessing

#### Training hyperparameters

## Evaluation

## Software

## Citation

## Model card contact

**Anas Khan**  
anaskhan@cse.iitb.ac.in  
anas290816007@gmail.com  
