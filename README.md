# 🥐 Bakery Sales Analytics & SPK
### Proyek Akhir Praktikum Sistem Informasi Manajemen

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=python&logoColor=white)

**Analisis data penjualan bakery 2006–2019 menggunakan Python — dari data wrangling hingga Sistem Pendukung Keputusan berbasis SAW & TOPSIS.**
<br>

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1J-4VsPtVTzSxtLVzceFHX5JJGWGVnefX#scrollTo=yz6D1r7aOKJQ)
[![Live Demo](https://img.shields.io/badge/Web%20Penjelasan-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://bakery-sales-analysis.vercel.app/)

</div>

---

## 👥 Tim

| Nama | NIM | Kontribusi |
|------|-----|------------|
| **Rivaldo** | *(NIM)* | Data Wrangling + Analisis Masalah + SPK |
| **Argya Ariella** | *(NIM)* | Exploratory Data Analysis (EDA) |
| **Annisa** | *(NIM)* | Visualisasi Data |

---

## 📦 Dataset

| Atribut | Detail |
|---------|--------|
| **Sumber** | [Kaggle — Bakery Sales Data 2006–19](https://www.kaggle.com/datasets/sanu12300/bakery-sales-data-2006-19) |
| **Jumlah Baris** | 5.113 baris |
| **Jumlah Kolom** | 9 kolom (8 setelah cleaning) |
| **Periode** | 1 Januari 2006 – 31 Desember 2019 |
| **Produk** | Cakes, Pies, Cookies, Smoothies, Coffee |

---

## 🗂️ Alur Proyek

```
Dataset (Kaggle)
      │
      ▼
┌─────────────┐
│  Tahap 1    │  Data Wrangling — pembersihan & persiapan data
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Tahap 2    │  EDA — eksplorasi pola, tren, korelasi
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Tahap 3    │  Visualisasi — 5 grafik informatif
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Tahap 4    │  Analisis Masalah — identifikasi & rumusan masalah
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Tahap 5    │  SPK — SAW & TOPSIS → ranking prioritas promosi
└─────────────┘
```

---

## 📊 Ringkasan Temuan

### 🏆 Produk Terlaris (Total 2006–2019)

```
Cookies   ████████████████████  306,719 unit  (29.6%)
Coffee    ████████████████      254,807 unit  (24.6%)
Smoothies ████████████          193,057 unit  (18.6%)
Pies      █████████             154,363 unit  (14.9%)
Cakes     ███████               127,957 unit  (12.3%)
```

### 🎯 Efektivitas Promosi per Produk

```
Cookies   +91.8%  ████████████████████
Coffee    +63.8%  █████████████
Smoothies +42.3%  █████████
Pies      +29.9%  ██████
Cakes     +26.1%  █████
```

---

## Tahapan Analisis

### Tahap 1 — Data Wrangling
- ✅ 0 missing values, 0 duplikat
- ✅ Konversi kolom `Date` ke `datetime64`
- ✅ Encoding kolom `promotion`: `"promotion"` → `1`, `"none"` → `0`
- ✅ Hapus kolom `Unnamed: 0` yang redundan
- ✅ Tambah kolom `month` dan `year` untuk analisis temporal

### Tahap 2 — EDA
- Statistik deskriptif per produk (mean, std, min, max)
- Analisis penjualan per hari dalam seminggu (heatmap produk × hari)
- Analisis dampak promosi per produk (% kenaikan)
- Tren penjualan mingguan & bulanan (2006–2019)
- Analisis korelasi antar produk + scatter plot

### Tahap 3 — Visualisasi Data (5 Grafik)

| # | Grafik | Insight |
|---|--------|---------|
| 1 | Bar Chart — Total Penjualan per Produk | Cookies & Coffee dominasi penjualan |
| 2 | Line Chart — Tren Tahunan | Penjualan stabil 14 tahun tanpa anomali |
| 3 | Pie Chart — Kontribusi % Tiap Produk | >54% dari hanya 2 produk |
| 4 | Heatmap — Korelasi Antar Produk | Nilai ≈ 0, tidak ada cross-selling organik |
| 5 | Boxplot — Promo vs Non-Promo | Promosi terbukti efektif naikkan penjualan |

### Tahap 4 — Analisis & Identifikasi Masalah

**3 masalah utama yang ditemukan:**

1. **Ketimpangan penjualan** — Cookies (306K) vs Cakes (127K), selisih 2.4×
2. **Efektivitas promosi tidak merata** — ROI promosi tiap produk sangat berbeda
3. **Tidak ada cross-selling organik** — korelasi antar produk mendekati 0

**Rumusan masalah SPK:**
> *"Produk mana yang harus diprioritaskan untuk mendapat alokasi promosi pada periode berikutnya?"*

### Tahap 5 — Implementasi SPK

**Alternatif:** 5 produk (Cakes, Pies, Cookies, Smoothies, Coffee)

**Kriteria:**

| Kode | Kriteria | Sumber | Tipe | Bobot |
|------|----------|--------|------|-------|
| C1 | Rata-rata penjualan harian | `df[products].mean()` | Benefit | 0.20 |
| C2 | % Kenaikan saat promosi | `promo_compare` | Benefit | **0.35** |
| C3 | Konsistensi penjualan (1/std) | `1 / df[products].std()` | Benefit | 0.20 |
| C4 | Kontribusi total penjualan | proporsi dari total | Benefit | 0.25 |

> Bobot C2 tertinggi karena tujuan SPK adalah mengoptimalkan alokasi promosi.

---

## 🏅 Hasil SPK

### Metode SAW (Simple Additive Weighting)

> Normalisasi: `r(i,j) = x(i,j) / max(kolom j)`
> Skor: `Σ [ r(i,j) × w(j) ]`

| Ranking | Produk | Skor SAW |
|---------|--------|----------|
| 🥇 1 | **Cookies** | **0.8836** |
| 🥈 2 | Coffee | 0.7180 |
| 🥉 3 | Smoothies | 0.5796 |
| 4 | Pies | 0.5101 |
| 5 | Cakes | 0.4873 |

### Metode TOPSIS

> Normalisasi Euclidean → jarak ke A+ dan A- → Closeness Coefficient

| Ranking | Produk | D+ | D- | Skor TOPSIS |
|---------|--------|----|----|-------------|
| 🥇 1 | **Cookies** | 0.0721 | 0.2172 | **0.7507** |
| 🥈 2 | Coffee | 0.1048 | 0.1345 | 0.5621 |
| 🥉 3 | Smoothies | 0.1616 | 0.0699 | 0.3018 |
| 4 | Cakes | 0.2172 | 0.0721 | 0.2493 |
| 5 | Pies | 0.2001 | 0.0571 | 0.2221 |

### Perbandingan & Kesimpulan

```
          SAW      TOPSIS
Cookies    1    =    1    ✅
Coffee     2    =    2    ✅
Smoothies  3    =    3    ✅
Pies       4    ≠    5    ⚠️  (swap — TOPSIS lebih sensitif thd konsistensi)
Cakes      5    ≠    4    ⚠️  (swap — Cakes lebih konsisten dari Pies)
```

**Rekomendasi:** Alokasikan anggaran promosi utama ke **Cookies** dan **Coffee** — konsisten di posisi teratas pada kedua metode, dengan ROI promosi tertinggi yang terbukti dari data historis 14 tahun.

---

## 🛠️ Cara Menjalankan

1. **Clone repository ini**
   ```bash
   git clone https://github.com/(username)/(repo-name).git
   ```

2. **Buka di Google Colab**
   - Upload notebook `.ipynb` ke [colab.research.google.com](https://colab.research.google.com)
   - Atau klik badge Colab di bagian atas

3. **Install dependencies**
   ```python
   !pip install opendatasets --quiet
   ```

4. **Jalankan sel secara berurutan** — Tahap 1 → 2 → 3 → 4 → 5

### Library yang Digunakan

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import opendatasets as od
```

---

## 📁 Struktur Repository

```
📦 bakery-sales-analytics
 ┣ 📓 bakery_sales_analysis.ipynb   ← notebook utama (semua tahap)
 ┣ 📊 grafik1_produk_laku.png
 ┣ 📊 grafik2_hari_ramai.png
 ┣ 📊 grafik3_pengaruh_promo.png
 ┣ 📊 grafik4_tren_penjualan.png
 ┣ 📊 grafik5_korelasi.png
 ┣ 📊 grafik6_boxplot_distribusi.png
 ┣ 📊 grafik_spk_ranking.png
 ┗ 📄 README.md
```

---

## 📌 Catatan Teknis

- Metode SPK diimplementasi **manual** menggunakan `numpy` dan `math` — tanpa library SPK eksternal (`scikit-criteria`, `pymcdm`, dsb.)
- Dataset diambil dari Kaggle (data nyata, bukan dummy/sintetis)
- Semua proses dijalankan di **Google Colaboratory**

---

## 🎨 Presentasi

[![Lihat Presentasi di Canva](https://img.shields.io/badge/Presentasi%20Canva-00C4CC?style=for-the-badge&logo=canva&logoColor=white)](https://canva.link/dvic9pkf0kybonl)

---

<div align="center">
  <sub>Proyek Akhir Praktikum Sistem Informasi Manajemen · 2026 · Kom A2 · Stambuk 2024 · Vokasi D3 Teknik Inforamtika Universitas Sumatera Utara</sub>
</div>
