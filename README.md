# Statistics in Python

### 1. Perhitungan
```python
df.describe()

# MaxMin 
df.max()
df['Harga'].max()
df['Harga'].min()

# Jumlah
df.sum()
df.sum(numeric_only=True)
df[['Harga', 'Pendapatan']].sum()

```
---
### 2. Subsetting (Mengambil data)

#### Subset/ Mengambil Kolom
```python
df['Pendapatan']
df[['Jenis Kelamin', 'Pendapatan']]
```
#### Subset/ Mengambil Baris
```python
# Baris ke-0 s/d 9
df[:10]

# Baris ke-3 s/d 5
df[3:6]

# Baris ke 1, 5, 9
df.loc[1, 5, 9]

# Kolom 'Jenis Kelamin' dan 'Pendapatan' pada Baris ke 1 s/d 10
df[['Jenis Kelamin','Pendapatan']][1:11]

# Kolom 'Jenis Kelamin' dan 'Pendapatan' pada Baris ke 1, 2, 10, 20
df[['Jenis Kelamin','Pendapatan']].loc[[1, 2, 10, 20]]

# Kolom spesifik dengan Baris tertentu
produk_A = df[df['Produk']=='A']
```
---
### 3. Mean (Rata-rata)
```python
# Menggunakan pandas, Nilai rata-rata dari pendapatan produk_A
produk_A['Pendapatan'].mean()

# Menggunakan numpy, Nilai rata-rata dari pendapatan produk_A
np.mean(produk_A['Pendapatan'])
```
---
### 4. Median 
```python
# Menggunakan pandas, Nilai tengah dari pendapatan produk_A
produk_A['Pendapatan'].median()

# Menggunakan numpy, Nilai tengah dari pendapatan produk_A
np.median(produk_A['Pendapatan'])
```
---
### 5. Modus (Yang Sering Muncul) 
menggunakan **.value_counts()**
```python
df['Produk'].value_counts()
```
---
### 6. Quantile
**Kuantil** atau **Fraktil** adalah nilai-nilai data yang membagi -data yang telah diurutkan sebelumnya- menjadi beberapa bagian yang sama besar ukurannya.
1. **Kuartil**: Adalah kuantil yang membagi data menjadi empat bagian sama besar. **Kuartil ke-2** dari adalah **median** data.
2. **Desil**: Adalah kuantil yang membagi data menjadi 10 bagian sama besar.
3. **Persentil**: Adalah kuantil yang membagi data menjadi 100 bagian sama besar.

```python
# Menggunakan pandas
df['Pendapatan'].quantile(q=0.5)

# Menggunakan numpy
np.quantile(df['Pendapatan'], q=0.5)
```
---
### 7. Aggregate 
Menghitung **mean dan median** sekaligus dengan **.agg([...])**
```python
# Menghitung mean dan median 'Pendapatan' dan 'Harga'
df[['Pendapatan','Harga']].agg([np.mean, np.median])

# Menghitung mean dan median 'Pendapatan' dan 'Harga' setiap produk
df[['Pendapatan','Harga','Produk']].groupby('Produk).agg([np.mean, np.median])
```
Result:

