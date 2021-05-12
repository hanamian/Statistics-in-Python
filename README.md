# Statistics in Python

### Perhitungan
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
### Subsetting (Mengambil data)

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
### Mean (Rata-rata)
```python
# Menggunakan pandas, Nilai rata-rata dari pendapatan produk_A
produk_A['Pendapatan'].mean()

# Menggunakan numpy, Nilai rata-rata dari pendapatan produk_A
np.mean(produk_A['Pendapatan'])
```
---
### Median 
```python
# Menggunakan pandas, Nilai tengah dari pendapatan produk_A
produk_A['Pendapatan'].median()

# Menggunakan numpy, Nilai tengah dari pendapatan produk_A
np.median(produk_A['Pendapatan'])
```
---
### Modus (Yang Sering Muncul) 
menggunakan **.value_counts()**
```python
df['Produk'].value_counts()
```
---
### Quantile
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
### Aggregate 
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

