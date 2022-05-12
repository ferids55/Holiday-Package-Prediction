# Holiday Package Prediction

## Project Overview
Perusahaan **Trips&Travel.com** ingin menawarkan paket liburan baru. Saat ini, ada 5 jenis paket yang ditawarkan perusahaan yaitu **Basic, Standard, Deluxe, Super Deluxe, King**. Berdasarkan data tahun lalu diketahui bahwa **hanya 18% pelanggan membeli yang paket. Namun, biaya pemasarannya cukup tinggi karena pelanggan dihubungi secara acak** tanpa melihat informasi yang tersedia. Perusahaan berencana untuk meluncurkan produk baru bernama **Wellness Tourism**. Perusahaan ingin memanfaatkan data yang tersedia dari pelanggan yang ada dan pelanggan potensial untuk membuat pengeluaran pemasaran lebih efisien.

## Business Problems
- Pelanggan yang membeli paket liburan hanya 18% karena pemasaran dilakukan secara acak pada tahun lalu sehingga biaya pemasaran yang digunakan cukup tinggi.
- Perusahaan ingin menggunakan data pelanggan yang ada dan pelanggan potensial untuk pemasaran paket liburan yang baru.

## Objectives
- Membuat sistem yang dapat membantu perusahaan dalam memprediksi pelanggan yang akan ditargetkan penawaran produk baru agar menaikkan tingkat konversi dan mengurangi biaya pemasaran.
- Mengetahui karakteristik pelanggan yang akan membeli paket liburan untuk mencari pelanggan baru.

## Analytics Approach
Melakukan **predictive analysis** dengan **supervised learning (classification)** untuk memprediksi pelanggan yang akan membeli paket liburan.

<hr>

