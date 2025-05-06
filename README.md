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
- Dataset Beijing PM2.5 dari UCI Machine Learning Repository (https://archive.ics.uci.edu/dataset/381/beijing%2Bpm2%2B5%2Bdata)
- Dataset yang digunakan berasal dari data observasi polusi udara di China dari tahun 2010 hingga 2014
- Jumlah baris dan kolom: (43824, 13)
- missing values: 2067 pada kolom pm2.5

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- `pm2.5` : Konsentrasi partikel PM2.5 dalam mikrogram per meter kubik (µg/m³)
- `DEWP` : Suhu titik embun (dew point temperature) dalam derajat Celsius
- `TEMP` : Suhu udara dalam derajat Celsius
- `PRES` : Tekanan atmosfer dalam hPa (hectopascal)
- `cbwd` : Arah angin
- `Iws` : Kecepatan angin kumulatif dalam m/s
- `Is` : Jumlah jam hujan ringan dalam satu jam
- `Ir` : Jumlah jam hujan lebat dalam satu jam

### Visualisasi Data
![image](https://github.com/user-attachments/assets/d9ccffa0-9d2e-4df7-a2ea-787e5196ca19)

Dari visualisasi distribusi PM2.5 jelas menunjukkan distribusi yang right-skewed, artinya mayoritas nilai PM2.5 berada di kisaran rendah, tapi ada sebagian kecil data dengan nilai sangat tinggi (outlier).

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

### Hasil Evaluasi
Evaluasi dilakukan pada empat model berbeda:

| Model               | MAE       | RMSE      | R² Score |
| ------------------- | --------- | --------- | -------- |
| Linear Regression   | 57.43     | 81.04     | 0.25     |
| Random Forest       | 49.90     | 75.24     | 0.36     |
| Tuned Random Forest | 48.70     | 72.10     | 0.41     |
| XGBoost             | **46.46** | **70.94** | **0.43** |

> Dari hasil evaluasi di atas, terlihat bahwa model XGBoost memiliki performa terbaik dengan nilai MAE dan RMSE paling rendah serta R² Score tertinggi. Hal ini berarti XGBoost mampu memprediksi nilai PM2.5 dengan kesalahan paling kecil dan menjelaskan sekitar 43% variasi dalam data target.

PM2.5 adalah nilai kontinu, RMSE membantu mengidentifikasi error besar akibat lonjakan PM2.5 yang berbahaya secara kesehatan, sedangkan MAE memberikan gambaran kesalahan umum. R² membantu menilai seberapa baik fitur menjelaskan fluktuasi kualitas udara. Dari hasil evaluasi ini, dapat disimpulkan model XGBoost merupakan model paling optimal untuk permasalahan prediksi kualitas udara pada proyek ini.

