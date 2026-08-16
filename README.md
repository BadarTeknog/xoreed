# Sistem Dompet Digital Perangkat Keras

**Non-Custodial · Keamanan Berlapis · Tanpa Komponen Mekanik**

## Abstrak

Dokumen ini menjelaskan rancangan dan prinsip kerja sistem dompet digital berbasis perangkat keras yang dirancang untuk memberikan keamanan tinggi, kerahasiaan data, serta kendali penuh di tangan pengguna. Sistem ini mengadopsi pendekatan **non-custodial**, di mana seluruh kunci keamanan dihasilkan, disimpan, dan digunakan secara eksklusif oleh pengguna tanpa keterlibatan pihak kami dalam bentuk apa pun.

## Daftar Isi

- [Tujuan Sistem](#tujuan-sistem)
- [Prinsip Desain](#prinsip-desain)
- [Arsitektur Umum](#arsitektur-umum)
- [Desain Tanpa Komponen Mekanik](#desain-tanpa-komponen-mekanik)
- [Model Keamanan](#model-keamanan)
- [Mekanisme Konfirmasi Tindakan](#mekanisme-konfirmasi-tindakan)
- [Penandatanganan Transaksi](#penandatanganan-transaksi)
- [Kriptografi dan Penyimpanan Data](#kriptografi-dan-penyimpanan-data)
- [Sumber Entropi dan Generasi Nilai Acak](#sumber-entropi-dan-generasi-nilai-acak)
- [Penerapan Kriptografi Kurva Eliptik](#penerapan-kriptografi-kurva-eliptik)
- [Keandalan Kriptografi Jangka Panjang](#keandalan-kriptografi-jangka-panjang)
- [Pencadangan Data dengan NFC](#pencadangan-data-dengan-nfc)
- [Model Non-Custodial dan Tanggung Jawab Pengguna](#model-non-custodial-dan-tanggung-jawab-pengguna)
- [Kemudahan Penggunaan](#kemudahan-penggunaan)
- [Pemulihan Dompet](#pemulihan-dompet)
- [Spesifikasi Material](#spesifikasi-material)
- [Kesimpulan](#kesimpulan)

## Tujuan Sistem

Tujuan utama sistem ini adalah menyediakan sarana penyimpanan dan penandatanganan transaksi aset kripto yang aman, tahan terhadap malware, serta andal untuk penggunaan jangka panjang. Sistem ini dirancang untuk mengurangi ketergantungan pada kepercayaan terhadap perangkat lunak eksternal dan meminimalkan risiko akibat kesalahan penggunaan.

## Prinsip Desain

1. Kendali penuh berada di tangan pengguna.
2. Kerahasiaan data sebagai prioritas utama.
3. Tidak adanya ketergantungan pada koneksi online.
4. Tidak adanya akses atau pengetahuan pihak kami terhadap data pengguna.
5. Ketahanan perangkat untuk penggunaan jangka panjang.

## Arsitektur Umum

Sistem bekerja secara terisolasi dari sistem komputer pengguna. Perangkat eksternal hanya berfungsi sebagai antarmuka untuk menampilkan informasi dan mengirim perintah, sementara seluruh proses sensitif dilakukan di dalam perangkat. Dengan pendekatan ini, sistem eksternal tidak memiliki kewenangan untuk menandatangani transaksi atau mengakses kunci keamanan.

## Desain Tanpa Komponen Mekanik

Perangkat dirancang tanpa komponen mekanik seperti tombol fisik. Seluruh interaksi dilakukan melalui tampilan visual dan mekanisme verifikasi digital. Desain ini bertujuan untuk:

- Mengurangi risiko kegagalan fisik
- Meningkatkan usia pakai perangkat
- Menjaga konsistensi perilaku perangkat dalam jangka panjang

## Model Keamanan

Keamanan sistem dibangun secara berlapis, mencakup:

- Autentikasi pengguna untuk akses perangkat
- Pembatasan jumlah percobaan untuk mencegah upaya penebakan
- Penguncian otomatis saat tidak ada aktivitas
- Konfirmasi visual untuk setiap tindakan penting

Seluruh tindakan sensitif memerlukan persetujuan aktif dari pengguna langsung melalui perangkat.

## Mekanisme Konfirmasi Tindakan

Setiap transaksi atau tindakan penting harus dikonfirmasi menggunakan kode verifikasi yang dihasilkan secara acak dan hanya berlaku satu kali. Kode ini ditampilkan langsung pada layar perangkat dan diverifikasi melalui aplikasi pendamping. Mekanisme ini memastikan bahwa tidak ada transaksi yang dapat dijalankan secara tersembunyi atau otomatis.

## Penandatanganan Transaksi

Perangkat berfungsi sebagai alat penandatanganan transaksi aset kripto. Proses penandatanganan hanya dapat dilakukan setelah pengguna memberikan persetujuan langsung. Kunci privat tidak pernah meninggalkan perangkat dan tidak pernah terekspos ke sistem eksternal.

## Kriptografi dan Penyimpanan Data

Data rahasia disimpan dalam bentuk terenkripsi menggunakan mekanisme kriptografi yang kuat. Setiap dompet memiliki perlindungan tersendiri dan tidak saling bergantung. Pemisahan kata sandi diterapkan antara akses perangkat, dompet, dan cadangan untuk membatasi dampak risiko apabila salah satu lapisan keamanan terganggu.

## Sumber Entropi dan Generasi Nilai Acak

Sistem ini menggunakan pendekatan penggabungan beberapa sumber entropi non-deterministik untuk seluruh proses kriptografi yang memerlukan nilai acak. Sumber entropi tersebut mencakup:

- **True Random Number Generator (TRNG)** internal
- Variasi **jitter waktu** internal
- **Noise** dari masukan analog yang tidak bersifat deterministik

Pendekatan ini dirancang untuk menghindari ketergantungan pada satu sumber entropi tunggal dan meminimalkan risiko kelemahan akibat bias, pola, atau kondisi lingkungan tertentu. Seluruh nilai entropi yang dikumpulkan digabungkan dan diproses menggunakan fungsi hash kriptografis sebagai mekanisme ekstraksi, sehingga menghasilkan keluaran dengan distribusi yang seragam dan sulit diprediksi.

Nilai acak yang dihasilkan tidak bergantung pada seed algoritmik statis, bersifat sementara, dan tidak disimpan setelah digunakan, sehingga mengurangi risiko kebocoran, pemanfaatan ulang, atau reproduksi nilai pada proses berikutnya.

## Penerapan Kriptografi Kurva Eliptik

Sistem ini mengadopsi kriptografi berbasis **Elliptic Curve** untuk pengelolaan kunci dan proses penandatanganan transaksi aset kripto. Seluruh proses generasi kunci privat dan nilai acak pendukung pada mekanisme ini memanfaatkan keluaran dari sistem penghasil entropi non-deterministik yang telah melalui proses penggabungan dan ekstraksi.

Pendekatan ini dirancang untuk:

- Mencegah penggunaan nilai nonce yang dapat diprediksi
- Menghindari penggunaan ulang nilai acak pada proses penandatanganan
- Menekan risiko kebocoran kunci privat akibat kualitas entropi yang tidak memadai

## Keandalan Kriptografi Jangka Panjang

Keamanan kriptografi tidak hanya bergantung pada kekuatan algoritma yang digunakan, tetapi juga pada kualitas sumber entropi yang menjadi fondasi sistem. Oleh karena itu, sistem ini dirancang dengan perhatian khusus terhadap kualitas bilangan acak sebagai bagian penting dari arsitektur keamanan, guna memastikan keandalan dan konsistensi untuk penggunaan jangka panjang.

## Pencadangan Data dengan NFC

Sebagai opsi tambahan, sistem menyediakan mekanisme pencadangan data terenkripsi menggunakan media NFC. Metode ini dirancang untuk memberikan kemudahan penggunaan dan ketahanan fisik yang lebih baik dibandingkan kertas. Data pada media NFC tetap tidak dapat digunakan tanpa kata sandi yang sesuai.

> **Catatan:** Metode ini bersifat opsional dan tidak menggantikan cadangan fisik utama yang dianjurkan untuk disimpan secara aman oleh pengguna.

## Model Non-Custodial dan Tanggung Jawab Pengguna

Sistem ini sepenuhnya bersifat **non-custodial**. Kami tidak mengetahui, menyimpan, atau memiliki akses terhadap kunci keamanan, data rahasia, maupun aset pengguna. Kami tidak memiliki kemampuan teknis untuk memulihkan dompet, mengatur ulang kata sandi, atau mengakses aset pengguna.

Seluruh tanggung jawab pengelolaan, penyimpanan cadangan, dan pemulihan berada sepenuhnya di tangan pengguna.

## Kemudahan Penggunaan

Meskipun dirancang dengan standar keamanan tinggi, sistem ini tetap mempertimbangkan kemudahan penggunaan. Alur interaksi dibuat sederhana, jelas, dan konsisten, sehingga dapat digunakan oleh pengguna tanpa latar belakang teknis mendalam.

## Pemulihan Dompet

Apabila perangkat mengalami kerusakan, pengguna dapat memulihkan dompet pada perangkat baru menggunakan data cadangan yang dimiliki. Proses ini dilakukan sepenuhnya oleh pengguna tanpa keterlibatan pihak kami.

## Spesifikasi Material

| Komponen | Material |
|---|---|
| Bodi | Faux Carbon Fiber |
| Penguat | Serat Aramid (Kevlar) |
| Resin | Epoxy Resin |

## Kesimpulan

Sistem dompet digital berbasis perangkat keras ini dirancang untuk memberikan keseimbangan antara keamanan, kerahasiaan, dan kemudahan penggunaan. Dengan pendekatan tanpa komponen mekanik, konfirmasi visual, kriptografi berlapis, serta model non-custodial, sistem ini ditujukan untuk menjadi solusi penyimpanan aset kripto yang aman, andal, dan berkelanjutan dalam jangka panjang.

---

## Disclaimer

Kami tidak mengetahui, menyimpan, atau memiliki akses terhadap data rahasia, kunci keamanan, maupun aset yang dikelola oleh pengguna. Seluruh tanggung jawab keamanan dan pemulihan aset sepenuhnya berada di tangan pengguna.