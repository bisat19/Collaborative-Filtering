# Laporan Proyek Machine Learning - Abisatya Hastarangga Pradana

## Project Overview

Di era digital saat ini, jumlah informasi yang tersedia, termasuk dalam bentuk buku, telah meningkat secara eksponensial. Pembaca seringkali dihadapkan pada tantangan besar dalam menemukan buku yang benar-benar sesuai dengan preferensi dan minat mereka di antara jutaan pilihan yang ada [(Miriyala; et.al, 2025)(https://ijnrd.org/papers/IJNRD2503444.pdf)]. Metode pencarian tradisional atau penelusuran manual seringkali tidak efisien dan memakan waktu, menyebabkan pengguna mungkin melewatkan karya-karya yang relevan atau merasa kewalahan dengan banyaknya pilihan. Fenomena ini dikenal sebagai information overload, dan sistem rekomendasi hadir sebagai solusi untuk membantu pengguna menavigasi lautan informasi ini.

Masalah kesulitan dalam pemilihan buku ini penting untuk diselesaikan karena berdampak langsung pada pengalaman membaca pengguna dan juga pada ekosistem literasi secara keseluruhan. Pengguna yang kesulitan menemukan buku yang menarik mungkin akan berkurang minat bacanya, sementara penulis dan penerbit buku-buku yang kurang populer (sering disebut sebagai long-tail items) mungkin kesulitan mendapatkan visibilitas yang layak. Sistem rekomendasi yang efektif dapat meningkatkan kepuasan pengguna dengan menyajikan pilihan yang lebih personal, mendorong penemuan buku-buku baru, dan membantu karya-karya yang beragam untuk menjangkau pembaca yang tepat [(Leukhong, 2025)(https://www.jisem-journal.com/index.php/journal/article/view/492)].

Proyek ini bertujuan untuk mengatasi masalah tersebut dengan merancang dan mengimplementasikan sistem rekomendasi buku menggunakan teknik collaborative filtering. Collaborative filtering adalah pendekatan yang populer dan terbukti efektif, yang bekerja dengan menganalisis pola perilaku dan preferensi dari banyak pengguna untuk membuat prediksi tentang minat seorang pengguna terhadap item yang belum pernah ia temui. 

Dengan memanfaatkan dataset Book-Crossings, yang berisi data rating buku dari sejumlah besar pengguna, proyek ini akan melakukan pra-pemrosesan data, analisis data eksploratif untuk memahami karakteristik data, melatih model UBCF dan SVD, dan mengevaluasinya menggunakan metrik standar seperti Precision. Pendekatan ini diharapkan dapat memberikan rekomendasi buku yang lebih personal dan relevan, sekaligus mengatasi tantangan umum dalam sistem rekomendasi seperti data sparsity (di mana sebagian besar pengguna hanya memberi rating pada sebagian kecil buku) dan cold start problem (kesulitan merekomendasikan untuk pengguna baru atau buku baru).

## Business Understanding

Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah:
- Pernyataan Masalah 1
- Pernyataan Masalah 2
- Pernyataan Masalah n

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Jawaban pernyataan masalah 1
- Jawaban pernyataan masalah 2
- Jawaban pernyataan masalah n

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution approach (algoritma atau pendekatan sistem rekomendasi).

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
