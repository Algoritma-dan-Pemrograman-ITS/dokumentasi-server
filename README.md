# Dokumentasi Server Laboratorium Algoritma dan Pemrogaman ITS

## Spesifikasi Server

TBD

## Koneksi ke Server Melalui SSH

Sebelum melakukan sambungan ke server Alpro, Anda diwajibkan memenuhi salah satu dari syarat antara lain:

- Berada di dalam jaringan kampus ITS
- Menggunakan [VPN ITS](https://id.its.ac.id/otp/)

Alamat IP dari server adalah `10.21.85.20` sehingga sambungan SSH dapat dilakukan dengan menggunakan perintah sebagai berikut:

```bash
ssh alpro@10.21.82.20
```

Kemudian Anda akan diminta kata sandi yang dapat diperoleh dari admin lain jika Anda tidak mengetahuinya. Setelah sambungan berhasil, Anda dapat mengakses shell dari server yang ditandai dengan teks sebagai berikut:

```bash
alpro@SERVER-ALPRO:~$
```

> Sambungan SSH menggunakan kata sandi sangat tidak direkomendasikan! Diharapkan anda mempelajari konsep [public key cryptography](https://youtu.be/GSIDS_lvRv4?si=OVtxEhVKyWRboUvr) kemudian membuat private key Anda sendiri (private key jangan sampai hilang maupun dicuri) melalui [petunjuk pembuatan private-public key](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-20-04) **hingga tahap ke-3!**

## Akses Internet pada Server

Secara default, server Alpro berjalan menggunakan internet ITS yang **mewajibkan penggunanya untuk login**. Oleh karena itu, Anda tidak dapat mengakses internet di awal menggunakan server baik melalui SSH maupun mengoperasikan servernya langsung di lab. Terdapat dua cara jika Anda ingin melakukan akses internet.

### Akses Internet Jika Server Dioperasikan Langsung dari Lab

Anda dapat membuka peramban yang ada di server dan login menggunakan akun ITS untuk akses internet selayaknya Anda menggunakan WiFi/Ethernet pada umumnya.

### Akses Internet Jika Server Dioperasikan Melalui Sambungan SSH

Anda tidak dapat mengakses GUI dan tentunya peramban pada sambungan SSH sehingga Anda memerlukan konfigurasi melalui proxy line sebagai berikut:

1. Buat VPN dan proxy melalui One Time Password sesuai dengan [petunjuk](https://www.its.ac.id/dptsi/wp-content/uploads/sites/8/2023/02/PANDUAN-PENGGUNAAN-VPN.pdf) **hingga langkah ketiga**
2. Perhatikan kolom **proxy line**. Inilah konfigurasi yang harus Anda copy untuk digunakan pada langkah-langkah berikutnya
3. Pastikan server telah terhubung dengan DNS Server ITS yaitu `202.46.129.2`. Anda dapat melakukan pemeriksaan menggunakan perintah `sudo resolvectl status` dan pastikan `Link 2 (enp3s0)` bernilai `202.46.129.2`
4. Eksekusi perintah `nano /home/alpro/.bashrc` dan masukkan dua baris berikut

   ```bash
   # Ganti variabel dibawah sesuai dengan proxy line di atas
   export http_proxy=http://SOMETHING@proxy.its.ac.id:8080
   export https_proxy=http://SOMETHING@proxy.its.ac.id:8080
   ```

5. Eksekusi perintah `source /home/alpro/.bashrc` untuk memuat ulang environment variable
6. Sampai langkah ini, Anda seharusnya sudah dapat mengakses internet. Namun, untuk menjalankan perintah APT, Anda perlu melanjutkan hingga langkah kebawah
7. Agar perintah APT dapat bekerja, Anda perlu mengubah konfigurasi proxynya dengan perintah `sudo nano /etc/apt/apt.conf.d/proxy.conf` kemudian mengisikan dua baris berikut (**jangan lupa mengganti proxynya sesuai dengan yang didapatkan**):

   ```txt
   Acquire::http::Proxy "http://SOMETHING@proxy.its.ac.id:8080";
   Acquire::https::Proxy "http://SOMETHING@proxy.its.ac.id:8080";
   ```

> Sangat disarankan untuk menghapus konfigurasi proxy pada `/home/alpro/.bashrc` dan `/etc/apt/apt.conf.d/proxy.conf` apabila sudah tidak memerlukan akses internet untuk menghindari fitnah!

## Aplikasi Web yang Tersedia

TBD, makan dulu
