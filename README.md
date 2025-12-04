# ANFORCOM DDSC COMPETITION 2025
Finalis ANFORCOM DDSC COMPETITION 2025 yang Diselenggarakan oleh Binus University


#   **Data Science Competition 2025 – Tim ThreeVolution**

**Finalis** ANFORCOM DDSC COMPETITION 2025 yang Diselenggarakan oleh **Binus University**

Anggota tim:

* **Dalila Tazkia**
* **Jihan Aqilah**
* **Asri Sabilla Putri**

Notebook ini memuat seluruh alur analisis data dan permodelan yang digunakan dalam kompetisi.

---
# Pengklasifikasi Teks Bahasa Indonesia: 8 Pilar Astacita

## Deskripsi Proyek

Proyek ini bertujuan untuk membangun model klasifikasi teks menggunakan arsitektur Transformer (BERT) untuk mengkategorikan teks-teks (dalam konteks ini, data tweet berbahasa Indonesia) ke dalam 8 pilar kebijakan/fokus utama yang disebut "Astacita".

Model dilatih untuk mengidentifikasi dan memetakan konten dari media sosial ke salah satu dari delapan kelas berikut:

1.  `harmoni`
2.  `hilirisasi`
3.  `ideologi`
4.  `pekerjaan`
5.  `pemerataan`
6.  `pertahanan`
7.  `reformasi`
8.  `sdm` (Sumber Daya Manusia)

## Teknologi dan Dependensi

Proyek ini dikembangkan menggunakan Python dan memanfaatkan ekosistem PyTorch dan Hugging Face `transformers`.

### Persyaratan Lingkungan

Pastikan Anda telah menginstal Python (disarankan versi 3.8+).

### Instalasi

Anda dapat menginstal semua *library* yang diperlukan menggunakan `pip`:

```bash
pip install transformers torch pandas scikit-learn accelerate datasets tqdm
```

*(Berdasarkan baris instalasi di)*

## Dataset

Model ini dilatih menggunakan data yang diasumsikan berada dalam file `train.csv` dan diuji pada data di `test.csv`. Kedua file tersebut harus memiliki kolom teks dan, untuk data pelatihan, kolom label.

## Struktur Repositori

```
.
├── FIX.ipynb               # Notebook Jupyter utama untuk pelatihan dan evaluasi model.
├── train.csv               # Data pelatihan (asumsi)
├── test.csv                # Data uji (asumsi)
├── indonesian-astacita-classifier/
│   ├── pytorch_model.bin   # Bobot model yang sudah dilatih
│   └── tokenizer_config.json # Konfigurasi tokenizer
└── README.md               # File README ini
```

## Penggunaan (Training & Prediksi)

Semua langkah pemrosesan data, pelatihan, dan prediksi diimplementasikan dalam `FIX.ipynb`.

### Langkah-langkah Utama

1.  **Preprocessing Data**: Data tweet dibersihkan (dikonversi ke huruf kecil, menghapus mention (`@`), dan hashtag (`#`)).
2.  **Pemilihan Model**: Model pra-terlatih (pre-trained) yang digunakan adalah `cahya/bert-base-indonesian-522M`.
3.  **Pelatihan**: Model dilatih selama 5 *epoch* dengan ukuran *batch* 16.
4.  **Penyimpanan Model**: Model yang sudah terlatih dan *tokenizer* disimpan ke direktori `indonesian-astacita-classifier`.
5.  **Prediksi**: Prediksi dilakukan pada data `test.csv` dan disimpan ke `test_predictions.csv`.

Anda dapat menjalankan seluruh alur kerja ini dengan menjalankan semua sel (cells) pada notebook `FIX.ipynb`.

## Hasil Evaluasi

Model dievaluasi pada data validasi (20% dari data pelatihan) setelah 5 *epoch*.

### Metrik Kinerja

| Metrik | Nilai |
| :--- | :--- |
| **Akurasi Validasi Akhir** | **0.6340** (atau 63.40%) |
| **Average Training Loss** | 0.3981 (Epoch 5) |
| **Validation Loss** | 1.3523 (Epoch 5) |

### Classification Report (Data Validasi)

| Kelas | Precision | Recall | F1-Score | Support |
| :--- | :--- | :--- | :--- | :--- |
| `harmoni` | 0.75 | 0.68 | 0.72 | 133 |
| `hilirisasi` | 0.36 | 0.41 | 0.38 | 37 |
| `ideologi` | 0.69 | 0.73 | 0.71 | 244 |
| `pekerjaan` | 0.49 | 0.38 | 0.43 | 69 |
| `pemerataan` | 0.38 | 0.41 | 0.40 | 61 |
| `pertahanan` | 0.77 | 0.80 | 0.79 | 214 |
| `reformasi` | 0.50 | 0.52 | 0.51 | 154 |
| `sdm` | 0.61 | 0.52 | 0.56 | 88 |
| **macro avg** | 0.57 | 0.56 | 0.56 | 1000 |
| **weighted avg** | 0.63 | 0.63 | 0.63 | 1000 |

*(Data dari Classification Report)*

## Prediksi Akhir

Hasil prediksi pada data `test.csv` disimpan dalam file:

`test_predictions.csv`

Kolom yang disimpan: `id`, `text`, dan `label` hasil prediksi.
