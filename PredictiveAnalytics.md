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
- Terdapat 5 kolom dengan tipe object, yaitu: Trip_ID , Type_of_Cab, Confidence_Life_Style_Index, Destination_Type dan Gender. Kolom ini merupakan categorical features (fitur non-numerik).
- Terdapat 5 kolom numerik dengan tipe data float64 yaitu: Trip_Distance, Customer_Since_Months, Life_Style_Index, Customer_Rating, dan Var1.
- Terdapat 4 kolom numerik dengan tipe data int64, yaitu: Cancellation_Last_1Month, Var2, Var3, dan Surge_Pricing_Type. Kolom Surge_Pricing_Type merupakan target fitur yang akan digunakan.
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
	
## Data Preparation
## Modeling
## Evaluation
