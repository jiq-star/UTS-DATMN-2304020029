# Prediksi Kualitas Wine 

## Konteks

Dalam industri wine, kualitas produk menjadi salah satu faktor penting yang dapat memengaruhi kepuasan konsumen dan nilai jual produk. Kualitas wine dapat dipengaruhi oleh berbagai karakteristik kimia, seperti tingkat keasaman, kadar alkohol, pH, kandungan sulfur dioxide, sulphates, dan beberapa faktor lainnya.

Penilaian kualitas wine secara manual dapat membutuhkan waktu dan bergantung pada subjektivitas penilai. Oleh karena itu, pendekatan berbasis machine learning dapat digunakan untuk membantu memprediksi kualitas wine secara lebih cepat dan konsisten berdasarkan data karakteristik kimia yang tersedia.

---

## Problem Statement

Permasalahan dalam project ini adalah bagaimana membuat model klasifikasi yang mampu memprediksi nilai `quality` pada wine berdasarkan fitur-fitur kimia yang tersedia.

Dataset training memiliki kolom `quality` sebagai target, sedangkan dataset testing tidak memiliki kolom `quality`, sehingga nilai tersebut perlu diprediksi menggunakan model yang telah dibuat.

Dengan adanya model klasifikasi ini, proses prediksi kualitas wine dapat dilakukan secara otomatis berdasarkan pola yang dipelajari dari dataset training.

---

## Tujuan

Tujuan dari project ini adalah membuat model klasifikasi untuk memprediksi kualitas wine pada dataset testing. Model dilatih menggunakan dataset training yang sudah memiliki label `quality`.

Selain itu, project ini juga bertujuan untuk melakukan proses analisis data secara terstruktur, mulai dari membaca dataset, membersihkan data, melakukan preprocessing, membangun model, mengevaluasi model, menyimpan model, hingga menghasilkan file prediksi dalam format CSV.

---

## Dataset

Dataset yang digunakan terdiri dari dua file, yaitu:

1. `data_training.csv`
2. `data_testing.csv`

Dataset training digunakan untuk melatih model karena sudah memiliki kolom target `quality`, sedangkan dataset testing digunakan untuk melakukan prediksi karena belum memiliki kolom `quality`.

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

---

## 1. Import Library

Pada tahap awal, dilakukan import library yang dibutuhkan. Library `pandas` digunakan untuk membaca dan mengolah dataset. Library `joblib` digunakan untuk menyimpan model yang telah dibuat. Sementara itu, library dari `sklearn` digunakan untuk preprocessing, pembuatan model klasifikasi, dan evaluasi model.

```python
import pandas as pd
import joblib

from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report
```

---

## 2. Load Dataset

Langkah berikutnya adalah membaca dataset training dan testing menggunakan fungsi `read_csv()`. Dataset training digunakan untuk melatih model, sedangkan dataset testing digunakan untuk proses prediksi akhir.

```python
data_training = pd.read_csv('/content/data_training.csv')
data_testing = pd.read_csv('/content/data_testing.csv')

data_training.head()
```

Berdasarkan tampilan awal dataset training, data memiliki beberapa fitur kimia wine seperti `fixed acidity`, `volatile acidity`, `citric acid`, `residual sugar`, `chlorides`, `free sulfur dioxide`, `total sulfur dioxide`, `density`, `pH`, `sulphates`, dan `alcohol`. Selain itu, terdapat kolom `quality` sebagai target prediksi dan kolom `Id` sebagai identitas setiap data.

---

## 3. Pembersihan Data

Sebelum model dibuat, dilakukan pengecekan missing values pada dataset training dan testing. Tahap ini penting karena nilai kosong dapat memengaruhi proses pelatihan model.

```python
print("Missing Values Data Training:")
print(data_training.isnull().sum())

print("\nMissing Values Data Testing:")
print(data_testing.isnull().sum())
```

Berdasarkan hasil pengecekan, tidak terdapat missing values pada dataset. Dengan demikian, data dapat langsung digunakan tanpa perlu dilakukan penghapusan data atau imputasi nilai kosong.

Apabila terdapat missing values, salah satu cara penanganannya adalah dengan mengisi nilai kosong menggunakan rata-rata dari masing-masing kolom numerik.

```python
data_training = data_training.fillna(data_training.mean(numeric_only=True))
data_testing = data_testing.fillna(data_testing.mean(numeric_only=True))
```

