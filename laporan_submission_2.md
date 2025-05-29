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
   Menggunakan algoritma KNN untuk menghitung kemiripan antar pengguna atau item berdasarkan rating buku.
2. **Matrix Factorization menggunakan Singular Value Decomposition (SVD)**
   Menggunakan pendekatan SVD untuk mengurai data rating ke dalam dimensi laten, memungkinkan prediksi rating bahkan pada data yang sangat sparse.

## Data Understanding
### Sumber Dataset
Dataset yang digunakan dalam proyek ini adalah **Book-Crossing: User review ratings**, yang tersedia secara publik melalui platform Kaggle pada tautan berikut:  
🔗 [Book-Crossing: User review ratings – Kaggle](https://www.kaggle.com/datasets/ruchi798/bookcrossing-dataset)

Database ini berisi 3 dataset yakni dataset BX-Book-Ratings.csv, BX-Users.csv, BX-Books.csv. Fataset ini tersedia secara publik untuk tujuan penelitian dan merupakan salah satu dataset yang sering digunakan untuk menguji sistem rekomendasi. Dataset ini terdiri dari sekitar 278.858 pengguna anonim, 271.379 buku, dan mencakup 1.149.780 rating (baik eksplisit maupun implisit).  Kondisi data mentah menunjukkan beberapa tantangan seperti nilai yang hilang pada beberapa kolom (misalnya, `Age` pada data pengguna dan Publisher pada data buku) dan format yang tidak konsisten atau tidak valid pada kolom `Year-Of-Publication`.  Dataset ini dikenal memiliki tingkat sparsity yang tinggi, artinya sebagian besar pengguna hanya memberikan rating pada sebagian kecil dari total buku yang tersedia.

---
### Fitur dalam Dataset

Variabel-variabel pada dataset Book-Crossings adalah sebagai berikut:
1. `BX-Users.csv` - Informasi Pengguna
File ini berisi informasi demografis pengguna.

| Nama Kolom | Deskripsi | Contoh Nilai | Catatan |
|------------|------------------------------------------------------------------------------------|--------------|---------|
| User-ID    | ID unik untuk setiap pengguna. Dipetakan ke integer dan bersifat anonim. | 276725, 1 | - |
| Location   | Lokasi geografis pengguna, biasanya dalam format "kota, provinsi/negara bagian, negara". | "nyc, new york, usa", "stockton, california, usa" | Format dapat bervariasi. |
| Age        | Usia pengguna. | 34.0, 18.0 | Mengandung banyak nilai NULL/NaN dan beberapa outlier (misalnya, usia > 99 atau < 5) yang memerlukan penanganan. |


2. `BX-Books.csv` - Informasi Buku
File ini berisi detail mengenai setiap buku.

| Nama Kolom      | Deskripsi                                                                 | Contoh Nilai                                                  | Catatan                                                                                  |
|------------------|---------------------------------------------------------------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------|
| ISBN            | International Standard Book Number, ID unik untuk setiap buku.            | "0195153448", "0002005018"                                     | ISBN yang tidak valid telah dihapus dari beberapa versi dataset.                        |
| Book-Title      | Judul buku.                                                               | "Classical Mythology", "Clara Callan"                          | -                                                                                        |
| Book-Author     | Penulis buku. Jika ada beberapa penulis, hanya yang pertama yang dicantumkan. | "Mark P. O. Morford", "Richard Bruce Wright"               | Mengandung sedikit nilai NULL.                                                          |
| Year-Of-Publication | Tahun publikasi buku.                                                 | 2002, 2001                                                     | Mengandung beberapa nilai tidak valid seperti 0 atau string nama penerbit.              |
| Publisher       | Penerbit buku.                                                            | "Oxford University Press", "HarperFlamingo Canada"            | Mengandung sedikit nilai NULL.                                                          |
| Image-URL-S     | URL ke gambar sampul buku ukuran kecil.                                   | http://images.amazon.com/...S.jpg                              | Umumnya tidak digunakan untuk collaborative filtering dan dapat dihapus.                |
| Image-URL-M     | URL ke gambar sampul buku ukuran sedang.                                  | http://images.amazon.com/...M.jpg                              | Umumnya tidak digunakan untuk collaborative filtering dan dapat dihapus.                |
| Image-URL-L     | URL ke gambar sampul buku ukuran besar.                                   | http://images.amazon.com/...L.jpg                              | Umumnya tidak digunakan untuk collaborative filtering dan dapat dihapus.                |

3. `BX-Book-Ratings.csv` - Informasi Rating Buku
File ini berisi informasi rating yang diberikan oleh pengguna terhadap buku.

| Nama Kolom    | Deskripsi                                                                                                               | Contoh Nilai                       | Catatan                                           |
|---------------|--------------------------------------------------------------------------------------------------------------------------|------------------------------------|---------------------------------------------------|
| User-ID       | ID unik pengguna yang memberikan rating (merujuk ke BX-Users.csv).                                                      | 276725, 276726                     | -                                                 |
| ISBN          | ISBN buku yang dirating (merujuk ke BX-Books.csv).                                                                      | "034545104X", "0155061224"         | -                                                 |
| Book-Rating   | Rating yang diberikan pengguna untuk buku. Rating bersifat eksplisit (1-10) atau implisit (0).                          | 0, 5, 3                            | Rating 0 menunjukkan interaksi implisit.          |

---
### Kondisi Data
Sebelum dilakukan pemodelan, dilakukan pemeriksaan terhadap kondisi awal dataset, dengan hasil sebagai berikut:
- Missing Value:
   -    Pada file `BX-Users.csv`, kolom Age memiliki sejumlah besar nilai yang hilang (sekitar 39.7% atau lebih).  Nilai-nilai ini seringkali diimputasi menggunakan median         atau mean setelah membersihkan outlier, atau pengguna dengan usia NaN dapat dihapus jika analisis tidak terlalu bergantung pada fitur usia. Pada tahap preparation          nanti, kita tidak akan menggunakan data usia
   -    Pada file `BX-Books.csv`, kolom Book-Author dan Publisher memiliki data yang hilang sebanyak 2.  Nilai yang hilang pada Book-Author dan          
        Publisher biasanya diganti dengan string seperti "Unknown" atau modus. Selanjutnya pun, data book-author dan publisher tidak digunakan.
   -    Pada file `BX-Book-Ratings.csv`, tidak ditemukan nilai yang hilang.
- Duplikasi:
  -    Pada ketiga file dataset tidak ditemui duplikasi data

---
Eksplorasi Data dan Visualisasi

Untuk memahami distribusi dan karakteristik awal dari data, dilakukan beberapa tahapan eksplorasi data berikut:
1. **Distribusi Rating**
   Hal ini dilakukan guna mengetahui distribusi rating yang diberikan kepada pelanggan seperti apa dan dominan ke arah apa.

   ![image](https://github.com/user-attachments/assets/65a258a6-67c9-48cc-b27e-fb874bf6ad4b)

## Data Preparation
Sebelum memulai proses pelatihan model, dilakukan beberapa tahap *data preparation* untuk memastikan bahwa data dalam kondisi bersih, lengkap, dan sesuai untuk dianalisis oleh algoritma machine learning.

### 1.  Gabung Dataset Rating dengan Dataset Buku

Menggabungkan data `BX-Book-Ratings` dengan `BX-Books` berdasarkan ISBN dan menghapus kolom-kolom yang tidak diperlukan.
Tujuan: Untuk mendapatkan data rating yang lengkap dengan judul buku agar bisa digunakan pada proses pivoting dan sistem rekomendasi berbasis judul.

### 2.  Filter Jumlah Minimum Rating
- Hanya menyertakan buku yang memiliki setidaknya X jumlah rating (misalnya ≥ 30).
- Hanya menyertakan pengguna yang telah memberikan sejumlah minimum rating (misalnya ≥ 10).
Alasan: Mengurangi sparsity data. Meningkatkan relevansi hasil rekomendasi. Menghindari pengguna/buku yang tidak signifikan secara statistik.

### 3.  Membuat Pivot Table Rating
Membentuk pivot table dengan Book-Title sebagai indeks dan User-ID sebagai kolom. Mengisi nilai kosong dengan 0 agar dapat digunakan pada model berbasis KNN.
Tujuan: Format ini dibutuhkan untuk perhitungan similarity antar item (item-based collaborative filtering).

### 4.  Membagi Data ke Train/Test
Data pengguna dibagi menjadi train_data dan test_data secara manual. Dalam hal ini data training dan data testing berbanding (80:20)
Tujuannya agar bisa menghitung Precision@K dan simulasi sistem rekomendasi.

### 5. Transformasi ke Format Library Surprise
Dataset diubah menjadi format rating triplet (`User-ID`, `Book-Title`, `Rating`). Dibentuk dengan `Dataset.load_from_df(...)` menggunakan Reader dari library Surprise.
Alasan: Ini memungkinkan digunakan untuk algoritma seperti SVD, KNNBasic, dsb.

## Modeling
Pada bagian ini dilakukan proses pembangunan dan evaluasi model sistem rekomendasi. Model dibangun untuk memberikan Top-N Recommendation bagi setiap pengguna berdasarkan data rating buku. Dua pendekatan algoritma digunakan untuk membandingkan performa dan pendekatannya terhadap permasalahan.

###  1. Model 1: Item-based KNN Collaborative Filtering
🔧 Deskripsi

Model pertama menggunakan pendekatan item-based collaborative filtering dengan algoritma K-Nearest Neighbors (KNN). Model mencari kemiripan antar item (buku) berdasarkan pola rating pengguna, kemudian merekomendasikan buku yang mirip dengan yang pernah disukai pengguna.

- Data digunakan dalam bentuk pivot table (`Book-Title` x `User-ID`).
- Kemiripan dihitung menggunakan metrik cosine similarity.

✅ Kelebihan:
- Interpretasi mudah karena mirip seperti logika manusia: “jika kamu suka buku A, kamu mungkin suka buku B yang mirip.”
- Tidak membutuhkan data user baru saat inferensi (bisa langsung berbasis item).

❌ Kekurangan:
- Tidak bisa merekomendasikan item yang belum pernah diberi rating oleh user mana pun (cold start problem untuk item).
- Tidak menangkap dimensi laten atau pola implisit yang tersembunyi dalam data.

###  2. Model 2: SVD + KNN (Latent Factor Hybrid)
🔧 Deskripsi
Model kedua menggabungkan pendekatan Matrix Factorization (SVD) dengan KNN. Langkahnya adalah:
- Melatih model SVD untuk mendapatkan vektor laten (latent factors) dari setiap item.
- Menggunakan hasil vektor laten tersebut sebagai input fitur ke KNN model.
- Kemudian mencari kemiripan antar item berdasarkan vektor laten.

✅ Kelebihan:
- Menggabungkan kekuatan model faktorisasi (SVD) untuk menangkap dimensi laten dari interaksi user-item.
- Lebih baik dalam mengatasi sparsity dan menghasilkan rekomendasi yang personal.

❌ Kekurangan:
- Interpretasi lebih sulit karena vektor laten tidak langsung bermakna.
- Membutuhkan lebih banyak pelatihan dan perhitungan.

### Output
Di sini kita menggunakan judul buku Exclusive sebagai input dan menampilkan 5 buku rekomendasi

###  1. Model 1: Item-based KNN Collaborative Filtering

```
For KNN, for book "Exclusive" direkomendasikan 5 buku berikut:
1. Free (jarak: 0.6196)
2. Breath of Scandal (jarak: 0.6705)
3. Temple (jarak: 0.6774)
4. Simisola (jarak: 0.6997)
5. Monsieur Ibrahim und die Blumen des Koran. ErzÃ?Â¤hlung. (jarak: 0.7310)
```

###  2. Model 2: SVD + KNN (Latent Factor Hybrid)

```
For SVD, for book "Exclusive" direkomendasikan 5 buku berikut:
1. Charade (jarak: 0.0202)
2. Harvest (jarak: 0.0309)
3. Kentucky Sunrise (jarak: 0.0322)
4. Journey (jarak: 0.0324)
5. Deadly Grace (jarak: 0.0329)
```

## Evaluation
Pada tahap ini, proyek melakukan evaluasi terhadap performa sistem rekomendasi yang dibangun menggunakan metrik yang sesuai dengan konteks dan tujuan.

### Metrik Evaluasi: Precision@K
Metrik utama yang digunakan dalam proyek ini adalah Precision@K, khususnya Precision@5, yang mengukur proporsi item yang direkomendasikan dan benar-benar relevan bagi pengguna. Ini sangat penting dalam konteks top-N recommendation, di mana sistem hanya perlu menampilkan sejumlah kecil rekomendasi terbaik.

### Formula dan Cara Kerja
Precision@K didefinisikan sebagai: 

$$Precision@K = (|Recommended Items ∩ Relevant Items|) / K$$

- Recommended Items: daftar item (buku) yang direkomendasikan oleh sistem (misalnya Top-5).
- Relevant Items: item yang benar-benar disukai oleh pengguna, berdasarkan interaksi historis (dalam hal ini, data uji).
- K: jumlah item yang direkomendasikan (dalam proyek ini, K = 5).

Evaluasi dilakukan hanya pada pengguna yang muncul dalam data latih (train set), untuk memastikan sistem memiliki informasi sebelumnya tentang pengguna.

### Hasil Evaluasi

| Model                          | Precision@5 |
|-------------------------------|-------------|
| KNN Collaborative Filtering   | 0.0119      |
| SVD + KNN (Hybrid)            | 0.0091      |

Berdasarkan hasil evaluasi, model **KNN Collaborative Filtering** sedikit lebih unggul dalam hal relevansi rekomendasi dibandingkan pendekatan hybrid SVD + KNN pada dataset ini. Meskipun precision secara keseluruhan masih rendah, hasil ini memberikan gambaran awal terhadap efektivitas pendekatan yang digunakan.

---

### 🔗 Hubungan dengan Problem Statement dan Goals

#### Problem Statement 1:
**Bagaimana cara merekomendasikan buku yang relevan kepada pengguna berdasarkan interaksi pengguna lain yang serupa?**

➡ Precision@5 menunjukkan *berapa relevan* rekomendasi terhadap preferensi pengguna. Nilai precision memberikan gambaran seberapa baik sistem mengenali item yang mungkin disukai pengguna.

---

#### Problem Statement 2:
**Bagaimana meningkatkan kualitas rekomendasi menggunakan metode collaborative filtering?**

➡ Meskipun kedua pendekatan masih menghasilkan precision yang relatif rendah, proyek ini menunjukkan proses eksplorasi awal dalam membandingkan dua metode collaborative filtering (KNN dan SVD), sebagai langkah penting menuju sistem yang lebih baik.

---

#### Problem Statement 3:
**Bagaimana mengevaluasi performa sistem rekomendasi dengan metrik yang sesuai?**

➡ Metrik Precision@K yang digunakan tepat sasaran karena fokus pada relevansi rekomendasi. Ini sangat cocok untuk sistem yang menampilkan sejumlah kecil rekomendasi utama kepada pengguna.

---

### 📌 Kesimpulan Evaluasi

Evaluasi menggunakan Precision@5 menunjukkan bahwa sistem rekomendasi masih memiliki ruang besar untuk peningkatan, terutama dalam konteks relevansi rekomendasi. Namun, perbandingan antara dua pendekatan memberikan wawasan tentang bagaimana preferensi pengguna dapat dimodelkan dengan cara berbeda.

Pengembangan lebih lanjut dapat mencakup eksplorasi algoritma lain, peningkatan preprocessing data, atau penggunaan metrik tambahan seperti Recall@K atau MAP untuk mendapatkan pemahaman yang lebih menyeluruh terhadap performa sistem.


