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
- Jumlah data: Dataset terdiri dari 43.824 baris dan 13 kolom.
- missing values: Terdapat 2.067 nilai kosong pada kolom pm2.5
- tidak terdapat data duplikat

### Variabel-variabel pada Dataset Beijing PM2.5 adalah sebagai berikut:
- `No` : nomor baris dataset
- `year` : tahun pengukuran
- `month` : bulan pengukuran
- `day` : hari pengukuran
- `hour` : jam pengukuran
- `pm2.5` : Konsentrasi partikel PM2.5 dalam mikrogram per meter kubik (µg/m³)
- `DEWP` : Suhu titik embun (°C)
- `TEMP` : Suhu udara (°C)
- `PRES` : Tekanan atmosfer dalam hPa (hectopascal)
- `cbwd` : Arah angin
- `Iws` : Kecepatan angin kumulatif (m/s)
- `Is` : Jumlah jam hujan ringan dalam satu jam
- `Ir` : Jumlah jam hujan lebat dalam satu jam

### Visualisasi Data
![image](https://github.com/user-attachments/assets/d9ccffa0-9d2e-4df7-a2ea-787e5196ca19)

Dari visualisasi distribusi PM2.5 jelas menunjukkan distribusi yang right-skewed, artinya mayoritas nilai PM2.5 berada di kisaran rendah, tapi ada sebagian kecil data dengan nilai sangat tinggi (outlier).

## Data Preparation

### Tahapan yang Dilakukan

1. **Data Cleaning**
   * Menghapus baris yang memiliki nilai null pada kolom `pm2.5` menggunakan `dropna()`.
   * Kolom waktu (`year`, `month`, `day`, `hour`) digabung menjadi satu kolom `datetime`.
   * Menetapkan kolom `datetime` sebagai index.
   * Menghapus kolom yang tidak relevan (seperti `No`)

2. **Encoding Fitur Kategorikal**
   * Menggunakan one-hot encoding untuk fitur kategorikal `cbwd`
  
3. **Feature Selection & Target**
   * Fitur numerik + one-hot `cbwd` digunakan sebagai input
   * `pm2.5` sebagai target

4. **Feature Scaling**
   * Menggunakan `StandardScaler` untuk normalisasi fitur numerik sebelum modeling.

5. **Data Splitting**
   * Dataset dibagi menjadi data training dan testing dengan rasio 80:20 menggunakan `train_test_split` dan `random_state=42`.

> **Catatan khusus untuk model Random Forest (Awal)**
> Model Random Forest pertama menggunakan pipeline persiapan data yang berbeda:
>
> * Setelah `dropna()`, fitur yang digunakan hanya: `DEWP`, `TEMP`, `PRES`, `Iws`, `Is`, dan `Ir`.
> * Fitur `cbwd` tidak diolah atau di-encode.
> * Tidak dilakukan scaling karena Random Forest tidak sensitif terhadap skala fitur.
> * Hal ini merupakan alasan mengapa model ini memiliki performa lebih rendah dibanding model dengan pipeline utama.

## Model Development
Tiga algoritma yang digunakan dalam modeling:
### 1. Linear Regression
* **Cara kerja**: Mencari garis lurus terbaik untuk memetakan hubungan antara fitur dan target.
* **Parameter**: Default.
* **Persiapan Data**: Menggunakan dataset dengan fitur hasil one-hot encoding dan hasil scaling.
* **Kelebihan**: Cepat dan mudah digunakan, tapi kurang cocok untuk data yang tidak linear.

### 2. Random Forest Regressor (Awal)
* **Deskripsi**: Model ensemble berbasis decision tree, digunakan sebelum dilakukan tuning.
* **Parameter**:

  * `random_state = 42`
* **Persiapan Data**: Menggunakan fitur numerik tanpa scaling dan tanpa encoding pada `cbwd`.
* **Kelebihan**: Cocok untuk data non-linear, robust terhadap outlier dan noise.
* **Catatan**: Performanya lebih rendah dibanding versi yang dituning karena pipeline persiapan datanya lebih sederhana.

### 3. Tuned Random Forest Regressor
* **Deskripsi**: Versi Random Forest yang dituning menggunakan GridSearchCV.
* **Cara Kerja**: Ensemble learning dengan banyak decision tree, hasil prediksi diambil rata-rata
* **Parameter terbaik hasil tuning**:

  * `n_estimators = 100`
  * `max_depth = 10`
  * `min_samples_split = 5`
  * `min_samples_leaf = 2`
  * `random_state = 42`
* **Persiapan Data**: Menggunakan fitur hasil one-hot encoding dan hasil scaling.
* **Hasil dan Kelebihan**: Meningkatkan akurasi dibanding Random Forest awal, tahan terhadap overfitting, serta menangani non-linearitas
  
### 4. XGBoost Regressor
* **Deskripsi**: Algoritma boosting yang efektif dan efisien.
* **Cara kerja**: Boosting bertahap, tree berikutnya fokus pada kesalahan model sebelumnya
* **Parameter**:

  * `n_estimators = 200`
  * `max_depth = 10`
  * `learning_rate = 0.1`
  * `random_state = 42`
* **Persiapan Data**: Sama seperti model Tuned RF.
* **Hasil dan Kelebihan**: Cepat, efisien, dan akurat; model dengan performa terbaik dalam proyek ini.

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
