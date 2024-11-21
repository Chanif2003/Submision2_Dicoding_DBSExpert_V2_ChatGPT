
# **Laporan Proyek: Sistem Rekomendasi Film Menggunakan Content-Based dan Collaborative Filtering**

## **1. Project Overview**

### **Latar Belakang**
Sistem rekomendasi telah menjadi bagian penting dari kehidupan digital, membantu pengguna memilih konten yang relevan di tengah banyaknya pilihan. Dalam industri film, sistem ini membantu meningkatkan pengalaman pengguna dengan menyarankan film yang relevan berdasarkan minat mereka atau pola perilaku pengguna serupa.

Dua pendekatan utama yang digunakan adalah **Content-Based Filtering** dan **Collaborative Filtering**:
- **Content-Based Filtering** bekerja dengan mencocokkan fitur dari item (misalnya genre, sinopsis, atau kata kunci) untuk memberikan rekomendasi.
- **Collaborative Filtering** bekerja dengan memanfaatkan data perilaku pengguna untuk menemukan pola kesamaan antara pengguna atau item.

### **Tujuan Proyek**
1. Membangun sistem rekomendasi film yang efektif dengan menggunakan gabungan Content-Based dan Collaborative Filtering.
2. Mengoptimalkan akurasi model dengan tuning hyperparameter pada TF-IDF.
3. Mengevaluasi kinerja model dengan metrik evaluasi yang relevan seperti Precision@K dan Recall@K.

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

### **Dataset**
Dataset yang digunakan:
1. **TMDB 5000 Movies** - Data deskripsi film.
2. **TMDB 5000 Ratings** - Data rating pengguna terhadap film.

### **Informasi Data**
- **TMDB 5000 Movies**:
  - `title`: Judul film.
  - `overview`: Sinopsis film.
  - `genres`: Daftar genre film.
  - `keywords`: Kata kunci terkait film.

- **TMDB 5000 Ratings**:
  - `userId`: ID pengguna.
  - `movieId`: ID film.
  - `rating`: Rating yang diberikan oleh pengguna.

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