---

## 4. Memisahkan Fitur dan Target

Pada tahap ini, dataset training dipisahkan menjadi fitur dan target. Kolom `quality` digunakan sebagai target karena nilai tersebut yang ingin diprediksi oleh model. Kolom `Id` tidak digunakan sebagai fitur karena hanya berfungsi sebagai identitas data.

```python
X = data_training.drop(columns=['quality', 'Id'])
y = data_training['quality']

X_testing = data_testing.drop(columns=['Id'])
```

Variabel `X` berisi fitur-fitur kimia wine, sedangkan variabel `y` berisi label atau target berupa nilai `quality`. Untuk dataset testing, kolom `Id` dipisahkan karena tidak digunakan dalam proses prediksi.

---

## 5. Feature Scaling

Setiap fitur pada dataset memiliki rentang nilai yang berbeda-beda. Misalnya, nilai `total sulfur dioxide` dapat lebih besar dibandingkan nilai `pH` atau `chlorides`. Oleh karena itu, dilakukan feature scaling menggunakan `StandardScaler` agar setiap fitur memiliki skala yang lebih seimbang.

```python
scaler = StandardScaler()

X_scaled = scaler.fit_transform(X)
X_testing_scaled = scaler.transform(X_testing)
```

Pada proses ini, `fit_transform()` digunakan pada data training agar scaler mempelajari skala dari data training. Sedangkan `transform()` digunakan pada data testing agar data testing mengikuti skala yang sama dengan data training.

---

## 6. Pembuatan Model Klasifikasi

Model yang digunakan dalam project ini adalah `RandomForestClassifier`. Model ini dipilih karena cocok untuk kasus klasifikasi dan mampu menangani banyak fitur dengan baik. Random Forest bekerja dengan membangun banyak decision tree, kemudian menggabungkan hasil prediksi dari setiap tree untuk menghasilkan keputusan akhir.

```python
model = RandomForestClassifier(
    n_estimators=300,
    random_state=42,
    class_weight='balanced'
)
```

Parameter `n_estimators=300` menunjukkan bahwa model menggunakan 300 pohon keputusan. Parameter `random_state=42` digunakan agar hasil model tetap konsisten ketika kode dijalankan ulang. Sedangkan `class_weight='balanced'` digunakan untuk membantu model dalam menangani kemungkinan ketidakseimbangan jumlah data pada setiap kelas `quality`.

---

## 7. Training Model

Setelah model dibuat, langkah berikutnya adalah melatih model menggunakan dataset training yang sudah melalui proses scaling. Pada tahap ini, model mempelajari hubungan antara fitur-fitur kimia wine dengan nilai `quality`.

```python
model.fit(X_scaled, y)
```

Setelah proses training selesai, model sudah dapat digunakan untuk mengenali pola kualitas wine berdasarkan karakteristik kimia yang tersedia.

---

## 8. Evaluasi Model

Evaluasi model dilakukan untuk mengetahui performa model terhadap data training. Metrik evaluasi yang digunakan adalah accuracy, confusion matrix, dan classification report.

```python
y_pred = model.predict(X_scaled)

accuracy = accuracy_score(y, y_pred)
print("Accuracy :", accuracy)

print(confusion_matrix(y, y_pred))
print(classification_report(y, y_pred))
```

Berdasarkan hasil evaluasi, model memperoleh akurasi sebesar `1.0` atau 100%. Hal ini menunjukkan bahwa model mampu memprediksi seluruh data training dengan benar.

Confusion matrix menunjukkan bahwa seluruh prediksi berada pada diagonal utama. Artinya, setiap kelas `quality` berhasil diprediksi sesuai dengan kelas aslinya dan tidak terdapat kesalahan klasifikasi pada data training.

Classification report juga menunjukkan nilai precision, recall, dan f1-score sebesar `1.00` pada seluruh kelas. Hal ini menunjukkan bahwa model memiliki performa yang sangat baik dalam mengenali pola pada dataset training.

Namun, hasil akurasi yang sangat tinggi perlu diperhatikan karena dapat mengindikasikan kemungkinan overfitting. Oleh karena itu, evaluasi tambahan menggunakan data validasi dapat dilakukan agar performa model terhadap data baru dapat dinilai secara lebih objektif.

---

## 9. Menyimpan Model

