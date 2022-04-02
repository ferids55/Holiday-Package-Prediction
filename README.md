# Holiday Package Prediction

## Latar Belakang
Sebuah perusahaan travel ingin meluncurkan paket 
perjalanan baru, tetapi perusahaan ingin memanfaatkan 
data yang tersedia dari pelanggan yang ada dan pelanggan 
potensial untuk membuat pengeluaran pemasaran lebih efisien.
Berdasarkan data tahun lalu diketahui bahwa 18% pelanggan membeli paket perjalanan. Namun, biaya pemasarannya cukup tinggi karena pelanggan dihubungi secara acak tanpa melihat informasi yang tersedia.
Bagaimana cara untuk membantu tim business mengetahui pelanggan yang tertarik untuk membeli paket perjalanan baru agar tidak dihubungi secara acak.
Bagaimana cara membuat sistem untuk mengetahui pelanggan mana yang akan membeli paket perjalanan baru.
Menggunakan business matrix “Conversion Rate”, yaitu persentase pelanggan akan membeli paket perjalanan baru.
Menggunakan analytical approach “Predictive Analytics” dengan membuat model yang mampu memprediksi bahwa pelanggan akan membeli paket perjalanan baru atau tidak.


## Preparation Data
Data yang digunakan adalah data Holiday Package Prediction. Sumber data dapat diakses [di sini](https://www.kaggle.com/susant4learning/holiday-package-purchase-prediction/code).  Dataset ini menggambarkan profil pelanggan yang sudah ada untuk digunakan dalam menganalisis dan memprediksi apakah customer tersebut akan membeli paket liburan terbaru atau tidak. Melakukan beberapa proses eksplorasi data (EDA) dan melakukan analisis statistika untuk mendapatkan insight yang menarik untuk dapat diolah dan divisualisasikan.

## Deskripsi Data
Dari info data tersebut diketahui bahwa:
- Data terdiri dari 4888 baris dan 20 kolom 
(14 kolom numerik dan 6 kolom kategorik).
- Tampak beberapa kolom yang memiliki nilai null/missing values (non-null count < total baris).
- Penamaan kolom dan tipe data terlihat sudah sesuai.

### Terdapat 20 fitur pada data ini, di antaranya yaitu:

- CustomerID : Customer ID yang unik
- ProdTaken : Produk dibeli atau tidak  
(0: Tidak dibeli, 1: Dibeli)
- Age : Usia dari customer
- TypeofContact : Cara customer dikontak (Company Invited or Self Inquiry)
- CityTier : Tingkat kota tergantung pada perkembangan kota, populasi, fasilitas, dan standar hidup. The categories are ordered i.e.
- DurationOfPitch : Duration of the pitch by a salesperson to the customer
- Occupation : Pekerjaan dari customer
- Gender : Jenis kelamin customer
- NumberOfPersonVisiting : Jumlah orang yang berencana melakukan trip bersama customer
- NumberOfFollowups : Jumlah follow-up yang telah dilakukan oleh sales setelah diberikan penawaran





