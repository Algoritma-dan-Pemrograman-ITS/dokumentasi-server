# Update DOMJudge Setiap Semester

## Latar Belakang

Untuk mengatasi security vulnerability maupun update tambahan fitur yang mungkin useful, maka hendaknya DOMJudge selalu diupdate minimal setiap pergantian semester atau ketika versi baru rilis.

## Langkah-Langkah

1. Clone repository [domjudge](https://github.com/Algoritma-dan-Pemrograman-ITS/dokumentasi-server) dari Github Alpro.
2. Tambahkan remote `repo-domjudge-asli` pada repository tersebut:
    ```bash
    git remote add repo-domjudge-asli git@github.com:DOMjudge/domjudge.git
    ```
3. Merge branch dari repo domjudge asli dengan nama branch sesuai dengan versi terbaru dari DOMJudge tanpa patch version. Contoh pada saat tutorial ini dibuat, versi terbaru adalah 8.2.1, maka nama branch-nya adalah 8.2:
    ```bash
    git fetch repo-domjudge-asli 8.2
    git merge repo-domjudge-asli/8.2
    ```
4. Tolong dibaca jika ada merge conflict dan lakukan commit apabila sudah di-fix
5. Push ke origin/main:
   ```bash
   git push origin main
   ```
6. [Buat release baru](https://github.com/Algoritma-dan-Pemrograman-ITS/domjudge/releases/new) di Github dengan nama tag sesuai versi lengkap DOMJudge diawali dengan v (Contoh: 8.2.1 menjadi v8.2.1). Judul dapat diisi dengan `DOMJudge [Versi] - [Dasar Pemrograman/Struktur Data] [Tahun]`, Contoh: `DOMJudge 8.2.1 - Dasar Pemrograman 2023`. Deskripsi dapat dikosongkan. Kemudian, publish release.
7. Clone repository [domjudge-packaging](https://github.com/Algoritma-dan-Pemrograman-ITS/domjudge-packaging)
8. Masuk ke folder `docker`
9. Buka versi yang ada pada [Github](https://github.com/Algoritma-dan-Pemrograman-ITS/domjudge/tags). Copy link untuk download source code (tar.gz).
10. Unduh source code tersebut:
    ```bash
    wget -O domjudge.tar.gz [URL yang dicopy]
    ``` 
11. TBD, lanjut kerja dulu
