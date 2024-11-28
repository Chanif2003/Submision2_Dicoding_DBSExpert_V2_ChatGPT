# Laporan Proyek: Sistem Rekomendasi Film Menggunakan Content-Based dan Collaborative Filtering

## 1. Project Overview

### A. Latar Belakang
Dalam era digital, pengguna sering menghadapi masalah dalam memilih konten yang relevan di tengah banyaknya pilihan yang tersedia. Dalam industri film, jumlah film yang terus bertambah setiap tahunnya membuat pengguna kesulitan menemukan film yang sesuai dengan minat mereka. Tanpa sistem rekomendasi, pengguna sering kali harus bergantung pada pencarian manual atau ulasan yang tidak selalu mencerminkan preferensi pribadi.

Masalah ini menjadi semakin relevan karena:
1. **Ledakan Data**: Industri hiburan memproduksi jutaan konten setiap tahun.
2. **Efisiensi Waktu**: Pengguna tidak memiliki waktu untuk mengeksplorasi semua opsi yang tersedia secara manual.
3. **Pengalaman Pengguna**: Tanpa personalisasi, pengguna sering merasa tidak puas dengan rekomendasi generik.

Sistem rekomendasi menawarkan solusi dengan memberikan saran personal yang relevan berdasarkan data historis pengguna dan karakteristik konten.
   
### B. Masalah yang Dihadapi
1. **Ketidakmampuan Sistem Generik**: Rekomendasi berbasis popularitas tidak mempertimbangkan preferensi unik pengguna.
2. **Keterbatasan Data Perilaku**: Tidak semua pengguna memiliki riwayat perilaku yang cukup untuk mendukung rekomendasi berbasis Collaborative Filtering.
3. **Kesalahan dalam Pemahaman Konteks**: Sistem rekomendasi tradisional sering gagal memahami konteks atau hubungan antara konten berdasarkan deskripsi tekstual.
   
### C. Tujuan Proyek
1. Membangun sistem rekomendasi yang efektif dengan menggabungkan pendekatan **Content-Based Filtering** dan **Collaborative Filtering**.
2. Menyediakan rekomendasi yang personal dan relevan bagi pengguna.
3. Mengoptimalkan akurasi rekomendasi melalui tuning hyperparameter, seperti pada TF-IDF.
   
### D. Manfaat Proyek
1. **Meningkatkan Pengalaman Pengguna**: Rekomendasi yang lebih relevan meningkatkan kepuasan pengguna.
2. **Efisiensi Waktu**: Membantu pengguna menemukan film yang sesuai tanpa harus mencari secara manual.
3. **Potensi Bisnis**: Sistem rekomendasi yang efektif dapat meningkatkan keterlibatan pengguna, yang pada akhirnya berdampak positif pada metrik bisnis seperti retensi pelanggan.

---

## 2. Business Understanding

### A. Problem Statements
1. Bagaimana memberikan rekomendasi film yang relevan untuk pengguna berdasarkan deskripsi film (Content-Based)?
2. Bagaimana meningkatkan kualitas rekomendasi dengan data perilaku pengguna (Collaborative Filtering)?
3. Bagaimana mengukur performa sistem rekomendasi secara kuantitatif?
   
### B. Goals
1. Memberikan rekomendasi personal yang relevan berdasarkan preferensi pengguna.
2. Meningkatkan akurasi model dengan kombinasi pendekatan dan tuning hyperparameter.
3. Membandingkan kinerja sistem dengan metrik evaluasi.
   
### C. Solution Statements
1. **Content-Based Filtering**:
   - Menggunakan TF-IDF untuk merepresentasikan fitur teks seperti genre, sinopsis, dan kata kunci.
   - Menghitung kesamaan menggunakan cosine similarity.
2. **Collaborative Filtering**:
   - Menggunakan data rating pengguna untuk membangun matriks kesamaan antar pengguna.
3. **Gabungan Kedua Pendekatan**:
   - Menggunakan weighted ensemble dari kedua metode untuk meningkatkan kualitas rekomendasi.
4. **Hyperparameter Tuning**:
   - Melakukan pencarian grid pada parameter TF-IDF untuk meningkatkan representasi data teks.

---

## 3. Data Understanding

