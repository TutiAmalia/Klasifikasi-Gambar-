# Laporan Proyek Machine Learning - Tuti Amalia

## Domain Proyek
-   Latar Belakang\
![Microsoft Store](https://user-images.githubusercontent.com/44547435/138543829-32f9b7da-2085-46b2-8efe-e3d0226c34c7.jpg)\
  Pada konsol smartphone biasa ditemukan aplikasi dari toko aplikasi bawaan smartphone seperti Google Play Store atau App Store, namun untuk mendapatkan aplikasi untuk pengguna PC atau laptop sebenarnya bisa dilakukan dengan mendownload di website-website yang menyediakan berbagai aplikasi PC atau laptop. Namun tentu ada resiko seperti malware atau virus yang bisa ikut serta ketika melakukan pengunduhan dan pemasangan aplikasi tersebut. Keamanan dari aplikasi yang bisa ditemukan melalui mesin pencarian juga perlu dipertanyakan.\
  Microsoft Store merupakan aplikasi untuk download aplikasi yang bisa didapatkan pertama kali memasang sistem operasi seperti Windows 8, 8.1, dan Windows 10. Aplikasi ini secara resmi diterbitkan oleh Microsoft dan dikhususkan bagi para pengguna sistem operasi dari Microsoft, dimana saat ini angka pengguna Windows menguasai penggunaan OS dibanding OS lain. Tentu saja segi keamanan akan sangat terjamin bila dibandingkan dengan melakukan download aplikasi dari website yang banyak tersebar di mesin pencarian. 

## Business Understanding
### Problem Statements
### Goals
### Solution statements

## Data Understanding
![1](https://user-images.githubusercontent.com/44547435/138543474-16640f22-7873-4dbc-853e-9514d894cb70.png)
Informasi dataset dapat dilihat pada tabel dibawah ini :

| Jenis                   | Keterangan                                                                              |
| ----------------------- | ---------------------------------------------------------------------------------------|
| Sumber                  | [Kaggle : Microsoft Store](https://www.kaggle.com/vishnuvarthanrao/windows-store) |
| Lisensi                 | CC0: Public Domain                                                                      |
| Kategori                | bisnis, seni dan hiburan, software                                            |
| Rating Penggunaan       | 10.0 (Gold)                                                                             |
| Jenis dan Ukuran Berkas | CSV (300 kB)                                                                          |

msft.csv merupakan dataset yang digunakan pada proses rekomendasi aplikasi untuk pengguna Microsoft Windows Store. Dataset ini berisi 5322 baris dan 6 kolom di mana tiap kolom memuat informasi tipe data yakni: 
- Terdapat 4 kolom dengan tipe object, yaitu: `Name` , `Category`, `Date`, dan `Price` (fitur non-numerik).
- Terdapat 1 kolom numerik dengan tipe data float64 yaitu: `Rating`
- Terdapat 1 kolom numerik dengan tipe data int64, yaitu: `No of people Rated`
Namun, terdapat juga data yang kossong (_missing value_) diantaranya pada variabel `Name`, `Rating`, `Category`, `Date`, dan `Price`\
Berikut penjelasan mengenai variabel yang terdapat pada dataset:
1. `Name`: Nama pada aplikasi di Windows Store.
2. `Rating `: Peringkat pada aplikasi.
3. `No of people Rated` : Jumlah pengguna yang menilai aplikasi
4. `Category` : Kategori pada aplikasi.
5. `Date` : Tanggal saat diposting
6. `Price` : Harga aplikasi
## Modelling
## _Referensi:_
