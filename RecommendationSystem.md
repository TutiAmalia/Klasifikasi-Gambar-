# Laporan Proyek Machine Learning - Tuti Amalia

## Domain Proyek
-   Latar Belakang\
![Microsoft Store](https://user-images.githubusercontent.com/44547435/138543829-32f9b7da-2085-46b2-8efe-e3d0226c34c7.jpg)\
    Pada konsol _smartphone_ biasa ditemukan aplikasi dari toko aplikasi bawaan _smartphone_ seperti Google Play Store atau App Store, namun untuk mendapatkan aplikasi bagi pengguna PC atau laptop sebenarnya bisa dilakukan dengan mengunduh di _website_ yang menyediakan berbagai aplikasi PC atau laptop. Namun tentu ada resiko seperti _Malware_ atau virus yang bisa ikut serta ketika melakukan pengunduhan dan pemasangan aplikasi tersebut. Keamanan dari aplikasi yang bisa ditemukan melalui mesin pencarian juga perlu dipertanyakan.
    
    Microsoft Store merupakan aplikasi untuk mengunduh aplikasi yang bisa didapatkan pertama kali pada sistem operasi seperti Windows 8, 8.1, dan Windows 10 [[1](https://id.wikipedia.org/wiki/Bursa_Microsoft)]. Aplikasi ini secara resmi diterbitkan oleh Microsoft dan dikhususkan bagi para pengguna sistem operasi dari Microsoft, dimana saat ini angka pengguna Windows menguasai penggunaan OS dibanding OS lain. Pada Microsoft Store terdapat berbagai pilihan aplikasi dengan berbagai konten yang menarik. Beberapa konten pada Microsoft Store juga tersedia secara gratis dan tentu saja dari segi keamanan akan sangat terjamin bila dibandingkan dengan melakukan pengunduhan aplikasi dari _website_ yang banyak tersebar di mesin pencarian.
    
    Maka dari itu, pada proyek kali ini dibuat sistem rekomendasi pada pengguna Microsoft Store dimana akan direkomendasikan beberapa aplikasi berdasarkan pada pencarian pengguna. 

## Business Understanding
### Problem Statements
  Berikut merupakan rincian masalah yang dapat diselesaikan pada proyek ini:
  - Bagaimana model yang digunakan dapat merekomendasi aplikasi berdasarkan pencarian pengguna?
### Goals
  Berikut adalah tujuan dari dibuatnya proyek ini:
  - Model dapat merekomendasikan aplikasi berdasarkan pencarian pengguna.
### Solution statements
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini diantaranya:
- Karena dataset yang digunakan terbilang cukup baik, maka untuk _preprocessing_ data dilakukan beberapa teknik _preprocessing_, sebagai berikut:
  - Membersihkan data kosong pada kolom.
  - Memperbaiki tipe data pada beberapa kolom.
- Sebelum dataset dimasukkan ke model diperlukan persiapan data atau _data preparation_ dimana pada model yang digunakan masing-masing memiliki teknik yang berbeda yakni:
  - K-Nearest Neighbor
    - Konversi kolom kategori dengan metode _One Hot Encoding_
    - Standarisasi kolom numerik dengan metode _MinMaxScaler_
  - Cosine Similarity
    - Ekstraksi fitur dengan metode TF-IDF Vectorizer
- Kemudian, setelah data telah dipersiapkan maka selanjutnya dimasukkan ke dalam model sistem rekomendasi berdasarkan _Content Based Filtering_. Alasannya karena menyesuaikan pada dataset yang digunakan. Beberapa algoritma/model yang digunakan untuk membuat sistem rekomendasi pada proyek kali ini yakni: 
  - K-Nearest Neighbor\
      Algoritma ini digunakan untuk kasus _clustering_ pada sistem rekomendasi. Prinsip algoritma ini adalah mencari nilai _similarity_ dan dengan proses perhitungan untuk mendapatkan hasil semirip mungkin dengan hasil pencarian.\
      Kelebihan dari KNN yakni:\
        - Algoritma mudah digunakan dan sederhana.\
        - Algortima sangat fleksibel, dapat diimplementasikan pada kasus klasifikasi, regresi, dan pencarian.\
       Kekurangan dari KNN yakni:\
        - Algoritma menjadi lebih lambat secara signifikan karena jumlah contoh dan/atau prediktor/variabel yang meningkat.
  - Cosine Similarity\
      Cosine similarity untuk mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama, dengan menghitung sudut _cosinus_ antara dua vektor. Semakin kecil sudut _cosinus_, semakin besar nilai _cosine similarity_.\
![Rumus cosine similarity](https://user-images.githubusercontent.com/44547435/138561226-b298627a-1f9e-4555-8e9e-96c352927344.jpeg)\
Cosine similarity menghitung kesamaan sebagai _dot product_ yang dinormalisasi dari masukan sampel x dan y. Sehingga, penggunaan _cosine similarity_ ini untuk mengukur kesamaan nama aplikasi dan kategori aplikasi pada Microsoft Store.

## Data Understanding
![1](https://user-images.githubusercontent.com/44547435/138543474-16640f22-7873-4dbc-853e-9514d894cb70.png)
Informasi dataset dapat dilihat pada tabel dibawah ini :

| Jenis                   | Keterangan                                                                              |
| ----------------------- | ---------------------------------------------------------------------------------------|
| Sumber                  | [Kaggle : Microsoft Store](https://www.kaggle.com/vishnuvarthanrao/windows-store) |
| Lisensi                 | CC0: Public Domain                                                                      |
| Kategori                | bisnis, seni dan hiburan, _software_                                            |
| Rating Penggunaan       | 10.0 (Gold)                                                                             |
| Jenis dan Ukuran Berkas | CSV (300 kB)                                                                          |

msft.csv merupakan dataset yang digunakan pada proses rekomendasi aplikasi untuk pengguna Microsoft Store. Dataset ini berisi 5322 baris dan 6 kolom dimana tiap kolom memuat informasi tipe data yakni: 
- Terdapat 4 kolom dengan tipe data `object`, yaitu: `Name` , `Category`, `Date`, dan `Price` (fitur non-numerik).
- Terdapat 1 kolom numerik dengan tipe data `float64` yaitu: `Rating`
- Terdapat 1 kolom numerik dengan tipe data `int64`, yaitu: `No of people Rated`
Namun, terdapat juga data yang kosong (_missing value_) diantaranya pada variabel `Name`, `Rating`, `Category`, `Date`, dan `Price`.

Berikut penjelasan mengenai variabel yang terdapat pada dataset:
1. `Name`: Nama pada aplikasi di Microsoft Store.
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
![jumlah orang yang menilai](https://user-images.githubusercontent.com/44547435/138562017-f6afee0c-365b-44d0-8da1-1eccba85f8c6.png)

## Data Preparation
- Berdasarkan _Solution statements_, berikut merupakan penjelasan dari tahapan-tahapan dalam melakukan _preprocessing_ data :
  - Membersihkan data kosong atau _missing value_ pada kolom. Pada kolom `Name`, `Rating`, `Category`, `Date`, dan `Price` masing-masing memiliki 1 data yang kosong. Sehingga, untuk mengatasi data null maka dilakukan pembersihan dengan menghapusnya karena tidak banyak informasi yang hilang dari keseluruhan datanya.
  - Memperbaiki tipe data pada beberapa kolom. Berikut kolom dari dataset yang perlu diperbaiki tipe datanya:
    - Kolom Rating: mengecek apakah terdapat nilai rating diatas 5.
    - Kolom Category: menghapus spasi pada kolom Categori menjadi garis bawah
    - Kolom Date: mengganti tipe data menjadi _datetime_.
    - Kolom Price: menghapus simbol '₹', ','. Mengubah nilai 'Free' menjadi '0' serta tipe datanya menjadi 'float64'
- Berikutnya untuk persiapan data atau _data preparation_, dilakukan tahapan sebagai berikut:
  - K-Nearest Neighbor
    - Konversi label kategori dengan metode _One Hot Encoding_.\
        Label kategori ini diubah dari data kategori menjadi data numerik untuk memudahkan pencarian nilai terdekat pada setiap aplikasi yang akan direkomendasikan. Metode _One Hot Encoding_ merepresentasikan data bertipe kategori sebagai vektor biner yang bernilai integer, 0 dan 1, dimana semua elemen akan bernilai 0 kecuali satu elemen yang bernilai 1, yaitu elemen yang memiliki nilai kategori tersebut. Kemudian label kategori akan disatukan kembali dengan _dataframe_ yang berisi label `Rating`, `No of people rated`, dan `Price`.
    - Standarisasi kolom numerik dengan metode MinMaxScaler.\
        Standarisasi adalah proses konversi nilai-nilai dari suatu fitur sehingga nilai-nilai tersebut memiliki skala yang sama. Metode MinMaxScaler membantu menskalakan data dalam rentang nilai minimum dan maksimum yang ditentukan yakni antara nilai 0-1. Nilai diskalakan dengan menggunakan rumus: \
         ![minmax](https://user-images.githubusercontent.com/44547435/139031741-e222e46e-2e4b-47c2-9fdc-aecd5c14a575.png) 
  - Cosine Similarity
    - Ekstraksi fitur dengan metode TF-IDF Vectorizer
        Metode ini digunakan pada sistem rekomendasi untuk menemukan representasi fitur penting dari setiap kategori aplikasi dimana fungsi yang digunakan diambil dari library [Sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html). Kemudian metode ini juga menghasilkan matriks yang menunjukkan korelasi antara kategori dengan nama aplikasi.
## Modelling
Setelah dilakukan _data preparation_, selanjutnya membuat model/sistem rekomendasi berdasarkan _Content based filtering_.
1. K-Nearest Neighbor\
   Model KNN untuk _clustering_ menggunakan fungsi [NearestNeighbor](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.NearestNeighbors.html) dari library Sklearn dengan parameter metriksnya yakni euclidean. Selanjutnya, dibuat fungsi `getRecomendationKnn` untuk memberikan rekomendasi terhadap suatu nama aplikasi berdasarkan urutan dari hasil nilai pendekatannya. Berikut tampilan hasil rekomendasi dengan menggunakan _Nearest Neighbor_:\
   ![knn](https://user-images.githubusercontent.com/44547435/139034969-ed95f816-1856-4124-b038-ce99c76da4a5.png)
2. Cosine Similarity\
   Menghitung _cosine similairity_ dari setiap dataset menggunakan fungsi [cosine_similarity](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.pairwise.cosine_similarity.html) dari library Sklearn. Pada tahapan ini, menghitung _cosine similarity_ pada _dataframe_ dengan membuat fungsi `getRecomendationCosine` untuk pemberian rekomendasi terhadap suatu nama aplikasi. Kemudian, diurutkan hasil perhitungan _cosine similarity_ dari score nilai tertinggi berdasarkan dengan jumlah nama aplikasi yang akan direkomendasikan. Berikut tampilan hasil rekomendasi dengan menggunakan _cosine similarity_:
   ![cosine](https://user-images.githubusercontent.com/44547435/139034973-55e48398-c10d-4de6-af86-c44ad2f2766a.png)

Dari kedua modelling yang digunakan terdapat perbedaan hasil rekomendasi untuk pengguna. 
   
## Evaluation
- Untuk mengukur kinerja model sistem rekomendasi dengan K-Nearest Neighbor digunakan metriks Davies Bouldin.\
    Skor Davies Bouldin didefinisikan sebagai ukuran kesamaan rata-rata dari setiap cluster dengan cluster yang paling mirip, dimana kesamaan adalah rasio jarak dalam cluster dengan jarak antar cluster. Skor dihitung dengan formula [[2](https://scikit-learn.org/stable/modules/clustering.html#clustering-performance-evaluation)] : \
![davies1](https://user-images.githubusercontent.com/44547435/138578848-85d16184-ae80-40fa-a410-71aee6f73677.png)\
![davies2](https://user-images.githubusercontent.com/44547435/138578850-6646b34d-bd55-4a13-8140-bbde49951a9d.png)\
    Kelebihan:
    - Komputasi lebih mudah daripada Skor Silhoutte.
    - Skor yang dihitung hanya jumlah dan fitur yang melekat pada dataset. \
    Kekurangan:
    - Metriks ini hanya baik digunakan pada kasus _convex cluster_.
    - Penggunaan jarak _centroid_ membatasi metriks jarak ke ruang Euclidean.\
  Hasil skor dari metriks Davies Bouldin yakni ![metrics](https://user-images.githubusercontent.com/44547435/139035597-5c66a21e-b1b9-44ee-b735-a9f31fba0d23.png) \
  Berdasarkan hasil diatas menandakan modelnya sudah memiliki separasi kluster yang cukup baik.
 - Berdasarkan metriks Precision. \
   Precision menggambarkan tingkat keakuratan antara data yang diminta dengan jumlah item rekomendasi yang relevan dari model yang digunakan. Maka, untuk menghitung tingkat akurasi model berdasarkan jumlah prediksi benar dibagi dengan jumlah keseluruhan prediksi. Untuk rumusnya digunakan [[3](https://chaitanyabelhekar.medium.com/recommender-system-metrics-clearly-explained-1f2ba6690216)] : \
   ![precision](https://user-images.githubusercontent.com/44547435/139037109-11d88c1a-c60e-4921-b124-294e840a01a3.png) \
   Hasil dari masing-masing model yakni: 
   - K-Nearest Neighbor: \
     ![prec_knn](https://user-images.githubusercontent.com/44547435/139037377-f071eb63-2e2f-4e5e-9ce8-eaa9d1efdd3c.png) 
   - Cosine Similarity: \
     ![prec_cos](https://user-images.githubusercontent.com/44547435/139037372-dbd47fdd-897c-49d7-9374-54f2af7a565c.png) \
   Berdasarkan hasil evaluasi sistem rekomendasi aplikasi untuk pengguna di Microsoft Store dengan metriks precision pada metode Knn memiliki nilai 0.99 dan cosine similarity memiliki nilai 1.0.
    
## _Referensi:_
[[1]((https://id.wikipedia.org/wiki/Bursa_Microsoft))] Anonim. Bursa Microsoft. online. https://id.wikipedia.org/wiki/Bursa_Microsoft \
[[2](https://scikit-learn.org/stable/modules/clustering.html#clustering-performance-evaluation)] Scikit-learn. (2021). Clustering - Performance Evaluation. https://scikit-learn.org/stable/modules/clustering.html#clustering-performance-evaluation \
[[3](https://chaitanyabelhekar.medium.com/recommender-system-metrics-clearly-explained-1f2ba6690216)] Belhekar Chaitanya. 2020. Recommender System Metrics — Clearly Explained. https://chaitanyabelhekar.medium.com/recommender-system-metrics-clearly-explained-1f2ba6690216