### A. Tautan sumber dataset:
   [TMDB 5000 Movie Dataset with Ratings on Kaggle](https://www.kaggle.com/datasets/aayushsoni4/tmdb-5000-movie-dataset-with-ratings)
   
### B. Uraian Setiap Fitur Data

#### Dataset 1 (tmdb_movie_dataset.csv) : Informasi Film
1. **`budget`:** Anggaran produksi film dalam satuan mata uang tertentu. (Tipe Data: Integer)
2. **`genres`:** Daftar genre film (misalnya, Action, Drama). (Tipe Data: Object (teks))
3. **`homepage`:** URL situs resmi film (jika ada). (Tipe Data: Object (teks))  
4. **`id`:** ID unik untuk setiap film. (Tipe Data: Integer)
5. **`keywords` :** Kata kunci terkait film (misalnya, tema atau konsep utama). (Tipe Data: Object (teks))  
6. **`original_language`:** Bahasa asli film dalam kode ISO 639-1 (misalnya, "en" untuk Inggris). (Tipe Data: Object (teks))  
7. **`original_title`:** Judul asli film. (Tipe Data: Object (teks))  
8. **`overview`:** Deskripsi: Sinopsis atau ringkasan cerita film. (Tipe Data: Object (teks))
9. **`popularity`:** Popularitas film berdasarkan skor tertentu. (Tipe Data: Float)
10. **`production_companies`:** Daftar perusahaan produksi yang terlibat dalam pembuatan film. (Tipe Data: Object (teks))
11. **`production_countries`:** Negara-negara tempat film diproduksi. (Tipe Data: Object (teks))
12. **`release_date`:** Tanggal rilis film. (Tipe Data: Object (teks, format tanggal))
13. **`revenue`:** Pendapatan total yang dihasilkan film dalam satuan mata uang tertentu. (Tipe Data: Integer)
14. **`runtime`:** Durasi film dalam menit. (Tipe Data: Float)
15. **`spoken_languages`:** Daftar bahasa yang digunakan dalam film (dalam kode ISO 639-1). (Tipe Data: Object (teks))
16. **`status`:** Status produksi film (misalnya, "Released"). (Tipe Data: Object (teks))
17. **`tagline`:** Tagline atau slogan film. (Tipe Data: Object (teks))
18. **`title`:** Judul resmi film. (Tipe Data: Object (teks))
19. **`vote_average`:** Rata-rata nilai rating film dari pengguna. (Tipe Data: Float)
20. **`vote_count`:** Jumlah total suara pengguna untuk film. (Tipe Data: Integer)
21. **`ratingId`:** ID yang merepresentasikan entri di sistem penilaian. (Tipe Data: Integer)
   
#### Dataset 2 (tmdb_movie_ratings.csv): Rating Pengguna
1. **`userId`:** ID unik pengguna yang memberikan rating. (Tipe Data: Integer)
2. **`movieId`:** ID unik film yang dirating pengguna. (Tipe Data: Integer)
3. **`rating`:** Nilai rating yang diberikan pengguna untuk film. (Tipe Data: Float) 
   
#### Dataset 3 (tmdb_movie_credits.csv): Cast dan Crew
1. **`id`:** ID unik untuk setiap film (sejalan dengan Dataset 1). (Tipe Data: Integer)  
2. **`cast`:** Daftar aktor yang terlibat dalam film (kemungkinan berbentuk JSON atau string). (Tipe Data: Object (teks))  
3. **`crew`:** Daftar kru film (misalnya, sutradara, produser, penulis skenario). (Tipe Data: Object (teks))
   
### Kesimpulan
- **Dataset Pertama**: Fokus pada informasi deskriptif film, cocok untuk analisis hubungan variabel seperti `budget`, `revenue`, dan genre.
- **Dataset Kedua**: Sangat besar dan cocok untuk membangun sistem rekomendasi film berdasarkan interaksi pengguna.
- **Dataset Ketiga**: Berguna untuk analisis pemain dan kru, termasuk kolaborasi dan keterlibatan mereka dalam film dengan rating tinggi.

---

## 4. Data Preparation

### Alasan Data Preparation
- Membersihkan teks memastikan hasil TF-IDF lebih representatif.
- Menggabungkan fitur memberikan lebih banyak informasi untuk **Content-Based Filtering.**
- Matriks diperlukan untuk menghitung kesamaan pengguna dalam **Collaborative Filtering.**

### Data Preparation untuk Content-Based Filtering
   
#### 1. Menggabungkan dan Menyaring Data
   - **Data Gabungan**: Menggabungkan informasi film dari dua sumber data (`movies_df` dan `credits_df`) berdasarkan kolom `id`.
   - **Pemilihan Kolom Penting**: Mengambil hanya kolom yang relevan, yaitu `id`, `title`, `overview`, `genres`, `keywords`, `cast`, dan `crew`.
   
#### 2. Membersihkan dan Memformat Data
   - **Mengonversi Format Data**: 
     - Genre, kata kunci, pemeran, dan kru yang berbentuk string JSON diubah menjadi daftar (list) untuk mempermudah pengolahan.
   - **Menghapus Nilai Kosong**: Menghapus baris dengan data yang hilang untuk memastikan kelengkapan informasi.
   - **Ekstraksi Data Penting**:
     - Mengambil nama sutradara dari kru (`crew`).
     - Menghapus spasi dari setiap elemen di daftar genre, kata kunci, pemeran, dan kru untuk menjaga konsistensi data.

#### 3. Menggabungkan Fitur
   - Semua informasi penting seperti ringkasan (`overview`), genre, kata kunci, pemeran, dan kru digabung menjadi satu kolom fitur tunggal (`features`) untuk setiap film.

#### 4. Representasi Numerik dengan TF-IDF
   - **Teknik TF-IDF**: Mengubah teks dalam kolom `features` menjadi vektor numerik menggunakan metode TF-IDF.
     - Kata-kata yang sering muncul di seluruh dokumen (film) mendapat bobot rendah.
     - Hanya 5000 kata paling relevan yang dipertimbangkan.
   
#### 5. Menghitung Kemiripan Antarfilm
   - **Cosine Similarity**:
     - Menghitung tingkat kemiripan antarfilm berdasarkan vektor fitur TF-IDF.
     - Hasilnya adalah matriks cosine similarity, di mana setiap elemen mewakili tingkat kemiripan antara dua film.
   
#### 6. Hasil Akhir
   - Matriks cosine similarity yang dihasilkan dapat digunakan untuk:
     - Menemukan film-film yang mirip dengan film tertentu.
     - Membuat rekomendasi film berdasarkan konten seperti genre, kata kunci, dan pemeran.
   
### Data Preparation untuk Collaborative-Based Filtering Dengan TruncatedSVD untuk Reduksi Data

#### 1. Pembersihan Data (Data Cleaning):
   - Langkah pertama adalah menghapus baris yang memiliki nilai kosong (NaN) pada kolom-kolom penting seperti userId, movieId, dan rating dalam dataset ratings_df.
   - Ini bertujuan untuk memastikan bahwa hanya data yang lengkap dan valid yang digunakan dalam proses selanjutnya.
   
#### 2. Penyelarasan Tipe Data (Data Type Consistency):
   - Setelah memastikan tidak ada data kosong, bagian mengonversi kolom userId dan movieId dalam ratings_df menjadi tipe data integer.
   - Ini memastikan bahwa data tersebut dapat diproses dengan benar dalam algoritma pemrosesan selanjutnya.
   
#### 3. Sinkronisasi ID di Dataset Film (movies_df):
   - bagian ini kemudian memastikan bahwa kolom id pada movies_df (dataset film) berisi data numerik yang valid.
   - Hal ini dilakukan dengan mengonversi kolom id menjadi numerik, menghapus baris yang memiliki nilai kosong pada kolom tersebut, dan memastikan bahwa tipe data ID film adalah integer.
   
#### 4. Pembuatan Matriks Sparse:
   - Selanjutnya, bagian membuat sebuah matriks sparse (csr_matrix) yang merepresentasikan rating yang diberikan oleh pengguna terhadap film. Matriks sparse ini hanya menyimpan nilai rating yang ada, sedangkan elemen-elemen lainnya (yang tidak diisi) disimpan secara efisien tanpa menggunakan ruang memori yang besar.
   - Selain itu, kode ini menyesuaikan indeks pengguna (userId) untuk dimulai dari 0, karena dalam Python indeks dimulai dari 0, sedangkan ID pengguna dalam dataset mungkin dimulai dari 1.
   
#### 5. Informasi Matriks yang Dihasilkan:
   - Setelah matriks sparse berhasil dibuat, bagian ini menampilkan informasi mengenai keberhasilan pembuatan matriks dan menunjukkan ukuran matriks tersebut, yang menggambarkan jumlah pengguna dan film yang ada.

### Data Preparation untuk Collaborative-Based Filtering Menggunakan Matrix Factorization SVD & Hybrid-Recomendation 
   - untuk Data Preparation pada **Model Collaborative-Based Filtering Menggunakan Matrix Factorization SVD** dan **Model Hybrid-Recomendation** menggunakan data preparation yang sudah di lakukan pada tahap sebelumnya.
   
---

## 5. Modeling

### Model Content-Based Filtering

#### 1. Content-Based Filtering

   **Content-Based Filtering** adalah metode dalam sistem rekomendasi yang menyarankan item berdasarkan **fitur konten** dari item tersebut. Dalam konteks film, fitur konten bisa berupa:
   - **Genre** film (misalnya: aksi, drama, komedi).
   - **Deskripsi** atau sinopsis film.
   - **Tag** atau label yang menggambarkan tema film (misalnya: horor, thriller).
   - **Pemeran** atau sutradara.
##### Prinsip Dasar: 
   - Content-Based Filtering berfokus pada kemiripan **fitur konten** antara item yang sudah dikenal oleh pengguna dan item lainnya dalam dataset.
   - **Jika pengguna menyukai suatu item**, mereka kemungkinan besar akan menyukai item lain yang memiliki kemiripan konten yang tinggi.
##### Proses Content-Based Filtering:
   1. **Penyusunan Fitur Item:** Setiap item (misalnya film) digambarkan dengan fitur-fitur numerik, seperti genre, tag, atau deskripsi.
   2. **Pengukuran Kemiripan:** Menggunakan metode matematis untuk mengukur kemiripan antara item yang satu dengan yang lain, umumnya dengan **cosine similarity**.
   3. **Rekomendasi:** Berdasarkan kemiripan ini, sistem akan merekomendasikan item yang paling mirip dengan item yang telah disukai atau dipilih oleh pengguna.
##### Kelebihan:
   - Tidak memerlukan data perilaku pengguna (misalnya klik atau rating).
   - Sistem rekomendasi lebih berbasis konten item itu sendiri.
##### Kekurangan:
   - **Masalah "cold start"**: Sulit memberikan rekomendasi untuk item yang baru karena mereka belum memiliki cukup informasi.
   - **Terbatas pada fitur yang ada**: Hanya fitur yang tersedia dalam dataset yang dapat digunakan untuk perbandingan.

#### 2. Cosine Similarity
   **Cosine Similarity** adalah metode matematis yang digunakan untuk mengukur kemiripan antara dua vektor dalam ruang berdimensi tinggi. Ini mengukur **seberapa dekat arah dua vektor**, tanpa memperhatikan panjang vektor tersebut.

##### Rumus Cosine Similarity:

  $$ \text{Cosine Similarity} = \frac{A \cdot B}{\|A\| \|B\|} $$
   - **A · B**: Produk titik (dot product) antara dua vektor A dan B.
   - **‖A‖** dan **‖B‖**: Norma (panjang) dari vektor A dan B.e
ktor A dan B.
##### Interpretasi Cosine Similarity:
   - **1**: Kedua vektor memiliki arah yang sama (sangat mirip).
   - **0**: Kedua vektor tidak memiliki arah yang sama (tidak mirip).
   - **-1**: Kedua vektor memiliki arah yang berlawanan (san
gat berbeda).
##### Penerapan dalam Sistem Rekomendasi:
   Setiap item (misalnya film) digambarkan oleh vektor fitur. Cosine similarity digunakan untuk mengukur seberapa mirip dua item berdasarkan vektor fitur mereka. Misalnya, dua film yang memiliki genre yang sama atau pemeran yang sama akan memiliki skor cosine similarity yang lebih tinggi, menunjukkan bahwa film tersebut mirip.

#### 3. Langkah-langkah Kerja Sistem
##### Langkah-langkah:
   1. **Input dari Pengguna:** Sistem menerima judul film yang diminta oleh pengguna.
   2. **Pencarian Film:** Sistem mencari film tersebut di dalam dataset berdasarkan **judul yang telah diubah menjadi huruf kecil** untuk mencocokkan tanpa memandang kapitalisasi huruf.
   3. **Validasi Cosine Similarity:** Sistem memastikan bahwa **matriks cosine similarity** sudah dihitung sebelumnya, yang berisi nilai kemiripan antara film satu dengan yang lain.
   4. **Penghitungan Kemiripan:** Sistem mencari skor kesamaan antara film yang diminta dan film lainnya dalam dataset menggunakan **cosine similarity**.
   5. **Rekomendasi:** Film yang memiliki skor kesamaan tertinggi akan direkomendasikan kepada pengguna.
   
#### 4. Kelebihan dan Kekurangan Content-Based Filtering
##### Kelebihan:
   - **Tidak bergantung pada data pengguna:** Hanya membutuhkan data konten item itu sendiri.
   - **Rekomendasi yang personal:** Dapat memberikan rekomendasi yang relevan berdasarkan kesamaan konten.
##### Kekurangan:
   - **Masalah "cold start":** Film baru yang tidak memiliki cukup informasi untuk dibandingkan akan sulit untuk direkomendasikan.
   - **Terbatas pada fitur yang ada:** Sistem hanya dapat merekomendasikan item berdasarkan fitur yang tersedia dalam dataset, jadi jika fitur yang digunakan tidak lengkap, rekomendasi juga bisa terbatas.

#### 5. Ringkasan:
   1. **Representasi Item:** Setiap item diwakili oleh vektor fitur.
   2. **Pengukuran Kemiripan:** Cosine similarity digunakan untuk mengukur kemiripan antara item berdasarkan vektor fitur.
   3. **Rekomendasi:** Item yang paling mirip dengan item yang sudah disukai oleh pengguna akan direkomendasikan.
   Content-Based Filtering menggunakan **cosine similarity** untuk mengukur kedekatan antara item berdasarkan konten mereka, dan memberikan rekomendasi berdasarkan Filtering.

---


### Model Collaborative Filtering Dengan TruncatedSVD

#### 1. Collaborative Filtering (CF)
   - **Collaborative Filtering** adalah teknik rekomendasi yang mengandalkan interaksi pengguna dengan item (misalnya film). Pendekatan ini tidak memerlukan informasi eksplisit mengenai item atau pengguna (seperti deskripsi film atau data demografis pengguna). Sebaliknya, sistem rekomendasi hanya menggunakan data interaksi atau **rating** antara pengguna dan item (film)
   - Ada dua pendekatan utama dalam Collaborative Filtering:
##### A. User-Based Collaborative Filtering:
   - **Teori**: Mengidentifikasi pengguna yang mirip satu sama lain berdasarkan pola interaksi atau rating mereka terhadap item (film). Misalnya, jika pengguna A dan pengguna B memberikan rating tinggi pada banyak film yang sama, maka mereka dianggap mirip. Oleh karena itu, film yang disukai oleh A tetapi belum dilihat oleh B bisa direkomendasikan untuk B.
   - **Masalah**: Pendekatan ini menjadi kurang efisien dan lebih sulit diimplementasikan ketika jumlah pengguna sangat besar.
##### B. Item-Based Collaborative Filtering:
   - **Teori**: Berfokus pada hubungan antara item. Pendekatan ini mencoba menemukan film yang mirip dengan film yang telah dinilai oleh pengguna. Jika pengguna A menyukai film X, dan film Y sangat mirip dengan film X berdasarkan rating pengguna lain, maka film Y dapat direkomendasikan kepada A.
   - **Keunggulan**: Item-based filtering lebih stabil dan lebih efisien dalam menangani jumlah pengguna yang sangat besar dibandingkan dengan user-based filtering.
   
   Pada proyek ini, pendekatan yang digunakan adalah **Item-Based Collaborative Filtering**, di mana kita menghitung **kesamaan antar item (film)** dan memberikan rekomendasi film berdasarkan kesamaan tersebut.
   
#### 2. Singular Value Decomposition (SVD) dan Truncated SVD
   **Singular Value Decomposition (SVD)** adalah teknik matematis untuk **faktorasi matriks**, yang digunakan untuk mengurangi dimensi data dan memproyeksikan data ke ruang vektor yang lebih rendah namun tetap menjaga sebanyak mungkin informasi penting. SVD memiliki banyak aplikasi, termasuk di bidang **rekomendasi**.
##### A. **SVD: Proses Dasar**
   SVD memfaktorkan matriks **m x n** menjadi tiga matriks:
$$
A = U \Sigma V^T
$$
   - **A**: Matriks asli, misalnya matriks rating pengguna terhadap film (dimensi: m x n, dengan m adalah jumlah pengguna dan n adalah jumlah film).
   - **U**: Matriks pengguna (dimensi m x m).
   - **Σ (Sigma)**: Matriks diagonal yang berisi nilai singular (dimensi m x n).
   - **V^T**: Matriks film (dimensi n x n, tetapi kita ambil transpose-nya agar bisa mengalikan dengan U dan Σ).
   Tujuan dari SVD adalah untuk menemukan struktur atau pola tersembunyi dalam data melalui proyeksi matriks menjadi beberapa komponen (faktor). Dalam konteks rekomendasi film:
   - **U** berisi representasi pengguna dalam ruang fitur yang lebih rendah.
   - **Σ** berisi informasi tentang seberapa penting masing-masing komponen dalam menjelaskan variansi data.
   - **V^T** berisi representasi film dalam ruang fitur yang lebih rendah.
##### B. **Truncated SVD**
   - **Teori**: Pada **Truncated SVD**, kita hanya mempertahankan sejumlah komponen singular terbesar dan mengabaikan sisanya. Ini mengurangi dimensi matriks tanpa kehilangan terlalu banyak informasi yang penting.
   - **Mengapa Truncated SVD?**
     - Matriks rating pengguna terhadap film sangat besar dan **sparse** (banyak nilai yang hilang atau kosong), yang membuat perhitungan menjadi sangat mahal.
     - Dengan **Truncated SVD**, kita dapat mengurangi dimensi data ke jumlah komponen tertentu, misalnya 50, dan masih mempertahankan sebagian besar informasi penting, yang membantu **mengurangi noise** dan **overfitting**.
   - **Truncated SVD** memberikan representasi yang lebih kompak dan lebih mudah dihitung dari data rating yang besar.
   
#### 3. Cosine Similarity untuk Mengukur Kesamaan Antar Item
   Setelah kita melakukan **reduksi dimensi** menggunakan Truncated SVD, kita dapat menghitung **kesamaan antar item (film)**. Salah satu cara yang umum digunakan untuk mengukur kesamaan antar vektor adalah dengan menggunakan **cosine similarity**.

##### a. Cosine Similarity:
   - Cosine similarity mengukur sudut antara dua vektor dalam ruang fitur. Jika dua vektor memiliki sudut kecil antara mereka, berarti mereka sangat mirip. Formula cosine similarity adalah:

   $$ \text{Cosine Similarity} = \frac{A \cdot B}{\|A\| \|B\|} $$
   - **A · B**: Produk titik (dot product) antara dua vektor A dan B.
   - **‖A‖** dan **‖B‖**: Norma (panjang) dari vektor A dan B.
   
   - Jikdua vektor memiliki nilai cosine similarity yang tinggi (mendekati 1), maka item-item yang mereka wakili sangat mirip. Dalam konteks ini, kita menghitung kesamaan antar film berdasarkan vektor fitur mereka yang diperoleh dari SVD.
   
##### b. Perhitungan Kesamaan Antara Film:
   Setelah matriks rating pengguna diubah menjadi ruang fitur yang lebih rendah melalui Truncated SVD, kita dapat menghitung kesamaan antara film-film tersebut dalam ruang tersebut, menggunakan **cosine similarity** pada matriks hasil SVD yang telah dikurangi dimensinya.

#### 4. Rekomendasi Berdasarkan Kesamaan
   Setelah kita mendapatkan matriks kesamaan antar item (film), kita dapat membuat rekomendasi dengan cara berikut:
   - Ambil rating pengguna di ruang yang sudah direduksi dimensinya (hasil dari SVD).
   - Hitung skor bobot untuk film yang belum dinilai oleh pengguna berdasarkan kesamaan film yang sudah dinilai oleh pengguna. Skor ini dihitung dengan mengalikan vektor kesamaan film dengan vektor rating pengguna.
   Kecualikan film yang sudah dinilai oleh pengguna dari daftar rekomendasi dengan memberi skor negatif pada film-film tersebut.
   - Ambil rekomendasi teratas dengan memilih film yang memiliki skor tertinggi yang belum dinilai oleh pengguna.

#### 5. Ringkasan Cara Kerja
   1. Reduksi Dimensi dengan Truncated SVD: Mengurangi dimensi matriks rating untuk menyederhanakan data dan menangkap struktur utama dalam data.
   2. Penghitungan Kesamaan Item dengan Cosine Similarity: Mengukur kesamaan antar film berdasarkan proyeksi dalam ruang fitur yang lebih rendah.
   3. Rekomendasi Film: Berdasarkan kesamaan antar film, menghitung skor untuk film yang belum dinilai oleh pengguna, kemudian memberikan rekomendasi teratas.

#### Kesimpulan
   - Collaborative Filtering adalah metode yang efektif untuk memberikan rekomendasi berdasarkan interaksi pengguna dengan item.
   - Truncated SVD digunakan untuk mereduksi dimensi data rating yang besar dan jarang, menyederhanakan perhitungan dan meningkatkan efisiensi.
   - Cosine Similarity digunakan untuk mengukur kesamaan antar film, yang memungkinkan kita memberikan rekomendasi yang relevan berdasarkan film yang sudah dinilai oleh pengguna.
   - Dengan pendekatan ini, sistem rekomendasi dapat memberikan saran film kepada pengguna tanpa perlu memahami konten film atau informasi pribadi pengguna, hanya berdasarkan data interaksi (rating).

### Model Matrix Factorization SVD

#### 1. Matriks Rating
Misalkan kita memiliki dataset berupa matriks yang menggambarkan interaksi antara pengguna (user) dan item (film), seperti contoh di bawah ini:

| User/Film | Film 1 | Film 2 | Film 3 | Film 4 |
|-----------|--------|--------|--------|--------|
| User 1    | 5      | ?      | 3      | ?      |
| User 2    | 4      | 4      | ?      | 2      |
| User 3    | ?      | 2      | 4      | 5      |
| User 4    | 2      | 3      | ?      | 4      |

Tanda `?` menunjukkan rating yang hilang atau belum ada. Tujuan utama dari model rekomendasi adalah **memprediksi rating yang hilang** ini (misalnya rating untuk `User 1` pada `Film 2`).

#### 2. Matrix Factorization (MF)
**Matrix factorization** adalah teknik untuk mengurangi dimensi matriks besar yang sangat jarang (sparse) seperti matriks rating di atas. Tujuannya adalah untuk mengungkapkan struktur tersembunyi dalam data tersebut dengan cara memfaktorkan matriks tersebut menjadi dua matriks yang lebih kecil, sehingga memungkinkan kita untuk memprediksi nilai yang hilang (rating yang belum diberikan).

Misalnya, kita ingin memfaktorkan matriks rating `R` menjadi dua matriks: **matriks pengguna (user matrix)** dan **matriks item (item matrix)**.

$$ R \approx U \times V^T $$

- **U** adalah matriks **pengguna** berukuran `n x k`, di mana `n` adalah jumlah pengguna dan `k` adalah jumlah faktor laten yang menggambarkan preferensi pengguna.
- **V** adalah matriks **item** berukuran `m x k`, di mana `m` adalah jumlah item (film) dan `k` adalah jumlah faktor laten yang menggambarkan karakteristik item.

#### 3. Singular Value Decomposition (SVD)
SVD adalah salah satu teknik yang paling umum digunakan dalam matrix factorization. Dalam SVD, matriks rating `R` dekomposisi menjadi tiga matriks:

$$ R = U \Sigma V^T $$

- **U** adalah matriks **pengguna** yang berukuran `n x k` (dimana `n` adalah jumlah pengguna dan `k` adalah jumlah faktor laten).
- **Σ (Sigma)** adalah matriks diagonal yang berisi **nilai singular**, yang merupakan faktor-faktor penting dalam data dan memiliki ukuran `k x k`.
- **V^T** adalah matriks **item** yang berukuran `m x k` (dimana `m` adalah jumlah item).

Proses ini menghasilkan representasi yang lebih kecil dari data asli tetapi tetap mempertahankan informasi yang penting.

##### Tujuan dari SVD:
- Mengurangi dimensi data (menjadi matriks yang lebih kecil).
- Mengungkapkan hubungan tersembunyi (faktor laten) antara pengguna dan item.
- Membantu memprediksi rating yang hilang dengan cara mengalikan matriks **U** dan **V^T**.

#### 5. Langkah-langkah Kerja SVD dalam Rekomendasi
Secara rinci, berikut langkah-langkah cara kerja SVD dalam rekomendasi film:

1. **Memulai dengan Matriks Rating**:
   Misalkan kita memiliki matriks rating yang besar dan sebagian besar nilai di dalamnya adalah kosong (rating yang hilang).

2. **Faktorasi Matriks**:
   SVD memecah matriks rating `R` menjadi dua matriks yang lebih kecil (U dan V). Matriks **U** mewakili profil preferensi pengguna, dan matriks **V** mewakili karakteristik atau fitur-fitur dari film.

3. **Pembelajaran Faktor Laten**:
   Model ini mempelajari hubungan yang ada dalam data dengan cara memperkirakan faktor laten yang ada di dalam matriks **U** dan **V**. Faktor laten ini menggambarkan karakteristik tersembunyi seperti genre film, preferensi pengguna, dll.

4. **Pemodelan Prediksi**:
   Setelah faktor laten ditemukan, kita dapat memprediksi rating yang hilang di matriks `R` dengan cara mengalikan matriks **U** dan **V^T**. Prediksi rating untuk suatu pengguna dan item dapat dihitung dengan rumus:

   $$ \hat{r}_{ui} = U_u \cdot V_i^T $$
   
   Di mana:
   - **u** adalah pengguna,
   - **i** adalah item (film),
   - **U_u** adalah vektor pengguna ke-`u` pada matriks **U**,
   - **V_i** adalah vektor item ke-`i` pada matriks **V**.

6. **Rekomendasi**:
   Setelah model dilatih, kita bisa memprediksi rating untuk semua film yang belum ditonton oleh pengguna. Film yang memiliki rating prediksi tertinggi kemudian direkomendasikan kepada pengguna.

#### 6. Mengoptimalkan Model SVD
Untuk menghasilkan model yang lebih baik, kita perlu mengoptimalkan beberapa parameter, seperti:
- **Jumlah faktor laten (`n_factors`)**: Menentukan jumlah fitur tersembunyi yang digunakan untuk menggambarkan hubungan antara pengguna dan item. Jumlah yang terlalu sedikit bisa menyebabkan model underfitting, sedangkan terlalu banyak bisa menyebabkan overfitting.
- **Regularisasi (`biased=True`)**: Untuk menghindari overfitting, kita menggunakan regularisasi pada model, yang mengurangi bobot yang terlalu besar pada faktor laten tertentu.
- **Cross-validation**: Seperti dalam kode, kita menggunakan cross-validation untuk mengevaluasi kinerja model menggunakan metrik seperti RMSE (Root Mean Squared Error), yang mengukur seberapa baik model memprediksi rating yang sebenarnya.

#### 7. Keuntungan dan Kekurangan SVD
##### Keuntungan:
- **Efisiensi**: SVD dapat menangani dataset besar dengan baik, karena mengurangi dimensi data.
- **Akurasi**: Dapat menghasilkan prediksi yang cukup akurat, terutama dalam konteks data sparseness.
- **Generalisasi**: Dengan menggunakan faktor laten, SVD mampu menangkap hubungan yang lebih kompleks dalam data.
##### Kekurangan:
- **Skalabilitas**: Untuk dataset yang sangat besar, proses dekomposisi matriks SVD bisa menjadi sangat mahal secara komputasional.
- **Kebutuhan Data yang Cukup**: Model SVD membutuhkan data yang cukup banyak untuk bisa menangkap pola yang valid. Jika data terlalu sedikit atau tidak merata, hasilnya mungkin tidak optimal.

#### 8. Kesimpulan
SVD adalah teknik powerful dalam sistem rekomendasi yang berfokus pada **matrix factorization** untuk memprediksi rating yang hilang. Dengan mengidentifikasi **faktor laten** yang menghubungkan pengguna dan item, SVD dapat memberikan rekomendasi yang relevan berdasarkan pola tersembunyi dalam data. Teknik ini sangat efektif untuk menangani data sparsity dan dapat digunakan pada skala besar dengan optimasi yang tepat.ngani data sparsity dan dapat digunakan pada skala besar dengan optimasi yang tepat.




---

### Model Hybrid-Recomendation

### Penjelasan Teoretis
Hybrid Recommender System menggabungkan pendekatan **Content-Based Filtering** dan **Collaborative Filtering** untuk memberikan rekomendasi yang lebih akurat dengan mengatasi kelemahan masing-masing metode.

### 1. Content-Based Filtering

#### **Teori Dasar**
Content-Based Filtering memberikan rekomendasi berdasarkan kesamaan antara item. Fokusnya adalah menganalisis atribut atau fitur dari item untuk menemukan item yang mirip dengan apa yang disukai pengguna.

#### **Langkah Kerja:**
1. **Representasi Data:**
   - Setiap film direpresentasikan dalam bentuk vektor fitur, seperti:
     - Genre: Action, Comedy, Drama.
     - Sutradara: Christopher Nolan, Steven Spielberg.
     - Pemeran utama, deskripsi, dll.
   - Teknik umum:
     - **TF-IDF (Term Frequency-Inverse Document Frequency)**.
     - **Word Embedding**.

2. **Menghitung Kemiripan:**
   - Menggunakan metrik seperti **Cosine Similarity** untuk menghitung kemiripan antara dua film:
     $$
     \text{Similarity}(A, B) = \frac{A \cdot B}{\|A\| \|B\|}
     $$
     - \(A\) dan \(B\) adalah vektor fitur dari dua film.

3. **Rekomendasi:**
   - Film yang paling mirip dengan film acuan diberikan sebagai rekomendasi.

#### **Kelebihan dan Kekurangan**
- **Kelebihan:**
  - Tidak bergantung pada data pengguna lain.
  - Mudah untuk dijelaskan: *"Film ini direkomendasikan karena mirip dengan X."*
- **Kekurangan:**
  - **Cold Start Problem**: Tidak bisa merekomendasikan film tanpa informasi fitur.
  - Hanya memberikan rekomendasi item yang mirip, tidak mengeksplorasi item baru.

### 2. Collaborative Filtering

#### **Teori Dasar**
Collaborative Filtering memberikan rekomendasi berdasarkan kesamaan pola perilaku pengguna. Fokusnya bukan pada item, melainkan pada pengguna yang memiliki preferensi serupa.

#### **Pendekatan:**
1. **User-Based Collaborative Filtering:**
   - Mencari pengguna lain dengan pola preferensi serupa.
   - Rekomendasi diambil dari item yang disukai pengguna serupa.

2. **Item-Based Collaborative Filtering:**
   - Mencari item yang sering dinilai mirip oleh pengguna.
   - Film yang sering ditonton bersama film lain menjadi rekomendasi.

#### **Representasi Data:**
- Data direpresentasikan dalam bentuk matriks pengguna-item:
  - Baris: Pengguna.
  - Kolom: Film.
  - Nilai: Skor atau rating yang diberikan pengguna.

#### **Masalah Umum:**
- **Sparsity:** Kebanyakan pengguna hanya menonton sedikit film, sehingga matriks pengguna-item menjadi jarang terisi.
- **Cold Start Problem:** Pengguna baru atau film baru tanpa data tidak dapat direkomendasikan.

### 3. Collaborative Filtering dengan SVD

#### **Teori Dasar**
Untuk mengatasi masalah sparsity, digunakan teknik **SVD (Singular Value Decomposition)** untuk mendekomposisi matriks pengguna-item.

$$
R \approx U \Sigma V^T
$$
- \(R\): Matriks pengguna-item (rating asli).
- \(U\): Matriks pengguna-latent (preferensi pengguna).
- \(\Sigma\): Matriks diagonal (representasi kepentingan fitur).
- \(V^T\): Matriks item-latent (karakteristik item).
#### **Langkah Kerja:**
1. Matriks \(R\) didekomposisi menggunakan algoritma SVD.
2. Nilai prediksi dihitung kembali dengan mengalikan matriks yang didekomposisi.
3. Film dengan skor tertinggi direkomendasikan kepada pengguna.
#### **Kelebihan:**
- Mengatasi masalah sparsity.
- Bisa merekomendasikan item baru yang tidak terkait langsung dengan preferensi awal pengguna.


### 4. Hybrid Filtering

#### **Teori Dasar**
Hybrid Filtering menggabungkan kelebihan dari Content-Based dan Collaborative Filtering untuk mengurangi kekurangan masing-masing metode.

#### **Mengapa Menggabungkan?**
- **Cold Start Problem:** Collaborative Filtering tidak bekerja baik dengan item baru, tetapi Content-Based bisa memberikan rekomendasi berdasarkan fitur.
- **Exploration vs Exploitation:** Content-Based cenderung eksploitasi (mencari yang mirip), sedangkan Collaborative Filtering lebih eksplorasi (menemukan item baru).

#### **Strategi Penggabungan:**
1. **Linear Combination:**
   - Skor dari dua metode digabungkan dengan bobot tertentu:
     $$
     \text{Final Score} = (\text{Content-Based Score} \times \text{Weight}) + (\text{Collaborative-Based Score} \times (1 - \text{Weight}))
     $$
2. **Switching:**
   - Menggunakan Content-Based untuk pengguna baru atau item baru, dan Collaborative Filtering untuk pengguna/item dengan banyak data.
3. **Blending:**
   - Menggunakan algoritma machine learning untuk memprediksi skor berdasarkan fitur dari kedua metode.

### 5. Kesimpulan Teoretis
- **Content-Based Filtering:** Melihat fitur internal item.
- **Collaborative Filtering:** Melihat pola eksternal pengguna.
- **Hybrid Filtering:** Menggabungkan keduanya untuk memberikan rekomendasi yang lebih akurat dan komprehensif.

--- lebih akurat dan komprehensif.

---

Apakah Anda ingin penjelasan dengan contoh data atau implementasi lebih rinci?


---

## 6. Evaluation

### Hasil Evaluasi Content-Based Filtering

#### 1. Daftar Rekomendasi
Model rekomendasi berbasis konten menghasilkan daftar film yang mirip dengan **"The Dark Knight"**. Daftar rekomendasi berikut menunjukkan hasil yang diberikan oleh model:
- **The Dark Knight Rises**: Sekuel langsung dari *The Dark Knight*.
- **Batman Begins**: Film pertama dalam trilogi *The Dark Knight*.
- **Batman Returns**, **Batman Forever**, dan **Batman & Robin**: Film lain dalam franchise Batman.
- **Batman v Superman: Dawn of Justice**: Memiliki karakter Batman sebagai tokoh utama.
- **The Lego Movie**: Meskipun berbeda konteks (animasi), karakter Batman muncul di film ini.
- Film lainnya (seperti **Superman** dan **Slow Burn**) kemungkinan memiliki elemen kemiripan tertentu, seperti genre atau tema.

Fitur yang digunakan untuk menilai kemiripan bisa berupa:
- **Deskripsi film**: Sinopsis, plot.
- **Meta-data**: Genre, sutradara, aktor, dll.
- **Representasi vektor**: Misalnya, embedding teks dari deskripsi film.

#### 2. Evaluasi dan Skor
Hasil evaluasi model adalah sebagai berikut:
##### **MAP (Mean Average Precision) Score**
- **MAP: 0.8008** 
  - Mengukur rata-rata presisi di berbagai posisi item relevan dalam daftar rekomendasi.
  - Skor **0.8008** menunjukkan bahwa 80.08% rekomendasi berada pada posisi relevan, menandakan model berkinerja sangat baik.
##### **Precision**
- **Precision: 0.5000**
  - Mengukur proporsi item relevan dari keseluruhan rekomendasi yang diberikan.
  - Skor **0.5000** berarti 50% dari rekomendasi adalah relevan, sementara sisanya kurang relevan.
##### **Recall**
- **Recall: 1.0000**
  - Mengukur sejauh mana model menemukan semua item relevan dalam dataset.
  - Skor sempurna **1.0000** berarti semua item relevan berhasil ditemukan.
##### **NDCG (Normalized Discounted Cumulative Gain)**
- **NDCG: 1.0000**
  - Mengukur kualitas urutan rekomendasi dengan memberikan bobot lebih besar pada item relevan yang berada di posisi atas.
  - Skor sempurna **1.0000** menunjukkan bahwa urutan item relevan sangat optimal.

#### 3. Interpretasi Hasil
- **Keunggulan model**:
  - Rekomendasi yang diberikan sangat relevan dan urutannya sesuai dengan preferensi pengguna (*NDCG* sempurna).
  - Semua item relevan berhasil ditemukan (Recall sempurna).
- **Kekurangan model**:
  - Precision hanya 50%, menunjukkan bahwa separuh rekomendasi tidak relevan. Masih ada ruang untuk perbaikan dalam mengurangi item tidak relevan.

#### 4. Teori di Balik Evaluasi

##### **Content-Based Filtering**
- Metode ini merekomendasikan item berdasarkan kemiripan fitur antara item dalam dataset. 
- Contoh fitur:
  - **Metadata**: Genre, sutradara, aktor, dll.
  - **Vektor embedding**: Representasi fitur tekstual menggunakan model seperti TF-IDF atau embedding neural network.

##### **Metode Evaluasi**
1. **MAP (Mean Average Precision)**:
   - Mengukur rata-rata presisi di berbagai posisi item relevan dalam rekomendasi.
   - Formula:
     $$
     \text{MAP} = \frac{1}{N} \sum_{i=1}^{N} \text{AP}(i)
     $$
     Di mana **AP(i)** adalah rata-rata presisi untuk setiap kueri rekomendasi.

2. **Precision**:
   - Mengukur proporsi item relevan dalam rekomendasi:
     $$
     \text{Precision} = \frac{\text{Item Relevan dalam Top-N}}{\text{Jumlah Item dalam Top-N}}
     $$

3. **Recall**:
   - Mengukur kemampuan model menemukan semua item relevan:
     $$
     \text{Recall} = \frac{\text{Item Relevan dalam Top-N}}{\text{Total Item Relevan di Dataset}}
     $$

4. **NDCG (Normalized Discounted Cumulative Gain)**:
   - Mengukur kualitas urutan rekomendasi:
     $$
     \text{NDCG} = \frac{\text{DCG}}{\text{IDCG}}, \quad \text{DCG} = \sum_{i=1}^{N} \frac{\text{Relevansi}_i}{\log_2(i + 1)}
     $$

## 5. Kesimpulan
Model rekomendasi ini menunjukkan performa tinggi berdasarkan:
- **MAP tinggi (0.8008)**.
- **Recall dan NDCG sempurna (1.0000)**.

Namun, precision yang hanya **0.5000** mengindikasikan perlunya perbaikan untuk mengurangi jumlah item tidak relevan dalam daftar rekomendasi.
VD
### Hasil Evaluasi Collaborative-Based Filtering Menggunakan SVD
### Hasil Evaluasi Hybrid-Recomendation

---

### Hasil Evaluasi Collaborative-Based Filtering dengan TruncatedSVD
up##a.

---

## **Hasil Rekomendasi**

Sistem merekomendasikan lima film untuk **user 7**, dengan prediksi rating sebagai berikut:

| **Film**                                   | **Prediksi Rating** |
|--------------------------------------------|---------------------|
| **Metropolis**                             | **2.42**            |
| **Dancer in the Dark**                     | **2.40**            |
| **Jarhead**                                | 1.68                |
| **Forrest Gump**                           | 1.52                |
| **Pirates of the Caribbean: The## Curse...** | 1.44                |

### **Interpretasi:**
- **Metropolis** dan **Dancer in the Dark** mendapatkan prediksi tertinggi, sehingga dianggap paling relevan.
- Skor prediksi keseluruhan cukup rendah (di bawah 3), yang mungkin disebabkan oleh:
  - **Keterbatasan data pengguna**.
  - **Algoritme yang kurang op**## dalam memprediksi prefer##ensi user 7.

---

## **Evaluasi Akurasi**

### **Metrik Evaluasi**
1. **Mean Absolute Error (MAE): 1.891**
   - Mengukur rata-rata kesalahan absolu$$antara prediksi dan nilai aktual.
   - Rumus:
     \[
     MA$$= \frac{1}{n} \sum_{i=1}^{n} | \hat{r}_i - r_i |
     \]

2. **Root Mean Squared Error (RMSE): 1.940**
   - Mengukur akar rata-rata kesalahan kuadrat$$lebih sensitif terhadap kesalahan besar.
   - Rumus:
     \[
     RMSE$$ \s##qrt{\frac{1}{n} \sum_{i=1}^{n} (\hat{r}_i - r_i)^2 }
     \]

### **Interpretasi Hasil Evaluasi**
- **MAE = 1.891:** Rata-rata kesalahan prediksi adalah **1.89 poin** dari nilai aktual.
- **RMSE = 1.940:** Nilai ini menunjukkan adanya kesalahan besar pada beberapa prediksi.

Idealnya, MAE dan RMSE harus mendekati 0 untuk menunjukkan ak t##inggi. Hasil ini menunjukkan bahwa sistem masih kurang akurat.

---

## **Kesimpulan**
1. **Rekomendasi:**
   - Sistem memberikan rekomendasi, tetapi skor prediksi menunjukkan bahwa model perlu ditingkatkan.
2. **Evaluasi:**
   - Kesalahanp ##tinggi, mengindikasikan predikningkatkan pola prediksi.
   - Normalisasi data untuk mengurangi bias skala rating.

2. **Peningkatan Algoritme:**
   - Gunakan metode seperti **Matrix Factorization** (contohnya, SVD).
   - Tera**
   - Sesuaikan parameter seperti jumlah tetangga (neighbors) atau tingkat regularis.

Dengan langkah ini, sistem dapat memberikan rekomendasi yang lebih relevan dan akurat. 😊


### Hasil Evaluasi Collaborative-Based Filtering Menggunakan SVD

# Penjelasan Hasil Rekomendasi SVD untuk User 7

Hasil rekomendasi menggunakan **SVD** (Singular Value Decomposition) untuk **user 7** berisi daftar film dengan prediksi rating untuk setiap film tersebut. SVD adalah teknik dalam **Collaborative Filtering** yang digunakan untuk menghasilkan rekomendasi berdasarkan matriks pengguna dan item.

## Hasil Rekomendasi untuk User 7

Berikut adalah daftar film yang direkomendasikan kepada user 7, beserta rating yang diprediksi:

1. **Saw II** - Predicted Rating: 4.3047  
2. **Terminator Salvation** - Predicted Rating: 4.2515  
3. **Dawn of the Dead** - Predicted Rating: 4.2279  
4. **Terminator 3: Rise of the Machines** - Predicted Rating: 4.1552  
5. **Gremlins 2: The New Batch** - Predicted Rating: 4.0977  
6. **Rebecca** - Predicted Rating: 4.0780  
7. **Ghost Rider** - Predicted Rating: 4.0703  
8. **Scarface** - Predicted Rating: 4.0509  
9. **Stranger Than Fiction** - Predicted Rating: 4.0484  
10. **Pandora's Box** - Predicted Rating: 3.9745  

## Evaluasi Model

Untuk mengevaluasi akurasi model rekomendasi, dua metrik evaluasi yang umum digunakan adalah **RMSE** dan **MAE**.

### 1. RMSE (Root Mean Squared Error)

- **Nilai RMSE** untuk model ini adalah **0.7131**.
- RMSE mengukur seberapa besar perbedaan antara nilai prediksi dan nilai sebenarnya. Nilai yang lebih rendah menunjukkan model yang lebih akurat.
- Formula RMSE:
  $$
  RMSE = \sqrt{\frac{1}{N} \sum_{i=1}^N (r_i - \hat{r_i})^2}
  $$
  Di mana $$ r_i $$ adalah rating sebenarnya dan $$ \hat{r_i} $$ adalah rating yang diprediksi.
  
- **Interpretasi**: Nilai RMSE sebesar 0.7131 menunjukkan bahwa perbedaan antara prediksi dan nilai sebenarnya relatif kecil, yang berarti model memberikan rekomendasi yang cukup akurat.

### 2. MAE (Mean Absolute Error)

- **Nilai MAE** untuk model ini adalah **0.5471**.
- MAE mengukur rata-rata perbedaan absolut antara nilai yang diprediksi dan nilai yang sebenarnya. Semakin kecil nilai MAE, semakin baik model dalam memberikan prediksi yang mendekati nilai sebenarnya.
- Formula MAE:
  $$
  MAE = \frac{1}{N} \sum_{i=1}^N |r_i - \hat{r_i}|
  $$
  Di mana $$ r_i $$ adalah rating sebenarnya dan $$ \hat{r_i} $$ adalah rating yang diprediksi.
  
- **Interpretasi**: Nilai MAE sebesar **0.5471** berarti rata-rata perbedaan absolut antara rating yang diprediksi dan rating yang sebenarnya adalah sekitar **0.55**. Ini menunjukkan bahwa model cukup baik dalam memprediksi rating yang sesuai dengan preferensi pengguna.

## Kesimpulan

Berdasarkan hasil evaluasi, **model SVD memberikan prediksi yang cukup akurat dengan RMSE sekitar 0.71 dan MAE sekitar 0.55.** Metrik ini menunjukkan bahwa model berhasil memprediksi rating yang cukup dekat dengan rating yang sebenarnya.

### Teori Evaluasi:

- **RMSE** lebih sensitif terhadap kesalahan besar (outlier), karena mengkuadratkan perbedaan antara nilai prediksi dan nilai nyata.
- **MAE** lebih sederhana dan memberikan gambaran yang lebih umum tentang seberapa jauh prediksi dari nilai nyata tanpa memberikan bobot lebih pada kesalahan yang besar.


### Hasil Evaluasi Hybrid-Recomendation

Hasil evaluasi model rekomendasi untuk pengguna yang terinspirasi dari **The Dark Knight** menunjukkan metrik berikut:

- **Precision: 0.3**
- **Recall: 0.6**
- **F1 Score: 0.4**

### 1. **Precision (0.3)**
Precision mengukur seberapa banyak item yang direkomendasikan benar-benar relevan dengan preferensi pengguna. Dengan nilai precision sebesar 0.3, ini berarti hanya 30% dari film yang direkomendasikan kepada pengguna yang relevan atau sesuai dengan preferensi mereka. **Precision yang rendah** ini menunjukkan bahwa model sering kali merekomendasikan film yang tidak sesuai dengan selera pengguna.

### 2. **Recall (0.6)**
Recall mengukur seberapa banyak item relevan yang berhasil direkomendasikan dari semua item relevan yang ada. Nilai recall sebesar 0.6 menunjukkan bahwa model mampu menemukan 60% dari film-film yang relevan atau sesuai dengan preferensi pengguna yang seharusnya direkomendasikan. **Recall yang lebih tinggi** ini mengindikasikan bahwa meskipun model memberikan beberapa rekomendasi yang tidak relevan, ia masih berhasil menemukan banyak film relevan untuk pengguna.

### 3. **F1 Score (0.4)**
F1 score adalah kombinasi antara precision dan recall yang digunakan untuk mengukur keseimbangan antara keduanya. Nilai F1 score dihitung dengan rumus:

$$
\text{F1} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
$$

Dengan precision 0.3 dan recall 0.6, nilai F1 score yang dihasilkan adalah 0.4. **F1 score yang lebih rendah** ini menunjukkan bahwa meskipun recall cukup baik, precision yang rendah menarik turun kinerja model secara keseluruhan. 

### Teori Evaluasi:

- **Precision** berfokus pada kualitas rekomendasi: apakah film yang diberikan sesuai dengan preferensi pengguna atau tidak. Precision yang tinggi berarti lebih sedikit rekomendasi yang salah.
  
- **Recall** berfokus pada kuantitas rekomendasi yang relevan: apakah model berhasil menemukan sebagian besar film relevan yang seharusnya direkomendasikan.

- **F1 Score** memberikan gambaran yang lebih seimbang antara precision dan recall, memastikan bahwa model tidak hanya mencari relevansi tetapi juga tidak terlalu banyak memberikan rekomendasi yang tidak relevan.

### Kesimpulan:
Secara keseluruhan, hasil evaluasi ini menunjukkan bahwa meskipun model ini berhasil menemukan beberapa rekomendasi relevan (recall tinggi), ia juga menghasilkan banyak rekomendasi yang tidak sesuai dengan preferensi pengguna (precision rendah), yang menyebabkan F1 score yang tidak terlalu baik.



--- yang tidak terlalu baik.



---

### Hasil Evaluasi Model Menggunakan Item-Similarity

1. **RMSE (Root Mean Squared Error)**:
   - Nilai RMSE: **3.4893**
   - RMSE mengukur rata-rata kesalahan antara nilai yang diprediksi oleh model dan nilai sebenarnya, dengan memberi bobot lebih pada kesalahan yang lebih besar. Semakin kecil nilai RMSE, semakin baik kinerja model dalam hal prediksi.
   - Nilai RMSE yang lebih tinggi menunjukkan bahwa model memiliki kesalahan prediksi yang lebih besar, sedangkan nilai yang lebih rendah berarti model lebih akurat.

2. **MAE (Mean Absolute Error)**:
   - Nilai MAE: **3.3166**
   - MAE mengukur rata-rata kesalahan absolut antara nilai yang diprediksi dan nilai sebenarnya tanpa memberi bobot tambahan pada kesalahan besar. Ini memberikan gambaran umum tentang seberapa besar kesalahan prediksi rata-rata.
   - MAE lebih mudah diinterpretasikan dibandingkan RMSE karena tidak ada penalti untuk kesalahan besar.

#### Kesimpulan:
Kedua metrik ini menunjukkan seberapa baik model dalam memprediksi hasil berdasarkan data pelatihan. Nilai RMSE dan MAE yang lebih rendah menunjukkan model yang lebih baik, namun nilai ini harus dibandingkan dengan baseline atau model lain untuk penilaian yang lebih akurat.

### Optimasi Bobot Evaluasi Model

#### 1. Optimized Weights
   - **content_weight**: 0.1
   - **collab_weight**: 0.9
   
   Bobot ini menunjukkan prioritas antara dua aspek dalam model. Dalam hal ini, **collab_weight** lebih dominan dengan bobot 0.9, yang mungkin mengindikasikan pentingnya faktor kolaboratif dibandingkan dengan faktor konten (content).

#### 2. Optimized Score
   - **Optimized Score**: 0.4
   
   Skor keseluruhan yang dioptimalkan oleh model. Meskipun demikian, skor ini mungkin belum mencerminkan kinerja yang sangat baik, tergantung pada konteks tugas yang dilakukan oleh model.

#### 3. Precision: 0.4
   - **Precision** mengukur seberapa akurat prediksi positif yang dihasilkan oleh model.
   - **Rumus Precision**:  
     $$
     \text{Precision} = \frac{TP}{TP + FP}
     $$
     di mana:
     - **TP (True Positive)** adalah jumlah prediksi benar yang positif.
     - **FP (False Positive)** adalah jumlah prediksi salah yang positif.
   
   Precision 0.4 berarti hanya 40% dari prediksi positif yang dilakukan oleh model yang benar-benar positif.

#### 4. Recall: 0.8
   - **Recall** mengukur seberapa banyak nilai positif yang sebenarnya berhasil ditemukan oleh model.
   - **Rumus Recall**:  
     $$
     \text{Recall} = \frac{TP}{TP + FN}
     $$
     di mana:
     - **FN (False Negative)** adalah jumlah prediksi salah yang negatif.
   
   Dengan recall 0.8, model ini berhasil menemukan 80% dari semua instansi yang benar-benar positif.

#### 5. F1-Score: 0.5333
   - **F1-Score** adalah rata-rata harmonis antara precision dan recall, memberikan keseimbangan antara keduanya.
   - **Rumus F1-Score**:
     $$
     \text{F1-Score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
     $$
   
   Dengan nilai precision 0.4 dan recall 0.8, F1-Score menjadi sekitar 0.5333. Ini menunjukkan bahwa meskipun recall cukup tinggi, precision relatif rendah, yang menghasilkan skor F1 yang moderat.

#### Kesimpulan
- **Precision 0.4** menunjukkan banyak prediksi positif yang salah, atau **False Positives** tinggi.
- **Recall 0.8** menunjukkan model cukup baik dalam menemukan contoh positif, namun ada kemungkinan sejumlah positif terlewat (**False Negatives**).
- **F1-Score 0.5333** menunjukkan keseimbangan yang rendah antara precision dan recall, dan ini menunjukkan trade-off antara false positive dan false negative yang perlu diperbaiki.

### Optimasi Throshold Evaluasi Model

#### 1. Threshold
Threshold menentukan batasan probabilitas yang digunakan untuk mengklasifikasikan instance sebagai positif atau negatif. Misalnya, jika threshold = 0.5, maka jika probabilitas prediksi model untuk suatu instance lebih besar dari 0.5, instance tersebut akan diklasifikasikan sebagai positif; jika lebih kecil, sebagai negatif. Menurunkan threshold memungkinkan model untuk memprediksi lebih banyak instance sebagai positif, meningkatkan recall tetapi menurunkan precision.

#### Analisi
- **Threshold rendah (0.1)**: Pada threshold ini, Precision adalah 1 (model sangat akurat dalam memprediksi positif), dan Recall relatif tinggi (sekitar 0.7793). F1-Score juga tinggi pada nilai ini. Hal ini menunjukkan bahwa model mendeteksi sebagian besar positif dengan akurasi tinggi.
  
- **Threshold tinggi (1.0 ke atas)**: Ketika threshold meningkat, precision tetap tinggi (lebih dari 0.99), namun recall menurun tajam. Ini karena model mulai lebih konservatif dalam mengklasifikasikan data positif. Pada threshold tinggi, model menjadi lebih ketat dan hanya memprediksi positif jika sangat yakin, yang menyebabkan banyak instance positif tidak terdeteksi. F1-Score juga menurun drastis, mencerminkan ketidakseimbangan antara precision dan recall.

- **Optimal Threshold**: Berdasarkan hasil ini, threshold yang memberikan keseimbangan terbaik antara precision, recall, dan F1-Score adalah **0.1**, karena pada titik ini F1-Score paling tinggi, yang menunjukkan keseimbangan terbaik antara sensitivitas dan akurasi.
ara sensitivitas dan akurasi.


### Hasil Optimasi Evaluasi Model Secara Keseluruhan

#### 1. RMSE (Root Mean Squared Error)
- **Interpretasi Hasil**: RMSE sebesar **3.4893** berarti bahwa secara rata-rata, kesalahan prediksi model adalah sekitar 3.49 unit dari nilai yang sebenarnya. Semakin rendah nilai RMSE, semakin baik model dalam melakukan prediksi.

#### 2. MAE (Mean Absolute Error)
- **Interpretasi Hasil**: MAE sebesar **3.3166** menunjukkan bahwa rata-rata kesalahan prediksi model adalah sekitar 3.32 unit. Seperti RMSE, semakin rendah MAE, semakin baik model dalam memprediksi.

#### 3. Precision
- **Interpretasi Hasil**: Precision sebesar **1.0000** menunjukkan bahwa semua prediksi positif yang dibuat oleh model benar (tidak ada false positives). Ini berarti model sangat akurat dalam mengidentifikasi prediksi positif.

#### 4. Recall
- **Interpretasi Hasil**:
  - **Recall pertama** sebesar **0.7793** berarti bahwa model berhasil mengidentifikasi sekitar 77.93% dari semua kejadian positif yang sebenarnya.
  - **Recall kedua** sebesar **0.8760** mungkin merupakan hasil recall untuk kelas yang berbeda atau model yang diuji dalam dua kondisi yang berbeda. Angka ini menunjukkan bahwa model berhasil mengidentifikasi sekitar 87.60% dari kejadian positif pada kondisi tersebut.

#### Kesimpulan
- **RMSE dan MAE** menunjukkan bahwa model memiliki kesalahan prediksi yang relatif rendah, dengan nilai kesalahan rata-rata sekitar 3.5.
- **Precision** yang sempurna (1.0000) menunjukkan bahwa ketika model memprediksi positif, prediksinya selalu benar, namun ini tidak memberi informasi tentang seberapa baik model menangkap semua kejadian positif (Recall).
- **Recall** yang lebih rendah pada pertama (0.7793) dan lebih tinggi pada kedua (0.8760) menunjukkan bahwa meskipun model mampu menangkap sebagian besar kejadian positif, masih ada ruang untuk peningkatan dalam menangkap semua kejadian positif secara sempurna.

---ng untuk peningkatan dalam menaal menangkap semua kejadian positif (Recall).


## 7. Kesimpulan Model Rekomendasi

### 1. **Content-Based Filtering**
   - **Solution Statement:**
     - Menggunakan TF-IDF untuk merepresentasikan fitur teks seperti genre, sinopsis, dan kata kunci.
     - Menghitung kesamaan menggunakan cosine similarity.
   
   - **Hasil Evaluasi:**
     - **Rekomendasi:** Berdasarkan evaluasi untuk *The Dark Knight*, rekomendasi yang diberikan seperti *The Dark Knight Rises*, *Batman Returns*, *Batman Begins*, dan film Batman lainnya menunjukkan bahwa sistem ini berhasil memberi saran yang mirip berdasarkan kesamaan konten (genre, tema, atau hubungan antara film).
     - **Metode yang Digunakan:** TF-IDF dan cosine similarity tampaknya digunakan untuk menghitung kemiripan berdasarkan teks (misalnya genre atau sinopsis), mengarah pada hasil rekomendasi yang relevan.
     - **Metrik Evaluasi:**
       - MAP (Mean Average Precision) = 0.8008, menunjukkan bahwa rekomendasi yang relevan cukup tinggi.
       - Precision = 0.5000 dan Recall = 1.0000 menandakan bahwa sebagian besar rekomendasi relevan, meskipun banyak rekomendasi tidak tepat (high precision, low false positives).
       - NDCG (Normalized Discounted Cumulative Gain) = 1.0000 menunjukkan hasil yang optimal dalam urutan rekomendasi.
   
   - **Kesimpulan:** Content-based filtering menunjukkan hasil yang solid dengan nilai MAP yang tinggi, precision dan recall yang baik, serta relevansi yang kuat berdasarkan konten film.

### 2. **Collaborative Filtering (User-Item Similarity & TruncatedSVD)**
   - **Solution Statement:**
     - Menggunakan data rating pengguna untuk membangun matriks kesamaan antar pengguna.
   
   - **Hasil Evaluasi:**
     - **Rekomendasi:** Rekomendasi seperti *Metropolis*, *Dancer in the Dark*, dan *Jarhead* menunjukkan pendekatan berbasis kolaborasi, di mana sistem memperhitungkan preferensi pengguna lain untuk memberikan rekomendasi.
     - **Model Evaluasi:** Menggunakan teknik seperti User-Item Similarity dan TruncatedSVD, hasil evaluasi untuk MAE (Mean Absolute Error) dan RMSE (Root Mean Squared Error) menunjukkan bahwa model ini memberikan prediksi rating yang cukup akurat meskipun ada sedikit kesalahan.
     - **Metrik Evaluasi:**
       - MAE = 1.891, menunjukkan bahwa kesalahan prediksi cukup besar.
       - RMSE = 1.940, juga menunjukkan bahwa model masih perlu ditingkatkan untuk memberikan prediksi yang lebih akurat.
   
   - **Kesimpulan:** Collaborative filtering memberikan rekomendasi yang berdasarkan data rating pengguna lain, tetapi masih memiliki margin error yang cukup tinggi, yang bisa menunjukkan bahwa model ini membutuhkan tuning lebih lanjut.

### 3. **Collaborative Filtering Menggunakan SVD**
   - **Solution Statement:**
     - Menggunakan teknik Singular Value Decomposition (SVD) untuk mengurangi dimensi dan memperbaiki rekomendasi.
   
   - **Hasil Evaluasi:**
     - **Rekomendasi:** Dengan teknik SVD, rekomendasi yang lebih spesifik seperti *Saw II* dan *Terminator Salvation* diberikan dengan prediksi rating yang lebih baik.
     - **Model Evaluasi:** RMSE dan MAE yang lebih rendah dibandingkan dengan metode sebelumnya menunjukkan bahwa SVD berhasil memperbaiki akurasi prediksi rating.
     - **Metrik Evaluasi:**
       - RMSE = 0.7131 dan MAE = 0.5471 menunjukkan prediksi yang lebih akurat dan lebih baik dibandingkan pendekatan collaborative filtering sebelumnya.
   
   - **Kesimpulan:** Penggunaan SVD berhasil meningkatkan kualitas prediksi dalam collaborative filtering, dengan nilai RMSE dan MAE yang lebih rendah, menunjukkan bahwa teknik ini dapat menghasilkan rekomendasi yang lebih akurat.

### 4. **Hybrid Recommendation**
   - **Solution Statement:**
     - Menggunakan gabungan dari kedua metode (content-based dan collaborative-based) untuk meningkatkan kualitas rekomendasi.
   
   - **Hasil Evaluasi:**
     - **Rekomendasi:** Hibrida antara content-based dan collaborative-based menghasilkan kombinasi rekomendasi dari kedua pendekatan, seperti *The Dark Knight Rises* dan *Batman Returns*.
     - **Metrik Evaluasi:**
       - Precision = 0.3, Recall = 0.6, F1-score = 0.4 menunjukkan bahwa meskipun ada banyak rekomendasi yang dihasilkan, banyak yang tidak relevan (precision rendah), namun recall cukup tinggi (menyertakan banyak film relevan).
   
   - **Kesimpulan:** Gabungan dari kedua pendekatan menghasilkan peningkatan jumlah rekomendasi, namun precision yang lebih rendah menunjukkan bahwa perlu dilakukan penyesuaian lebih lanjut dalam bobot antara metode.

### 5. **Item-Similarity (Collaborative Filtering)**
   - **Solution Statement:**
     - Menggunakan kesamaan item untuk merekomendasikan film berdasarkan kesamaan antar item.
   
   - **Hasil Evaluasi:**
     - **Metrik Evaluasi:**
       - RMSE = 3.4893, MAE = 3.3166, menunjukkan bahwa meskipun sistem ini dapat memberikan rekomendasi, akurasinya jauh lebih rendah dibandingkan metode SVD dan hybrid.
       - Precision dan Recall sangat tinggi untuk item-similarity, dengan precision = 1.0000 dan recall = 0.7793, tetapi hasil ini mungkin dipengaruhi oleh overfitting model atau data yang kurang representatif.
   
   - **Kesimpulan:** Hasil evaluasi menunjukkan bahwa meskipun metode ini memiliki precision yang tinggi, akurasi keseluruhan rendah (RMSE dan MAE yang tinggi), yang menunjukkan potensi masalah dalam model atau data yang digunakan.

### **Kesimpulan Umum**
- **Content-Based Filtering** memberikan hasil yang baik dengan akurasi yang tinggi, terutama dalam memberikan rekomendasi berdasarkan kesamaan konten.
- **Collaborative Filtering** dengan teknik seperti User-Item Similarity dan SVD menghasilkan rekomendasi yang lebih beragam, meskipun perlu dilakukan perbaikan untuk akurasi prediksi.
- **Hybrid Recommendation** memberikan solusi yang menarik untuk menggabungkan kedua pendekatan, meskipun precision masih perlu ditingkatkan.
- **Item-Similarity** mungkin kurang efektif dibandingkan dengan teknik lain, terutama dalam hal akurasi prediksi.


---
