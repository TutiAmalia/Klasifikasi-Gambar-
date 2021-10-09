# Laporan Proyek Machine Learning - Tuti Amalia

## Domain Proyek

-   Latar Belakang

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

sigma_cabs.csv merupakan dataset yang digunakan pada proses analis prediksi lonjakan harga pada layanan taksi. Dataset ini berisi 131662 baris dan 14 kolom di mana tiap kolom memuat informasi tipe data yakni: terdapat 5 buah data numerik (tipe data float64), int64(4), object(5)
- Terdapat 5 kolom dengan tipe object, yaitu: Trip_ID , Type_of_Cab, Confidence_Life_Style_Index, Destination_Type dan Gender. Kolom ini merupakan categorical features (fitur non-numerik).
- Terdapat 5 kolom numerik dengan tipe data float64 yaitu: Trip_Distance, Customer_Since_Months, Life_Style_Index, Customer_Rating, dan Var1.
- Terdapat 4 kolom numerik dengan tipe data int64, yaitu: Cancellation_Last_1Month, Var2, Var3, dan Surge_Pricing_Type. Kolom Surge_Pricing_Type merupakan target fitur yang akan digunakan.

Pada berkas yang diunduh yakni `water_potability.csv` berisi informasi metriks kualitas air untuk 3276 jenis air yang berbeda. Terdapat 9 buah data numerik (tipe data float64) dan 1 buah data kategori (tipe data int64). Terdapat juga beberapa kolom yang memiliki data kosong diantaranya pada kolom `pH`, `Sulfate` dan `Trihalomethanes`. Untuk penjelasan mengenai variabel-variable pada data _water quality_ dapat dilihat pada poin-poin berikut :
## Data Preparation
## Modeling
## Evaluation
