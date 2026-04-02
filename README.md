# Cassiterite Mineral Identification from Microscopic Images Using Mask R-CNN

This repository contains code, documentation, and research artifacts for an undergraduate thesis.

- Thesis Title: Identifikasi Mineral Kasiterit Pada Citra Mikroskop Menggunakan Model Mask R-CNN
- Author: Kevin Naufal Dany
- Study Program: Informatics Engineering, Institut Teknologi Sumatera
- Student ID: 122140222

## Important Links

- Model demo (Hugging Face Space): https://huggingface.co/spaces/kevinndny/cassiterite-segmentation
- Institutional repository/archive: https://repo.itera.ac.id/depan/submission/SB2602200095

## Project Overview

This work develops an instance segmentation pipeline to identify cassiterite minerals in microscopic images using Mask R-CNN variants, including standard and amodal approaches for occlusion handling.

The main scripts in the code directory cover:

- k-fold cross-validation training
- standard test-set evaluation
- tiled test-set evaluation

## Directory Highlights

- code/train.py: k-fold model training
- code/test_evaluation.py: standard test-set evaluation
- code/test_evaluation_tiled.py: tiled evaluation (tile-based inference)
- code/requirements.txt: Python dependencies
- thesis: thesis manuscript source (LaTeX)
- figure: experiment visualizations and outputs

## Environment Setup

This section explains how to fully reproduce the environment from scratch.

### 1. Programming Language and Versions

- Python 3.10+ (recommended: Python 3.10 or 3.11)
- PyTorch 2.x
- OS compatibility: Windows/Linux (commands below can be adapted)

### 2. Libraries and Dependencies

Dependencies are defined in code/requirements.txt, including:

- torch, torchvision
- numpy, opencv-python, Pillow
- scikit-learn, albumentations
- matplotlib, seaborn, tqdm
- pycocotools, wandb, shapely

### 3. Installation Steps (From Zero)