Setelah model selesai dilatih, model disimpan menggunakan `joblib`. Penyimpanan model dilakukan agar model dapat digunakan kembali tanpa perlu melakukan proses training ulang.

```python
joblib.dump(model, 'model_klasifikasi_wine.pkl')
```

File model disimpan dalam format `.pkl` karena yang disimpan adalah model machine learning, bukan hasil prediksi. File hasil prediksi nantinya akan disimpan dalam format `.csv`.

---

## 10. Prediksi Data Testing

Setelah model terlatih, model digunakan untuk memprediksi nilai `quality` pada dataset testing. Dataset testing hanya memiliki fitur-fitur kimia wine dan kolom `Id`, sehingga nilai `quality` harus diprediksi menggunakan model yang telah dibuat.

```python
prediksi_quality = model.predict(X_testing_scaled)
```

Pada tahap ini, model menghasilkan prediksi nilai `quality` berdasarkan pola yang telah dipelajari dari dataset training.

---

## 11. Membuat DataFrame Hasil Prediksi

Hasil prediksi kemudian disusun ke dalam dataframe baru. Dataframe ini hanya berisi dua kolom, yaitu `Id` dan `quality`, sesuai dengan format yang diminta.

```python
hasil_prediksi = pd.DataFrame({
    'Id': data_testing['Id'],
    'quality': prediksi_quality
})

hasil_prediksi.head()
```

Kolom `Id` digunakan sebagai identitas setiap data pada dataset testing, sedangkan kolom `quality` merupakan hasil prediksi kualitas wine dari model klasifikasi.

---

## 12. Menyimpan Hasil Prediksi ke CSV

Tahap terakhir adalah menyimpan hasil prediksi ke dalam file CSV. File ini menjadi output akhir dari proses prediksi kualitas wine.

```python
hasil_prediksi.to_csv('hasilprediksi_3digitNIMterakhir.csv', index=False)
```

File CSV yang dihasilkan hanya berisi dua kolom, yaitu `Id` dan `quality`, sesuai dengan format hasil prediksi yang telah ditentukan.

---

## Hasil

Model Random Forest Classifier berhasil dibuat dan digunakan untuk memprediksi kualitas wine. Berdasarkan evaluasi pada data training, model memperoleh akurasi sebesar 100%. Hasil confusion matrix menunjukkan bahwa seluruh data training berhasil diklasifikasikan dengan benar. Selain itu, classification report menunjukkan nilai precision, recall, dan f1-score sebesar 1.00 pada seluruh kelas `quality`.

Hasil prediksi pada dataset testing kemudian disimpan dalam bentuk file CSV dengan format sebagai berikut:

| Id | quality |
|---|---|
| 222 | 5 |
| 1514 | 6 |
| 417 | 5 |

Tabel tersebut menunjukkan bahwa setiap data pada dataset testing memiliki `Id` sebagai identitas dan `quality` sebagai hasil prediksi dari model.

---

## Kesimpulan

Berdasarkan seluruh tahapan yang telah dilakukan, model klasifikasi berhasil dibuat untuk memprediksi kualitas wine berdasarkan fitur-fitur kimia yang tersedia. Proses analisis dimulai dari membaca dataset, mengecek missing values, memisahkan fitur dan target, melakukan feature scaling, membuat model Random Forest Classifier, melatih model, mengevaluasi model, menyimpan model, hingga melakukan prediksi pada dataset testing.

Model menunjukkan performa yang sangat baik pada data training dengan akurasi 100%. Namun, karena hasil tersebut diperoleh dari data training, perlu diperhatikan kemungkinan overfitting. Oleh karena itu, untuk pengembangan selanjutnya, model dapat dievaluasi menggunakan data validasi atau metode train-test split agar kemampuan model dalam memprediksi data baru dapat diukur secara lebih objektif.

---

## Recommendation

Beberapa rekomendasi untuk pengembangan model selanjutnya adalah:

1. Menggunakan data validasi atau train-test split agar performa model dapat diuji secara lebih objektif.
2. Melakukan hyperparameter tuning untuk mencari kombinasi parameter terbaik pada model Random Forest.
3. Mencoba model lain seperti Decision Tree, XGBoost, LightGBM, atau CatBoost sebagai perbandingan.
4. Melakukan analisis feature importance untuk mengetahui fitur kimia mana yang paling berpengaruh terhadap kualitas wine.
5. Memantau performa model jika digunakan pada data baru agar hasil prediksi tetap akurat.
