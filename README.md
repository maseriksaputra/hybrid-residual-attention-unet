# 🫀 Segmentasi Semantik Tumor Ginjal pada Citra CT Scan menggunakan Hybrid Residual-Attention U-Net

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-EE4C2C.svg)](https://pytorch.org/)
[![Dataset](https://img.shields.io/badge/Dataset-KiTS23-green.svg)](https://kits-challenge.org/kits23/)

Repositori ini memuat kode dan hasil penelitian dari skripsi **"Implementasi Metode Hybrid Residual-Attention U-Net untuk Segmentasi Semantik Tumor Ginjal pada Citra CT Scan"**. Penelitian ini bertujuan untuk mengotomatisasi delineasi batas tumor ginjal secara akurat menggunakan pendekatan *Deep Learning*, guna membantu radiolog dalam mendiagnosis dan menentukan strategi pengobatan.

---

## 📖 Latar Belakang & Metode

Analisis manual citra CT Scan untuk deteksi tumor ginjal memakan waktu lama dan rentan terhadap variabilitas pengamat (*inter-observer variability*). Untuk itu, diusulkan arsitektur **Hybrid Residual-Attention U-Net**. 

Arsitektur ini menggabungkan:
1. **Residual Learning (Blok ResNet):** Memfasilitasi jaringan yang lebih dalam tanpa mengalami degradasi performa akibat gradien yang hilang (*vanishing gradient*), sehingga mengekstraksi fitur kompleks secara lebih kaya.
2. **Attention Gates (AG):** Memimik sistem visual manusia dengan memberikan bobot lebih pada area target (tumor) dan menekan latar belakang (*background*) yang tidak relevan, secara efektif meminimalisir *false positive*.

### 🧠 Ilustrasi Algoritma Hybrid
*(Catatan: Unggah gambar arsitektur Anda dengan nama `Arsitektur_Hybrid_UNet.png` di repositori ini)*
<p align="center">
<img width="2816" height="1536" alt="Image" src="https://github.com/user-attachments/assets/8792f4cf-4ce9-4aa0-9345-8ec51f97a67a" />
  <br>
  <i>Gambar: Arsitektur Hybrid Residual-Attention U-Net Usulan</i>
</p>

---

## 📊 Evaluasi Kinerja (Grafik Evaluasi)

Kinerja model diukur dan dibandingkan dengan U-Net Standar menggunakan beberapa metrik tingkat piksel:
- **Dice Similarity Coefficient (DSC)**
- **Intersection over Union (IoU)**
- **Cross-Entropy Loss**

Dalam proses *training* menggunakan 488 studi kasus dari dataset KiTS23, model usulan (Hybrid U-Net) menunjukkan dinamika penurunan *loss* yang lebih stabil dan mencapai akurasi segmentasi yang lebih tinggi.

*(Catatan: Unggah gambar grafik evaluasi Anda dengan nama `Grafik_Loss_Akurasi.png`)*
<p align="center">
<img width="3608" height="1184" alt="Image" src="https://github.com/user-attachments/assets/7c6d0d1a-7e00-4467-b249-d6fcef7a3658" />
  <br>
  <i>Gambar: Perbandingan Grafik Penurunan Loss antara U-Net Standar dan Hybrid U-Net</i>
</p>

---

## 🖼️ Sampel Hasil Segmentasi

Visualisasi di bawah ini menampilkan perbandingan *slice-by-slice* antara Citra Asli, *Ground Truth* (Anotasi Dokter Ahli), dan Prediksi dari model Hybrid U-Net. Model mampu mendelineasi batas dengan baik:
* **Hijau**: Jaringan Ginjal Normal
* **Abu-abu**: Jaringan Tumor

*(Catatan: Pastikan Anda mengunggah file `Visualisasi_6_Sampel_Tumor.png` hasil dari Jupyter Notebook Anda ke direktori utama repositori)*
<p align="center">
<img width="2756" height="1056" alt="Image" src="https://github.com/user-attachments/assets/c7f5e005-2a85-4ca0-9389-49ad3c294096" />
  <br>
  <i>Gambar: (Kiri) CT Scan Asli, (Tengah) Ground Truth Dokter, (Kanan) Prediksi Hybrid U-Net</i>
</p>

---

## 🚀 Cara Menjalankan (*Quick Start*)

### 1. Persiapan Lingkungan
Silakan *clone* repositori dan pastikan Anda menginstall dependensi yang dibutuhkan:
```bash
git clone [https://github.com/username-anda/nama-repo.git](https://github.com/username-anda/nama-repo.git)
cd nama-repo
pip install nibabel monai seaborn openpyxl scikit-learn torch
2. Pra-pemrosesan Data (Preprocessing)
Sistem menggunakan dataset KiTS23 (.nii.gz). Model loader telah dikonfigurasi untuk menyesuaikan nilai radio-densitas (Hounsfield Unit) menjadi rentang kontras jaringan ginjal/tumor (-150 hingga 250), dan disesuaikan ukurannya (crop/pad) ke spatial resolution 256x256 piksel untuk menghemat penggunaan RAM (Lazy Loading).

3. Menjalankan Training & Visualisasi
Jalankan file Jupyter Notebook running_berhasil;_kits23.ipynb secara berurutan. File ini dirancang kompatibel untuk dieksekusi di Google Colab dan mencakup fungsi-fungsi berikut:

Pengunduhan otomatis 489 data pasien (Auto-Retry Download System).

Definisi Dataset Loader (Memory-Efficient).

Tahap Training Model Komparasi secara End-to-End.

Pembuatan Grafik Akurasi/Loss dan Visualisasi Gambar Segmentasi Semantik.

👨‍💻 Penulis
Erika Dwi Saputra

Program Studi Ilmu Komputer, Fakultas Sains dan Kesehatan