1. Clone the repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd Repo_TA_Kevin
```

2. Create and activate a virtual environment

Windows (PowerShell):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Linux/macOS:

```bash
python -m venv .venv
source .venv/bin/activate
```

3. Upgrade pip and install dependencies

```bash
python -m pip install --upgrade pip
pip install -r code/requirements.txt
```

4. Verify installation

```bash
python -c "import torch; import torchvision; import cv2; import albumentations; print('Environment ready')"
```

### 4. Data Preparation

By default, training expects a dataset directory named dataset142 (see the default data_dir argument in code/train.py).

Ensure your dataset follows the expected experiment format, where each image has its paired JSON annotation. If your dataset is stored elsewhere, pass the custom path through data_dir.

## Running the Code

Run all commands from the repository root.

### 1. Training (K-Fold)

Example (basic training):

```bash
python code/train.py --data_dir dataset142 --n_folds 5 --model_type amodal --backbone resnet50_fpn_v2 --optimizer sgd --lr 0.01 --epochs 50 --batch_size 1 --output_dir output --checkpoint_dir checkpoints
```

Example (Adam optimizer):

```bash
python code/train.py --data_dir dataset142 --n_folds 5 --model_type amodal --backbone resnet50_fpn_v1 --optimizer adam --lr 1e-4 --epochs 50 --batch_size 1 --output_dir output --checkpoint_dir checkpoints
```

### 2. Standard Test-Set Evaluation

```bash
python code/test_evaluation.py --checkpoint checkpoints/<checkpoint_name>.pth --model_type standard --backbone resnet50_fpn_v2 --testset_dir testset --output_dir test_evaluation --threshold 0.5 --iou_threshold 0.5 --confidence_threshold 0.7
```

### 3. Tiled Test-Set Evaluation

```bash
python code/test_evaluation_tiled.py --checkpoint checkpoints/<checkpoint_name>.pth --model_type amodal --backbone resnet50_fpn_v1 --testset_dir testset --output_dir test_evaluation_tiled --threshold 0.5 --iou_threshold 0.5 --confidence_threshold 0.7
```

### 4. Frequently Tuned Parameters

- model_type: standard or amodal
- backbone: resnet50_fpn_v1 or resnet50_fpn_v2
- optimizer: sgd or adam
- lr: learning rate
- n_folds: number of cross-validation folds

## How to Cite

If this repository, model, or thesis contributes to your work, please cite it as follows.

### Text Citation

Kevin Naufal Dany. 2026. Identifikasi Mineral Kasiterit Pada Citra Mikroskop Menggunakan Model Mask R-CNN. Undergraduate Thesis, Informatics Engineering Program, Institut Teknologi Sumatera.

### BibTeX

```bibtex
@thesis{dany2026kasiterit,
    author      = {Kevin Naufal Dany},
    title       = {Identifikasi Mineral Kasiterit Pada Citra Mikroskop Menggunakan Model Mask R-CNN},
    type        = {Undergraduate Thesis},
    school      = {Informatics Engineering Program, Institut Teknologi Sumatera},
    year        = {2026},
    url         = {https://repo.itera.ac.id/depan/submission/SB2602200095},
    note        = {Code and demo: https://huggingface.co/spaces/kevinndny/cassiterite-segmentation}
}
```

## Notes

- Historical review notes are available in LOGBOOK.md and history/review.md.
- For reproducible experiments, use the same random seed as the main runs.

---

# Identifikasi Mineral Kasiterit pada Citra Mikroskop Menggunakan Mask R-CNN

Repositori ini berisi kode, dokumentasi, dan artefak penelitian untuk skripsi sarjana.

- Judul Skripsi: Identifikasi Mineral Kasiterit Pada Citra Mikroskop Menggunakan Model Mask R-CNN
- Penulis: Kevin Naufal Dany
- Program Studi: Teknik Informatika, Institut Teknologi Sumatera
- NIM: 122140222

## Tautan Penting

- Demo model (Hugging Face Space): https://huggingface.co/spaces/kevinndny/cassiterite-segmentation
- Repositori/arsip institusi: https://repo.itera.ac.id/depan/submission/SB2602200095

## Ringkasan Proyek

Penelitian ini mengembangkan pipeline instance segmentation untuk mengidentifikasi mineral kasiterit pada citra mikroskop menggunakan varian Mask R-CNN, termasuk pendekatan standard dan amodal untuk menangani oklusi.

Script utama pada folder code mencakup:

- training berbasis k-fold cross validation
- evaluasi test set standar
- evaluasi test set berbasis tile

## Struktur Direktori Utama

- code/train.py: training model k-fold
- code/test_evaluation.py: evaluasi test set standar
- code/test_evaluation_tiled.py: evaluasi tiled (inferensi per tile)
- code/requirements.txt: dependensi Python
- thesis: sumber dokumen skripsi (LaTeX)
- figure: visualisasi dan hasil eksperimen

## Setup Environment

Bagian ini menjelaskan langkah reproduksi environment secara lengkap dari awal.

### 1. Bahasa Pemrograman dan Versi

- Python 3.10+ (disarankan Python 3.10 atau 3.11)
- PyTorch 2.x
- Kompatibel untuk Windows/Linux (command dapat disesuaikan)

### 2. Library dan Dependencies

Dependensi didefinisikan di code/requirements.txt, antara lain:

- torch, torchvision
- numpy, opencv-python, Pillow
- scikit-learn, albumentations
- matplotlib, seaborn, tqdm
- pycocotools, wandb, shapely

### 3. Langkah Instalasi dari Nol

1. Clone repository

```bash
git clone <URL_REPOSITORY_KAMU>
cd Repo_TA_Kevin
```

2. Buat dan aktifkan virtual environment

Windows (PowerShell):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Linux/macOS:

```bash
python -m venv .venv
source .venv/bin/activate
```

3. Upgrade pip dan install dependencies

```bash
python -m pip install --upgrade pip
pip install -r code/requirements.txt
```

4. Verifikasi instalasi

```bash
python -c "import torch; import torchvision; import cv2; import albumentations; print('Environment ready')"
```

### 4. Persiapan Data

Secara default, training membaca folder dataset bernama dataset142 (lihat nilai default argumen data_dir di code/train.py).

Pastikan format data mengikuti format eksperimen, yaitu setiap image berpasangan dengan file anotasi JSON. Jika lokasi data berbeda, berikan path tersebut melalui argumen data_dir.

## Cara Menjalankan Kode

Jalankan seluruh command dari root repository.

### 1. Training (K-Fold)

Contoh training dasar:

```bash
python code/train.py --data_dir dataset142 --n_folds 5 --model_type amodal --backbone resnet50_fpn_v2 --optimizer sgd --lr 0.01 --epochs 50 --batch_size 1 --output_dir output --checkpoint_dir checkpoints
```

Contoh training dengan Adam:

```bash
python code/train.py --data_dir dataset142 --n_folds 5 --model_type amodal --backbone resnet50_fpn_v1 --optimizer adam --lr 1e-4 --epochs 50 --batch_size 1 --output_dir output --checkpoint_dir checkpoints
```

### 2. Evaluasi Test Set Standar

```bash
python code/test_evaluation.py --checkpoint checkpoints/<nama_checkpoint>.pth --model_type standard --backbone resnet50_fpn_v2 --testset_dir testset --output_dir test_evaluation --threshold 0.5 --iou_threshold 0.5 --confidence_threshold 0.7
```

### 3. Evaluasi Test Set Tiled

```bash
python code/test_evaluation_tiled.py --checkpoint checkpoints/<nama_checkpoint>.pth --model_type amodal --backbone resnet50_fpn_v1 --testset_dir testset --output_dir test_evaluation_tiled --threshold 0.5 --iou_threshold 0.5 --confidence_threshold 0.7
```

### 4. Parameter yang Sering Diubah

- model_type: standard atau amodal
- backbone: resnet50_fpn_v1 atau resnet50_fpn_v2
- optimizer: sgd atau adam
- lr: learning rate
- n_folds: jumlah fold cross-validation

## Cara Sitasi (How to Cite)

Jika repositori, model, atau skripsi ini membantu penelitian Anda, silakan gunakan sitasi berikut.

### Format Sitasi Teks

Kevin Naufal Dany. 2026. Identifikasi Mineral Kasiterit Pada Citra Mikroskop Menggunakan Model Mask R-CNN. Skripsi, Program Studi Teknik Informatika, Institut Teknologi Sumatera.

### BibTeX

```bibtex
@thesis{dany2026kasiterit,
    author      = {Kevin Naufal Dany},
    title       = {Identifikasi Mineral Kasiterit Pada Citra Mikroskop Menggunakan Model Mask R-CNN},
    type        = {Skripsi},
    school      = {Program Studi Teknik Informatika, Institut Teknologi Sumatera},
    year        = {2026},
    url         = {https://repo.itera.ac.id/depan/submission/SB2602200095},
    note        = {Kode dan demo: https://huggingface.co/spaces/kevinndny/cassiterite-segmentation}
}
```

## Catatan

- Catatan review historis tersedia di LOGBOOK.md dan history/review.md.
- Untuk menjaga reproduktibilitas eksperimen, gunakan random seed yang sama dengan eksperimen utama.
