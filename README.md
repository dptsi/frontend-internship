# Coding Challenge - Frontend

Coding challenge ini bertujuan untuk menguji kemampuan Anda dalam mengembangkan aplikasi web frontend dengan menggunakan **Next.js**, **TypeScript**, **Chakra UI**, dan beberapa library lainnya.

Anda perlu melakukan **commit** dan **push** ke repositori ini selama pengerjaan. Waktu pengerjaan adalah selama tiga hari, mulai dari Senin, 4 Maret 2023 hingga **Rabu**, 6 Maret 2023 pukul **23:59**. Setelah melewati batas waktu, peserta tidak dapat lagi melakukan **push** ke repo.

## Deskripsi
Anda diminta untuk membuat sebuah aplikasi web yang berfungsi sebagai platform berita online. Aplikasi ini memiliki beberapa fitur, antara lain:

- **Halaman Login** untuk pengguna yang sudah terdaftar.
- **Halaman Daftar Berita** yang menampilkan judul dan tanggal pembuatan berita yang sudah dipublikasikan.
- **Halaman Detail Berita** yang menampilkan informasi lengkap tentang berita tertentu.
- **Halaman Dasbor Daftar Berita** untuk pengguna yang berperan sebagai penulis atau moderator berita.
- **Halaman Dasbor Buat Berita** untuk pengguna yang berperan sebagai penulis berita.
- **Halaman Dasbor Ubah Berita** untuk pengguna yang berperan sebagai penulis atau moderator berita.

Aplikasi ini juga mendukung fitur **i18n (internasionalisasi)** dengan menggunakan library **next-intl**. Untuk coding challenge ini, Anda hanya perlu menyiapkan setup untuk **Bahasa Indonesia** saja.

## Spesifikasi
Berikut adalah spesifikasi teknis dan fungsional yang harus Anda penuhi dalam coding challenge ini:

### Kriteria Umum
- Gunakan **Next.js versi 14.1.0** dengan fitur **Pages Route** untuk mengatur routing aplikasi⁶[6].
- Gunakan framework CSS **Chakra UI** untuk membuat tampilan antarmuka yang responsif dan konsisten.
- Gunakan bahasa **TypeScript** untuk meningkatkan kualitas kode dan menghindari kesalahan.
- Gunakan **SWR** dan **Axios** untuk melakukan data fetching di sisi klien (client-side).
- Gunakan **next-intl** untuk library i18n. Siapkan setup untuk **Bahasa Indonesia** saja.
- Semua route yang memerlukan autentikasi harus redirect ke halaman login ketika pengguna belum terautentikasi.

### Fitur-Fitur
#### Halaman Login
- Halaman ini berisi form input email dan kata sandi.
- Jika pengguna sudah terautentikasi, redirect ke halaman daftar berita.

#### Daftar Berita
- Halaman ini tidak memerlukan autentikasi.
- Halaman ini berisikan daftar judul dan tanggal pembuatan berita yang sudah dipublikasi.
- Setiap item berita mengarah ke halaman detail berita.
- Halaman ini adalah halaman beranda dari aplikasi.
- Tampilkan skeleton loading jika state masih loading data.
- Tampilkan pesan jika tidak ada berita.
- Tampilkan pesan error jika gagal memuat berita.

#### Detail Berita
- Halaman ini tidak memerlukan autentikasi.
- Berita yang dapat diakses hanyalah berita berstatus "published".
- Berita diakses menggunakan slug.
- Halaman ini berisikan data berikut dari berita:
  - Judul berita
  - Pembuat berita
  - Moderator berita
  - Waktu pembuatan
  - Konten berita
- Tampilkan skeleton loading jika state masih loading data.
- Tampilkan pesan jika berita tidak ditemukan.
- Tampilkan pesan error jika gagal memuat berita.

#### Dasbor Daftar Berita (User)
- Halaman ini memerlukan autentikasi.
- Halaman ini hanya dapat diakses oleh pengguna yang berperan sebagai "user".
- Berita yang ditampilkan HANYA berita yang dibuat oleh pengguna tersebut dengan status apapun.
- Setiap item berita mengarah ke halaman dasbor ubah berita.
- Tampilkan skeleton loading jika state masih loading data.
- Tampilkan pesan jika berita belum tersedia.
- Tampilkan pesan error jika gagal memuat berita.

