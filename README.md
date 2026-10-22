# voipweb

Softphone berbasis web: panggil nomor lewat browser, lihat riwayat panggilan, kelola akun. Antarmuka dibangun dengan Next.js dan dirancang untuk berbicara dengan server SIP **Kamailio** di belakangnya.

## Fitur

- **Dialpad** lengkap dengan status panggilan (idle, calling, ringing, in-call, ended)
- **Riwayat panggilan** per pengguna
- **Login** memakai nomor SIP dan password, state-nya dijaga lewat React context
- **Dashboard** dan halaman About
- Lapisan data ke MySQL (skema Kamailio) lewat connection pool

## Stack

- Next.js 15 (App Router) + React 19 + TypeScript
- Tailwind CSS + komponen Radix UI
- MySQL (`mysql2`) sebagai database Kamailio
- SIP signaling: `src/lib/sip-service.ts` (saat ini masih mock; siap diganti ke [JsSIP](https://jssip.net) atau [SIP.js](https://sipjs.com) untuk koneksi nyata ke Kamailio)

## Struktur

```
src/app/            halaman: login, dashboard, call, about
src/app/components/  dialpad, call-history, navbar, footer
src/lib/sip-service.ts  lapisan SIP (connect, call, hangup, event)
src/lib/db.ts           pool koneksi MySQL ke Kamailio
```

## Menjalankan

Butuh Node.js 18+ dan server Kamailio dengan database MySQL.

```bash
npm install
cp .env.example .env.local   # isi kredensial DB kalau filenya ada
npm run dev
```

Buka http://localhost:3000.

Konfigurasi database lewat environment variable (lihat `src/lib/db.ts`):

```
DB_HOST=localhost
DB_USER=kamailio
DB_PASSWORD=...
DB_NAME=kamailio
```

## Status

Proyek pembelajaran seputar VoIP dan WebRTC/SIP. Bagian UI dan alur panggilan sudah jalan; koneksi SIP nyata ke Kamailio masih berupa mock yang tinggal disambungkan ke JsSIP/SIP.js.
