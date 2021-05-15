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
### 11. Varian dan Standar Deviasi
Menghitung variansi dan standar deviasi sampel pada kolom 'Pendapatan' dan 'Harga'
```python
df[['Pendapatan', 'Harga']].agg([np.var, np.std], ddof = 1)
```
---
### 12. Korelasi
**Korelasi** digunakan untuk mengukur seberapa besar hubungan antara satu variabel dengan variabel lainnya. Misalnya mencari hubungan antara tinggi badan dengan berat badan. Jenis-jenis korelasi adalah:
1. Korelasi **Pearson**
   Pearson menghasilkan correlation coefficient. Digunakan untuk mengukur kekuatan hubungan antar dua variabel.
   
   ![image](https://user-images.githubusercontent.com/49611937/118357286-7e686680-b5a3-11eb-8c72-c183bf7997a3.png)
   Syarat penggunaan Pearson adalah:
   - Nilai berskala interval/rasio
   - Terdapat hubungan linear antara kedua variabel (garis lurus)
   - Kedua variabel berdistribusi normal
   - Homoskedastis (data berdistribusi seragam dalam garis regresi)
   
   Rumusnya adalah:
   
   ![image](https://user-images.githubusercontent.com/49611937/118357335-d8692c00-b5a3-11eb-9761-e9cf4e0ea0cd.png)

2. Korelasi **Spearman**
   Spearman merupakan pengukuran korelasi non-prametrik. Rumusnya adalah:
   
   ![image](https://user-images.githubusercontent.com/49611937/118357375-0d757e80-b5a4-11eb-8499-34ec12973161.png)

   Keterangan:
      - _ρ_ adalah nilai korelasi Spearman
      - _di_ adalah nilai beda antara kedua variabel
      - _n_ adalah jumlah data
   
   Syarat penggunaan Spearman adalah:
   - Nilai berskala interval/rasio
   - Terdapat hubungan linear antara kedua variabel (garis lurus)
   - Kedua variabel berdistribusi normal
   - Homoskedastis (data berdistribusi seragam dalam garis regresi)
            
4. Korelasi **Kendall**

