# Laporan Proyek Machine Learning - Tuti Amalia

## Domain Proyek

-   Latar Belakang
Layanan agregator taksi populer saat ini dan pengguna dapat mengunduh aplikasi mereka di ponsel cerdas dan memesan taksi dari mana saja di kota tempat mereka beroperasi. Aplikasi ini akan mencari taksi dari berbagai penyedia layanan dan memberikan opsi terbaik kepada klien mereka di seluruh opsi yang tersedia. Proyek ini bertujuan untuk membangun model prediktif untuk membantu menentukan jenis harga lonjakan untuk setiap perjalanan berdasarkan karakteristiknya. Ini dapat membantu mengalokasikan sumber daya secara efektif dan meningkatkan efisiensi transportasi.

## Business Understanding
### Problem Statements
### Goals
### Solution statements

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

sigma_cabs.csv merupakan dataset yang digunakan pada proses analisis prediksi lonjakan harga pada layanan taksi. Dataset ini berisi 131662 baris dan 14 kolom di mana tiap kolom memuat informasi tipe data yakni: terdapat 5 buah data numerik (tipe data float64), int64(4), object(5)
- Terdapat 5 kolom dengan tipe object, yaitu: `Trip_ID` , `Type_of_Cab`, `Confidence_Life_Style_Index`, `Destination_Type`, dan `Gender`. Kolom ini merupakan categorical features (fitur non-numerik).
- Terdapat 5 kolom numerik dengan tipe data float64 yaitu: `Trip_Distance`, `Customer_Since_Months`, `Life_Style_Index`, `Customer_Rating`, dan `Var1`.
- Terdapat 4 kolom numerik dengan tipe data int64, yaitu: `Cancellation_Last_1Month`, `Var2`, `Var3`, dan `Surge_Pricing_Type`. Kolom `Surge_Pricing_Type` merupakan target fitur yang akan digunakan.
Namun, terdapat juga data yang kossong (missing value) diantaranya pada variabel `Type_of_Cab`, `Customer_Since_Months`, `Life_Style_Index`, `Confidence_Life_Style_Index`, dan `Var1`

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
Berdasarkan _Solution statements_, berikut merupakan penjelasan dari tahapan-tahapan dalam melakukan preprocessing data :

-   Mengatasi data yang kosong atau missing value dengan nilai rata rata atau **_(mean substitution)_** dan mode kolom.
![Uploading missing value.png…]()
Dapat dilihat dari informaasi diatas bahwa terdapat beberapa variabel/kolom yang memiliki data null, dari kolom Type_of_Cab 15.35%, Customer_Since_Months 4.5%, Life_Style_Index 15.34%, Confidence_Life_Style_Index 15.34%, dan Var1 53,95%.
Sehingga, untuk mengatasi data null maka dilakukan manipulasi data dengan mengisi data yang kosong dengan nilai rata-rata dan mode pada masing-masing kolom. Manipulasi data ini berguna agar data yang digunakan tidak kehilangan banyak informasi, dan model tetap dapat memperoleh informasi dari data yang ada pada kolom lainnya.



## Modeling
## Evaluation