#### Dasbor Buat Berita (User)
- Halaman ini memerlukan autentikasi
- Halaman ini hanya dapat diakses oleh pengguna yang berperan sebagai "user"
- Halaman ini berisikan input berikut:
  - Judul berita
  - Slug berita
  - Isi berita
- Terdapat validasi input dengan ketentuan sebagai berikut:
  - Judul: Required, max length 255
  - Slug: Required, max length 255, hanya berisi lowercase dan dash ("-")
  - Isi berita: Required, max length 2048
- Arahkan ke halaman ubah berita pada berita yang baru dibuat
- Tampilkan toast berisi pesan status berhasil/tidaknya berita dibuat
- Tampilkan pesan ke pengguna jika sedang dalam proses submit ke backend

#### Dasbor Ubah Berita (User)
- Halaman ini hanya dapat diakses oleh pengguna yang sudah log in
- Berita diakses menggunakan ID
- Halaman ini hanya dapat diakses oleh pengguna yang berperan sebagai "user"
- Halaman ini berisikan input berikut:
  - Judul berita
  - Slug berita
  - Isi berita
- Terdapat validasi input dengan ketentuan sebagai berikut:
  - Judul: Required, max length 255
  - Slug: Required, max length 255, hanya berisi lowercase dan dash ("-")
  - Isi berita: Required, max length 2048
- Berita hanya dapat diubah jika dan hanya jika memiliki status "draft"
- Tombol submit berita hanya aktif ketika berita berstatus "draft"
- Tampilkan skeleton loading jika state masih loading data
- Tampilkan pesan jika berita tidak ada
- Tampilkan pesan error jika gagal memuat berita
- Tampilkan pesan ke pengguna jika sedang dalam proses ubah/submit berita ke backen
- Tampilkan toast berisi pesan status berhasil/tidaknya berita diubah/disubmit
- Refetch state dari status berita setelah berita berhasil disubmit untuk moderasi tanpa reload halaman penuh

#### Dasbor Daftar Berita (Moderator)
- Halaman ini memerlukan autentikasi
- Halaman ini hanya dapat diakses oleh pengguna yang berperan sebagai "moderator"
- Berita yang ditampilkan HANYA berita dengan status "in_moderation" atau "published"
- Setiap item berita mengarah ke halaman dasbor ubah berita
- Tampilkan skeleton loading jika state masih loading data
- Tampilkan pesan jika berita belum tersedia
- Tampilkan pesan error jika gagal memuat berita

#### Dasbor Ubah Berita (Moderator)
- Halaman ini hanya dapat diakses oleh pengguna yang sudah log in
- Berita diakses menggunakan ID
- Halaman ini hanya dapat diakses oleh pengguna yang berperan sebagai "moderator"
- Halaman ini berisikan input berikut:
  - Judul berita
  - Slug berita
  - Isi berita
- Terdapat validasi input dengan ketentuan sebagai berikut:
  - Judul: Required, max length
  - Slug: Required, max length 255, hanya berisi lowercase dan dash ("-")
  - Isi berita: Required, max length 2048
- Berita hanya dapat diubah jika dan hanya jika memiliki status "in_moderation"
- Tombol publikasi berita hanya aktif ketika berita berstatus "in_moderation"
- Tampilkan skeleton loading jika state masih loading data
- Tampilkan pesan jika berita tidak ada
- Tampilkan pesan error jika gagal memuat berita
- Tampilkan pesan ke pengguna jika sedang dalam proses ubah/publikasi berita ke backend
- Tampilkan toast berisi pesan status berhasil/tidaknya berita diubah/dipublikasi
- Refetch state dari status berita setelah berita berhasil dipublikasi tanpa reload halaman penuh

## Penilaian
Coding challenge ini akan dinilai berdasarkan beberapa aspek, antara lain:

- Kualitas kode: seberapa rapi, mudah dibaca, dan terstruktur kode yang Anda buat
- Fungsionalitas: seberapa baik aplikasi Anda berfungsi sesuai dengan spesifikasi yang diberikan
- User interface: seberapa menarik, responsif, dan konsisten tampilan antarmuka aplikasi Anda
- Error handling: seberapa baik Anda menangani kemungkinan error atau kegagalan yang terjadi pada aplikasi Anda
- Dokumentasi: seberapa lengkap dan jelas Anda mendokumentasikan aplikasi Anda, termasuk cara instalasi, penggunaan, dan testing.

Selamat mengerjakan coding challenge ini dan semoga berhasil. 🌟
