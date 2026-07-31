# Cara deploy "DompetKu" ke GitHub Pages + domain custom

Folder ini berisi aplikasi siap pakai:
- `index.html` — aplikasinya
- `manifest.json` — identitas aplikasi (nama, ikon, warna)
- `service-worker.js` — bikin bisa dibuka offline & terasa seperti app
- `icons/` — ikon aplikasi (isi sendiri kalau belum ada, lihat catatan di bawah)
- `CNAME` — domain custom kamu (wajib diedit sebelum upload!)

Data transaksi disimpan di **localStorage** browser/HP masing-masing orang yang membuka — jadi tidak perlu server database.

---

## Langkah 1 — Siapkan repository di GitHub

1. Buat repository baru (public) di https://github.com/new, misalnya nama `dompetku-pwa`.
2. Upload semua isi folder `dompetku-pwa` ke repo itu (lewat web "Add file → Upload files", atau lewat `git push`).
3. Buka **Settings → Pages** di repo tersebut.
4. Di bagian **Build and deployment → Source**, pilih **Deploy from a branch**.
5. Pilih branch `main` dan folder `/ (root)`, lalu **Save**.
6. GitHub akan memberi URL sementara seperti `https://username.github.io/dompetku-pwa/` — pastikan ini sudah bisa dibuka dulu sebelum lanjut ke domain custom.

## Langkah 2 — Edit file CNAME

Buka file `CNAME` di dalam folder ini, ganti isinya dengan domain kamu sendiri, contoh:

```
dompetku.namadomainmu.com
```

atau kalau pakai domain utama (apex), cukup:

```
namadomainmu.com
```

File ini **wajib** ada di root repo (bukan di dalam subfolder) supaya GitHub Pages tahu domain custom-nya apa.

## Langkah 3 — Atur DNS di penyedia domain kamu

Pilih salah satu sesuai jenis domain:

**A. Subdomain (misalnya `dompetku.namadomainmu.com`) — pakai CNAME record**
| Type  | Host/Name | Value |
|-------|-----------|-------|
| CNAME | `dompetku` | `username.github.io` |

**B. Domain utama/apex (misalnya `namadomainmu.com`) — pakai A record ke IP GitHub Pages**
| Type | Host/Name | Value |
|------|-----------|-------|
| A    | `@`       | `185.199.108.153` |
| A    | `@`       | `185.199.109.153` |
| A    | `@`       | `185.199.110.153` |
| A    | `@`       | `185.199.111.153` |
| AAAA | `@`       | `2606:50c0:8000::153` |
| AAAA | `@`       | `2606:50c0:8001::153` |
| AAAA | `@`       | `2606:50c0:8002::153` |
| AAAA | `@`       | `2606:50c0:8003::153` |

> Nama field DNS bisa beda-beda tergantung penyedia (Niagahoster, Cloudflare, Domainesia, dll), tapi intinya sama: arahkan domain ke GitHub Pages.
> Propagasi DNS bisa memakan waktu beberapa menit sampai beberapa jam.

## Langkah 4 — Aktifkan domain custom di GitHub

1. Kembali ke **Settings → Pages** di repo.
2. Di bagian **Custom domain**, masukkan domain yang sama seperti isi file `CNAME`, lalu **Save**.
3. Tunggu sampai GitHub selesai memeriksa DNS (tanda centang hijau "DNS check successful").
4. Centang **Enforce HTTPS** supaya situs otomatis pakai `https://` (aman & disyaratkan untuk PWA bisa di-install).

## Langkah 5 — Install di HP

**Android (Chrome):**
Buka domain custom kamu → ketuk menu titik tiga (⋮) → **"Tambahkan ke layar utama" / "Install app"**.

**iPhone (Safari):**
Buka domain custom kamu → ketuk ikon **Share/Bagikan** → **"Tambah ke Layar Utama"**.

Setelah itu ikon "DompetKu" muncul di home screen dan terbuka layar penuh tanpa address bar, seperti aplikasi native.

---

## Catatan soal ikon

Folder `icons/` masih kosong — silakan isi 3 file ini (ukuran & nama harus persis sama, format PNG):
- `icons/icon-192.png` (192×192 px)
- `icons/icon-512.png` (512×512 px)
- `icons/icon-maskable-512.png` (512×512 px, dengan padding aman di tengah untuk ikon "maskable")

Kalau belum punya, kasih tahu saya — bisa saya buatkan.

## Catatan soal update di kemudian hari

- Setiap kali kamu upload ulang/push perubahan ke repo, GitHub Pages otomatis re-deploy dalam waktu singkat (biasanya <1 menit).
- Karena ada service worker, HP yang sudah install app mungkin butuh dibuka ulang 1-2 kali untuk narik versi terbaru (service worker mengambil file baru di background lalu dipakai saat app dibuka lagi). Kalau mau perubahan langsung kepakai, naikkan nomor versi di baris pertama `service-worker.js`, misalnya `dompetku-cache-v1` → `dompetku-cache-v2`.

## Catatan penting soal data

- Data tersimpan **per browser/per perangkat** (localStorage), bukan disinkron antar HP.
- Kalau cache/data browser dibersihkan, catatan transaksi ikut hilang — sebaiknya jangan gunakan mode "Private/Incognito".
- Kalau nanti butuh data tersinkron antar HP (misalnya HP dan laptop sama-sama update saldo), itu perlu backend/database — beri tahu saya kalau mau dibuatkan.
