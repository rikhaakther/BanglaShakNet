# 🌿 BanglaShakNet: A Fine-Grained Image Dataset of Bangladeshi Leafy Vegetables (Shak)

**BanglaShakNet** is a publicly available image dataset of 539 RGB photographs covering 17 commonly consumed Bangladeshi leafy vegetables (*shak*), together with a transfer-learning baseline using four ImageNet-pretrained CNNs.

> Companion paper: *BanglaShakNet: Fine-Grained Classification of Bangladeshi Leafy Vegetables Using Transfer Learning*, 5th Int. Conf. on Innovations in Science, Engineering and Technology (ICISET 2026), Chittagong, Bangladesh.

This repository is a **dataset and baseline study**. It does not propose a new architecture. Results are a baseline, not evidence of statistical superiority (see [Limitations](#6-limitations)).

---

## 1. Overview

Leafy vegetables are an important part of the Bangladeshi diet. Many varieties look alike in leaf shape, colour and texture, which makes fine-grained recognition hard. BanglaShakNet provides images captured under natural, uncontrolled conditions to support research on this problem.

- **Modality:** RGB images only (single modality).
- **Labels:** one class label per image, taken from the class-named folder.
- **Task:** 17-class image classification.

---

## 2. Dataset Specifications

| Property | Value |
| :--- | :--- |
| Total images | **539** RGB photographs |
| Classes | **17** leafy vegetables |
| Images per class | 4 to 85 (imbalanced) |
| Capture | Smartphone cameras, real markets and households in Dhaka, Bangladesh, under varying lighting, background, scale, orientation and viewing angle |
| Capture devices | Samsung Galaxy S10+, Xiaomi Poco X3, Redmi Note 7 Pro |
| Label source | Class-named folders (`<class>/image files`) |
| Specimen identifiers | **Not recorded** (near-duplicate photos of the same specimen may exist) |

<!-- TODO: confirm original image resolution of the files in this repo (older README said 512x512). Models in the paper use 224x224 inputs. -->

### Class distribution

| Folder / class | Total images |
| :--- | ---: |
| `alu_shak` | 9 |
| `bilati_dhone_pata` | 4 |
| `chukai_pata_shak` | 9 |
| `data_shak` | 85 |
| `dheki_shak` | 13 |
| `helencha_shak` | 78 |
| `kochu_shak` | 23 |
| `kolmi_shak` | 32 |
| `kumro_shak` | 18 |
| `lal_shak` | 34 |
| `lau_shak` | 58 |
| `mula_shak` | 22 |
| `palong_shak` | 6 |
| `pat_shak` | 56 |
| `pui_shak` | 80 |
| `shapla_pata_shak` | 4 |
| `thankuni_shak` | 8 |
| **Total** | **539** |

Ten of the 17 classes have fewer than 25 images.

---

## 3. Baseline Experiment (as reported in the paper)

**Split:** random, non-stratified, seed 42, two stages (70% train; remaining 30% divided equally into validation and test).
Train / validation / test = **377 / 81 / 81**. Because the split is not stratified, `thankuni_shak` and `shapla_pata_shak` have **no test images**, so the test set covers 15 of 17 classes.

**Models:** MobileNetV2, EfficientNetB0, DenseNet121, ResNet50V2 (ImageNet weights).
**Pipeline:** 224×224 inputs, online augmentation on training images only, class weights `w_c = N / (K·n_c)` (0.38–7.39), Adam, batch size 16, two-stage training (frozen backbone, then fine-tuning of the last 30 / 30 / 40 layers of EfficientNetB0 / DenseNet121 / ResNet50V2 at 1e-5; MobileNetV2 uses Stage 1 only), TensorFlow 2.20 / Keras. Full hyperparameters are in the paper.

### Test-set results (81 images, single run, single split)

| Model | Acc. (%) | Prec. (%) | Rec. (%) | F1 (%) | Macro-F1 (%) | ROC-AUC (%) |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: |
| MobileNetV2 | 77.78 | 84.64 | 77.78 | 79.29 | 74 | 96.87 |
| DenseNet121 | 79.01 | 81.80 | 79.01 | 78.96 | 76 | 99.05 |
| ResNet50V2 | 90.12 | 90.48 | 90.12 | 90.01 | 94 | 99.58 |
| **EfficientNetB0** | **91.36** | **92.82** | **91.36** | **91.51** | 90 | **99.84** |

Precision, recall and F1 are support-weighted averages. ROC-AUC is one-vs-rest over the 15 classes present in the test set.

EfficientNetB0: 74 of 81 correct (95% Wilson interval 83.2–95.8%). ResNet50V2 got 73 of 81, so the two should be viewed as similar. One test image is about 1.2 percentage points.

---

## 4. Getting Started

```
BanglaShakNet/
├── alu_shak/
├── bilati_dhone_pata/
├── ...                      # one folder per class (17 total)
├── BanglaShakNet_projects_2.ipynb
└── README.md
```

Class labels can be read directly from folder names (e.g. `tf.keras.utils.image_dataset_from_directory`).

<!-- TODO: add exact split files (train/val/test file lists, seed 42) and the final training code/notebook so the paper results can be reproduced. -->

**Data access:** this repository.
<!-- TODO: add Mendeley Data / DOI link here only if the dataset is actually deposited there. -->

---

## 5. License

<!-- TODO: add a LICENSE file and state it here (e.g. CC BY 4.0 for data, MIT for code). Do not leave the dataset without a license. -->

---

## 6. Limitations

- Small dataset (539 images) collected in Dhaka; not validated on other regions, seasons, devices or lighting.
- Imbalanced classes (4–85 images); several classes have only 1–2 test images.
- Two classes have no test images; reported metrics cover 15 classes.
- Single split, single run; no k-fold CV, repeated splits or significance tests.
- Best model was chosen using test-set results.
- No specimen identifiers, so near-duplicate leakage between splits cannot be excluded.
- MobileNetV2 used different input scaling and augmentation, so it is not strictly like-for-like with the other models.
- No ablations, from-scratch baseline, Grad-CAM, or latency/model-size measurements.

---

## 7. Citation

```bibtex
@inproceedings{akther2026banglashaknet,
  title     = {BanglaShakNet: Fine-Grained Classification of Bangladeshi Leafy Vegetables Using Transfer Learning},
  author    = {Akther, Rikha and Bappy, Mehedi Hassan and Adnan, S I M and Das, Sourav},
  booktitle = {2026 5th International Conference on Innovations in Science, Engineering and Technology (ICISET)},
  address   = {Chittagong, Bangladesh},
  year      = {2026}
}
```

---

## 8. Authors and Contact

Department of Computer Science & Engineering, Southeast University, 262 Tejgaon I/A, Dhaka 1208, Bangladesh.

- Rikha Akther
- Mehedi Hassan Bappy
- Sourav Das
- S I M Adnan (corresponding author) — sim.adnan@seu.edu.bd

**Keywords:** `BanglaShakNet`, `leafy vegetable classification`, `shak dataset`, `transfer learning`, `agricultural image classification`, `Bangladesh`
