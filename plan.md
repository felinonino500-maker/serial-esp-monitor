# Rencana implementasi — Serial Monitor ESP

## Ruang lingkup dan arsitektur

Membangun satu halaman web ringan untuk serial monitor ESP32/ESP8266, bukan flasher firmware. `index.html` memuat Vue 3 dan Tailwind CSS melalui CDN, mengelola state serta log di sisi klien, dan berkomunikasi dengan perangkat lewat Web Serial API. Tidak ada server aplikasi atau penyimpanan data; project memakai server file statis untuk Preview. Pengguna harus membuka situs di browser yang mendukung Web Serial (umumnya Chrome/Edge desktop) melalui HTTPS atau localhost.

Alur utama: pengguna memilih baud rate, meminta izin pemilihan port, lalu membuka port pada serial API; pembaca stream mengonsumsi data hingga koneksi dihentikan. Input perintah menulis ke writer stream yang sama dengan akhiran baris yang dapat dipilih. Log menyertakan timestamp dan arah RX/TX, dapat dihapus, dan auto-scroll kecuali pengguna menggulir ke atas.

Struktur: `index.html` berisi markup, Vue app, gaya Tailwind, dan seluruh interaksi; `public/manus-routes.json` menyatakan route `/`; `TODO.md` melacak kelompok hasil; `plan.md` menyimpan keputusan implementasi/desain.

## Desain

Tiga arah alternatif (probabilitas rendah): panel lab gelap bergaya osiloskop (0,06); terminal hijau retro (0,04); utilitas teknisi terang dengan aksen biru (0,08). Dipilih: panel lab gelap bergaya osiloskop.

**Design Movement:** perangkat lunak instrumentasi lab modern, bukan terminal retro.

**Prinsip inti:** status koneksi sangat terbaca; densitas informasi tinggi namun teratur; semua kontrol penting dekat dengan monitor; warna status semantik dan aksesibel.

**Filosofi warna:** latar arang kebiruan untuk mengurangi silau; bidang sedikit lebih terang membentuk lapisan alat; cyan menjadi warna brand untuk serial/data; hijau dan merah hanya menandai keberhasilan dan gangguan.

**Paradigma tata letak:** panel kontrol sempit di sisi kiri pada desktop dan bertumpuk di atas monitor pada layar kecil; area log menjadi kanvas utama yang luas.

**Elemen khas:** indikator koneksi berbentuk titik dengan halo; label RX/TX berwarna; garis kisi terminal sangat samar.

**Interaksi dan animasi:** perubahan status instan dengan transisi pendek 150 ms; tidak ada animasi yang mengganggu stream. Tombol berstatus jelas, fokus keyboard terlihat; hormati `prefers-reduced-motion`.

**Tipografi:** Inter untuk antarmuka dan JetBrains Mono untuk baud rate, input, serta log; hierarki ringkas dengan judul panel semibold dan metadata kecil berkontras cukup.

**Esensi merek:** konsol serial ringkas bagi teknisi dan pembuat perangkat ESP; praktis, presisi, tenang.

**Suara merek:** instruksi langsung dan jelas. Contoh: “Pilih port untuk mulai membaca.” “Koneksi terputus; log tetap tersedia.”

**Wordmark/logo:** simbol gelombang serial tiga garis dengan titik RX dan label “SERIAL ESP”. **Warna brand:** cyan terang yang menandai kanal data.

## Hasil produk

- Pilih port serial dan atur baud rate.
- Hubungkan atau putuskan koneksi serial ke ESP32/ESP8266.
- Tampilkan data serial masuk di log monitor.
- Kirim teks atau perintah melalui serial.
- Hapus log monitor.
