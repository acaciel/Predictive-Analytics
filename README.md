# Laporan Proyek Machine Learning - Anissa Shanniyah Aprilia

## Domain Proyek

Proyek ini berfokus pada domain **analitik prediktif dalam kualitas udara**, khususnya dalam memprediksi nilai *PM2.5* (partikulat berukuran kecil) berdasarkan fitur cuaca dan polusi udara lainnya. Prediksi *PM2.5* sangat penting karena partikel ini dapat menyebabkan masalah kesehatan yang serius jika kadarnya melebihi ambang batas aman.

### Mengapa Masalah Ini Penting?

Menurut WHO, paparan jangka panjang terhadap PM2.5 dapat meningkatkan risiko penyakit kardiovaskular, paru-paru, dan bahkan kematian dini. Oleh karena itu, membangun model prediksi yang andal untuk memantau kadar PM2.5 bisa menjadi langkah penting dalam pengambilan keputusan untuk kesehatan publik.

## Business Understanding

### Problem Statements
1. Bagaimana memprediksi kadar PM2.5 berdasarkan fitur-fitur cuaca dan polusi udara lainnya?
2. Fitur apa yang paling berpengaruh terhadap kadar PM2.5?

### Goals
1. Menghasilkan model prediksi untuk kadar PM2.5 dengan akurasi evaluasi yang baik.
2. Mengidentifikasi fitur paling signifikan terhadap PM2.5 melalui proses modeling.

### Solution Statements
* Membangun beberapa model regresi seperti **Linear Regression**, **Random Forest Regressor**, dan **XGBoost Regressor**.
* Melakukan **hyperparameter tuning** menggunakan `GridSearchCV` dan `RandomizedSearchCV` untuk model yang kompleks.
* Mengukur performa menggunakan **MAE**, **RMSE**, dan **R² score**.

## Data Understanding

Dataset yang digunakan berasal dari data observasi polusi udara di China dari tahun 2010 hingga 2014, berisi informasi seperti:

* `pm2.5`: konsentrasi partikulat PM2.5 (target variabel)
* `DEWP`: tekanan titik embun
* `TEMP`: temperatur
* `PRES`: tekanan udara
* `cbwd`: arah angin gabungan
* `Iws`: kecepatan angin kumulatif
* `Is`: kecepatan angin
* `Ir`: curah hujan kumulatif

Data dimuat dari file:
`PRSA_data_2010.1.1-2014.12.31.csv`

Contoh snippet pemuatan data:

```python
data = pd.read_csv('/content/drive/MyDrive/PRSA_data_2010.1.1-2014.12.31.csv')
data.head()
```

---

## Data Preparation

### Tahapan yang Dilakukan

1. **Pembersihan Data**
   * Menghapus nilai null pada kolom `pm2.5`
   * Konversi kolom tanggal (`year`, `month`, `day`, `hour`) menjadi datetime
   * Menghapus kolom yang tidak relevan (seperti `No`)

2. **Feature Engineering**
   * Membuat fitur waktu tambahan (`dayofweek`, `hour`)
   * Menggunakan one-hot encoding untuk fitur kategorikal `cbwd`

3. **Feature Scaling**
   * Menggunakan `StandardScaler` pada fitur numerik sebelum modeling.

## Modeling
Tiga algoritma yang digunakan dalam modeling:
### 1. Linear Regression
* Baseline model
* Hasil: cepat dilatih, namun memiliki performa kurang baik pada data non-linear.

### 2. Random Forest Regressor
* Mengurangi overfitting dengan pengambilan rata-rata banyak pohon keputusan
* Hyperparameter tuning menggunakan `GridSearchCV`

### 3. XGBoost Regressor
* Model boosting yang sangat efisien dan akurat
* Hyperparameter tuning menggunakan `RandomizedSearchCV`
* Model terbaik berdasarkan evaluasi metrik.

## Evaluation
### Metrik yang Digunakan
* **MAE (Mean Absolute Error)**: rata-rata absolut selisih antara nilai prediksi dan aktual.
* **RMSE (Root Mean Squared Error)**: akar dari rata-rata kuadrat kesalahan, sensitif terhadap outlier.
* **R² Score**: seberapa besar variasi target dijelaskan oleh model (semakin mendekati 1, semakin baik).

### Hasil Evaluasi (contoh)

| Model             | MAE  | RMSE | R² Score |
| ----------------- | ---- | ---- | -------- |
| Linear Regression | 46.2 | 61.3 | 0.54     |
| Random Forest     | 28.9 | 39.7 | 0.81     |
| XGBoost           | 26.5 | 36.8 | 0.85     |

> Berdasarkan hasil di atas, **XGBoost Regressor** menjadi model terbaik karena memiliki R² tertinggi dan error terendah.


---

## Domain Proyek
Mengapa dan bagaimana masalah ini harus diselesaikan?

Polusi udara, terutama konsentrasi PM2.5 (partikulat halus dengan diameter kurang dari 2.5 mikrometer), merupakan salah satu ancaman besar terhadap kesehatan manusia, terutama di kota-kota besar yang padat penduduk. PM2.5 dapat terhirup ke dalam saluran pernapasan dan menyebabkan berbagai penyakit, seperti asma, bronkitis, bahkan meningkatkan risiko kanker paru-paru dan penyakit jantung. Organisasi Kesehatan Dunia (WHO) mencatat bahwa polusi udara menyebabkan lebih dari 4 juta kematian premature setiap tahunnya di seluruh dunia.

