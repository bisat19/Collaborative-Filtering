# Laporan Proyek Machine Learning - Abisatya Hastarangga Pradana

## Project Overview

Di era digital saat ini, jumlah informasi yang tersedia, termasuk dalam bentuk buku, telah meningkat secara eksponensial. Pembaca seringkali dihadapkan pada tantangan besar dalam menemukan buku yang benar-benar sesuai dengan preferensi dan minat mereka di antara jutaan pilihan yang ada [(Miriyala; et.al, 2025)](https://ijnrd.org/papers/IJNRD2503444.pdf). Metode pencarian tradisional atau penelusuran manual seringkali tidak efisien dan memakan waktu, menyebabkan pengguna mungkin melewatkan karya-karya yang relevan atau merasa kewalahan dengan banyaknya pilihan. Fenomena ini dikenal sebagai information overload, dan sistem rekomendasi hadir sebagai solusi untuk membantu pengguna menavigasi lautan informasi ini.

Masalah kesulitan dalam pemilihan buku ini penting untuk diselesaikan karena berdampak langsung pada pengalaman membaca pengguna dan juga pada ekosistem literasi secara keseluruhan. Pengguna yang kesulitan menemukan buku yang menarik mungkin akan berkurang minat bacanya, sementara penulis dan penerbit buku-buku yang kurang populer (sering disebut sebagai long-tail items) mungkin kesulitan mendapatkan visibilitas yang layak. Sistem rekomendasi yang efektif dapat meningkatkan kepuasan pengguna dengan menyajikan pilihan yang lebih personal, mendorong penemuan buku-buku baru, dan membantu karya-karya yang beragam untuk menjangkau pembaca yang tepat [(Leukhong, 2025)](https://www.jisem-journal.com/index.php/journal/article/view/492).

Proyek ini bertujuan untuk mengatasi masalah tersebut dengan merancang dan mengimplementasikan sistem rekomendasi buku menggunakan teknik collaborative filtering. Collaborative filtering adalah pendekatan yang populer dan terbukti efektif, yang bekerja dengan menganalisis pola perilaku dan preferensi dari banyak pengguna untuk membuat prediksi tentang minat seorang pengguna terhadap item yang belum pernah ia temui. 

Dengan memanfaatkan dataset Book-Crossings, yang berisi data rating buku dari sejumlah besar pengguna, proyek ini akan melakukan pra-pemrosesan data, analisis data eksploratif untuk memahami karakteristik data, melatih model UBCF dan SVD, dan mengevaluasinya menggunakan metrik standar seperti Precision. Pendekatan ini diharapkan dapat memberikan rekomendasi buku yang lebih personal dan relevan, sekaligus mengatasi tantangan umum dalam sistem rekomendasi seperti data sparsity (di mana sebagian besar pengguna hanya memberi rating pada sebagian kecil buku) dan cold start problem (kesulitan merekomendasikan untuk pengguna baru atau buku baru).

## Business Understanding

Sistem rekomendasi merupakan salah satu komponen penting dalam banyak platform digital, termasuk e-commerce dan layanan berbasis konten. Dalam konteks platform rekomendasi buku, memahami preferensi pengguna menjadi kunci untuk meningkatkan keterlibatan pengguna dan kepuasan pelanggan.

---
### Problem Statements

1. **Pernyataan Masalah 1:** Bagaimana cara merekomendasikan buku yang relevan kepada pengguna berdasarkan interaksi pengguna lain yang serupa?
2. **Pernyataan Masalah 2:** Bagaimana meningkatkan kualitas rekomendasi menggunakan metode collaborative filtering?
3. **Pernyataan Masalah 3:** Bagaimana mengevaluasi performa sistem rekomendasi dengan metrik yang sesuai?

---
### Goals

Tujuan utama dari proyek ini adalah:

- **Tujuan 1:** Membangun sistem rekomendasi buku yang memanfaatkan interaksi pengguna-pengguna lain (user-based collaborative filtering).
Sistem akan memanfaatkan kesamaan antar pengguna untuk memberikan rekomendasi buku yang disukai pengguna-pengguna serupa.
- **Tujuan 2:** Mengimplementasikan dan membandingkan dua pendekatan collaborative filtering: KNN dan SVD.
Pendekatan ini memungkinkan sistem untuk memahami pola preferensi pengguna berdasarkan data historis.
- **Tujuan 3:** Melakukan eksplorasi hasil rekomendasi dari dua pendekatan untuk mengetahui keunggulan masing-masing metode secara kualitatif.
Perbandingan dilakukan dengan melihat hasil rekomendasi yang dihasilkan oleh masing-masing algoritma.

---
### Solution Statements

Untuk menjawab pertanyaan dan mencapai tujuan di atas, pendekatan solusi yang digunakan meliputi:

1. **Solusi 1: Collaborative Filtering menggunakan K-Nearest Neighbors (KNN)**
   Menggunakan algoritma KNN dari pustaka Surprise untuk menghitung kemiripan antar pengguna atau item berdasarkan rating buku.
2. **Matrix Factorization menggunakan Singular Value Decomposition (SVD)**
   Menggunakan pendekatan SVD untuk mengurai data rating ke dalam dimensi laten, memungkinkan prediksi rating bahkan pada data yang sangat sparse.

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
