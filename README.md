# Wine Quality Analysis 

## Konteks

Dalam industri minuman, kualitas produk menjadi faktor utama yang memengaruhi kepuasan konsumen dan reputasi perusahaan. Terutama pada anggur, karakteristik kimiawi menentukan rasa, aroma, dan kualitas akhir yang diterima konsumen. Analisis berbasis data sangat penting untuk memahami pola kualitas anggur, mengidentifikasi faktor kritis, dan memastikan konsistensi produk.

Dataset yang digunakan mencakup fitur kimia seperti kadar alkohol, asam tetap (`fixed acidity`), asam volatil (`volatile acidity`), gula sisa (`residual sugar`), klorida (`chlorides`), dan kadar sulfat (`sulphates`), beserta label `quality` yang menunjukkan kualitas akhir anggur. Dengan informasi ini, produsen dapat memprediksi kualitas anggur sebelum distribusi, sehingga risiko produk yang tidak memenuhi standar dapat diminimalkan.

## Problem Statement

Perusahaan menghadapi tantangan untuk memprediksi kualitas anggur secara akurat berdasarkan data kimiawi. Fitur yang saling berkorelasi dan distribusi yang berbeda antar kelas kualitas membuat model harus mampu menangkap pola kompleks. Tantangan tambahan adalah membedakan kelas kualitas yang berdekatan, misalnya antara kualitas 5 dan 6, yang dapat memengaruhi keputusan produksi dan seleksi bahan baku.

Prediksi kualitas yang tepat dapat membantu:  
1. Mengidentifikasi anggur dengan kualitas tinggi sebelum distribusi.  
2. Memberikan rekomendasi proses produksi untuk memperbaiki anggur yang berpotensi kualitas rendah.  
3. Meminimalkan risiko ketidakpuasan konsumen dan kerugian finansial akibat produk yang tidak sesuai standar.

## Tujuan

1. Mengembangkan beberapa model klasifikasi untuk memprediksi kualitas anggur.  
2. Mengevaluasi performa model dan memilih model terbaik.  
3. Menentukan fitur-fitur paling berpengaruh terhadap kualitas.  
4. Memberikan rekomendasi berbasis data untuk strategi produksi dan kontrol kualitas.

## Dataset

Dataset terdiri dari variabel numerik berikut:  

- `fixed acidity` : kadar asam tetap  
- `volatile acidity` : kadar asam volatil  
- `citric acid` : kadar asam sitrat  
- `residual sugar` : kadar gula sisa  
- `chlorides` : kadar klorida  
- `free sulfur dioxide` : kandungan sulfur dioksida bebas  
- `total sulfur dioxide` : kandungan sulfur dioksida total  
- `density` : densitas anggur  
- `pH` : tingkat keasaman  
- `sulphates` : kadar sulfat  
- `alcohol` : kadar alkohol  
- `quality` : label kualitas anggur

## Hasil Prediksi

Dari tiga model klasifikasi yang diuji, **Random Forest** dipilih sebagai model terbaik karena performa paling tinggi. Hasil prediksi kualitas untuk data testing, **5 baris pertama dan 5 baris terakhir**, adalah sebagai berikut:

**5 baris pertama**

| Id   | quality |
|------|---------|
| 222  | 5       |
| 1514 | 6       |
| 417  | 5       |
| 754  | 5       |
| 516  | 5       |

**5 baris terakhir**

| Id    | quality |
|-------|---------|
| 1147  | 6       |
| 296   | 5       |
| 170   | 5       |
| 1439  | 5       |
| 946   | 7       |

Tabel ini membantu produsen langsung melihat anggur mana yang diprediksi memiliki kualitas tinggi dan mana yang mungkin perlu perhatian tambahan dalam proses produksi.

## Insight dari Analisis

- Fitur `alcohol`, `volatile acidity`, dan `sulphates` paling memengaruhi kualitas anggur.  
- Random Forest mampu menangkap pola kompleks antar fitur sehingga prediksi lebih akurat dibanding Decision Tree atau KNN.  
- Kesalahan prediksi sebagian besar terjadi pada kelas kualitas yang berdekatan, namun masih dapat diterima dalam konteks produksi.

## Kesimpulan

1. Dari tiga model yang diuji, **Random Forest** memberikan performa terbaik dalam memprediksi kualitas anggur.  
2. Fitur utama yang memengaruhi kualitas dapat menjadi fokus kontrol proses produksi.  
3. Model ini membantu produsen membuat keputusan berbasis data untuk meningkatkan konsistensi produk.

## Rekomendasi

**Untuk Produsen:**  
1. Gunakan model untuk memprediksi kualitas anggur sebelum distribusi.  
2. Fokus kontrol kualitas pada fitur yang paling memengaruhi kualitas akhir.  
3. Pantau model secara berkala agar prediksi tetap akurat dan relevan.
