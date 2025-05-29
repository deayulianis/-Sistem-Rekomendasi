# Laporan Proyek Machine Learning - Dea Yuliani Sabrina

## Project Overview

### **Latar Belakang**

Anime adalah bentuk hiburan yang sangat populer dengan jumlah judul yang terus bertambah setiap tahun. Banyaknya pilihan membuat pengguna kesulitan memilih anime yang sesuai dengan preferensi mereka. Oleh karena itu, sistem rekomendasi menjadi solusi penting untuk membantu pengguna menemukan tontonan yang relevan secara otomatis dan efisien. Proyek ini menggunakan dataset anime.csv yang berisi informasi seperti judul, genre, skor, dan rating pengguna untuk membangun sistem rekomendasi berbasis data.

![image](https://github.com/user-attachments/assets/911a88a9-367f-4ec0-b4b4-364a858fb80b)


Pentingnya proyek ini didukung oleh riset yang menyebutkan bahwa sistem rekomendasi dapat meningkatkan pengalaman pengguna dan mengurangi kelelahan dalam memilih informasi (information overload). Ricci, Rokach, dan Shapira (2015) menjelaskan bahwa sistem rekomendasi membantu pengguna menemukan konten yang sesuai dari kumpulan data besar dan berperan penting dalam mempertahankan loyalitas pengguna pada platform digital.

**Referensi:** [Recommender Systems Handbook (2nd ed.)](https://doi.org/10.1007/978-1-4899-7637-6)

## Business Understanding

### **Problem Statements**

- Bagaimana cara membantu pengguna menemukan anime yang sesuai dengan preferensi mereka di antara ribuan judul yang tersedia?
- Bagaimana meningkatkan pengalaman pengguna agar mereka tetap terlibat dan puas saat menggunakan platform rekomendasi anime?
- Bagaimana memanfaatkan data yang tersedia (genre, skor, rating, dll) untuk memberikan rekomendasi yang relevan?

### **Goals**

- Membangun sistem rekomendasi yang mampu memberikan saran anime yang sesuai dengan minat pengguna secara otomatis.
- Meningkatkan kenyamanan pengguna dalam memilih anime dan mengurangi waktu pencarian.
- Menggunakan fitur-fitur dalam dataset seperti genre, skor, dan popularitas untuk membuat model rekomendasi yang akurat.

### **Solution Approach**

Untuk mencapai tujuan di atas, proyek ini akan menggunakan pendekatan sistem rekomendasi sebagai berikut:

1. Content-Based Filtering

Pendekatan ini merekomendasikan anime berdasarkan kemiripan fitur konten. Sistem akan membandingkan anime berdasarkan **genre**, **type**, **jumlah episode**, dan **rating**. 

2. Popularity-Based Recommendation

Pendekatan ini menyarankan anime berdasarkan **jumlah anggota (members)** atau **rating tertinggi**. Ini berguna sebagai baseline model dan untuk pengguna baru (cold start), karena sistem bisa langsung menyarankan anime yang populer dan disukai banyak orang tanpa memerlukan data interaksi pengguna.

# Data Understanding

Dataset yang digunakan dalam proyek ini merupakan dataset tentang anime. Dataset ini dapat diunduh di [Kaggle:Anime Recommendations Database](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database?select=anime.csv)

*Load Dataset & Melihat Struktur Awal*

![image](https://github.com/user-attachments/assets/46af3920-07cf-4a8c-a3a1-00d5da8db3e0)

- Menampilkan 5 data teratas

## Exploratory Data Analysis

*Cek Variabel*

![image](https://github.com/user-attachments/assets/7c763fb1-7ca7-4c9b-a228-f90bcc105929)

*Variabel-variabel pada dataset anime adalah sebagai berikut:*
- **anime_id** : ID unik untuk setiap anime.
- **name** : 	Judul atau nama anime.
- **genre** : Kategori atau jenis anime, seperti Action, Comedy, Romance, dll.
- **type** : Jenis media dari anime tersebut, misalnya TV (serial televisi), Movie (film), OVA (Original Video Animation), dll.
- **episodes** : Jumlah episode yang dimiliki oleh anime tersebut. Nilainya bisa berupa angka atau string 'Unknown' untuk anime yang belum lengkap informasinya.
- **rating** : 	Skor rata-rata dari pengguna terhadap anime dalam skala 1–10..
- **members** : Jumlah anggota (pengguna) yang menambahkan anime ke dalam daftar tontonan mereka.

*Mengetahui ukuran (dimensi) dari dataset*

![image](https://github.com/user-attachments/assets/2a074d2c-8dc1-4ca7-8938-1ffff377ae0f)

- Mengetahui ukuran (dimensi) dari dataset yaitu 12294 baris dengan 7 kolom.

*Melihat Informasi Struktur Dataset*

![image](https://github.com/user-attachments/assets/f6440cec-deb6-4aa6-88fc-d81e391cb15b)

- Terdapat 4 kolom dengan tipe object, yaitu: name, genre, type, dan episodes. Kolom ini merupakan categorical features (fitur non-numerik).
- Terdapat 1 kolom numerik dengan tipe data float64 yaitu: rating. Ini merupakan fitur numerik yang merupakan hasil pengukuran secara fisik.
- Terdapat 2 kolom numerik dengan tipe data int64, yaitu: anime_id, dan members.

*Statistik Deskriptif*

![image](https://github.com/user-attachments/assets/ccb5ba23-2acd-4e01-884a-dc2f0cf23930)

✅ Kolom **anime_id**
- ID tidak berurutan (rentang 1 – 34.527).
- Nilai mean lebih tinggi dari median → distribusi cenderung ke kanan (banyak ID kecil, sedikit ID besar).

✅ Kolom **rating**
- Terdapat 230 anime yang tidak memiliki rating.
- Rata-rata rating: 6.47.
- Nilai rating berkisar antara 1.67 – 10.
- 25% anime memiliki rating < 5.88.
- 50% (median) anime memiliki rating = 6.57.
- 75% anime memiliki rating < 7.18.
- Mayoritas anime memiliki rating menengah, hanya sedikit yang rating-nya sangat tinggi.

✅ Kolom **members**
- Rata-rata jumlah anggota: 18.071.
- Nilai minimum: 5 anggota.
- Nilai maksimum: 1.013.917 anggota.
- 25% anime punya < 225 anggota.
- 50% (median) anime punya 1.550 anggota.
- 75% anime punya < 9.437 anggota.
- Data sangat skewed ke kanan → hanya sebagian kecil anime yang sangat populer.

*Mengecek Missing Values*

![image](https://github.com/user-attachments/assets/943ae41f-8f13-455c-83f6-3716675bd176)

- anime_id, name, episodes, members : Tidak ada missing value (0) → Data pada kolom ini lengkap.
- Terdapat 62 data yang tidak memiliki genre → bisa jadi karena data belum dilengkapi atau anime tersebut sulit dikategorikan.
- Terdapat 25 data tanpa tipe media (TV, Movie, OVA, dll) → kemungkinan data tidak tersedia atau belum diketahui.
- Terdapat 230 data tanpa nilai rating → bisa jadi anime tersebut belum cukup banyak ditonton atau belum dinilai oleh pengguna.














