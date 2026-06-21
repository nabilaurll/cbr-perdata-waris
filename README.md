# CBR Perdata Waris

## Deskripsi Proyek

Proyek ini mengimplementasikan metode **Case-Based Reasoning (CBR)** untuk perkara **Perdata Waris** menggunakan dokumen putusan Mahkamah Agung Republik Indonesia.

Sistem dibangun melalui lima tahapan utama:

1. Case Base Construction
2. Case Representation
3. Case Retrieval
4. Case Solution Reuse
5. Model Evaluation

Dataset berasal dari putusan perkara Perdata Waris yang dikonversi dari PDF menjadi teks dan diproses untuk mendukung pencarian kasus serupa serta prediksi hasil putusan.

---

## Struktur Folder

```text
CBR-Perdata-Waris
│
├── data
│   ├── pdf
│   │   └── *.pdf
│   │
│   ├── raw
│   │   └── case_001.txt
│   │   └── case_002.txt
│   │   └── ...
│   │
│   ├── processed
│   │   ├── cases.csv
│   │   └── cases.json
│   │
│   ├── eval
│   │   ├── queries.json
│   │   ├── retrieval_metrics.csv
│   │   ├── prediction_metrics.csv
│   │   ├── retrieval_failures.csv
│   │   └── error_analysis.txt
│   │
│   └── results
│       └── predictions.csv
│
├── logs
│   ├── cleaning.log
│   └── cleaning.csv
│
├── notebooks
│   ├── 01_preprocessing.ipynb
│   ├── 02_representation.ipynb
│   ├── 03_retrieval.ipynb
│   ├── 04_solution_reuse.ipynb
│   └── 05_evaluation.ipynb
│
└── README.md
```

---

# Tahap 1 — Case Base

## Tujuan

Membangun korpus putusan Perdata Waris sebagai basis kasus.

## Proses

- Mengumpulkan minimal 30 putusan PDF.
- Konversi PDF menjadi plain text.
- Pembersihan:
  - Header
  - Footer
  - Watermark
  - Nomor halaman
- Normalisasi karakter dan spasi.
- Penyimpanan hasil ke:

```text
data/raw/
```

## Output

```text
data/raw/case_001.txt
data/raw/case_002.txt
...
logs/cleaning.log
logs/cleaning.csv
```

---

# Tahap 2 — Case Representation

## Tujuan

Merepresentasikan setiap putusan dalam bentuk data terstruktur.

## Metadata yang Diekstrak

- Nomor Perkara
- Tanggal Putusan
- Jenis Perkara
- Pasal
- Pihak

## Konten Kunci

- Ringkasan Fakta
- Argumen Hukum Utama

## Feature Engineering

- Length (jumlah kata)
- Bag of Words
- QA Pairs

## Output

```text
data/processed/cases.csv
data/processed/cases.json
```

Contoh atribut:

| case_id | no_perkara | tanggal | pasal | pihak |
|----------|-----------|----------|--------|--------|
| case_001 | 123/Pdt.G | 2023-02-10 | Pasal 124 KUHPer | A vs B |

---

# Tahap 3 — Case Retrieval

## Tujuan

Menemukan kasus lama yang paling mirip dengan kasus baru.

## Metode

### TF-IDF

Menggunakan:

```python
TfidfVectorizer()
```

### Cosine Similarity

Mengukur kemiripan antara query dan seluruh kasus.

### SVM Assisted Retrieval

Menggunakan:

```python
LinearSVC()
```

untuk membantu retrieval berdasarkan label solusi.

## Fungsi Retrieval

```python
retrieve(query, k=5)
```

Output:

```python
[
  case_001,
  case_015,
  case_022,
  case_010,
  case_031
]
```

## Output

```text
data/eval/queries.json
```

---

# Tahap 4 — Case Solution Reuse

## Tujuan

Menggunakan solusi dari kasus lama untuk memprediksi hasil kasus baru.

## Pendekatan

### Majority Voting

Memilih solusi yang paling sering muncul pada top-k kasus.

### Weighted Similarity

Memberikan bobot berdasarkan skor similarity retrieval.

## Fungsi

```python
predict_outcome(query)
```

## Output

```text
data/results/predictions.csv
```

Format:

| query_id | predicted_solution | top_5_case_ids |
|-----------|-------------------|----------------|
| Q001 | mengabulkan | case_001, case_010, case_022 |

---

# Tahap 5 — Evaluation

## Evaluasi Retrieval

Menggunakan:

- Accuracy
- Precision
- Recall
- F1-Score

## Evaluasi Prediction

Mengukur kesesuaian hasil prediksi terhadap putusan sebenarnya.

## Output

```text
data/eval/retrieval_metrics.csv
data/eval/prediction_metrics.csv
data/eval/retrieval_failures.csv
data/eval/error_analysis.txt
data/eval/retrieval_chart.png
```

---

# Library Utama

```bash
pip install pandas numpy scikit-learn
pip install pypdf
pip install tqdm
pip install matplotlib
pip install seaborn
```

---

# Hasil Implementasi

Dataset yang digunakan merupakan putusan perkara Perdata Waris Mahkamah Agung RI.

Model retrieval yang digunakan:

- TF-IDF + Cosine Similarity
- SVM Assisted Retrieval

Metode reuse:

- Majority Voting
- Weighted Similarity

Evaluasi dilakukan menggunakan metrik:

- Accuracy
- Precision
- Recall
- F1-Score

---

# Penulis

Proyek Case-Based Reasoning (CBR)

Perdata Waris

Program Studi Informatika

Universitas Muhammadiyah Malang