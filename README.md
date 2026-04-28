# web-scrapper-twitter-basic
it's not optimal scrapper you know. Some data may not record in the output file but you can try. 


# 🐦 Twitter/X Web Scraper menggunakan Tweet-Harvest

## 📝 Deskripsi
Proyek ini adalah *script* berbasis Google Colab / Jupyter Notebook untuk mengekstrak data tweet (*web scraping*) dari Twitter/X. Alat ini menggunakan **[tweet-harvest](https://github.com/vkrx/tweet-harvest)** untuk melakukan *crawling* data tanpa API resmi Twitter, serta **Pandas** untuk membaca dan memanipulasi data hasil *scraping* dalam format CSV.

## ✨ Fitur
* **Tanpa API Berbayar**: Menggunakan `auth_token` dari sesi login browser.
* **Kustomisasi Pencarian**: Mendukung operator pencarian lanjutan Twitter (Advanced Search) seperti filter bahasa, rentang waktu, pencarian *hashtag*, hingga mengambil balasan dari sebuah *thread*.
* **Otomatisasi Ekspor**: Hasil *scraping* langsung disimpan dalam format `.csv` dan siap diolah.

## ⚙️ Persiapan (Prerequisites)
1. **Google Colab / Jupyter Notebook**: Disarankan menggunakan Google Colab agar tidak perlu mengatur *environment* lokal.
2. **Twitter Auth Token**: Anda memerlukan token dari akun Twitter/X aktif. 
   * *Cara mendapatkan*: Buka browser web (Chrome/Firefox) -> Login Twitter -> Buka Developer Tools (F12) -> Tab `Application` (atau `Storage`) -> `Cookies` -> `https://twitter.com` -> Cari *Value* dari *Name* `auth_token`.

## 🚀 Cara Penggunaan

### 1. Konfigurasi Awal
Masukkan *auth token* Twitter Anda ke dalam *script*.

```python
twitter_auth_token = "MASUKKAN_AUTH_TOKEN_ANDA_DI_SINI"
```

### 2. Instalasi Dependensi (Python & Node.js)
Proses ini akan menginstal `pandas` untuk pengolahan data dan mengonfigurasi Node.js (versi 20) yang menjadi syarat berjalannya `tweet-harvest`. Jalankan perintah berikut di dalam sel notebook Anda:

```bash
# Install Pandas
!pip install pandas

# Update apt-get dan install sertifikat yang dibutuhkan
!sudo apt-get update
!sudo apt-get install -y ca-certificates curl gnupg

# Menambahkan GPG Key NodeSource
!curl -fsSL [https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key](https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key) | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg

# Menambahkan repository Node.js v20
!NODE_MAJOR=20 && echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] [https://deb.nodesource.com/node_$NODE_MAJOR.x](https://deb.nodesource.com/node_$NODE_MAJOR.x) nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list

# Install Node.js
!sudo apt-get update
!sudo apt-get install nodejs -y

# Cek versi Node.js untuk memastikan instalasi berhasil
!node -v
```


### 3. Konfigurasi dan Eksekusi web scrapper
Tentukan parameter scraping Anda, seperti nama file output, batas jumlah data (limit), dan kata kunci pencarian. Setelah itu, instal browser engine dan jalankan proses crawling.

 ``` python
# Menentukan nama file output dan ID Tweet target
filename = 'data.csv'
#target_id bisa diganti
target_id = '2040575505964191995' 


# Jika ingin memastikan balasannya hanya bahasa Indonesia:
search_keyword = f"conversation_id:{target_id} lang:id"

# Mencari tweet tentang "pemilu" dari 1 Januari 2024 sampai 14 Februari 2024
#search_keyword = "pemilu since:2024-01-01 until:2024-02-14"

# Mencari kata spesifik
#search_keyword = "kecerdasan buatan"

# Mencari hashtag
#search_keyword = "#teknologi"

# Mencari kata "banjir" khusus dalam bahasa Indonesia
#search_keyword = "banjir lang:id"
limit = 500

# Install dependencies untuk browser engine bawaan (Playwright)
!npx playwright install-deps

# Menjalankan proses scraping dengan tweet-harvest
!npx -y tweet-harvest@2.6.1 -o "{filename}" -s "{search_keyword}" --tab "LATEST" -l {limit} --token {twitter_auth_token}
'''
### 4. Membaca dan Menampilkan Hasil Ekstraksi
Setelah proses *scraping* selesai, data akan secara otomatis tersimpan di dalam direktori `tweets-data`. Langkah terakhir ini menggunakan *library* Pandas untuk memuat file CSV tersebut ke dalam DataFrame, menampilkan pratinjau tabel datanya, serta menghitung total tweet yang berhasil ditarik.

```python
import pandas as pd

# Menentukan jalur file CSV hasil crawling
file_path = f"tweets-data/{filename}"

# Membaca data ke dalam DataFrame Pandas
df = pd.read_csv(file_path)

# Menampilkan pratinjau data
display(df)

# Menampilkan total tweet yang berhasil diambil
num_tweets = len(df)
print(f'Jumlah tweet yang berhasil diekstrak adalah: {num_tweets}')
```
