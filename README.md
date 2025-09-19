# Syntactic Feature Probing in Code-Switched Text

[![Paper](https://img.shields.io/badge/Paper-PDF-blue)](link-to-paper)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

This repository contains datasets and code accompanying the paper:

**Syntactic Feature Encoding in Multilingual BERT: A Layer-Wise Probing Study on Code-Switched Language**  
*Chaitanya Chakka, Mithun Kumar S R, Aruna Malapati, Asif Ekbal*

---

## 📖 Overview

Code-switching (mixing two or more languages in a sentence) poses unique challenges for multilingual models such as **mBERT**.  
This work introduces **novel probing datasets** and conducts a **layer-wise probing analysis** of mBERT on English–Spanish code-switched text.

We focus on **five syntactic properties**:

- **Gender**
- **Mood**
- **Number**
- **Person**
- **Tense**

Our results show that:
- **Lower layers** in mBERT encode surface-level syntactic features.
- **Higher layers** capture abstract, semantic properties.
- Code-switching disrupts contextual feature capture, particularly for **gender** and **person**.

---

## 📂 Repository Structure

```
Lince_Number_spaeng/
  ├── train/
  │    ├── data-00000-of-00001.arrow
  │    ├── dataset_info.json
  │    └── state.json
  ├── validation/
  │    ├── data-00000-of-00001.arrow
  │    ├── dataset_info.json
  │    └── state.json
  ├── test/
  │    ├── data-00000-of-00001.arrow
  │    ├── dataset_info.json
  │    └── state.json
```

---

## 🚀 Usage

### Load the dataset
```python
from datasets import load_from_disk

ds = load_from_disk("Lince_Tense_spaeng")
print(ds)
print(ds['train'][0])
```

### Probing setup
- Tokenization: WordPiece (mBERT tokenizer)
- Embeddings: extracted from all 12 layers
- Probing model: simple classification head (frozen mBERT)
- Evaluation: **Matthews Correlation Coefficient (MCC)** and **F1-score**

---

## 📊 Results (Summary)

| Task   | Best Layer | MCC  | F1   |
|--------|------------|------|------|
| Gender | Layer 1    | 0.60 | 0.97 |
| Number | Layer 1-2  | 0.74 | 0.89 |
| Mood   | Layer 3    | 0.75 | 0.97 |
| Person | Layer 5    | 0.69 | 0.96 |
| Tense  | Layer 5    | 0.76 | 0.95 |

➡️ Lower layers: strong for **Gender, Number, Person**  
➡️ Mid-to-upper layers: stronger for **Mood, Tense**

---

## 📚 Citation

If you use these datasets or results, please cite:

```bibtex
@article{chakka2025syntactic,
  title={Syntactic Feature Encoding in Multilingual BERT: A Layer-Wise Probing Study on Code-Switched Language},
  author={Chakka, Chaitanya and S R, Mithun Kumar and Malapati, Aruna and Ekbal, Asif},
  journal={Preprint},
  year={2025}
}
```

---

## 📝 License

This project is licensed under the [MIT License](LICENSE).

---

## Acknowledgments

- [LINCE Benchmark](https://ritual.uh.edu/lince/datasets)
- [UniMorph Project](https://unimorph.github.io/)
- HPC support from **BITS Pilani, Hyderabad Campus**
