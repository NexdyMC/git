### Cara 1: Simpan Sementara Perubahan Anda (Paling Aman)

Jika Anda ingin menyimpan perubahan yang sedang dikerjakan saat ini tanpa menghapusnya, gunakan perintah **Stash**:

```bash
git stash

```

Setelah itu, jalankan kembali perintah *checkout* Anda:

```bash
git checkout 73ade17

```

*(Catatan: Jika nanti Anda ingin mengembalikan perubahan yang di-*stash* tadi, tinggal ketik `git stash pop`)*.

---

### Cara 2: Hapus Permanen Perubahan Lokal (Discard Changes)

⚠️ **Peringatan:** Cara ini akan **menghapus semua perubahan lokal** yang belum di-commit pada file-file tersebut secara permanen. Gunakan ini hanya jika Anda yakin perubahan saat ini tidak diperlukan lagi:

```bash
git reset --hard

```

Setelah itu, langsung jalankan ulang perintah *checkout*:

```bash
git checkout 73ade17

```
