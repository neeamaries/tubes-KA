# 📘 Tugas 2 — Rencana Kerja Kelompok 5
**Klasifikasi Gangguan Neurodegeneratif | Metode: Decision Tree & K-Nearest Neighbor (KNN)**

---

## 🗂️ Pembagian Tugas Anggota

| Bagian | Penanggung Jawab | Isi Pekerjaan |
|---|---|---|
| **A** — System Workflow + Flowchart | Julio Chrysanto Tanlain | Buat flowchart lengkap + penjelasan tiap tahap |
| **B** — Ablation Study: Skenario 1 & 2 | Bethari Nevyta Amaries | Tanpa preprocessing & tanpa feature selection |
| **C** — Ablation Study: Skenario 3 & 4 | A'ilah Nailul Fa'izah | Tanpa KNN / hanya Decision Tree & sebaliknya |
| **D** — Analisis Komponen + Perakitan Dokumen | Fathir Al Farih | Analisis kontribusi komponen + gabung semua bagian |

> [!IMPORTANT]
> Semua bagian digabung menjadi **satu dokumen akhir** yang juga memuat hasil Tugas 1 yang sudah final.

---

## 📌 Bagian A — System Workflow (Flowchart)

**Penanggung jawab: Julio**

### Alur yang harus dibuat:

```
[INPUT]
Dataset NDCTD-45K (45.000 baris, 123 kolom)
        ↓
[1. PEMAHAMAN DATA]
- Cek jumlah baris & kolom
- Identifikasi tipe data
- Cek missing values, duplikat, outlier
        ↓
[2. EXPLORATORY DATA ANALYSIS (EDA)]
- Statistik deskriptif per kelas (AD, PD, ALS, FTD, LBD, HC)
- Visualisasi distribusi fitur
- Heatmap proporsi gejala
- Analisis korelasi antar fitur
        ↓
[3. PREPROCESSING]
- Penanganan missing values
- Encoding variabel kategorik & ordinal
- Standardisasi variabel numerik (untuk KNN)
- Hapus Patient_ID
- Cek potensi kebocoran data (data leakage)
        ↓
[4. PEMBAGIAN DATA]
- Train set : Test set = 80:20
- Stratified split (menjaga proporsi kelas)
        ↓
[5. PEMODELAN]
┌─────────────────┐    ┌──────────────────────┐
│  Decision Tree   │    │  K-Nearest Neighbor   │
│  - Kriteria: Gini│    │  - Nilai K optimal    │
│  - Max depth     │    │  - Jarak: Euclidean   │
│  - Min samples   │    │  - Bobot: uniform     │
└────────┬────────┘    └──────────┬───────────┘
         └──────────┬─────────────┘
                    ↓
[6. EVALUASI MODEL]
- Accuracy
- Macro-F1
- Precision & Recall per kelas
- Confusion Matrix
- Stratified 5-Fold Cross Validation
                    ↓
[OUTPUT]
Prediksi Kelas: AD / PD / ALS / FTD / LBD / HC
+ Laporan performa model
```

### Yang harus ditulis Julio:
1. Gambar flowchart di atas dalam bentuk diagram (bisa pakai draw.io / Canva / Word SmartArt)
2. Tabel penjelasan fungsi tiap tahap (lihat tabel di bawah)

### Tabel Penjelasan Fungsi Tiap Tahap:

| Tahap | Fungsi | Input | Output |
|---|---|---|---|
| Pemahaman Data | Memastikan kualitas dan struktur dataset | File CSV/Excel | Laporan statistik awal |
| EDA | Memahami pola dan karakteristik tiap kelas | Dataset bersih | Visualisasi & insight |
| Preprocessing | Menyiapkan data agar siap dimodelkan | Dataset mentah | Dataset terproses |
| Pembagian Data | Mencegah data leakage saat evaluasi | Dataset terproses | Train & Test set |
| Decision Tree | Klasifikasi berbasis aturan pemisahan fitur | Train set | Model DT + prediksi |
| KNN | Klasifikasi berbasis kedekatan data tetangga | Train set (ternormalisasi) | Model KNN + prediksi |
| Evaluasi | Mengukur performa model secara objektif | Prediksi vs label asli | Metrik performa |

---

## 📌 Bagian B — Ablation Study: Skenario 1 & 2

**Penanggung jawab: Bethari**

### Apa itu Ablation Study?
Eksperimen yang menghilangkan satu komponen sistem untuk melihat seberapa besar kontribusinya terhadap performa.

---

### Skenario 1 — Tanpa Preprocessing

| Item | Isi |
|---|---|
| **Tujuan** | Mengukur seberapa besar preprocessing mempengaruhi akurasi model |
| **Yang dihilangkan** | Penanganan missing values, encoding, standardisasi |
| **Alasan dipilih** | Preprocessing adalah fondasi data; tanpanya, model menerima data kotor |
| **Cara uji** | Jalankan Decision Tree & KNN langsung pada data mentah |
| **Metrik ukur** | Accuracy, Macro-F1, jumlah error prediksi |
| **Hipotesis** | Performa turun signifikan karena data tidak konsisten |

---

### Skenario 2 — Tanpa Standardisasi (Khusus KNN)

