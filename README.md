# Sistem Case-Based Reasoning (CBR) - Retrieval Hukum Waris Islam

Proyek ini merupakan implementasi sistem **Case-Based Reasoning (CBR)** untuk melakukan *retrieval* (pencarian kemiripan) yurisprudensi kasus sengketa waris berdasarkan **Kompilasi Hukum Islam (KHI)**. Proyek ini disusun untuk memenuhi tugas besar mata kuliah Praktikum Kecerdasan Buatan / Temu Kembali Informasi di **Informatika, Fakultas Teknik, Universitas Muhammadiyah Malang**.

---

## 📌 Alur Pipeline Sistem (Siklus CBR)
Proyek ini dibagi menjadi 5 tahapan terstruktur berbasis Jupyter Notebook (`.ipynb`):
1. **01_Data_Acquisition.ipynb** – Proses memuat dan merapikan korpus dokumen putusan hukum sengketa waris.
2. **02_Text_Preprocessing.ipynb** – Pembersihan teks (*case folding*, *filtering*, *stopword removal*, dan *stemming* hukum).
3. **03_Retrieval.ipynb** – Pembangunan mesin pencari menggunakan pembobotan **TF-IDF**, Klasifikasi **SVM** (Machine Learning), dan **IndoBERT Embedding** (Transformer).
4. **04_Prediction.ipynb** – Proses *Reuse* & *Revise* solusi hukum (Amar Putusan) berdasarkan *query* kasus baru.
5. **05_Evaluation.ipynb** – Pengujian performa sistem menggunakan metrik resmi `sklearn.metrics`.

---

## 📊 Hasil Evaluasi Performa Model
Berdasarkan pengujian pada **Tahap 5**, berikut adalah tabel perbandingan performa pencarian dokumen hukum menggunakan metrik **Top-5 Retrieval (Hit@5)**:

| Model / Pendekatan | Accuracy | Precision | Recall | F1-Score |
| :--- | :---: | :---: | :---: | :---: |
| **TF-IDF Murni** | 1.0 | 1.0 | 1.0 | 1.0 |
| **TF-IDF + SVM** | 1.0 | 1.0 | 1.0 | 1.0 |
| **BERT Embedding** | 1.0 | 1.0 | 1.0 | 1.0 |

> 💡 *Catatan Laporan: Evaluasi menggunakan skala metrik penuh. Nilai 1.0 mengindikasikan bahwa dokumen hukum target yang dicari selalu berhasil masuk ke dalam 5 rekomendasi teratas (Top-5) yang disajikan oleh sistem.*

---

## 📂 Struktur Direktori Proyek
```text
├── data/
│   ├── processed/
│   │   └── cases.csv             # Korpus data hukum hasil preprocessing
│   ├── eval/
│   │   ├── queries.json          # Berkas kueri uji (Ground Truth)
│   │   ├── retrieval_metrics.csv # Output metrik evaluasi retrieval
│   │   └── prediction_metrics.csv# Output metrik prediksi solusi (Skala 100%)
│   └── results/
│       └── predictions.csv       # Hasil prediksi amar putusan kasus baru
├── notebooks/
│   ├── 01_data_acquisition.ipynb
│   ├── 02_text_preprocessing.ipynb
│   ├── 03_retrieval.ipynb
│   ├── 04_predict.ipynb
│   └── 05_evaluation.ipynb
└── README.md                     # Dokumentasi utama proyek
