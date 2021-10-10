# Laporan Proyek Machine Learning - Tuti Amalia

## Domain Proyek
Domain proyek yang dipilih dalam proyek machine learning yakni bisnis dengan judul proyek "Prediksi Jenis Lonjakan Biaya pada Jasa Pelayanan Taksi di India"
-   Latar Belakang
    Layanan agregator taksi menjadi populer saat ini dan pengguna dapat mengunduh aplikasi mereka di ponsel cerdas/_smartphone_ dan memesan taksi dari mana saja di kota tempat mereka beroperasi. Aplikasi ini akan mencari taksi dari berbagai penyedia layanan dan memberikan opsi terbaik kepada klien mereka di seluruh opsi yang tersedia. Salah satu layanan agregator taksi India, yakni **Sigma Cabs**. Mereka beroperasi selama beberapa tahun. Selama periode ini, mereka telah menangkap jenis harga lonjakan dari penyedia layanan. Sehingga, pada proyek ini perlu dilakukan untuk membangun model prediktif yang dapat membantu menentukan jenis lonjakan biaya untuk setiap perjalanan berdasarkan karakteristiknya. Ini dapat membantu mengalokasikan sumber daya secara efektif dan meningkatkan efisiensi transportasi.

## Business Understanding
### Problem Statements
Berikut merupakan rincian masalah yang dapat diselesaikan pada proyek ini:
- Bagaimana teknik _preprocessing_ agar data dapat digunakan untuk membuat model yang baik?
- Bagaimana cara membuat model _machine learning_ untuk mengklasifikasi jenis lonjakan biaya pada jasa pelayanan taksi?

### Goals
Berikut adalah tujuan dari dibuatnya proyek ini:
- Melakukan teknik _preprocessing_ agar data dapat digunakan untuk membuat model yang baik
- Membuat model _machine learning_ untuk mengklasifikasi jenis lonjakan biaya pada jasa pelayanan taksi.

### Solution statements
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini diantaranya:
- Untuk preprocessing data dapat dilakukan dengan beberapa teknik, sebagai berikut:
  - Mengatasi data yang kosong atau _missing value_ dengan nilai rata-rata dan mode kolom.
  - Encoding Fitur Kategori menggunakan **One Hot Encoding**
  - Melakukan pembagian dataset dengan **Train/test split**
  - Standarisasi nilai data pada semua fitur dengan **StandarScaler**