## Data Requirement
Dataset yang digunakan berasal dari [Kaggle](https://www.kaggle.com/datasets/susant4learning/holiday-package-purchase-prediction). Dataset terdiri dari 4888 baris dan 20 kolom dengan atribut sebagai berikut.

- **CustomerID** : Unique customer ID
- **ProdTaken** : Product taken or not (0: No, 1: Yes)
- **Age** : Age of customer
- **TypeofContact** : How customer was contacted (Company Invited or Self Inquiry)
- **CityTier** : City tier depends on the development of a city, population, facilities, and living standards. The categories are ordered i.e.
- **DurationOfPitch** : Duration of the pitch by a salesperson to the customer
- **Occupation** : Occupation of customer
- **Gender** : Gender of customer
- **NumberOfPersonVisiting** : Total number of persons planning to take the trip with the customer
- **NumberOfFollowups** : Total number of follow-ups has been done by the salesperson after the sales pitch
- **ProductPitched** : Product pitched by the salesperson
- **PreferredPropertyStar** : Preferred hotel property rating by customer
- **MaritalStatus** : Marital status of customer
- **NumberOfTrips** : Average number of trips in a year by customer
- **Passport** : The customer has a passport or not (0: No, 1: Yes)
- **PitchSatisfactionScore** : Sales pitch satisfaction score
- **OwnCar** : Whether the customers own a car or not (0: No, 1: Yes)
- **NumberOfChildrenVisiting** : Total number of children with age less than 5 planning to take the trip with the customer
- **Designation** : Designation of the customer in the current organization
- **MonthlyIncome** : Gross monthly income of the customer

Dari 20 kolom tersebut yang akan dipilih sebagai target adalah kolom `ProdTaken` sedangkan kolom lainnya digunakan sebagai feature dan akan diseleksi kembali mana yang cocok.

## Exploratory Data Analysis
1. Multivariate Analysis (kolom numerik terhadap target)
![multivariate1](/fig/multivariate_analysis_num.png)

2. Multivariate Analysis (kolom categorik terhadap target)
![multivariate2](/fig/multivariate_analysis_cat.png)

3. Produk Basic lebih banyak dibeli pelanggan
![produk](/fig/insight1.png)

4. Tiap jenis produk hanya ditawarkan pada 1 jabatan saja
![jabatan](/fig/04.png)

5. Kelompok umur remaja(17-25 tahun) cenderung lebih suka membeli paket liburan
![umur](/fig/01.png)

6. Jumlah follow up yang semakin banyak sangat mempengaruhi pembelian paket liburan
![followup](/fig/insight2.png)


## Preprocessing
1. Ditemukan data yang tidak konsisten
    - Pada kolom `Gender` seharusnya **"Fe Male"** menjadi **"Female"**
    - Pada kolom `MaritalStatus` seharusnya **"Single"** diartikan sama dengan **"Unmarried"**
2. Ditemukan *missing values* pada 8 kolom dan akan ditangani dengan metode imputasi berikut ini
    - Kolom `Age` akan diisi dengan nilai mean
    - Kolom `TypeofContact` akan diisi dengan nilai 'Unknown'
    - Kolom `DurationOfPitch` akan disi dengan nilai median
    - Kolom `NumberOfFollowups` akan disi dengan nilai min
    - Kolom `PreferredPropertyStar` akan diisi dengan nilai 3
    - Kolom `NumberOfTrips` akan disi dengan nilai median
    - Kolom `NumberOfChildrenVisiting` akan diisi dengan nilai 0
    - Kolom `MonthlyIncome` akan disi dengan nilai median
3. Ditemukan 141 baris data yang duplikat sehingga perlu dihapus
4. Ditemukan bebearapa data yang dianggap outlier dengan pendekatan **Z-Score**
5. Membuat kolom baru bernama `TotalVisiting` = `NumberOfPersonVisiting` + `NumberOfChildrenVisiting`
6. Melakukan encoding data pada kolom kategorik
    - Kolom `Gender`, `ProductPitched` dan `Designation` dilakukan **Label Encoding**
    - Kolom `TypeofContact`, `Occupation`, dan `MaritalStatus` dilakukan **One Hot Encoding**
7. Melakukan transformasi data pada kolom numerik
    - Kolom `Age` ditransformasi dengan normalisasi
    - Kolom `DurationOfPitch` dan `MonthlyIncome` ditransformasi dengan standardisasi
8. Pemilihan fitur menggunakan metode **Pearson Correlation dan Chi Square Test**

## Modelling
- Data dibagi menjadi train set dan test set dengan **proporsi 80:20**
- Algoritma yang digunakan dalam pemodelan, yaitu **Logistic Regression, Decision Tree, Random Forest, AdaBoost, dan XGBoost**
- Metric evaluasi yang dipilih adalah **F1-Score dan AUC**
- Melakukan hyperparameter tuning
- Membuat feature importance dari model terbaik

<hr>

## Result

### Best Model
![result](/fig/model_result.png)

**XGBoost** menjadi model yang terbaik dengan **F1-Score paling tinggi yaitu 82.39% dan AUC 0.9707** dengan hasil confusion matrix yaitu

    - True Positive 131
    - False Positive 17
    - True Negative 760
    - False Negative 39

### Modelling Insights
1. Ada 4 feature yang cukup berpengaruh yaitu `Passport`, `ProductPitched`, `MaritalStatus`, dan `CityTier`
![feat_importance](/fig/feature_importance.png)

2. Hanya produk Standard yang cenderung suka dibeli orang yang tidak memiliki passsport
![passport](/fig/06.png)

3. Jenis produk ditawarkan berdasarkan jabatan atau pendapatan bulanan
![income](/fig/05.png)

4. Produk Basic lebih banyak dibeli pelanggan dengan yang belum menikah
![status](/fig/07.png)

5. Pelanggan yang tinggal di City Tier 1 atau 2 lebih banyak membeli produk Basic sedangkan di City Tier 3 lebih banyak yang membeli produk Deluxe
![city](/fig/08.png)

### Business Impact
Berdasarkan pengujian terhadap test data, model machine learning yang dibuat berhasil **menaikkan conversion rate 88.5%** (148 orang dari 170 orang) dan **mengurangi biaya pemasaran 83%** (35097 USD).
![impact](/fig/model_impact.PNG)

<hr>

## Recommendation
1. Melakukan **marketing campaign terhadap potential customer untuk paket Wellness Tourism** dengan ketentuan:
    - Jika paket Wellness terdiri dari beberapa jenis maka bisa diprioritaskan **dari yang paling murah sesuai dengan jabatan** pekerjaan pelanggannya.
    - Prioritaskan dahulu pada kelompok umur **Remaja (18-25 tahun) dengan durasi pitch di bawah 20 menit**.
    - **Paket Wellness paling murah** bisa ditawarkan pada pelanggan dengan **status unmarried atau tinggal di city tier 1 atau 2**.
    - **Paket Wellness yang medium** bisa ditawarkan pada pelanggan yang **belum memiliki passport atau tinggal di city tier 3**.
    - **Paket Wellness lainnya bisa ditawarkan sesuai dengan montly income** pelanggan tersebut.
    - Jangan lupa melakukan **follow up lebih dari 3 kali**.
2. Jika menggunakan model, revenue yang didapatkan lebih sedikit, maka kami merekomendasikan **marketing cost yang tersisa untuk digunakan mencari basis pelanggan baru** sehingga revenue yang dihasilkan meningkat.