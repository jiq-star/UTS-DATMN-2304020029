# Prediksi Kualitas Wine Menggunakan Model Klasifikasi

## Konteks

Dalam industri wine, kualitas produk menjadi salah satu faktor penting yang dapat memengaruhi kepuasan konsumen dan nilai jual produk. Kualitas wine dapat dipengaruhi oleh berbagai karakteristik kimia, seperti tingkat keasaman, kadar alkohol, pH, kandungan sulfur dioxide, sulphates, dan beberapa faktor lainnya.

Penilaian kualitas wine secara manual dapat membutuhkan waktu dan bergantung pada subjektivitas penilai. Oleh karena itu, pendekatan berbasis machine learning dapat digunakan untuk membantu memprediksi kualitas wine secara lebih cepat dan konsisten berdasarkan data karakteristik kimia yang tersedia.

## Problem Statement

Permasalahan dalam project ini adalah bagaimana membuat model klasifikasi yang mampu memprediksi nilai `quality` pada wine berdasarkan fitur-fitur kimia yang tersedia. Dataset training memiliki kolom `quality` sebagai target, sedangkan dataset testing tidak memiliki kolom `quality`, sehingga nilai tersebut perlu diprediksi menggunakan model yang dibuat.

Dengan adanya model klasifikasi ini, proses prediksi kualitas wine dapat dilakukan secara otomatis berdasarkan pola yang dipelajari dari dataset training.

## Tujuan

Tujuan dari project ini adalah membuat model klasifikasi untuk memprediksi kualitas wine pada dataset testing. Model dilatih menggunakan dataset training yang sudah memiliki label `quality`.

Selain itu, project ini juga bertujuan untuk melakukan proses analisis data secara terstruktur, mulai dari membaca dataset, membersihkan data, melakukan preprocessing, membangun model, mengevaluasi model, menyimpan model, hingga menghasilkan file prediksi dalam format CSV.

## Dataset

Dataset yang digunakan terdiri dari dua file, yaitu:

1. `data_training.csv`
2. `data_testing.csv`

Dataset training digunakan untuk melatih model karena sudah memiliki kolom target `quality`. Sedangkan dataset testing digunakan untuk melakukan prediksi karena belum memiliki kolom `quality`.

Variabel yang terdapat dalam dataset adalah:

- `fixed acidity`
- `volatile acidity`
- `citric acid`
- `residual sugar`
- `chlorides`
- `free sulfur dioxide`
- `total sulfur dioxide`
- `density`
- `pH`
- `sulphates`
- `alcohol`
- `quality`
- `Id`

Kolom `quality` merupakan target prediksi, sedangkan kolom `Id` digunakan sebagai identitas setiap data.

## Proses Analisis

Tahap pertama yang dilakukan adalah membaca dataset training dan testing menggunakan library `pandas`. Setelah data berhasil dimuat, dilakukan pengecekan struktur data untuk memastikan bahwa seluruh kolom terbaca dengan benar.

Selanjutnya dilakukan pengecekan missing values pada dataset training dan testing. Hasil pengecekan menunjukkan bahwa tidak terdapat nilai kosong pada dataset, sehingga data dapat langsung digunakan tanpa perlu dilakukan imputasi atau penghapusan data.

Setelah itu, data dipisahkan menjadi fitur dan target. Kolom `quality` digunakan sebagai target, sedangkan kolom `Id` tidak digunakan sebagai fitur karena hanya berfungsi sebagai identitas data.

Tahap berikutnya adalah melakukan feature scaling menggunakan `StandardScaler`. Proses ini dilakukan agar setiap fitur memiliki skala yang lebih seimbang, karena setiap fitur memiliki rentang nilai yang berbeda-beda.

## Pembuatan Model

Model yang digunakan dalam project ini adalah `RandomForestClassifier`. Model ini dipilih karena cocok untuk kasus klasifikasi dan mampu menangani banyak fitur dengan baik.

Random Forest bekerja dengan membangun beberapa decision tree, kemudian menggabungkan hasil prediksi dari setiap tree untuk menghasilkan keputusan akhir. Model dilatih menggunakan dataset training yang telah melalui proses preprocessing.

## Evaluasi Model

Evaluasi model dilakukan menggunakan beberapa metrik, yaitu accuracy, confusion matrix, dan classification report.

Berdasarkan hasil evaluasi pada data training, model memperoleh akurasi sebesar 1.0 atau 100%. Hal ini menunjukkan bahwa model mampu memprediksi seluruh data training dengan benar.

Confusion matrix menunjukkan bahwa seluruh prediksi berada pada diagonal utama, yang berarti tidak terdapat kesalahan klasifikasi pada data training. Selain itu, classification report menunjukkan nilai precision, recall, dan f1-score sebesar 1.00 pada seluruh kelas `quality`.

Namun, hasil akurasi yang sangat tinggi perlu diperhatikan karena dapat mengindikasikan kemungkinan overfitting. Oleh karena itu, evaluasi tambahan menggunakan data validasi dapat dilakukan untuk mengetahui kemampuan model dalam memprediksi data baru secara lebih objektif.

## Hasil Prediksi

Setelah model selesai dilatih, model digunakan untuk memprediksi nilai `quality` pada dataset testing. Dataset testing hanya memiliki fitur kimia wine dan kolom `Id`, sehingga nilai `quality` diprediksi menggunakan model yang telah dibuat.

Hasil prediksi kemudian disusun dalam file CSV dengan format:

| Id | quality |
|---|---|
| 222 | 5 |
| 1514 | 6 |

File hasil prediksi hanya berisi dua kolom, yaitu `Id` dan `quality`, sesuai dengan format yang telah ditentukan.

## Kesimpulan

Berdasarkan seluruh tahapan yang telah dilakukan, model klasifikasi berhasil dibuat untuk memprediksi kualitas wine berdasarkan karakteristik kimia yang tersedia.

Proses analisis dimulai dari membaca dataset, mengecek missing values, melakukan feature scaling, membuat model Random Forest Classifier, mengevaluasi model, menyimpan model, hingga melakukan prediksi pada dataset testing.

Model menunjukkan performa yang sangat baik pada data training dengan akurasi 100%. Namun, karena hasil tersebut diperoleh dari data training, perlu diperhatikan kemungkinan overfitting. Untuk pengembangan selanjutnya, model dapat dievaluasi menggunakan data validasi atau metode train-test split.

## Recommendation

Beberapa rekomendasi untuk pengembangan model selanjutnya adalah:

1. Menggunakan data validasi agar performa model dapat diuji secara lebih objektif.
2. Melakukan hyperparameter tuning untuk mencari kombinasi parameter terbaik.
3. Mencoba model lain seperti Decision Tree, XGBoost, LightGBM, atau CatBoost sebagai perbandingan.
4. Melakukan analisis feature importance untuk mengetahui fitur kimia mana yang paling berpengaruh terhadap kualitas wine.
5. Memantau performa model jika digunakan pada data baru agar hasil prediksi tetap akurat.
