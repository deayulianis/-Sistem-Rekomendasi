# Laporan Proyek Machine Learning - Dea Yuliani Sabrina

## Project Overview

### Latar Belakang

Seiring dengan pesatnya pertumbuhan industri perfilman dan kemunculan berbagai platform streaming digital seperti Netflix, Disney+, dan Amazon Prime, pengguna kini dihadapkan pada ribuan pilihan film yang dapat ditonton kapan saja. Banyaknya pilihan ini justru menimbulkan tantangan tersendiri, yaitu kesulitan dalam menentukan film yang sesuai dengan preferensi masing-masing pengguna. Oleh karena itu, sistem rekomendasi menjadi solusi penting dalam membantu pengguna menemukan konten yang relevan dan menarik.Sistem rekomendasi tidak hanya meningkatkan pengalaman pengguna dengan memberikan saran yang dipersonalisasi, tetapi juga memiliki nilai strategis bagi penyedia layanan dengan mendorong peningkatan engagement dan retensi pelanggan.

![image](https://github.com/user-attachments/assets/1877e93f-f407-4fc8-92bd-f72d56f5c0bd)

### Mengapa dan Bagaimana Masalah Ini Harus Diselesaikan?

Masalah kelebihan informasi dalam pemilihan film tidak hanya berdampak pada pengalaman pengguna, tetapi juga terhadap bisnis penyedia layanan hiburan. Tanpa sistem rekomendasi yang efektif, pengguna cenderung menghabiskan waktu lebih lama dalam proses pencarian atau bahkan meninggalkan platform.Membangun sistem rekomendasi yang andal dapat membantu menyaring informasi secara otomatis, memberikan personalisasi, dan menciptakan pengalaman menonton yang lebih menyenangkan dan efisien. 

Dengan pendekatan content-based, pengguna akan menerima rekomendasi yang mirip dengan film yang disukai sebelumnya, sementara collaborative filtering membantu menemukan film populer yang disukai pengguna lain dengan selera serupa.Kedua pendekatan ini saling melengkapi dan dapat dibandingkan dari sisi efektivitas dan akurasi dalam menyajikan rekomendasi yang relevan.

### Referensi : [Introduction to Recommender Systems Handbook. Recommender Systems Handbook](https://link.springer.com/chapter/10.1007/978-0-387-85820-3_1)

# Business Understanding

Pada bagian ini, dijelaskan proses klarifikasi masalah yang ingin diselesaikan melalui proyek sistem rekomendasi film menggunakan pendekatan Content-Based Filtering dan Collaborative Filtering.

### Problem Statements
- Pengguna sering mengalami kesulitan dalam menemukan film yang sesuai dengan preferensi mereka akibat banyaknya pilihan film yang tersedia di platform digital.
- Belum adanya sistem rekomendasi yang dipersonalisasi berdasarkan minat atau histori pengguna dapat menurunkan pengalaman pengguna dan keterlibatan terhadap platform film.
- Diperlukan evaluasi pendekatan sistem rekomendasi yang paling efektif untuk membantu pengguna menemukan film yang relevan dan menarik dari dataset yang sangat besar.

### Goals
- Mengembangkan sistem rekomendasi film yang dapat menyaring dan merekomendasikan film sesuai dengan preferensi pengguna untuk mempermudah proses pencarian.
- Mengimplementasikan sistem rekomendasi dengan pendekatan Content-Based Filtering dan Collaborative Filtering untuk meningkatkan pengalaman personalisasi pengguna.
- Melakukan evaluasi terhadap performa kedua pendekatan untuk mengetahui mana yang paling sesuai dengan karakteristik data serta mampu memberikan hasil yang akurat dan relevan.

### Solution Approach
Untuk mencapai tujuan di atas, dua pendekatan utama yang akan digunakan adalah:

**1. Content-Based Filtering**
Pendekatan ini merekomendasikan film kepada pengguna berdasarkan kesamaan atribut dari film yang pernah disukai sebelumnya. Contoh atribut yang akan digunakan antara lain:
- Genre
- Deskripsi/sinopsis film
- Tagline dan kata kunci
Model ini bekerja dengan cara menghitung kemiripan antar film menggunakan teknik seperti TF-IDF dan cosine similarity dari teks sinopsis atau metadata film lainnya.

**Kelebihan:**
- Tidak bergantung pada data pengguna lain.
- Dapat memberikan hasil yang konsisten berdasarkan preferensi sebelumnya.

**Kekurangan:**
- Kurang mampu merekomendasikan film di luar "lingkaran" preferensi pengguna.
- Terbatas jika informasi film (fitur) tidak lengkap.

**2.Collaborative Filtering**
Pendekatan ini menyarankan film berdasarkan pola perilaku pengguna lain yang memiliki preferensi serupa. Karena dataset ini tidak secara langsung menyediakan interaksi pengguna, pendekatan ini akan menggunakan model matrix factorization berdasarkan kolom vote_average dan vote_count untuk meniru rating atau preferensi pengguna.

**Kelebihan:**
- Dapat memberikan rekomendasi yang lebih beragam dan mengejutkan (sering disebut "serendipity").
- Tidak memerlukan detail isi film.

**Kekurangan:**
- Membutuhkan cukup banyak data pengguna (user-item interactions).
- Rentan terhadap masalah cold-start, terutama untuk film atau pengguna baru.

# Data Understanding
Dataset yang digunakan dalam proyek ini merupakan data diabetes. Dataset ini dapat diunduh di [Kaggle : Full TMDB Movies Dataset 2024 (1M Movies)](https://www.kaggle.com/datasets/asaniczka/tmdb-movies-dataset-2023-930k-movies)

![image](https://github.com/user-attachments/assets/3fc02b7c-bd77-4ceb-9cc0-267002695c02)

- Melihat 5 baris pertama dari dataset yang berisi data diabetes.

**Variabel (Kolom) pada Dataset**
1. id: ID unik untuk setiap film dalam database TMDB.
2. title: Judul film.
3. vote_average: Nilai rata-rata dari semua penilaian pengguna.
4. vote_count: Jumlah total pengguna yang memberikan penilaian.
5. status: Status rilis film (misalnya Released, Post Production).
6. release_date: Tanggal rilis film.
7. revenue: Pendapatan kotor film secara global (dalam USD).
8. runtime: Durasi film dalam menit.
9. adult: Apakah film diklasifikasikan untuk penonton dewasa (True/False).
10. backdrop_path: Path ke gambar latar belakang film.
11. original_title: Judul asli film (sebelum diterjemahkan).
12. overview: Ringkasan singkat atau sinopsis dari film.
13. popularity: Skor popularitas yang dihitung oleh TMDB berdasarkan interaksi pengguna.
14. poster_path: Path ke poster resmi film.
15. tagline: Kalimat pemasaran pendek yang digunakan dalam promosi film.
16. genres: Genre film, misalnya Action, Drama, Comedy (berbentuk list).
17. production_companies: Nama-nama perusahaan produksi yang terlibat dalam pembuatan film.
18. roduction_countries: Negara-negara tempat produksi film.
19. spoken_languages: Bahasa yang digunakan dalam film.
20. keywords: Kata kunci deskriptif yang berkaitan dengan isi film.
21. budget: Anggaran produksi film.
22. homepage: Situs web resmi film.
23. original_language: Bahasa asli film.
24. imdb_id: ID film berdasarkan database IMDb.
    
## Exploratory Data Analysis

**Mengetahui ukuran(dimensi) dari dataset**

![image](https://github.com/user-attachments/assets/8991245d-6639-4d89-8515-608cec6f2e19)

- Mengetahui ukuran (dimensi) dari dataset yaitu 1231078 baris dengan 24 kolom.

**Mengetahui struktur dasar dataset**

![image](https://github.com/user-attachments/assets/e2b3cd97-2fe6-4777-a597-08b2c1258b73)

- Terdapat 16 kolom dengan tipe object, yaitu: title, status, release_date, backdrop_path, homepage, imdb_id, original_language, original_title, overview, poster_path, tagline,  genres, production_companies, production_countries, spoken_languages, dan keywords. Kolom ini merupakan categorical features (fitur non-numerik).
- Terdapat 2 kolom numerik dengan tipe data float64 yaitu: vote_average, dan popularity. Ini merupakan fitur numerik yang merupakan hasil pengukuran secara fisik.
- Terdapat 4 kolom numerik dengan tipe data int64, yaitu:  id, revenue, runtime, dan budget. 
- Terdapat 1 kolom dengan tipe bool, yaitu: adult.

**Melakukan analisis statistik deskriptif**

![image](https://github.com/user-attachments/assets/3dde2c78-cb15-46e3-add2-6133053f8f8f)

- **vote_average:** Rata-rata nilai voting sangat rendah (mean = 1.76 dari maksimal 10), dan median adalah 0. Ini menunjukkan bahwa banyak film yang belum mendapatkan voting sama sekali.
- **vote_count:** Sebagian besar film belum mendapat voting sama sekali (median = 0), dan hanya sedikit yang mendapat banyak voting (lihat max = 34.495).
- **revenue & budget:** Banyak nilai 0, menandakan banyak film yang tidak memiliki data pendapatan atau anggaran. Namun, ada juga nilai ekstrem dengan revenue hingga 5 miliar dan budget hingga 1 miliar.
- **runtime:** Ada nilai negatif, yang tidak logis untuk durasi film (minimum = -28). Ini kemungkinan adalah kesalahan data (data anomali).
- **popularity:** Nilainya sangat kecil rata-rata (mean = 1.16), tetapi dengan rentang yang sangat besar (maksimal = 2.994).













