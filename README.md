
# Resources

- 📄 **Paper**: https://arxiv.org/abs/2601.15891  
- 🤗 **Hugging Face**: https://huggingface.co/AIDELab-IITBombay/RadJEPA  
- 💻 **Code (GitHub)**: https://github.com/aidelab-iitbombay/RadJEPA


# RadJEPA

RadJEPA is a self-supervised vision encoder for chest X-ray images based on a **Joint Embedding Predictive Architecture (JEPA)**.  
The model learns visual representations by predicting latent features of masked image regions, without text supervision or pixel-level reconstruction.

RadJEPA is intended as a **general-purpose radiology image backbone** for downstream tasks.

## Overview

- **Model type:** Vision Transformer–based JEPA encoder  
- **Training:** Self-supervised latent prediction  
- **Input:** Chest X-ray images
- **Finetuned from model:** [`ijepa`](https://github.com/facebookresearch/ijepa)

## Intended use

The model is a vision backbone that can be plugged to other models for downstream tasks.
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

We used images from five public, deidentified chest X-ray datasets to train this checkpoint of RAD-DINO.

| Dataset   | Num. images |
| --------- | ----------: |
| [MIMIC-CXR](https://www.nature.com/articles/s41597-019-0322-0) | 300 491 |
| [CheXpert](https://ojs.aaai.org/index.php/AAAI/article/view/3834) | 224 316 |
| [NIH-CXR](https://openaccess.thecvf.com/content_cvpr_2017/html/Wang_ChestX-ray8_Hospital-Scale_Chest_CVPR_2017_paper.html) | 112 120 |
| [PadChest](https://www.sciencedirect.com/science/article/abs/pii/S1361841520301614) | 160 817 |
| [BRAX](https://www.nature.com/articles/s41597-022-01608-8) | 41 620 |
| **TOTAL** | 839 364 |

### Biases, risks, and limitations

<!-- This section is meant to convey both technical and sociotechnical limitations. -->

RAD-DINO was trained with data from three countries; therefore, it might be biased towards the population in the training data.
Underlying biases of the training datasets may not be well characterized.

### Training procedure

We refer to the [manuscript](https://arxiv.org/abs/2601.15891) for a detailed description of the training procedure.

## Evaluation

Our evaluation is best described in the [manuscript](https://arxiv.org/abs/2601.15891).

### Baselines

We report results for a subset of consistently competitive baselines for clarity.
Notably, RadJEPA uses a ViT-B/14 backbone (86M parameters), making it substantially smaller than I-JEPA (ViT-H/14, 0.6B parameters), yet it achieves superior performance across classification, segmentation, and report generation tasks.
Furthermore, Rad-DINO and RadJEPA are the only methods pretrained on comparable chest X-ray datasets at similar scale, enabling a direct and fair comparison of self-supervised objectives under matched data and model capacity.
| Model       | Backbone | # Params |
|-------------|----------|---------:|
| Rad-DINO    | ViT-B/14 | 87M      |
| I-JEPA      | ViT-H/14 | 0.6B     |
| **RadJEPA** | ViT-B/14 | 86M      |

### Classification

| Model        | VinDr-CXR (Agg. AP) | RSNA (AP / AUC) |
|--------------|--------------------:|----------------:|
| RAD-DINO     | 52.8                | 71.0 / 88.4     |
| I-JEPA       | 50.0                | 70.2 / 87.4     |
| **RadJEPA**  | **55.2**            | **72.7 / 89.2** |

### Segmentation

| Model       | Decoder  | Lungs | Lung Zones | Ribs |
|-------------|----------|------:|-----------:|-----:|
| Rad-DINO    | UPerNet  | 98.0  | 91.2       | 85.3 |
| I-JEPA      | UPerNet  | 97.9  | 92.0       | 85.2 |
| **RadJEPA** | UPerNet  | **98.3** | **93.7** | **89.6** |

### Report Generation

| Model       | MIMIC (ROUGE-L / BLEU-4) | IU (ROUGE-L / BLEU-4)|
|-------------|--------------------------|----------------------|
| Rad-DINO    | 24.6 / 9.3               | 25.8 / 9.0           |
| I-JEPA      | 25.6 / 9.5               | 26.7 / 9.4           |
| **RadJEPA** | **26.1 / 10.1**          | **28.4 / 9.9**       |



## Software

We leveraged the code in [`ijepa`](https://github.com/facebookresearch/ijepa) for training.
We used [SimpleITK](https://simpleitk.org/) and [Pydicom](https://pydicom.github.io/) for processing of DICOM files.

## Citation

```bibtex
@misc{khan2026radjeparadiologyencoderchest,
      title={RadJEPA: Radiology Encoder for Chest X-Rays via Joint Embedding Predictive Architecture}, 
      author={Anas Anwarul Haq Khan and Mariam Husain and Kshitij Jadhav},
      year={2026},
      eprint={2601.15891},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2601.15891}, 
}
```

## <span style="color:#1F2937;">Model Card Contact</span>

<span style="color:#0F172A;">Anas Anwarul Haq Khan</span><br>
Artificial Intelligence in Digital Health Lab (KCDH)<br>
Computation for Indian Language Technology Lab<br>
Department of Computer Science and Engineering<br>
Indian Institute of Technology Bombay (IIT Bombay)<br><br>

<span style="color:#2563EB;">📧 anaskhan@cse.iitb.ac.in</span> <br>
<span style="color:#2563EB;">📧 anas290816007@gmail.com</span>
