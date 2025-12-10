# 🌿 BanglaShakNet: A Benchmark Multi-modal Dataset for Leafy Vegetable Classification in Bangladesh

### 📄 Project Status: Dataset Benchmark & Research Submission
### 🔗 GitHub Repository: 
### 📝 Related Publication: BanglaShakNet (1).pdf

---

## 🎯 1. Project Overview & Objective

Leafy vegetables, known as 'shak' in Bangladesh, are vital for nutrition and agriculture but are often neglected in organized digital investigations. This project introduces **BanglaShakNet**, a new dataset created to identify and recognize the country's common leafy vegetables.

* **Objective:** To establish a benchmark multi-modal dataset for agricultural image analysis in the region.
* **Focus:** Providing a practical, realistic baseline for research in machine learning and deep learning.

---

## 💻 2. Technology Stack & Validation Models

### A. Data Collection Tools

| Tool | Purpose |
| :--- | :--- |
| **Samsung Galaxy S10+** | Image capture in natural light |
| **Xiaomi Poco X3** | Image capture in natural light |
| **Redmi Note 7 Pro** | Image capture in natural light |

### B. Baseline Classifiers (Used for Validation)

The dataset's reliability was assessed using two baseline classifiers:
* **Best ML Model:** Tuned Random Forest Classifier
* **Deep Learning Model:** Feed-forward Deep Learning Model

---

## 📊 3. Dataset Specifications (BanglaShakNet)

### A. Core Details

* **Total Images:** **539** color photographs.
* **Total Classes:** **17** distinct leafy vegetable varieties (e.g., *Alu Shak*, *Pui Shak*, *Lal Shak*).
* **Image Preprocessing:** Images were resized to **512x512 pixels**.
* **Collection Location:** Farms, local markets, and gardens in Dhaka, Bangladesh.

### B. Data Modality

Each image is labelled with:
* Bengali and scientific names.
* Metadata on image quality and plant health scores.

---

## 📈 4. Baseline Evaluation Results

The performance of the models on the dataset's test set:

| Model Type | Accuracy (Test Set) | Macro-F1 (Test Set) |
| :--- | :--- | :--- |
| **Best ML (Random Forest, Tuned)** | **0.954** | **0.868** |
| Deep Learning (Feed-Forward) | 0.731 | 0.580 |

* **DL Model Training:** The deep learning model was trained for **50 epochs**.

---

## 🚀 5. Getting Started

### Data Access

The full dataset is available via Mendeley Data (reference URL below) and in this repository.

### Dataset Structure

The project structure is organized with clear folders for each vegetable category, including both Bengali and scientific names for easy implementation.

---

## 📧 6. Authors and Contact

This work was conducted by researchers from the Department of Computer Science & Engineering, Southeast University, Dhaka 1208, Bangladesh.

### Authors
* Md. Mijanur Rahman
* **Rikha Akther**
* Shahed Hossen Raihan
* Nusrat Jahan Ananna
* Syed Salman Rumon

### Corresponding Author Emails
* Rikha Akther: `2022100000093@seu.edu.bd`
* Shahed Hossen Raihan: `2023000000080@seu.edu.bd`

### Keywords
`BanglaShakNet, Leafy Vegetable Classification, Shak Dataset, Image Classification, Agricultural AI`
