# Fullmoon Fam Trip Thailand 2027

Form pendaftaran FFT 2027 — frontend di **Vercel**, backend di **Google Apps Script** (Google Sheet + email admin).

```
fft-2027/
├── index.html          ← frontend (Vercel)
├── assets/             ← logo FFT
├── vercel.json         ← route /ph untuk market Filipina
└── apps-script/
    └── Code.gs         ← backend (copy ke Apps Script, BUKAN ke Vercel)
```

## Link
| Market | URL |
|---|---|
| Indonesia | `https://<domain>/` |
| Philippines | `https://<domain>/ph` |

## 1. Deploy backend (Apps Script)
1. Buka project Apps Script lama → ganti isi `Code.gs` dengan `apps-script/Code.gs`.
2. Hapus file `Index.html` di Apps Script (sudah tidak dipakai).
3. **Deploy → New deployment → Web app**
   - Execute as: **Me**
   - Who has access: **Anyone**
4. Copy URL yang berakhiran `/exec`.

> Setiap ubah `Code.gs`: **Deploy → Manage deployments → Edit → Version: New version**. URL tetap sama.

## 2. Sambungkan frontend
Di `index.html`, cari:
```js
var API_URL = '';
```
Ganti jadi:
```js
var API_URL = 'https://script.google.com/macros/s/XXXX/exec';
```
Kalau `API_URL` kosong, form jalan dalam **mode demo** (tidak tersimpan).

## 3. Deploy frontend (GitHub + Vercel)
1. Push folder ini ke repo GitHub baru.
2. Vercel → **Add New Project** → import repo → Framework: **Other** → Deploy.
3. Setiap `git push` ke `main` otomatis deploy ulang.

## Ubah jadwal / program
Data jadwal ada di **dua tempat**, harus sama:
- `index.html` → `PERIODS_DATA` (tampilan) dan `ITIN` (highlight itinerary)
- `apps-script/Code.gs` → `PERIODS` (kuota & sheet)

Jangan ubah `sheetName` dan `kodePrefix` di `Code.gs` supaya data lama tetap terbaca.
