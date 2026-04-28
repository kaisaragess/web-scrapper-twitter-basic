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
