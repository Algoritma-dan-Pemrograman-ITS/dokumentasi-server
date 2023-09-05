# Migrasi Database Setiap Semester

## Latar Belakang

Implementasi DOMJudge saat ini mewajibkan database untuk dimigrasi demi kemudahan dalam pencarian soal (DOMJudge tidak memiliki fitur pencarian soal pada dropdown).

## Langkah-Langkah

1. Pastikan koor praktikum sebelumnya sudah melakukan backup data baik soal maupun scoreboard untuk keperluan arsip
2. Buat database baru di [phpMyAdmin](https://www.its.ac.id/informatika/domjudge/db/) dengan nama `dasar_pemrograman_20XX` atau `struktur_data_20XX` (buatkan usernya juga)
3. Ubah `MYSQL_DATABASE`, `MYSQL_USER`, dan `MYSQL_PASSWORD` pada `/home/alpro/alpro-domjudge-packaging/docker/.env` sesuai dengan nilai yang ada di poin sebelumnya
4. Jalankan perintah berikut pada direktori tersebut:

    ```bash
    docker compose -p domjudge up -d
    ```

5. Jalankan perintah berikut untuk mendapatkan password admin dan judgehost baru:

    ```bash
    docker logs domserver
    ```

6. Cari baris yang berisikan berikut pada keluaran langkah nomor 5:

    ```bash
    Initial admin password is SOMETHING

    Initial judgehost password is SOMETHING
    ```

7. Update `JUDGEDAEMON_PASSWORD` pada .env di atas dengan nilai judgehost password pada langkah sebelumnya.
8. Ulangi langkah nomor 4
9. Login portal menggunakan initial admin password di atas
10. Lakukan konfigurasi sesuai dengan lampiran

## Petunjuk Impor Data Praktikan dan Asisten

Hubungi Bagas atau Nopal

## Lampiran

### Perubahan Scoring Configuration

|Setting|Nilai|Keterangan|
|---|---|---|
|Result remap|`no-output -> wrong-answer`|Membingungkan praktikan|

### Perubahan Display Configuration

|Setting|Nilai|Keterangan|
|---|---|---|
|Time format|`D, j F H:i A`|Defaultnya hanya `H:i` dimana tidak deskriptif untuk revisi yang berhari-hari|
|Allow team submission download|kondisional|<ul><li>Untuk praktikum dianjurkan bernilai `yes` (agar praktikan bisa belajar dari kesalahan)</li><li>Untuk contest ICPC-based seperti Quadrathlon HMTC (jika ada), maka nilainya `no`</li></ul>|

### Perubahan External System Configuration

|Setting|Nilai|Keterangan|
|---|---|---|
|Data source|`configuration data external`|Wajib agar dapat menggunakan `external_id` pada teams dan user yang akan diisi dengan NRP untuk keperluan autentikasi|

### Languages

- Disable semua yang tidak dipakai