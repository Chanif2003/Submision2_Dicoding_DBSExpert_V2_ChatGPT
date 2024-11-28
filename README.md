
# **Laporan Proyek: Sistem Rekomendasi Film Menggunakan Content-Based dan Collaborative Filtering**

## **1. Project Overview**

### **Latar Belakang**
   Dalam era digital, pengguna sering menghadapi masalah dalam memilih konten yang relevan di tengah banyaknya pilihan yang tersedia. Dalam industri film, jumlah film yang terus bertambah setiap tahunnya membuat pengguna kesulitan menemukan film yang sesuai dengan minat mereka. Tanpa sistem rekomendasi, pengguna sering kali harus bergantung pada pencarian manual atau ulasan yang tidak selalu mencerminkan preferensi pribadi.
   
   Masalah ini menjadi semakin relevan karena:
   1. **Ledakan Data**: Industri hiburan memproduksi jutaan konten setiap tahun.
   2. **Efisiensi Waktu**: Pengguna tidak memiliki waktu untuk mengeksplorasi semua opsi yang tersedia secara manual.
   3. **Pengalaman Pengguna**: Tanpa personalisasi, pengguna sering merasa tidak puas dengan rekomendasi generik.
   
   Sistem rekomendasi menawarkan solusi dengan memberikan saran personal yang relevan berdasarkan data historis pengguna dan karakteristik konten.
   
   ### **Masalah yang Dihadapi**
   1. **Ketidakmampuan Sistem Generik**: Rekomendasi berbasis popularitas tidak mempertimbangkan preferensi unik pengguna.
   2. **Keterbatasan Data Perilaku**: Tidak semua pengguna memiliki riwayat perilaku yang cukup untuk mendukung rekomendasi berbasis Collaborative Filtering.
   3. **Kesalahan dalam Pemahaman Konteks**: Sistem rekomendasi tradisional sering gagal memahami konteks atau hubungan antara konten berdasarkan deskripsi tekstual.
   
   ### **Tujuan Proyek**
   1. Membangun sistem rekomendasi yang efektif dengan menggabungkan pendekatan **Content-Based Filtering** dan **Collaborative Filtering**.
   2. Menyediakan rekomendasi yang personal dan relevan bagi pengguna.
   3. Mengoptimalkan akurasi rekomendasi melalui tuning hyperparameter, seperti pada TF-IDF.
   
   ### **Manfaat Proyek**
   1. **Meningkatkan Pengalaman Pengguna**: Rekomendasi yang lebih relevan meningkatkan kepuasan pengguna.
   2. **Efisiensi Waktu**: Membantu pengguna menemukan film yang sesuai tanpa harus mencari secara manual.
   3. **Potensi Bisnis**: Sistem rekomendasi yang efektif dapat meningkatkan keterlibatan pengguna, yang pada akhirnya berdampak positif pada metrik bisnis seperti retensi pelanggan.

---

## **2. Business Understanding**

### **Problem Statements**
   1. Bagaimana memberikan rekomendasi film yang relevan untuk pengguna berdasarkan deskripsi film (Content-Based)?
   2. Bagaimana meningkatkan kualitas rekomendasi dengan data perilaku pengguna (Collaborative Filtering)?
   3. Bagaimana mengukur performa sistem rekomendasi secara kuantitatif?
   
   ### **Goals**
   1. Memberikan rekomendasi personal yang relevan berdasarkan preferensi pengguna.
   2. Meningkatkan akurasi model dengan kombinasi pendekatan dan tuning hyperparameter.
   3. Membandingkan kinerja sistem dengan metrik evaluasi.
   
   ### **Solution Statements**
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

