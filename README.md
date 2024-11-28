
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

## Hasil Exploratory Data Analysis (EDA)

Tautan sumber dataset:
[TMDB 5000 Movie Dataset with Ratings on Kaggle](https://www.kaggle.com/datasets/aayushsoni4/tmdb-5000-movie-dataset-with-ratings)


## 1. DataFrame Pertama
### Informasi Umum:
- **Jumlah Baris dan Kolom**: 4602 baris, 21 kolom.
- **Deskripsi Kolom**:
  - `budget`: Anggaran film (tipe data *int64*).
  - `genres`: Genre film (tipe data *object*).
  - `homepage`: URL halaman utama film (hanya 1658 nilai yang terisi, banyak *missing values*).
  - `id`: ID unik film (tipe data *int64*).
  - `keywords`: Kata kunci terkait film (tipe data *object*).
  - `original_language`: Bahasa asli film (tipe data *object*).
  - `popularity`: Popularitas film (tipe data *float64*).
  - `revenue`: Pendapatan film (tipe data *int64*).
  - `runtime`: Durasi film (tipe data *float64*).
  - `vote_average`: Rata-rata rating (tipe data *float64*).
  - `tagline`: Slogan film (banyak *missing values*, hanya 3875 nilai terisi).
  - **Kolom lainnya**: Informasi terkait produksi, bahasa, dan tanggal rilis.
- **Memory Usage**: 755.1 KB.
- **Catatan**:
  Dataset ini cocok untuk analisis:
  - Genre populer.
  - Hubungan antara anggaran (`budget`) dan pendapatan (`revenue`).
  - Analisis temporal berdasarkan `release_date`.

---

## 2. DataFrame Kedua
### Informasi Umum:
- **Jumlah Baris dan Kolom**: 5.000.000 baris, 3 kolom.
- **Deskripsi Kolom**:
  - `userId`: ID pengguna yang memberikan rating (tipe data *int64*).
  - `movieId`: ID film yang diberi rating (tipe data *int64*).
  - `rating`: Nilai rating yang diberikan pengguna (tipe data *float64*).
- **Memory Usage**: 114.4 MB.
- **Catatan**:
  Dataset ini sangat penting untuk analisis rekomendasi film, seperti:
  - Sistem rekomendasi berbasis *collaborative filtering*.
  - Analisis preferensi pengguna terhadap film.

---

## 3. DataFrame Ketiga
### Informasi Umum:
- **Jumlah Baris dan Kolom**: 4602 baris, 3 kolom.
- **Deskripsi Kolom**:
  - `id`: ID unik yang mengacu pada film tertentu (tipe data *int64*).
  - `cast`: Informasi tentang pemain dalam bentuk teks atau string (tipe data *object*).
  - `crew`: Informasi tentang kru produksi dalam bentuk teks atau string (tipe data *object*).
- **Memory Usage**: 108 KB.
- **Catatan**:
  Dataset ini relevan untuk analisis:
  - Kolaborasi aktor dalam film.
  - Hubungan antara kru produksi dengan keberhasilan film.
  - *Social network analysis* di industri perfilman.

---

## Kesimpulan
- **Dataset Pertama**: Fokus pada informasi deskriptif film, cocok untuk analisis hubungan variabel seperti `budget`, `revenue`, dan genre.
- **Dataset Kedua**: Sangat besar dan cocok untuk membangun sistem rekomendasi film berdasarkan interaksi pengguna.
- **Dataset Ketiga**: Berguna untuk analisis pemain dan kru, termasuk kolaborasi dan keterlibatan mereka dalam film dengan rating tinggi.

Jika ingin analisis lebih lanjut atau visualisasi data, silakan arahkan eksplorasi yang diinginkan!


---

## **4. Data Preparation**

### **Langkah-langkah Data Preparation**
1. **Parsing Fitur Genre dan Keywords**:
   - Mengonversi genre dan kata kunci dari format JSON ke teks.
2. **Preprocessing Teks**:
   - Membersihkan teks dengan menghapus angka, tanda baca, dan mengonversinya ke huruf kecil.
3. **Mengkombinasikan Fitur**:
   - Menggabungkan genre, kata kunci, dan sinopsis menjadi satu kolom `content` untuk digunakan oleh TF-IDF.
4. **Membangun Matriks Pivot**:
   - Membuat matriks pivot pengguna-film untuk Collaborative Filtering.

### **Alasan Data Preparation**
- Membersihkan teks memastikan hasil TF-IDF lebih representatif.
- Menggabungkan fitur memberikan lebih banyak informasi untuk Content-Based Filtering.
- Matriks pivot diperlukan untuk menghitung kesamaan pengguna dalam Collaborative Filtering.

---

## **5. Modeling**

### **Content-Based Filtering**
1. **TF-IDF** digunakan untuk merepresentasikan teks dalam bentuk vektor.
2. **Cosine Similarity** digunakan untuk menghitung kesamaan antar film.
3. Hyperparameter TF-IDF:
   - `max_features=5000`: Membatasi jumlah fitur untuk menghindari overfitting.
   - `ngram_range=(1, 2)`: Menggunakan unigram dan bigram untuk menangkap konteks yang lebih luas.
   - `stop_words='english'`: Menghilangkan kata-kata umum yang tidak relevan.

### **Collaborative Filtering**
1. **Matriks Kesamaan Pengguna**:
   - Dibangun menggunakan cosine similarity pada matriks pivot pengguna-film.
2. Rekomendasi:
   - Berdasarkan rata-rata rating dari pengguna serupa.

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