![image](https://user-images.githubusercontent.com/49611937/117940698-89b55b00-b333-11eb-8587-36dfff323aea.png)

---
### 8. Measures of Dispersion (Ukuran sebaran)
1. Tipe Data Nominal dan Ordinal : Proporsi Kategori (Categorical Proportion), Persen Proporsi (Percent Proportion), Rasio Variasi (Variation Ratio)
2. Tipe Data Interval dan Rasio  : Rentang (Range), Variansi (Variance), Deviasi Baku (Standard Deviation)
```python
# Proporsi tiap produk
df['Produk'].value_counts()/df.shape[0]
```
Result:
```
D    0.25
B    0.20
C    0.20
A    0.20
E    0.15
Name: Produk, dtype: float64
```
Ukuran sebaran data pada data interval dan rasio adalah **rentang**. Rentang adalah jarak antara nilai maksimum dengan nilai minimum.
```python
df['Pendapatan'].max()-df['Pendapatan'].min()
```
Result:
```
6050000
```
---
### 9. Varian
- Menggunakan pandas : menggunakan variansi sampel
- Menggunakan numpy  : menggunakan variansi populasi

Cara agar pandas menggunakan variansi populasi maka kodenya dilengkapi dengan **var(ddof=0)**
```python
df['Pendapatan'].var()
np.var(df['Pendapatan'])

df['Pendapatan'].var(ddof=0)
```
Result:
```
1645684210526.3157
1563400000000.0
1563400000000.0
```
---
### 10. Standar Deviasi
- pandas : std sampel
- numpy  : std populasi
```python
df['Pendapatan'].std()
np.std(df['Pendapatan'])
```
Result:
```
1282842.2391417876
1282842.2391417876
```
---
### 11. Varian dan Standar Deviasi
Menghitung variansi dan standar deviasi sampel pada kolom 'Pendapatan' dan 'Harga'
```python
df[['Pendapatan', 'Harga']].agg([np.var, np.std], ddof = 1)
```
---
### 12. Korelasi
**Korelasi** digunakan untuk mengukur seberapa besar hubungan antara satu variabel dengan variabel lainnya. Misalnya mencari hubungan antara tinggi badan dengan berat badan.
Kriteria hubungan atau korelasi antar variabel adalah:

![image](https://user-images.githubusercontent.com/49611937/118376522-a0d5a080-b5f2-11eb-9195-53480a4b7404.png)

Jenis-jenis korelasi adalah:
1. Korelasi **Pearson**
   Pearson menghasilkan _correlation coefficient_. Digunakan untuk mengukur kekuatan hubungan antar dua variabel.
   
   ![image](https://user-images.githubusercontent.com/49611937/118357286-7e686680-b5a3-11eb-8c72-c183bf7997a3.png)
   
   Syarat penggunaan Pearson adalah:
   - Nilai berskala interval/rasio
   - Terdapat hubungan linear antara kedua variabel (garis lurus)
   - Kedua variabel berdistribusi normal
   - Homoskedastis (data berdistribusi seragam dalam garis regresi)
   
   Rumusnya adalah:
   
   ![image](https://user-images.githubusercontent.com/49611937/118357335-d8692c00-b5a3-11eb-9761-e9cf4e0ea0cd.png)

2. Korelasi **Spearman**
   Spearman merupakan pengukuran **korelasi non-prametrik**. Bisa untuk tipe data **ordinal**. Tidak menghiraukan asumsi seperti distribusi dari kedua variabel dan asumsi lainnya. Bedanya dengan Pearson adalah adanya pengubahan data dalam bentuk ranking sebelum menghitung nilai korelasinya. Rumusnya adalah:
   
   ![image](https://user-images.githubusercontent.com/49611937/118376259-17719e80-b5f1-11eb-8378-0a33e696bc54.png)

   Keterangan:
      - _ρ_ adalah nilai korelasi Spearman
      - _di_ adalah nilai beda antara kedua variabel
      - _n_ adalah jumlah data
            
3. Korelasi **Kendall**
   Kendall atau korelasi Tau (τ) adalah pengukuran **korelasi non-parametrik**. Rumusnya adalah:
   
   ![image](https://user-images.githubusercontent.com/49611937/118376337-a7174d00-b5f1-11eb-9913-7ca45d9936b9.png)
   
   ![image](https://user-images.githubusercontent.com/49611937/118376348-b39ba580-b5f1-11eb-81ca-3adf343cf827.png)

```python
df.corr()
df.corr(method='kendall')
df.corr(method='spearman')
```
Result:

![image](https://user-images.githubusercontent.com/49611937/118376468-358bce80-b5f2-11eb-8adc-72f53a1895d5.png)

![image](https://user-images.githubusercontent.com/49611937/118376477-43d9ea80-b5f2-11eb-83ac-e93774eef89e.png)

![image](https://user-images.githubusercontent.com/49611937/118376481-4f2d1600-b5f2-11eb-8958-551d65d0d6d2.png)

---
### 13. Statistik dalam Visualisasi

![image](https://user-images.githubusercontent.com/49611937/118376624-49840000-b5f3-11eb-8de6-a4ff10d4105d.png)

![image](https://user-images.githubusercontent.com/49611937/118377009-92d54f00-b5f5-11eb-9fcd-4b350e5a6539.png)

![image](https://user-images.githubusercontent.com/49611937/118377039-b4ced180-b5f5-11eb-814f-29acbc80017a.png)

Bar plot bisa digunakan untuk menghitung frekuensi dari data.
```python
import pandas as pd
import matplotlib.pyplot as plt
plt.clf()

df  = pd.read_csv("https://storage.googleapis.com/dqlab-dataset/dataset_statistic.csv", sep=';')
freq = df['Pendapatan'].value_counts()
print(freq)

plt.bar(x=freq.index, height=freq.values)
plt.title('plt.bar dari matplotlib.pyplot', size=14)
plt.tight_layout()
plt.show()
```
Result:
```
800000     4
1200000    3
950000     3
600000     3
400000     2
1100000    1
6450000    1
1700000    1
700000     1
1000000    1
Name: Pendapatan, dtype: int64
```
![image](https://user-images.githubusercontent.com/49611937/118377457-86ea8c80-b5f7-11eb-93aa-34d61f0df415.png)

Pie Chart.
```
import matplotlib.pyplot as plt
plt.clf()

plt.figure()
plt.pie(freq.values, labels=freq.index)
plt.title('plt.pie dari matplotlib.pyplot', size=14)
plt.tight_layout()
plt.show()
```
![image](https://user-images.githubusercontent.com/49611937/118377833-f792a880-b5f9-11eb-84ec-72304ad01191.png)

---
### 14. Transformasi Data
Mengubah dari suatu nilai ke nilai yang lain. Misalnya pada model regresi linear. 

![image](https://user-images.githubusercontent.com/49611937/118377917-6a038880-b5fa-11eb-9a19-ea805001ffb7.png)

**stats.skew(**
```python
# Membandingkan mana yang transformasi skewnya paling mendekati 0 (distribusi normal)
from scipy import stats

hasil1 = np.power(df['Pendapatan'], 1/5)
stats.skew(hasil1)

hasil2 = stats.boxcox(df['Pendapatan'])
stats.skew(hasil2)
```

- Data **skew kanan** diubah ke distribusi normal: menggunakan fungsi logaritma **.log()**, akar kuadrat **.sqrt()**, akar tiga dan akar resiprokal lainnya
- Data **skew kiri** diubah ke distribusi normal : menggunakan kuadrat, pangkat 3, dan pangkat n **.power()**.
```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from scipy import stats
plt.clf()

df  = pd.read_csv("https://storage.googleapis.com/dqlab-dataset/dataset_statistic.csv", sep=';')
```
```
plt.figure()
df['Pendapatan'].hist()
plt.title('Histogram Pendapatan', size=14)
plt.tight_layout()
plt.show()
```
Result:

![image](https://user-images.githubusercontent.com/49611937/118378403-db910600-b5fd-11eb-8e0b-0ae97ac41d1b.png)

```python
plt.figure()
np.power(df['Pendapatan'], 1/5).hist()
plt.title('Histogram pendapatan - transformasi menggunakan akar lima', size=14)
plt.tight_layout()
plt.show()
```
Result:

![image](https://user-images.githubusercontent.com/49611937/118378488-75f14980-b5fe-11eb-85b1-dc2c8d61a442.png)

```python
# Menyimpan hasil transformasi
hasil_transformasi = np.power(df['Pendapatan'], 1/5)

plt.figure()
stats.probplot(hasil_transformasi, plot=plt)
plt.title('qqplot pendapatan - transformasi menggunakan akar lima', size=14)
plt.tight_layout()
plt.show()
```
Result:

![image](https://user-images.githubusercontent.com/49611937/118378568-eef0a100-b5fe-11eb-89ce-73b839486fbf.png)

```python
plt.figure()
stats.probplot(df['Pendapatan'], plot=plt)
plt.title('qqplot pendapatan', size=14)
plt.tight_layout()
plt.show()
```
Result:

![image](https://user-images.githubusercontent.com/49611937/118378597-26f7e400-b5ff-11eb-9416-f097b71b3ecb.png)

---
### 15. Transformasi Box-Cox dari Scipy
```python
from scipy import stats

hasil, _ = stats.boxcox(df['Pendapatan'])

# Histogram
plt.figure()
pt.hist(hasil)
plt.title('Histogram', size=14)
plt.tight_layout()
plt.show()

# QQPlot
stats.probplot(hasil, plot=plt)
plt.title('qqplot', size=14)
plt.tight_layout()
plt.show()
```
Result:

![image](https://user-images.githubusercontent.com/49611937/118378734-f5334d00-b5ff-11eb-9e16-47ee9052430a.png)

![image](https://user-images.githubusercontent.com/49611937/118378737-f9f80100-b5ff-11eb-9af1-2ac0ab034891.png)

---
### 16. Transformasi Kategorik ke Angka
Menggunakan **Dummy encoding** atau  **one-hot encoding** yang dapat mengubah data bertipe karakter menjadi angka bernilai **1 dan 0**. Kita cukup menerapkan method **.get_dummies()** dari pandas.
```
dummies = pd.get_dummies(df['Produk'])

print(df['Produk']
print(dummies)
```
Sebelum transformasi:
```
0     A
1     D
2     D
3     A
4     D
5     B
6     B
7     E
8     E
9     E
10    A
11    B
12    C
13    D
14    C
15    B
16    C
17    D
18    A
19    C
Name: Produk, dtype: object
```
Setelah transformasi:
```
    A  B  C  D  E
0   1  0  0  0  0
1   0  0  0  1  0
2   0  0  0  1  0
3   1  0  0  0  0
4   0  0  0  1  0
5   0  1  0  0  0
6   0  1  0  0  0
7   0  0  0  0  1
8   0  0  0  0  1
9   0  0  0  0  1
10  1  0  0  0  0
11  0  1  0  0  0
12  0  0  1  0  0
13  0  0  0  1  0
14  0  0  1  0  0
15  0  1  0  0  0
16  0  0  1  0  0
17  0  0  0  1  0
18  1  0  0  0  0
19  0  0  1  0  0
```
---
### 17. Matrix Korelasi
menampilkan korelasi dari beberapa variabel numerik sekaligus, menggunakan method **.corr()** dari pandas untuk mendapatkan nilai korelasi dari tiap pasang variabel lalu menggunakan **plt.matshow(...)** dari matplotlib ATAU **sns.heatmap(...)** untuk membuat visualisasi.
```
import matplotlib.pyplot as plt
import seaborn as sns
plt.clf()

# Mengatur ukuran gambar
plt.rcParams['figure.dpi'] = 100

# Pandas
plt.figure()
plt.matshow(df.corr())
plt.title('Plot correlation matriks dengan .matshow', size=14)
plt.tight_layout()
plt.show()

# Seaborn
plt.figure()
sns.heatmap(df.corr(), annot=True)
plt.title('Plot correlation matriks dengan sns.heatmap', size=14)
plt.tight_layout()
plt.show()
```
Result:
![image](https://user-images.githubusercontent.com/49611937/118379328-d3d46000-b603-11eb-9180-ee1f61ea23c2.png)
![image](https://user-images.githubusercontent.com/49611937/118379336-da62d780-b603-11eb-9d39-a064df703988.png)

---
### 18. Group boxplot
```python
import matplotlib.pyplot as plt
plt.clf()

# boxplot biasa tanpa pengelompokkan
plt.figure()
df.boxplot(rot=90)

plt.title('Boxplot tanpa pengelompokkan', size=14)
plt.tight_layout()
plt.show()


# box plot dengan pengelompokkan kolom 'Produk'
plt.figure()
df.boxplot(by='Produk')
plt.tight_layout()
plt.show()
```
Result:
![image](https://user-images.githubusercontent.com/49611937/118379463-c23f8800-b604-11eb-894e-2efc80e03542.png)
![image](https://user-images.githubusercontent.com/49611937/118379465-c9669600-b604-11eb-8d4a-c6123abf5ef9.png)

---
### 19. Group Histogram
```
import matplotlib.pyplot as plt
plt.clf()

plt.figure()
df[df['Produk'] == 'A'].hist()
plt.tight_layout()
plt.show()

plt.figure()
df[df['Produk'] == 'B'].hist()
plt.tight_layout()
plt.show()

plt.figure()
df[df['Produk'] == 'C'].hist()
plt.tight_layout()
plt.show()

plt.figure()
df[df['Produk'] == 'D'].hist()
plt.tight_layout()
plt.show()

plt.figure()
df[df['Produk'] == 'E'].hist()
plt.tight_layout()
plt.show()
```
Result:

![image](https://user-images.githubusercontent.com/49611937/118379569-85c05c00-b605-11eb-8a3f-9724d04214ed.png)







