# Cara deploy "Alur" jadi aplikasi yang bisa di-install

Folder ini berisi aplikasi siap pakai:
- `index.html` — aplikasinya
- `manifest.json` — identitas aplikasi (nama, ikon, warna)
- `service-worker.js` — bikin bisa dibuka offline & terasa seperti app
- `icons/` — ikon aplikasi

Data transaksi disimpan di **localStorage** browser/HP masing-masing orang yang membuka — jadi tidak perlu server database.

## Opsi termudah & gratis: Netlify Drop (tanpa akun pun bisa)

1. Buka https://app.netlify.com/drop di browser.
2. Seret (drag & drop) seluruh folder `alur-pwa` ke halaman tersebut.
3. Tunggu beberapa detik — Netlify akan memberi URL publik seperti `https://nama-acak.netlify.app`.
4. Buka URL itu di HP (Chrome/Safari) → akan muncul opsi **"Tambahkan ke Layar Utama" / "Install app"**.
5. Selesai — ikonnya akan muncul di HP seperti aplikasi biasa.

> Kalau mau nama domain lebih rapi atau update di kemudian hari, buat akun gratis Netlify lalu hubungkan ke folder yang sama.

## Alternatif: GitHub Pages

1. Buat repository baru di GitHub, upload semua isi folder `alur-pwa`.
2. Buka **Settings → Pages**, pilih branch `main` dan folder `/root`.
3. GitHub akan memberi URL seperti `https://username.github.io/nama-repo/`.
4. Buka URL itu di HP → install seperti langkah di atas.

## Cara install di HP setelah situsnya online

**Android (Chrome):**
Buka link → ketuk menu titik tiga (⋮) → **"Tambahkan ke layar utama" / "Install app"**.

**iPhone (Safari):**
Buka link → ketuk ikon **Share/Bagikan** → **"Tambah ke Layar Utama"**.

Setelah itu ikon "Alur" muncul di home screen dan terbuka layar penuh tanpa address bar, seperti aplikasi native.

## Catatan penting soal data

- Data tersimpan **per browser/per perangkat** (localStorage), bukan disinkron antar HP.
- Kalau cache/data browser dibersihkan, catatan transaksi ikut hilang — sebaiknya jangan gunakan mode "Private/Incognito".
- Kalau nanti butuh data tersinkron antar HP (misalnya HP dan laptop sama-sama update saldo), itu perlu backend/database — beri tahu saya kalau mau dibuatkan.