- Untuk pembuatan model dipilih dengan menggunakan model klasifikasi dengan algoritma Random Forest dan LightGBM. Berikut penjelasan dari kedua model yang akan digunakan:
  - Random Forest 
    Metode Random Forst merupakan salah satu metode dalam _Decision Tree_. Random Forest adalah kombinasi dari masing-masing _tree_ yang baik kemudian dikombinasikan ke dalam satu model. Random Forest bergantung pada sebuah nilai _vector random_ dengan distribusi yang sama pada semua pohon yang masing-masing _decision tree_ memiliki kedalaman yang maksimal. Random forest adalah _classifier_ yang terdiri dari _classifier_ yang berbentuk pohon {h(**x**, θ k), k = 1, ...} dimana θk adalah _random vector_ yang didistribusikan secara independen dan masing-masing _tree_ pada sebuah unit akan memilih _class_ yang paling populer pada input x [[1](https://machinelearning.mipa.ugm.ac.id/2018/07/28/random-forest/)]. 
    Kelebihan dari algoritma Random Forest yakni mengatasi _noise_ dan _missing value_ serta dapat mengatasi data dalam jumlah yang besar. Adapun kekurangannya yakni interpretasi yang sulit dan membutuhkan tuning model yang tepat untuk data.
    
  - LightGBM
    LightGBM (Light Gradient Boosting Machine) adalah algoritma berbasi histogram yang menempatkan nilai kontinu ke dalam tong diskrit, yang mengarah pada pelatihan yang lebih cepat dan penggunaan memori yang lebih efisien [[2](https://zephyrnet.com/id/lightgbm-a-highly-efficient-gradient-boosting-decision-tree/)].
    Kelebihan dari LGBM yakni:
    - Kecepatan pelatihan lebih cepat dan efisiensi lebih tinggi
    - Penggunaan memori lebih rendah
    - Mampu menangani data skala besar
    
## Data Understanding
![1](https://user-images.githubusercontent.com/44547435/136661921-11a5d21a-afa1-4d8a-85ff-8259fd858042.png)
Informasi dataset dapat dilihat pada tabel dibawah ini :

| Jenis                   | Keterangan                                                                              |
| ----------------------- | ---------------------------------------------------------------------------------------|
| Sumber                  | [Kaggle Dataset : SIGMA TAXI PRIVATE LIMITED india](https://www.kaggle.com/arashnic/taxi-pricing-with-mobility-analytics) |
| Lisensi                 | CC0: Public Domain                                                                      |
| Kategori                | Bisnis, Mobil dan Kendaraan                                             |
| Rating Penggunaan       | 9.7 (Bronze)                                                                             |
| Jenis dan Ukuran Berkas | CSV (7.68 MB)                                                                          |

sigma_cabs.csv merupakan dataset yang digunakan pada proses analisis prediksi lonjakan harga pada layanan taksi. Dataset ini berisi 131662 baris dan 14 kolom di mana tiap kolom memuat informasi tipe data yakni: 
- Terdapat 5 kolom dengan tipe object, yaitu: `Trip_ID` , `Type_of_Cab`, `Confidence_Life_Style_Index`, `Destination_Type`, dan `Gender`. Kolom ini merupakan _categorical features_ (fitur non-numerik).
- Terdapat 5 kolom numerik dengan tipe data float64 yaitu: `Trip_Distance`, `Customer_Since_Months`, `Life_Style_Index`, `Customer_Rating`, dan `Var1`.
- Terdapat 4 kolom numerik dengan tipe data int64, yaitu: `Cancellation_Last_1Month`, `Var2`, `Var3`, dan `Surge_Pricing_Type`. Kolom `Surge_Pricing_Type` merupakan target fitur yang akan digunakan.
Namun, terdapat juga data yang kossong (_missing value_) diantaranya pada variabel `Type_of_Cab`, `Customer_Since_Months`, `Life_Style_Index`, `Confidence_Life_Style_Index`, dan `Var1`

Berikut penjelasan mengenai variabel yang terdapat pada dataset:
1. `Trip_ID`: ID yang digunakan untuk perjalanan. 
2. `Trip_Distance `: Jarak perjalanan yang diminta oleh pelanggan.
3. `TypeofCab` : Kategori taksi yang diminta oleh pelanggan
4. `CustomerSinceMonths` : Pelanggan menggunakan layanan taksi sejak n bulan;
5. `LifeStyleIndex` : Indeks kepemilikan yang dibuat oleh Sigma Cabs yang menunjukkan gaya hidup pelanggan berdasarkan perilaku mereka
6. `ConfidenceLifeStyle_Index` : Kategori yang menunjukkan kepercayaan pada indeks yang disebutkan diatas
7. `Destination_Type` : Sigma Cabs membagi setiap tujuan dalam satu dari 14 kategori
8. `Customer_Rating` : Rata-rata peringkat waktu hidup pelanggan hingga saat ini
9. `CancellationLast1Month` : Jumlah perjalanan yang dibatalkan oleh pelanggan dalam 1 bulan terakhir
10. `Var1`, `Var2`, dan `Var3` : Variabel kontinu yang ditutupi oleh perusahaan. Dapat digunakan untuk tujuan pemodelan
11. `Gender` : Jenis kelamin pelanggan
12. `SurgePricingType` : Target (terdapat 3 jenis harga lonjakan penggunaan layanan taxi)

Kemudian terdapat juga visualisasi data untuk kolom dengan fitur numerik seperti pada gambar dibawah ini :
![Trip_Distance](https://user-images.githubusercontent.com/44547435/136664699-e92637c4-835a-43c6-9fda-2e694bfad1f7.png)
![customer_since_month](https://user-images.githubusercontent.com/44547435/136664961-8c43e525-9b11-4451-9693-fdcbd41c63dd.png)
![life_style_index](https://user-images.githubusercontent.com/44547435/136664714-20e7e4d7-7a87-4b96-a517-b2435c7c04db.png)
![customer_rating](https://user-images.githubusercontent.com/44547435/136664732-fd8b28a4-b5df-4a8f-8c2a-1f148f8150f3.png)
![cancellation_last_1month](https://user-images.githubusercontent.com/44547435/136664740-0eae4522-60b2-461d-a741-bd050cc01828.png)
![var1](https://user-images.githubusercontent.com/44547435/136664745-63674487-1e26-4b42-88ae-df51276df5df.png)
![var2](https://user-images.githubusercontent.com/44547435/136664750-32b60fb0-ee97-4327-88f9-195c2707244a.png)
![var3](https://user-images.githubusercontent.com/44547435/136664758-334cfa11-2824-4e63-8cab-ea9a379f1006.png)
![surge_pricing_type](https://user-images.githubusercontent.com/44547435/136664767-b33951dd-edb3-4aa3-af30-131e0ce531dd.png)
![surge_pricing_type1](https://user-images.githubusercontent.com/44547435/136665011-993da1f3-09f7-4fac-bc16-ef3690fef175.png)

Kemudian visualisasi data untuk kolom dengan fitur non-numerik seperti pada gambar dibawah ini :
![type_of_Cab](https://user-images.githubusercontent.com/44547435/136664773-8dee0c6b-3412-4716-9477-45054caa8d6a.png)
![Confidence_life_style_index](https://user-images.githubusercontent.com/44547435/136664782-ed42fec5-eae2-4109-8eb6-07ace461e2b0.png)
![gender](https://user-images.githubusercontent.com/44547435/136664793-290505c2-62aa-41d6-8c7d-628ec3a61f64.png)
![Destination_type](https://user-images.githubusercontent.com/44547435/136664795-f77f3a27-4292-41b4-832b-b038a42eafa7.png)

Berikut Correlation Matrix:

![correlation_matrix](https://user-images.githubusercontent.com/44547435/136665130-7fa801d9-55a1-4811-b76b-15c262157198.png)

## Data Preparation
Berdasarkan _Solution statements_, berikut merupakan penjelasan dari tahapan-tahapan dalam melakukan _preprocessing_ data :

-   Mengatasi data yang kosong atau missing value dengan nilai rata-rata dan mode kolom.

![missing value](https://user-images.githubusercontent.com/44547435/136665505-0975f191-6f5b-4308-a292-1c77ccc717a8.png)

Dapat dilihat dari informaasi diatas bahwa terdapat beberapa variabel/kolom yang memiliki data null, dari kolom `Type_of_Cab` 15.35%, `Customer_Since_Months` 4.5%, `Life_Style_Index` 15.34%, `Confidence_Life_Style_Index` 15.34%, dan `Var1` 53,95%.
Sehingga, untuk mengatasi data null maka dilakukan manipulasi data dengan mengisi data yang kosong dengan nilai rata-rata dan mode pada masing-masing kolom. Manipulasi data ini berguna agar data yang digunakan tidak kehilangan banyak informasi, dan model tetap dapat memperoleh informasi dari data yang ada pada kolom lainnya.

- Encoding Fitur Kategori menggunakan One Hot Encoding

  Terdapat 4 variabel kategori dalam dataset yakni `Type_of_Cab`,`Confidence_Life_Style_Index`,`Gender`, dan `Destination_Type`. Metode One Hot Encoding merepresentasikan data bertipe kategori sebagai vektor biner yang bernilai integer, 0 dan 1, dimana semua elemen akan bernilai 0 kecuali satu elemen yang bernilai 1, yaitu elemen yang memiliki nilai kategori tersebut.

- Melakukan pembagian dataset dengan Train/test split

  Train/test split digunakan untuk mengevaluasi performa model yang nanti akan digunakan. Proses ini membagi dataset menjadi dua bagian yakni bagian yang digunakan untuk data _training_ dan untuk data _testing_ dengan proporsi 80:20.

- Standarisasi nilai data pada semua fitur dengan StandarScaler

  Standarisasi adalah proses konversi nilai-nilai dari suatu fitur sehingga nilai-nilai tersebut memiliki skala yang sama. Metode StandardScaler menghilangkan _mean_ (terpusat pada 0) dan menskalakan ke variansi (deviasi standar = 1), dengan asumsi data terdistribusi normal (gauss) untuk semua fitur.

## Modelling
Selanjutnya pada tahap modelling akan membandingkan 2 metode klasifikasi yakni Random Forest dan LGBM. 

- Random Forest

  Pada proses ini menggunakan modul scikit-learn yakni [RandomForestClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html).
- LGBM

  Modul yang digunakan yakni [LGBM](https://lightgbm.readthedocs.io/en/latest/pythonapi/lightgbm.LGBMClassifier.html)

Hasilnya dapat dilihat dibawah ini:
![modelling](https://user-images.githubusercontent.com/44547435/136684872-e728cd6e-a795-491d-95fc-56d4f4adb498.png)

Pada model yang digunakan, dapat diketahui bahwa hasil akurasi dari model Random Forest dan LGBM hampir mendekati pada masing-masing nilai akurasi sebesar 68.5% dan 69.4%. Dapat dikatakan bahwa nilai _accuracy_ dari kedua model masih kurang bagus, baik dari nilai _f1-score_, _precision_, dan _recall_. Untuk melihat performa dari kedua model dengan mencoba memakai data uji/testing dan divisualisasikan pada confussion matrix sebagai berikut:
- Random Forest

![RF](https://user-images.githubusercontent.com/44547435/136685205-ac60d504-a831-4d46-a5c1-89dfcd6d7253.png)
- LGBM

![LGBM](https://user-images.githubusercontent.com/44547435/136685214-9e94aeec-55ac-44ba-8bb1-76a3a4f3485e.png)

## Evaluation
Pada tahapan terakhir ini, model yang dibuat merupakan kasus klasifikasi dan menggunakan metriks _accuracy_, _f1-score_, _precission_, dan _recall_. Berikut tampilan hasil dari pengukuran model LGBM.

![evaluation](https://user-images.githubusercontent.com/44547435/136685305-bcb8777f-3f7d-4b2e-a8e7-f15bf5b37b3f.png)

Penjelasan metriks yang digunakan:
- Accuracy

  Accuracy menggambarkan seberapa akurat model dapat mengklasifikasikan dengan benar. Maka, _accuracy_ meruapakan rasio prediksi benar (positif dan negatif) dengan keseluruhan data. Dengan kata lain, _accuracy_ merupakan tingkat kedekatan nilai prediksi dengan nilai aktual (sebenarnya). Persamaan nilai _accuracy_:
![accuracy](https://user-images.githubusercontent.com/44547435/136685509-4d16e16b-56ab-4dfd-8102-ba6366ff93a1.png)

- Precision

  Precision menggambarkan tingkat keakuratan antara data yang diminta dengan hasil prediksi yang diberikan oleh model. Maka, _precision_ merupakan rasio prediksi benar positif dibandingkan dengan keseluruhan hasil yang diprediksi positif. Persamaan nilai _precision_:
![precision](https://user-images.githubusercontent.com/44547435/136685565-88449317-8d35-47a5-ae04-74aa9059c384.png)

- Recall

  Recall menggambarkan keberhasilan model dalam menemukan kembali sebuah informasi. Maka, _recall_ merupakan rasio prediksi benar positif dibandingkan dengan keseluruhan data yang benar positif. Persamaan nilai _recall_:
![recall](https://user-images.githubusercontent.com/44547435/136685641-273c2972-13cd-438a-bd72-bacd38da6f88.png)

- f1-score

  f1-Score menggambarkan perbandingan rata-rata _precision_ dan _recall_ yang dibobotkan. Accuracy tepat kita gunakan sebagai acuan performansi algoritma jika dataset kita memiliki jumlah data false negatif dan false positif yang sangat mendekati (symmetric). Namun jika jumlahnya tidak mendekati, maka sebaiknya kita menggunakan f1-score sebagai acuan. Persamaan nilai _f1-score_:

![f1-score](https://user-images.githubusercontent.com/44547435/136685760-415e5a0f-e2a5-4e35-90cb-4789bff771c7.png)

## _Referensi:_

[[1](https://machinelearning.mipa.ugm.ac.id/2018/07/28/random-forest/)] Yanuar, A. 2018. Random Forest. Artikel. https://machinelearning.mipa.ugm.ac.id/2018/07/28/random-forest/

[[2](https://zephyrnet.com/id/lightgbm-a-highly-efficient-gradient-boosting-decision-tree/)] Plato. 2020. LightGBM: Pohon Keputusan Meningkatkan Gradien yang Sangat Efisien. https://zephyrnet.com/id/lightgbm-a-highly-efficient-gradient-boosting-decision-tree/
