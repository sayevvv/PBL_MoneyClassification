# Monev - Intelligent Money Clasiifier

Proyek ini bertujuan untuk membangun sistem Machine Learning yang mampu mengenali dan mengklasifikasikan nominal uang kertas Rupiah Indonesia. Sistem ini memanfaatkan teknik Computer Vision untuk ekstraksi fitur dan membandingkan kinerja algoritma klasifikasi seperti Support Vector Machine atau SVM dan XGBoost.

## Daftar Isi

* Tentang Proyek
* Backend Flask
* Dataset
* Metodologi
* Model dan Evaluasi
* Struktur File
* Instalasi dan Penggunaan

## Tentang Proyek

Sistem ini dirancang untuk membedakan berbagai pecahan uang kertas Rupiah serta mengidentifikasi objek yang bukan uang. Pendekatan yang digunakan menggabungkan beberapa fitur visual yaitu Warna, Tekstur, dan Bentuk. Penggabungan ini menghasilkan identitas data yang kuat bagi model klasifikasi.

## Backend Flask

Proyek ini memiliki implementasi backend terpisah menggunakan Flask untuk kebutuhan deployment atau API.

**Repositori Backend**
Anda dapat mengakses kode sumber backend melalui tautan di bawah ini
https://github.com/sayevvv/Monev-BE

## Dataset

Dataset terdiri dari gambar uang kertas Rupiah yang diambil dari berbagai sudut dan kondisi pencahayaan. Kelas yang dikenali berdasarkan versi V3 adalah sebagai berikut.

* Rp 1.000
* Rp 2.000
* Rp 5.000
* Rp 10.000
* Rp 20.000
* Rp 50.000
* Rp 100.000
* Negative atau Bukan Uang

## Metodologi

Proses pengolahan data dibagi menjadi dua tahap utama sebelum masuk ke pemodelan.

### Preprocessing

Setiap citra masukan melalui tahapan berikut.

**Resize**
Citra diubah ukurannya menjadi 250x250 piksel untuk keseragaman data.

**Gaussian Blur**
Proses ini dilakukan untuk mengurangi noise pada gambar.

**Konversi Ruang Warna**
Mengubah format citra dari BGR ke HSV untuk fitur warna dan Grayscale untuk fitur tekstur serta bentuk.

### Ekstraksi Fitur

Model dilatih menggunakan gabungan tiga jenis fitur dengan total panjang vektor 469.

**Warna**
Menggunakan HSV Histogram yang mengambil data dari channel Hue dan Saturation untuk mengenali warna dominan uang.

**Tekstur**
Menggunakan Local Binary Pattern atau LBP uniform untuk mendeteksi pola unik pada tekstur kertas uang.

**Bentuk**
Menggunakan Hu Moments yang terdiri dari 7 invarian momen untuk mengenali karakteristik bentuk global objek.

## Model dan Evaluasi

Proyek ini mengeksplorasi dua algoritma utama dengan penyetelan hyperparameter.

### Support Vector Machine atau SVM V3

**Kernel**
RBF atau Radial Basis Function

**Performa**
Model ini mencapai akurasi sekitar 96% pada data uji menggunakan 8 kelas. Algoritma ini sangat baik dalam menangani data dengan dimensi tinggi.

### XGBoost V2

**Objective**
Multi-softmax

**Performa**
Model ini mencapai akurasi sekitar 99% pada data uji untuk 7 kelas uang. Algoritma ini dikenal cepat dan sangat akurat untuk data terstruktur.

## Struktur File

Berikut adalah penjelasan singkat mengenai file utama dalam repositori ini.

**PBL_PreprocessingV3.ipynb**
Ini adalah skrip rekomendasi terbaru. Notebook ini memproses dataset, mengekstraksi fitur gabungan, dan menangani 8 kelas termasuk kelas negative. Output dari proses ini adalah file fitur `features_X_v3.joblib`.

**PBL_SVMV3.ipynb**
Notebook ini digunakan untuk melatih model SVM menggunakan data dari Preprocessing V3. Di dalamnya mencakup evaluasi dan visualisasi prediksi.

**PBL_XGBOOSTV2.ipynb**
Notebook ini digunakan untuk melatih model XGBoost menggunakan data dari Preprocessing V2.

## Instalasi dan Penggunaan

Ikuti langkah berikut untuk menjalankan proyek ini di lingkungan lokal Anda.

### Requirements

Pastikan Anda telah menginstal library Python berikut
* opencv-python
* scikit-learn
* scikit-image
* xgboost
* matplotlib
* seaborn
* joblib
* tqdm

### Cara Menjalankan

**Siapkan Dataset**
Letakkan gambar uang Anda dalam folder yang terpisah berdasarkan kelasnya.

**Jalankan Preprocessing**
Buka file `PBL_PreprocessingV3.ipynb` lalu sesuaikan direktori dataset Anda. Jalankan semua sel untuk menghasilkan file fitur.

**Latih Model**
Buka file `PBL_SVMV3.ipynb`, pastikan path ke file fitur sudah benar, lalu jalankan training.

---
*Dibuat untuk memenuhi tugas Project Based Learning.*
