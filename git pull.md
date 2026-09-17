# Penggunaan Git Pull

Bayangkan histori Git itu seperti tumpukan blok mainan (commit) yang disusun ke atas dari bawah ke atas.

## 1. Kondisi Awal (Awal Mula Bentrok)
Kamu dan GitHub awalnya punya fondasi yang sama di blok A dan B. Lalu:
Di GitHub (Remote), ada orang lain (atau kamu dari HP/laptop lain) yang menambahkan blok C.
Di Lokal (PC kamu), kamu bikin fitur baru yaitu blok D.

```Plaintext
[ GitHub ]           [ PC Lokal ]
   (C)                   (D)
    |                     |
   (B)                   (B)
    |                     |
   (A)                   (A)
```
Karena ujungnya beda (C vs D), Git akan menolak kalau kamu langsung git push.

## 2. Bedanya Saat Kamu Melakukan pull
Cara A: `git pull origin main (Standard Merge)`
Git mengambil blok C dari GitHub, lalu membuat satu blok perekat baru (Merge Commit E) untuk menyatukan jalur C dan D.

```Plaintext
       [ PC Lokal Setelah Pull ]

                 (E) <--- Blok Merge Perekat
                /   \
              (D)   (C) <--- Diambil dari Remote
                \   /
                 (B)
                  |
                 (A)
```
Hasil: Histori kamu bercabang dan menyatu lagi. Ada blok tambahan E yang isinya cuma catatan "Menggabungkan branch".

Cara B: `git pull origin main --rebase (Rebase)`
Git secara pintar melepas dulu blok D milik kamu, memasang blok C dari GitHub di bawah, lalu menempelkan kembali blok kamu (D') di paling atas.

```Plaintext
   [ PC Lokal Setelah Pull --rebase ]

                 (D') <--- Blok kamu ditempel ulang di atas
                  |
                 (C)  <--- Diambil dari Remote
                  |
                 (B)
                  |
                 (A)
```
Hasil: Historinya lurus sempurna. Seolah-olah kamu baru mulai bikin blok D setelah blok C ada di GitHub.

## 3. Proses Akhir (git push)
Setelah salah satu proses pull di atas selesai, PC lokal kamu sekarang sudah punya histori C. Baru setelah itu kamu bisa git push dengan lancar:

```Plaintext
[ PC Lokal ]                       [ GitHub Baru ]
   (D')                                (D')
    |      ====== Push ======>          |
   (C)                                 (C)
    |                                   |
   (B)                                 (B)
```
## 4. Fun Fack
Merge (git pull): "Gabungkan dua jalan ini dan buat persimpangan baru."
Rebase (git pull --rebase): "Angkat pekerjaan saya sebentar, masukkan perubahan remote ke bawah, lalu taruh pekerjaan saya di atasnya."

## 5. kesimpulan
Ambil perubahan remote lalu satukan (Direkomendasikan)
Tarik perubahan dari GitHub dulu, lalu push kembali:

```Bash
git pull origin main --rebase
```
Jika ada conflict, selesaikan file yang conflict, lalu jalankan 

```bash
git rebase --continue.
```

Setelah proses rebase selesai, tinggal push:
```Bash
git push -u origin main
```