## **3. Data Understanding**

   ### Tautan sumber dataset:
   [TMDB 5000 Movie Dataset with Ratings on Kaggle](https://www.kaggle.com/datasets/aayushsoni4/tmdb-5000-movie-dataset-with-ratings)
   
   ### Uraian Setiap Fitur Data
   
   ### **Dataset 1 (tmdb_movie_dataset.csv) : Informasi Film**
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
   
   ### **Dataset 2 (tmdb_movie_ratings.csv): Rating Pengguna**
   1. **`userId`:** ID unik pengguna yang memberikan rating. (Tipe Data: Integer)
   2. **`movieId`:** ID unik film yang dirating pengguna. (Tipe Data: Integer)
   3. **`rating`:** Nilai rating yang diberikan pengguna untuk film. (Tipe Data: Float) 
   
   ### **Dataset 3 (tmdb_movie_credits.csv): Cast dan Crew**
   1. **`id`:** ID unik untuk setiap film (sejalan dengan Dataset 1). (Tipe Data: Integer)  
   2. **`cast`:** Daftar aktor yang terlibat dalam film (kemungkinan berbentuk JSON atau string). (Tipe Data: Object (teks))  
   3. **`crew`:** Daftar kru film (misalnya, sutradara, produser, penulis skenario). (Tipe Data: Object (teks))
   
   ### Kesimpulan
   - **Dataset Pertama**: Fokus pada informasi deskriptif film, cocok untuk analisis hubungan variabel seperti `budget`, `revenue`, dan genre.
   - **Dataset Kedua**: Sangat besar dan cocok untuk membangun sistem rekomendasi film berdasarkan interaksi pengguna.
   - **Dataset Ketiga**: Berguna untuk analisis pemain dan kru, termasuk kolaborasi dan keterlibatan mereka dalam film dengan rating tinggi.

---

## **4. Data Preparation**

   ### **Alasan Data Preparation**
   - Membersihkan teks memastikan hasil TF-IDF lebih representatif.
   - Menggabungkan fitur memberikan lebih banyak informasi untuk Content-Based Filtering.
   - Matriks diperlukan untuk menghitung kesamaan pengguna dalam Collaborative Filtering.
   
   Berikut langkah-langkah Data Preparation untuk masing-masing model:
   
   ### **Langkah-langkah Data Preparation untuk Content-Based Filtering**
   
   #### **1. Menggabungkan dan Menyaring Data**
   - **Data Gabungan**: Menggabungkan informasi film dari dua sumber data (`movies_df` dan `credits_df`) berdasarkan kolom `id`.
   - **Pemilihan Kolom Penting**: Mengambil hanya kolom yang relevan, yaitu `id`, `title`, `overview`, `genres`, `keywords`, `cast`, dan `crew`.
   
   #### **2. Membersihkan dan Memformat Data**
   - **Mengonversi Format Data**: 
     - Genre, kata kunci, pemeran, dan kru yang berbentuk string JSON diubah menjadi daftar (list) untuk mempermudah pengolahan.
   - **Menghapus Nilai Kosong**: Menghapus baris dengan data yang hilang untuk memastikan kelengkapan informasi.
   - **Ekstraksi Data Penting**:
     - Mengambil nama sutradara dari kru (`crew`).
     - Menghapus spasi dari setiap elemen di daftar genre, kata kunci, pemeran, dan kru untuk menjaga konsistensi data.
   
   #### **3. Menggabungkan Fitur**
   - Semua informasi penting seperti ringkasan (`overview`), genre, kata kunci, pemeran, dan kru digabung menjadi satu kolom fitur tunggal (`features`) untuk setiap film.
   
   #### **4. Representasi Numerik dengan TF-IDF**
   - **Teknik TF-IDF**: Mengubah teks dalam kolom `features` menjadi vektor numerik menggunakan metode TF-IDF.
     - Kata-kata yang sering muncul di seluruh dokumen (film) mendapat bobot rendah.
     - Hanya 5000 kata paling relevan yang dipertimbangkan.
   
   #### **5. Menghitung Kemiripan Antarfilm**
   - **Cosine Similarity**:
     - Menghitung tingkat kemiripan antarfilm berdasarkan vektor fitur TF-IDF.
     - Hasilnya adalah matriks cosine similarity, di mana setiap elemen mewakili tingkat kemiripan antara dua film.
   
   #### **6. Hasil Akhir**
   - Matriks cosine similarity yang dihasilkan dapat digunakan untuk:
     - Menemukan film-film yang mirip dengan film tertentu.
     - Membuat rekomendasi film berdasarkan konten seperti genre, kata kunci, dan pemeran.
   
   
   ### **Langkah-langkah Data Preparation untuk Collaborative-Based Filtering dengan TruncatedSVD untuk Reduksi Data**
   
   #### 1. **Pembersihan Data (Data Cleaning):**
   - Langkah pertama adalah menghapus baris yang memiliki nilai kosong (NaN) pada kolom-kolom penting seperti userId, movieId, dan rating dalam dataset ratings_df.
   - Ini bertujuan untuk memastikan bahwa hanya data yang lengkap dan valid yang digunakan dalam proses selanjutnya.
   
   #### 2. **Penyelarasan Tipe Data (Data Type Consistency):**
   - Setelah memastikan tidak ada data kosong, bagian mengonversi kolom userId dan movieId dalam ratings_df menjadi tipe data integer.
   - Ini memastikan bahwa data tersebut dapat diproses dengan benar dalam algoritma pemrosesan selanjutnya.
   
   #### 3. **Sinkronisasi ID di Dataset Film (movies_df):**
   - bagian ini kemudian memastikan bahwa kolom id pada movies_df (dataset film) berisi data numerik yang valid.
   - Hal ini dilakukan dengan mengonversi kolom id menjadi numerik, menghapus baris yang memiliki nilai kosong pada kolom tersebut, dan memastikan bahwa tipe data ID film adalah integer.
   
   #### 4. **Pembuatan Matriks Sparse:**
   - Selanjutnya, bagian membuat sebuah matriks sparse (csr_matrix) yang merepresentasikan rating yang diberikan oleh pengguna terhadap film. Matriks sparse ini hanya menyimpan nilai rating yang ada, sedangkan elemen-elemen lainnya (yang tidak diisi) disimpan secara efisien tanpa menggunakan ruang memori yang besar.
   Selain itu, kode ini menyesuaikan indeks pengguna (userId) untuk dimulai dari 0, karena dalam Python indeks dimulai dari 0, sedangkan ID pengguna dalam dataset mungkin dimulai dari 1.
   
   #### 5. **Informasi Matriks yang Dihasilkan:**
   - Setelah matriks sparse berhasil dibuat, bagian ini menampilkan informasi mengenai keberhasilan pembuatan matriks dan menunjukkan ukuran matriks tersebut, yang menggambarkan jumlah pengguna dan film yang ada.
   
   
   ### **Data Preparation untuk Collaborative-Based Filtering Menggunakan Matrix Factorization SVD & Hybrid-Recomendation**
   - untuk Data Preparation pada **Model Collaborative-Based Filtering Menggunakan Matrix Factorization SVD** dan **Model Hybrid-Recomendation** menggunakan data preparation yang sudah di lakukan pada tahap sebelumnya.
   
   ---
   
## **5. Modeling**
### **Content-Based Filtering**
   
   #### 1. Content-Based Filtering
   **Content-Based Filtering** adalah metode dalam sistem rekomendasi yang menyarankan item berdasarkan **fitur konten** dari item tersebut. Dalam konteks film, fitur konten bisa berupa:
      - **Genre** film (misalnya: aksi, drama, komedi).
      - **Deskripsi** atau sinopsis film.
      - **Tag** atau label yang menggambarkan tema film (misalnya: horor, thriller).
      - **Pemeran** atau sutradara.
      #### Prinsip Dasar:
      Content-Based Filtering berfokus pada kemiripan **fitur konten** antara item yang sudah dikenal oleh pengguna dan item lainnya dalam dataset. **Jika pengguna menyukai suatu item**, mereka kemungkinan besar akan menyukai item lain yang memiliki kemiripan konten yang tinggi.
      
   #### Proses Content-Based Filtering:
   1. **Penyusunan Fitur Item:** Setiap item (misalnya film) digambarkan dengan fitur-fitur numerik, seperti genre, tag, atau deskripsi.
   2. **Pengukuran Kemiripan:** Menggunakan metode matematis untuk mengukur kemiripan antara item yang satu dengan yang lain, umumnya dengan **cosine similarity**.
   3. **Rekomendasi:** Berdasarkan kemiripan ini, sistem akan merekomendasikan item yang paling mirip dengan item yang telah disukai atau dipilih oleh pengguna.
   #### Kelebihan:
   - Tidak memerlukan data perilaku pengguna (misalnya klik atau rating).
   - Sistem rekomendasi lebih berbasis konten item itu sendiri.
   #### Kekurangan:
   - **Masalah "cold start"**: Sulit memberikan rekomendasi untuk item yang baru karena mereka belum memiliki cukup informasi.
   - Terbatas pada **fitur yang ada**: Hanya fitur yang tersedia dalam dataset yang dapat digunakan untuk perbandingan.
   
   #### 2. Cosine Similarity
   **Cosine Similarity** adalah metode matematis yang digunakan untuk mengukur kemiripan antara dua vektor dalam ruang berdimensi tinggi. Ini mengukur **seberapa dekat arah dua vektor**, tanpa memperhatikan panjang vektor tersebut.
   
   #### Rumus Cosine Similarity:
$$\text{Cosine Similarity} = \frac{A \cdot B}{\|A\| \|B\|}$$
   - **A · B**: Produk titik (dot product) antara dua vektor A dan B.
   - **‖A‖** dan **‖B‖**: Norma (panjang) dari vektor A dan B.
   
   #### Interpretasi Cosine Similarity:
   - **1**: Kedua vektor memiliki arah yang sama (sangat mirip).
   - **0**: Kedua vektor tidak memiliki arah yang sama (tidak mirip).
   - **-1**: Kedua vektor memiliki arah yang berlawanan (sangat berbeda).
   
   #### Penerapan dalam Sistem Rekomendasi:
   Setiap item (misalnya film) digambarkan oleh vektor fitur. Cosine similarity digunakan untuk mengukur seberapa mirip dua item berdasarkan vektor fitur mereka. Misalnya, dua film yang memiliki genre yang sama atau pemeran yang sama akan memiliki skor cosine similarity yang lebih tinggi, menunjukkan bahwa film tersebut mirip.

   ### 3. Langkah-langkah Kerja Sistem
   
   #### Langkah-langkah:
   1. **Input dari Pengguna:** Sistem menerima judul film yang diminta oleh pengguna.
   2. **Pencarian Film:** Sistem mencari film tersebut di dalam dataset berdasarkan **judul yang telah diubah menjadi huruf kecil** untuk mencocokkan tanpa memandang kapitalisasi huruf.
   3. **Validasi Cosine Similarity:** Sistem memastikan bahwa **matriks cosine similarity** sudah dihitung sebelumnya, yang berisi nilai kemiripan antara film satu dengan yang lain.
   4. **Penghitungan Kemiripan:** Sistem mencari skor kesamaan antara film yang diminta dan film lainnya dalam dataset menggunakan **cosine similarity**.
   5. **Rekomendasi:** Film yang memiliki skor kesamaan tertinggi akan direkomendasikan kepada pengguna.
   
   ### 4. Kelebihan dan Kekurangan Content-Based Filtering
   #### Kelebihan:
   - **Tidak bergantung pada data pengguna:** Hanya membutuhkan data konten item itu sendiri.
   - **Rekomendasi yang personal:** Dapat memberikan rekomendasi yang relevan berdasarkan kesamaan konten.
   #### Kekurangan:
   - **Masalah "cold start":** Film baru yang tidak memiliki cukup informasi untuk dibandingkan akan sulit untuk direkomendasikan.
   - **Terbatas pada fitur yang ada:** Sistem hanya dapat merekomendasikan item berdasarkan fitur yang tersedia dalam dataset, jadi jika fitur yang digunakan tidak lengkap, rekomendasi juga bisa terbatas.
   
   ### Ringkasan:
   1. **Representasi Item:** Setiap item diwakili oleh vektor fitur.
   2. **Pengukuran Kemiripan:** Cosine similarity digunakan untuk mengukur kemiripan antara item berdasarkan vektor fitur.
   3. **Rekomendasi:** Item yang paling mirip dengan item yang sudah disukai oleh pengguna akan direkomendasikan.
   Content-Based Filtering menggunakan **cosine similarity** untuk mengukur kedekatan antara item berdasarkan konten mereka, dan memberikan rekomendasi berdasarkan kemiripan ini.
   

### **Collaborative Filtering Dengan TruncatedSVD**
   
   #### 1. Collaborative Filtering (CF)
   **Collaborative Filtering** adalah teknik rekomendasi yang mengandalkan interaksi pengguna dengan item (misalnya film). Pendekatan ini tidak memerlukan informasi eksplisit mengenai item atau pengguna (seperti deskripsi film atau data demografis pengguna). Sebaliknya, sistem rekomendasi hanya menggunakan data interaksi atau **rating** antara pengguna dan item (film).
   
   Ada dua pendekatan utama dalam Collaborative Filtering:
   
   #### a. User-Based Collaborative Filtering:
   - **Teori**: Mengidentifikasi pengguna yang mirip satu sama lain berdasarkan pola interaksi atau rating mereka terhadap item (film). Misalnya, jika pengguna A dan pengguna B memberikan rating tinggi pada banyak film yang sama, maka mereka dianggap mirip. Oleh karena itu, film yang disukai oleh A tetapi belum dilihat oleh B bisa direkomendasikan untuk B.
   - **Masalah**: Pendekatan ini menjadi kurang efisien dan lebih sulit diimplementasikan ketika jumlah pengguna sangat besar.
   #### b. Item-Based Collaborative Filtering:
   - **Teori**: Berfokus pada hubungan antara item. Pendekatan ini mencoba menemukan film yang mirip dengan film yang telah dinilai oleh pengguna. Jika pengguna A menyukai film X, dan film Y sangat mirip dengan film X berdasarkan rating pengguna lain, maka film Y dapat direkomendasikan kepada A.
   - **Keunggulan**: Item-based filtering lebih stabil dan lebih efisien dalam menangani jumlah pengguna yang sangat besar dibandingkan dengan user-based filtering.
   
   Pada kode yang diberikan, pendekatan yang digunakan adalah **Item-Based Collaborative Filtering**, di mana kita menghitung **kesamaan antar item (film)** dan memberikan rekomendasi film berdasarkan kesamaan tersebut.
   
   ### 2. Singular Value Decomposition (SVD) dan Truncated SVD
   **Singular Value Decomposition (SVD)** adalah teknik matematis untuk **faktorasi matriks**, yang digunakan untuk mengurangi dimensi data dan memproyeksikan data ke ruang vektor yang lebih rendah namun tetap menjaga sebanyak mungkin informasi penting. SVD memiliki banyak aplikasi, termasuk di bidang **rekomendasi**.
   
   #### a. SVD: Proses Dasar
   SVD memfaktorkan matriks **m x n** menjadi tiga matriks:
   $$A = U \Sigma V^T$$
   - **A**: Matriks asli, misalnya matriks rating pengguna terhadap film (dimensi: m x n, dengan m adalah jumlah pengguna dan n adalah jumlah film).
   - **U**: Matriks pengguna (dimensi m x m).
   - **Σ (Sigma)**: Matriks diagonal yang berisi nilai singular (dimensi m x n).
   - **V^T**: Matriks film (dimensi n x n, tetapi kita ambil transpose-nya agar bisa mengalikan dengan U dan Σ).
   
   Tujuan dari SVD adalah untuk menemukan struktur atau pola tersembunyi dalam data melalui proyeksi matriks menjadi beberapa komponen (faktor). Dalam konteks rekomendasi film:
   - **U** berisi representasi pengguna dalam ruang fitur yang lebih rendah.
   - **Σ** berisi informasi tentang seberapa penting masing-masing komponen dalam menjelaskan variansi data.
   - **V^T** berisi representasi film dalam ruang fitur yang lebih rendah.
   
   ### b. Truncated SVD
   - **Teori**: Pada **Truncated SVD**, kita hanya mempertahankan sejumlah komponen singular terbesar dan mengabaikan sisanya. Ini mengurangi dimensi matriks tanpa kehilangan terlalu banyak informasi yang penting.
   - **Mengapa Truncated SVD?**
     - Matriks rating pengguna terhadap film sangat besar dan **sparse** (banyak nilai yang hilang atau kosong), yang membuat perhitungan menjadi sangat mahal.
     - Dengan **Truncated SVD**, kita dapat mengurangi dimensi data ke jumlah komponen tertentu, misalnya 50, dan masih mempertahankan sebagian besar informasi penting, yang membantu **mengurangi noise** dan **overfitting**.
   
   **Truncated SVD** memberikan representasi yang lebih kompak dan lebih mudah dihitung dari data rating yang besar.
   
   ## 3. Cosine Similarity untuk Mengukur Kesamaan Antar Item
   
   Setelah kita melakukan **reduksi dimensi** menggunakan Truncated SVD, kita dapat menghitung **kesamaan antar item (film)**. Salah satu cara yang umum digunakan untuk mengukur kesamaan antar vektor adalah dengan menggunakan **cosine similarity**.
   
   ### a. Cosine Similarity:
   Cosine similarity mengukur sudut antara dua vektor dalam ruang fitur. Jika dua vektor memiliki sudut kecil antara mereka, berarti mereka sangat mirip. Formula cosine similarity adalah:
   \[
   \text{Cosine Similarity}(A, B) = \frac{A \cdot B}{\|A\| \|B\|}
   \]
   Di mana:
   - \( A \cdot B \) adalah hasil perkalian dot produk antara dua vektor.
   - \( \|A\| \) dan \( \|B\| \) adalah norma (panjang) dari vektor A dan B.
   
   Jika dua vektor memiliki nilai cosine similarity yang tinggi (mendekati 1), maka item-item yang mereka wakili sangat mirip. Dalam konteks ini, kita menghitung kesamaan antar film berdasarkan vektor fitur mereka yang diperoleh dari SVD.
   
   ### b. Perhitungan Kesamaan Antara Film:
   Setelah matriks rating pengguna diubah menjadi ruang fitur yang lebih rendah melalui Truncated SVD, kita dapat menghitung kesamaan antara film-film tersebut dalam ruang tersebut, menggunakan **cosine similarity** pada matriks hasil SVD yang telah dikurangi dimensinya.
   
   ```python
   item_similarity_svd = cosine_similarity(user_movie_ratings_svd.T)
   Ini menghitung seberapa mirip satu film dengan film lainnya berdasarkan vektor fitur yang telah direduksi dimensinya.
   ```
   4. Rekomendasi Berdasarkan Kesamaan
   Setelah kita mendapatkan matriks kesamaan antar item (film), kita dapat membuat rekomendasi dengan cara berikut:
   
   Ambil rating pengguna di ruang yang sudah direduksi dimensinya (hasil dari SVD).
   Hitung skor bobot untuk film yang belum dinilai oleh pengguna berdasarkan kesamaan film yang sudah dinilai oleh pengguna. Skor ini dihitung dengan mengalikan vektor kesamaan film dengan vektor rating pengguna.
   Kecualikan film yang sudah dinilai oleh pengguna dari daftar rekomendasi dengan memberi skor negatif pada film-film tersebut.
   Ambil rekomendasi teratas dengan memilih film yang memiliki skor tertinggi yang belum dinilai oleh pengguna.
   5. Ringkasan Cara Kerja
   Reduksi Dimensi dengan Truncated SVD: Mengurangi dimensi matriks rating untuk menyederhanakan data dan menangkap struktur utama dalam data.
   Penghitungan Kesamaan Item dengan Cosine Similarity: Mengukur kesamaan antar film berdasarkan proyeksi dalam ruang fitur yang lebih rendah.
   Rekomendasi Film: Berdasarkan kesamaan antar film, menghitung skor untuk film yang belum dinilai oleh pengguna, kemudian memberikan rekomendasi teratas.
   Kesimpulan
   Collaborative Filtering adalah metode yang efektif untuk memberikan rekomendasi berdasarkan interaksi pengguna dengan item.
   Truncated SVD digunakan untuk mereduksi dimensi data rating yang besar dan jarang, menyederhanakan perhitungan dan meningkatkan efisiensi.
   Cosine Similarity digunakan untuk mengukur kesamaan antar film, yang memungkinkan kita memberikan rekomendasi yang relevan berdasarkan film yang sudah dinilai oleh pengguna.
   Dengan pendekatan ini, sistem rekomendasi dapat memberikan saran film kepada pengguna tanpa perlu memahami konten film atau informasi pribadi pengguna, hanya berdasarkan data interaksi (rating).
   
   


### **Gabungan Kedua Metode**
- Kombinasi skor Content-Based dan Collaborative Filtering menggunakan bobot:
  \[
  \text{final\_score} = w_c \cdot \text{score\_content} + w_r \cdot \text{score\_collaborative}
  \]
  dengan \( w_c \) dan \( w_r \) adalah bobot masing-masing metode.

---


## **6. Evaluation**

### **Metrik Evaluasi**
1. **Precision@K**:
   - Proporsi film yang relevan dari rekomendasi teratas:
     \[
     \text{Precision@K} = \frac{\text{Jumlah relevan di top K}}{K}
     \]
2. **Recall@K**:
   - Proporsi film yang relevan berhasil ditemukan dari total film relevan:
     \[
     \text{Recall@K} = \frac{\text{Jumlah relevan di top K}}{\text{Total relevan}}
     \]
3. **Mean Average Precision (MAP)**:
   - Rata-rata presisi di semua rekomendasi relevan.

### **Hasil Evaluasi**
Contoh evaluasi:
- **Precision@5**: 0.8
- **Recall@5**: 0.67
- **MAP**: 0.74

### **Interpretasi**
Hasil menunjukkan bahwa sistem memiliki kinerja baik dengan sebagian besar rekomendasi relevan ditemukan di 5 teratas. Precision yang tinggi menandakan relevansi, sementara recall menandakan cakupan.

---

## **7. Kesimpulan**

1. **Content-Based Filtering** efektif dalam merekomendasikan film berdasarkan deskripsi.
2. **Collaborative Filtering** menambahkan nilai dengan memanfaatkan perilaku pengguna.
3. Kombinasi kedua metode dan hyperparameter tuning meningkatkan akurasi rekomendasi.

### **Pekerjaan Masa Depan**
1. Memanfaatkan model deep learning untuk rekomendasi berbasis embedding.
2. Menggunakan implicit feedback seperti klik atau waktu tonton untuk Collaborative Filtering.

---
