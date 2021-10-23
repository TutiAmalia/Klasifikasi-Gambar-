# Laporan Proyek Machine Learning - Tuti Amalia

## Domain Proyek
-   Latar Belakang\
![Microsoft Store](https://user-images.githubusercontent.com/44547435/138543829-32f9b7da-2085-46b2-8efe-e3d0226c34c7.jpg)\
  Pada konsol smartphone biasa ditemukan aplikasi dari toko aplikasi bawaan Smartphone seperti Google Play Store atau App Store, namun untuk mendapatkan aplikasi bagi pengguna PC atau laptop sebenarnya bisa dilakukan dengan mendownload di website-website yang menyediakan berbagai aplikasi PC atau laptop. Namun tentu ada resiko seperti malware atau virus yang bisa ikut serta ketika melakukan pengunduhan dan pemasangan aplikasi tersebut. Keamanan dari aplikasi yang bisa ditemukan melalui mesin pencarian juga perlu dipertanyakan.\
  Microsoft Store merupakan aplikasi untuk download aplikasi yang bisa didapatkan pertama kali pada sistem operasi seperti Windows 8, 8.1, dan Windows 10 [[1](https://id.wikipedia.org/wiki/Bursa_Microsoft)]. Aplikasi ini secara resmi diterbitkan oleh Microsoft dan dikhususkan bagi para pengguna sistem operasi dari Microsoft, dimana saat ini angka pengguna Windows menguasai penggunaan OS dibanding OS lain. Pada Microsoft Store terdapat berbagai pilihan aplikasi dengan berbagai konten yang menarik. Beberapa konten pada Microsoft store juga tersedia secara gratis dan tentu saja dari segi keamanan akan sangat terjamin bila dibandingkan dengan melakukan download aplikasi dari website yang banyak tersebar di mesin pencarian.
  Maka dari itu, pada proyek kali ini dibuat sistem rekomendasi pada pengguna Microsoft Store di mana akan direkomendasikan beberapa aplikasi berdasarkan pada pencarian pengguna. 

## Business Understanding
### Problem Statements\
  Berikut merupakan rincian masalah yang dapat diselesaikan pada proyek ini:
  - Bagaimana model yang digunakan dapat merekomendasi aplikasi berdasarkan pencarian pengguna?
### Goals
  Berikut adalah tujuan dari dibuatnya proyek ini:
  - Model dapat merekomendasikan aplikasi berdasarkan pencarian pengguna.\
### Solution statements
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini diantaranya:
- Untuk preprocessing data dapat dilakukan dengan beberapa teknik, sebagai berikut:
  - Memperbaiki tipe data pada setiap kolom.
  - Membersihkan data kosong pada kolom.
  - Memperbaiki nilai pada kolom Price.
- Sebelum dataset dimasukkan ke model diperlukan persiapan data atau data preparation di mana terdapat beberapa teknik diantanya:
  - Konversi kolom kategori menjadi one hot encoding
  - Standarisasi kolom numerik dengan StandardScaler
- Kemudian, setelah data telah dipersiapkan maka selanjutnya dimasukkan ke dalam model sistem rekomendasi berdasarkan _Content based Filtering_. Alasannya karena menyesuaikan pada dataset yang digunakan. Beberapa algoritma/model yang digunakan untuk membuat sistem rekomendasi pada proyek kali ini yakni:
  - Cosine Similarity\
      Cosine similarity untuk mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama, dengan menghitung sudut cosinus anatara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity.\
      ![Rumus cosine similarity](https://user-images.githubusercontent.com/44547435/138561226-b298627a-1f9e-4555-8e9e-96c352927344.jpeg)\
      Cosine similarity menghitung kesamaan sebagai dot product yang dinormalisasi dari masukan sampel X dan Y. Sehingga, penggunaan cosine similarity ini untuk mengukur kesamaan nama aplikasi dan kategori aplikasi pada Microsoft Store.
  - K-Nearest Neighbor.
      Algoritma ini digunakan untuk kasus clustering pada sistem rekomendasi. Prinsip algoritma ini adalah mencari nilai similarity dan dengan proses perhitungan untuk mendapatkan hasil semirip mungkin dengan hasil pencarian.\
      Kelebihan dari knn yakni:
        - Algoritma mudah digunakan dan sederhana
        - Algortima sangat fleksibel, dapat diimplementasikan pada kasus klasifikasi, regresi, dan pencarian.\
       Kekurangan dari knn yakni:
        - Algoritma menjadi lebih lambat secara signifikan karena jumlah contoh dan/atau prediktor/variabel yang meningkat.

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

Kemudian terdapat juga visualisasi data untuk kolom datasetnya :\
![Jumlah aplikasi berdasarkan peringkat](https://user-images.githubusercontent.com/44547435/138562006-ee9cd392-ceb8-4d22-9334-20f01753e364.png)\
![Jumlah aplikasi berdasarkan kategori](https://user-images.githubusercontent.com/44547435/138562008-2046d49b-fd43-4247-abeb-6aa8c5460a62.png)\
![rata-rata peringkat berdasarkan kategori dan jumlah orang yang menilai](https://user-images.githubusercontent.com/44547435/138562009-c3f344c1-83c3-4bf6-bfb2-abb4134d624a.png)\
![rasio harga pada aplikasi](https://user-images.githubusercontent.com/44547435/138562012-5f5181bf-e5fe-40ba-8fbf-03a3a362b40c.png)\
![jumlah orang yang menilai](https://user-images.githubusercontent.com/44547435/138562017-f6afee0c-365b-44d0-8da1-1eccba85f8c6.png)\

## Modelling
## _Referensi:_
[[1]((https://id.wikipedia.org/wiki/Bursa_Microsoft))] Anonim. Bursa Microsoft. online: https://id.wikipedia.org/wiki/Bursa_Microsoft