Di banyak kota besar, data tentang kualitas udara dan konsentrasi PM2.5 sangat penting untuk mengambil langkah-langkah preventif dalam mengurangi dampaknya terhadap kesehatan masyarakat. Oleh karena itu, memprediksi level PM2.5 dengan akurat dapat memberikan manfaat besar, seperti membantu pemerintah dan lembaga kesehatan dalam merancang kebijakan pengelolaan polusi, serta memberi informasi kepada masyarakat agar dapat menghindari paparan polusi saat kualitas udara buruk.

Salah satu pendekatan untuk mengatasi masalah polusi udara adalah dengan memanfaatkan teknologi machine learning untuk memprediksi konsentrasi PM2.5. Dengan mengumpulkan data terkait faktor-faktor yang mempengaruhi kualitas udara, seperti suhu, kelembaban, tekanan atmosfer, dan kecepatan angin, kita dapat membangun model yang dapat memprediksi tingkat polusi udara (PM2.5) pada waktu tertentu.

Metode ini memungkinkan untuk memberikan peringatan dini mengenai kualitas udara dan dapat digunakan untuk perencanaan jangka panjang dalam mengurangi polusi udara. Dengan memanfaatkan model prediktif, kita dapat memperkirakan kondisi kualitas udara di masa depan berdasarkan data historis dan kondisi cuaca saat ini, yang dapat memberikan waktu bagi individu dan pihak berwenang untuk mengambil tindakan mitigasi.

## Business Understanding
### Problem Statements
Pernyataan Masalah: Level PM2.5 adalah masalah kesehatan utama, dan memprediksinya dapat membantu manajemen kesehatan masyarakat dan kebijakan lingkungan.

### Goals
Tujuan: Membangun model regresi untuk memprediksi konsentrasi PM2.5 berdasarkan data cuaca dan faktor kualitas udara lainnya.

### Solution statements
Pernyataan Solusi: Menggunakan algoritma machine learning seperti Linear Regression dan Random Forest Regressor untuk memprediksi level PM2.5, dievaluasi menggunakan metrik kinerja seperti RMSE.

## Data Understanding
- Dataset Beijing PM2.5 dari UCI Machine Learning Repository (https://archive.ics.uci.edu/dataset/381/beijing%2Bpm2%2B5%2Bdata)
- Dataset ini berisi data cuaca (suhu, titik embun, tekanan, dll.) dan level PM2.5 di Beijing.
- Jumlah baris dan kolom: (43824, 13)
- missing values: 2067 pada kolom pm2.5

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- pm2.5 : Konsentrasi partikel PM2.5 dalam mikrogram per meter kubik (µg/m³)
- DEWP : Suhu titik embun (dew point temperature) dalam derajat Celsius
- TEMP : Suhu udara dalam derajat Celsius
- PRES : Tekanan atmosfer dalam hPa (hectopascal)
- cbwd : Arah angin
- Iws : Kecepatan angin kumulatif dalam m/s
- Is : Jumlah jam hujan ringan dalam satu jam
- Ir : Jumlah jam hujan lebat dalam satu jam

### Visualisasi Data
![image](https://github.com/user-attachments/assets/d9ccffa0-9d2e-4df7-a2ea-787e5196ca19)

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.
📈 Hasil Evaluasi Proyek
Evaluasi dilakukan pada empat model berbeda:

| Model               | MAE       | RMSE      | R² Score |
| ------------------- | --------- | --------- | -------- |
| Linear Regression   | 57.43     | 81.04     | 0.25     |
| Random Forest       | 49.90     | 75.24     | 0.36     |
| Tuned Random Forest | 48.70     | 72.10     | 0.41     |
| XGBoost             | **46.46** | **70.94** | **0.43** |

Dari hasil evaluasi di atas, terlihat bahwa model XGBoost memiliki performa terbaik dengan nilai MAE dan RMSE paling rendah serta R² Score tertinggi. Hal ini berarti XGBoost mampu memprediksi nilai PM2.5 dengan kesalahan paling kecil dan menjelaskan sekitar 43% variasi dalam data target.

PM2.5 adalah nilai kontinu, RMSE membantu mengidentifikasi error besar akibat lonjakan PM2.5 yang berbahaya secara kesehatan, sedangkan MAE memberikan gambaran kesalahan umum. R² membantu menilai seberapa baik fitur menjelaskan fluktuasi kualitas udara. Dari hasil evaluasi ini, dapat disimpulkan model XGBoost merupakan model paling optimal untuk permasalahan prediksi kualitas udara pada proyek ini.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.

## Evaluation
Metrik Evaluasi yang Digunakan
Dalam proyek ini, digunakan tiga metrik utama untuk mengevaluasi kinerja model regresi dalam memprediksi kadar PM2.5, yaitu:

1. Mean Absolute Error (MAE)
MAE mengukur rata-rata selisih absolut antara nilai aktual dengan prediksi. Metrik ini mudah diinterpretasikan karena berada dalam satuan yang sama dengan target (µg/m³).
Nilai MAE yang lebih kecil menunjukkan bahwa model melakukan prediksi yang lebih akurat secara umum.

2. Root Mean Squared Error (RMSE)
RMSE menghitung akar dari rata-rata kuadrat selisih antara prediksi dan nilai aktual. Metrik ini lebih sensitif terhadap error besar karena adanya pemangkatan.
Semakin kecil RMSE, semakin baik performa model. Cocok digunakan saat outlier penting untuk diperhatikan.

3. R-squared (R² Score)
R² mengukur seberapa baik model menjelaskan variasi dari target. Nilai R² berkisar dari 0 hingga 1.
Nilai R² yang lebih tinggi menunjukkan bahwa model menjelaskan lebih banyak variasi dalam data target.
