# Proyek Sistem Rekomendasi Film

Repositori ini berisi implementasi sistem rekomendasi film menggunakan dataset "TMDB 5000 Movie Dataset". Dua pendekatan algoritma yang digunakan adalah **Content-Based Filtering** dan **Popularity-Based Recommendation**.

## Ringkasan Proyek

Sistem ini bertujuan untuk memberikan rekomendasi film kepada pengguna.
* **Content-Based Filtering**: Merekomendasikan film berdasarkan kemiripan konten (genre, overview, kata kunci, aktor, sutradara).
* **Popularity-Based Recommendation**: Merekomendasikan film yang populer secara umum berdasarkan skor popularitas yang dihitung.

## Dataset

* **Sumber**: [TMDB 5000 Movie Dataset dari Kaggle](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)
* Terdiri dari dua file utama: `tmdb_5000_movies.csv` (detail film) dan `tmdb_5000_credits.csv` (kredit film).
* Setelah digabung dan diproses, dataset yang digunakan untuk modeling terdiri dari [jumlah baris: 4800] film dan [jumlah kolom: 21] fitur.

## Fitur Utama yang Digunakan

* **Untuk Content-Based Filtering**: `overview`, `genres`, `keywords`, `cast` (aktor utama), `crew` (sutradara). Fitur-fitur ini digabungkan menjadi satu kolom `tags`.
* **Untuk Popularity-Based Recommendation**: `vote_average` dan `vote_count`.

## Metodologi

### 1. Data Preprocessing
* Pemuatan dan penggabungan dataset `movies` dan `credits`.
* Penanganan missing values (misalnya, pengisian `overview` dengan string kosong, penghapusan baris dengan `runtime` atau `release_date` kosong, penghapusan kolom `homepage`).
* Parsing fitur JSON-like (`genres`, `keywords`, `cast`, `crew`) untuk mengekstrak informasi relevan.
* Pembersihan teks (menghilangkan spasi internal pada nama/frasa, konversi ke lowercase).
* Pembuatan kolom `tags` gabungan untuk model content-based.

### 2. Model Content-Based Filtering
* **Vectorization**: Kolom `tags` diubah menjadi matriks fitur numerik menggunakan `TfidfVectorizer`.
* **Similarity**: Kemiripan antar film dihitung menggunakan `cosine_similarity` pada matriks fitur TF-IDF.
* **Rekomendasi**: Fungsi dibuat untuk mengambil judul film input dan mengembalikan N film paling mirip.

### 3. Model Popularity-Based Recommendation
* **Scoring**: Film diberi skor menggunakan formula *Weighted Rating* yang memperhitungkan `vote_average` dan `vote_count` (dengan batas minimum `vote_count` dari persentil ke-90).
* **Rekomendasi**: Fungsi dibuat untuk mengembalikan N film dengan skor popularitas tertinggi.

## Hasil (Contoh Output)

### Rekomendasi Content-Based

* **Input: 'Avatar'**
    1.  Falcon Rising
    2.  Battle: Los Angeles
    3.  Apollo 18
    4.  Star Trek Into Darkness
    5.  Titan A.E.

### Rekomendasi Popularity-Based

1.  The Shawshank Redemption
2.  Fight Club
3.  The Dark Knight
4.  Pulp Fiction
5.  Inception

## Cara Menjalankan Proyek
1.  Pastikan Anda memiliki Python dan library yang dibutuhkan terinstal (`pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`). Anda bisa menggunakan file `requirements.txt` (jika Anda membuatnya).
2.  Unduh dataset (`tmdb_5000_movies.csv` dan `tmdb_5000_credits.csv`) dan letakkan dalam direktori yang sama dengan notebook.
3.  Jalankan Jupyter Notebook `[Nama_Notebook_Anda].ipynb`.
4.  Ikuti sel-sel kode untuk melihat proses dan hasil rekomendasi.

## Struktur Repositori
* `Sistem_rekomendasi_film_AriefFathin.ipynb`: Notebook utama berisi semua kode dan analisis.
* `tmdb_5000_movies.csv`: Dataset film.
* `tmdb_5000_credits.csv`: Dataset kredit film.

---
**Kontributor:** [Arief Fathin Abrar]
