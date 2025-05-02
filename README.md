# Laporan Proyek Machine Learning - Anissa Shanniyah Aprilia

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
- Dataset: Dataset Beijing PM2.5 dari UCI Machine Learning Repository (https://archive.ics.uci.edu/ml/datasets/Beijing+PM2.5+Data)
- Deskripsi: Dataset ini berisi data cuaca (suhu, titik embun, tekanan, dll.) dan level PM2.5 di Beijing.

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- pm2.5 : Konsentrasi partikel PM2.5 dalam mikrogram per meter kubik (µg/m³)
- DEWP : Suhu titik embun (dew point temperature) dalam derajat Celsius
- TEMP : Suhu udara dalam derajat Celsius
- PRES : Tekanan atmosfer dalam hPa (hectopascal)
- cbwd : Arah angin
- Iws : Kecepatan angin kumulatif dalam m/s
- Is : Jumlah jam hujan ringan dalam satu jam
- Ir : Jumlah jam hujan lebat dalam satu jam

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.

## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**
