# Essendiary

Aplikasi jurnal perasaan (PWA): tuliskan apa yang kamu rasakan di menit dan jam tertentu.
Login dan penyimpanan memakai **Firebase** (Authentication Email/Password + Cloud Firestore), di-host lewat **GitHub Pages**.

## Fitur
- Daftar / masuk / reset kata sandi
- Catat perasaan dengan cap waktu otomatis (menit & jam), bisa diubah manual
- 10 pilihan suasana hati, cari & filter jurnal, ubah / hapus catatan
- Ringkasan: total catatan, hari beruntun, perasaan 30 hari, jam paling sering menulis
- Ekspor jurnal ke .txt, bisa dibuka offline, bisa di-install ke layar utama

## Struktur
```
icons/  .nojekyll  README.md  index.html  manifest.json  service-worker.js
```

## Setup Firebase (project essendiary-9cdf7)
1. **Authentication → Sign-in method**: Email/Password sudah *Enabled*.
2. **Firestore Database → Rules**: ganti aturan `if false` dengan aturan di bawah lalu **Publish**.

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/entries/{entryId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```
3. (Opsional) **Authentication → Settings → Authorized domains**: tambahkan `USERNAME.github.io`.

## Deploy ke GitHub Pages
1. Upload semua isi folder ini ke repository GitHub (root).
2. **Settings → Pages → Deploy from a branch → main / (root)**.
3. Buka `https://USERNAME.github.io/NAMA-REPO/`.

Data tersimpan di `users/{uid}/entries/{id}` dengan field: `text`, `mood`, `at`, `createdAt`, `updatedAt`.