| Item | Isi |
|---|---|
| **Tujuan** | Mengukur pengaruh normalisasi data terhadap performa KNN |
| **Yang dihilangkan** | Standardisasi / normalisasi fitur numerik |
| **Alasan dipilih** | KNN sangat sensitif terhadap skala fitur karena berbasis jarak |
| **Cara uji** | Jalankan KNN tanpa StandardScaler |
| **Metrik ukur** | Accuracy, Macro-F1, waktu komputasi |
| **Hipotesis** | KNN tanpa standardisasi akan buruk; Decision Tree tidak terpengaruh |

---

## 📌 Bagian C — Ablation Study: Skenario 3 & 4

**Penanggung jawab: A'ilah**

---

### Skenario 3 — Hanya Decision Tree (Tanpa KNN)

| Item | Isi |
|---|---|
| **Tujuan** | Mengevaluasi apakah Decision Tree saja sudah cukup baik |
| **Yang dihilangkan** | Model KNN |
| **Alasan dipilih** | Membandingkan kontribusi masing-masing model secara terpisah |
| **Cara uji** | Jalankan sistem hanya dengan Decision Tree |
| **Metrik ukur** | Accuracy, Macro-F1, Confusion Matrix |
| **Hipotesis** | Decision Tree lebih mudah diinterpretasi tapi mungkin kurang akurat untuk kelas yang beririsan |

---

### Skenario 4 — Hanya KNN (Tanpa Decision Tree)

| Item | Isi |
|---|---|
| **Tujuan** | Mengevaluasi apakah KNN saja sudah cukup baik |
| **Yang dihilangkan** | Model Decision Tree |
| **Alasan dipilih** | Mengukur kontribusi KNN secara independen |
| **Cara uji** | Jalankan sistem hanya dengan KNN (dengan standardisasi) |
| **Metrik ukur** | Accuracy, Macro-F1, Confusion Matrix |
| **Hipotesis** | KNN bisa lebih baik pada kelas yang karakteristiknya dekat di ruang fitur |

---

### Tabel Ringkasan Semua Skenario (untuk A'ilah jadikan tabel di dokumen akhir):

| Skenario | Komponen Dihilangkan | Model Dipakai | Metrik Utama | Penanggung Jawab |
|---|---|---|---|---|
| Baseline | — (sistem lengkap) | DT + KNN | Accuracy, Macro-F1 | Semua |
| S1 | Preprocessing | DT + KNN | Accuracy, Macro-F1 | Bethari |
| S2 | Standardisasi | KNN saja | Accuracy, Macro-F1 | Bethari |
| S3 | KNN | DT saja | Accuracy, Macro-F1 | A'ilah |
| S4 | Decision Tree | KNN saja | Accuracy, Macro-F1 | A'ilah |

---

## 📌 Bagian D — Analisis Kontribusi Komponen + Perakitan

**Penanggung jawab: Fathir**

### Yang harus ditulis Fathir:

#### 1. Analisis Komponen Paling Berkontribusi

Setelah semua skenario dijalankan (atau direncanakan), tulis analisis:

> **Komponen yang diperkirakan paling berpengaruh:**
>
> - **Preprocessing** → Jika dihilangkan, data kotor akan menurunkan performa kedua model secara drastis karena ada missing values dan skala fitur yang tidak konsisten.
> - **Standardisasi** → Sangat krusial untuk KNN karena algoritma ini berbasis jarak Euclidean; tanpa normalisasi, fitur dengan nilai besar (seperti usia) mendominasi perhitungan jarak.
> - **Decision Tree** → Memberikan interpretabilitas tinggi dan tidak sensitif terhadap skala, cocok untuk data dengan fitur kategorik dominan.
> - **KNN** → Efektif mengenali pola lokal antar data, terutama untuk kelas yang memiliki karakteristik klinis yang serupa.
>
> **Kesimpulan perkiraan:** Preprocessing dan Standardisasi adalah komponen paling fundamental. Tanpa keduanya, model apapun tidak akan bekerja optimal pada dataset NDCTD-45K yang memiliki banyak missing values dan variabel berskala berbeda.

#### 2. Checklist Perakitan Dokumen Akhir

- [ ] Hasil Tugas 1 (sudah final) — taruh di bagian awal
- [ ] System Workflow + Flowchart (dari Julio)
- [ ] Ablation Study Skenario 1 & 2 (dari Bethari)
- [ ] Ablation Study Skenario 3 & 4 (dari A'ilah)
- [ ] Analisis kontribusi komponen (dari Fathir)
- [ ] Tabel kontribusi anggota diperbarui

---

## 📅 Saran Timeline Pengerjaan

| Hari | Target |
|---|---|
| Hari 1 | Masing-masing baca bagiannya, pahami tugasnya |
| Hari 2 | Draft masing-masing bagian selesai |
| Hari 3 | Review bersama, perbaikan |
| Hari 4 | Fathir rakit semua jadi dokumen final |

---

> [!TIP]
> Gunakan Google Docs bersama agar semua anggota bisa mengerjakan secara paralel dan Fathir bisa langsung merakit tanpa menunggu file dikirim satu per satu.
