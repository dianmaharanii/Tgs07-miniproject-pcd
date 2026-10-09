# Miniproject Pengolahan Citra Ijazah: OCR dan Deteksi Tanda Tangan

## Deskripsi Proyek
Miniproject ini menguji pengolahan citra pada gambar ijazah untuk membantu membaca nomor ijazah menggunakan **Optical Character Recognition (OCR)** dan mendeteksi indikasi keberadaan tanda tangan kepala sekolah pada area gambar yang ditentukan.

Proyek menguji sembilan kondisi gambar:
1. `01_HighQuality_Enhanced.jpg`
2. `02_LowContrast.jpg`
3. `03_Blurred.jpg`
4. `04_HighNoise.jpg`
5. `05_LowResolution_Upsampled.jpg`
6. `06_Faded_Underexposed.jpg`
7. `07_ColorShift_WarmTint.jpg`
8. `08_JPEGCompression_Artifacts.jpg`
9. `09_CombinedDegradation.jpg`

Pastikan nama file dan nomor ijazah acuan sesuai dengan data yang benar-benar digunakan di notebook.

## Tujuan
- Membaca nomor ijazah dari gambar menggunakan OCR.
- Membandingkan metode enhancement.
- Menghitung **Character Error Rate (CER)**.
- Memeriksa indikasi keberadaan tanda tangan kepala sekolah.
- Menyimpan hasil evaluasi sebagai CSV dan grafik.

## Metode yang Digunakan

### 1. Grayscale
Mengubah gambar berwarna menjadi citra keabuan sehingga pemrosesan lebih berfokus pada perbedaan intensitas.

### 2. CLAHE
**Contrast Limited Adaptive Histogram Equalization (CLAHE)** meningkatkan kontras secara lokal agar teks yang kurang jelas lebih mudah terlihat.

### 3. Sharpening
Mempertajam tepi dan detail gambar agar karakter lebih mudah dikenali OCR. Jika terlalu kuat, metode ini dapat memperjelas noise atau artefak.

### 4. Adaptive Threshold
Mengubah gambar menjadi hitam putih berdasarkan ambang intensitas lokal untuk membantu memisahkan teks dari latar belakang.

### 5. OCR
OCR (*Optical Character Recognition*) mengekstraksi teks dari area nomor ijazah. Hasilnya dibandingkan dengan nomor acuan.

### 6. Deteksi indikasi tanda tangan
Sistem memeriksa area gambar yang ditentukan dan menghitung indikasi piksel tinta. Jika nilainya melewati ambang batas dalam kode, sistem menandai adanya indikasi tinta/tanda tangan.

**Batasan:** ini merupakan deteksi sederhana berbasis piksel tinta. Sistem tidak dapat memastikan keaslian tanda tangan atau selalu membedakan tanda tangan dari tulisan dan noda lain. Hasil perlu diperiksa secara visual.

### 7. Character Error Rate (CER)
CER mengukur kesalahan karakter OCR terhadap teks acuan:

`CER = (S + D + I) / N`

- `S`: karakter yang diganti (*substitution*).
- `D`: karakter yang terhapus (*deletion*).
- `I`: karakter yang ditambahkan (*insertion*).
- `N`: jumlah karakter pada teks acuan.

Semakin rendah CER, semakin baik hasil OCR. CER `0%` berarti hasil OCR sama dengan teks acuan untuk pengujian tersebut. Pastikan teks acuan benar sebelum menyimpulkan metode terbaik.

## Hasil Evaluasi
Notebook dapat menghasilkan:
- `hasil_evaluasi_9_ijazah.csv`
- `ringkasan_akurasi_OCR.csv`
- `grafik_perbandingan_CER.png`

Metode enhancement paling efektif ditentukan berdasarkan nilai CER terendah pada hasil pengujian. Jika beberapa metode memiliki CER terendah yang sama, laporkan hasil seri berdasarkan metrik CER. Jangan menyimpulkan metode terbaik sebelum memeriksa hasil akhir pada seluruh gambar.

## Cara Menjalankan Kode (*How to Run*)

### Google Colab
1. Unggah file notebook `.ipynb` ke repository GitHub.
2. Buka [Google Colab](https://colab.research.google.com/).
3. Pilih **File → Open notebook → GitHub**, lalu masukkan URL repository atau cari repository yang sudah diunggah.
4. Buka notebook miniproject.
5. Unggah sembilan gambar pengujian ke sesi Colab, atau sesuaikan kode agar membaca gambar dari Google Drive.
6. Periksa dan sesuaikan nama file gambar, nomor ijazah acuan, koordinat area nomor ijazah, koordinat area tanda tangan, serta parameter enhancement dan ambang deteksi tanda tangan.
7. Jalankan sel notebook secara berurutan menggunakan **Runtime → Run all** atau tombol ▶.
8. Periksa hasil OCR, nilai CER, dan hasil indikasi tanda tangan.
9. Pastikan file CSV dan grafik berhasil dibuat, lalu unduh jika diperlukan.

### Komputer lokal
Untuk menjalankan secara lokal, siapkan Python dan semua dependensi yang digunakan notebook. Periksa bagian instalasi dan semua perintah `import`; kebutuhan pustaka bergantung pada isi kode notebook.

## Struktur Repository yang Disarankan
```text
miniproject-ocr-ijazah/
├── README.md
├── miniproject_ocr_ijazah.ipynb
├── data/
│   └── (gambar pengujian, jika aman dibagikan)
└── hasil/
    ├── hasil_evaluasi_9_ijazah.csv
    ├── ringkasan_akurasi_OCR.csv
    └── grafik_perbandingan_CER.png
```
Nama file dan folder di atas hanya contoh; sesuaikan dengan file yang benar-benar diunggah. Jika gambar ijazah berisi data pribadi, jangan unggah gambar asli ke repository publik tanpa izin. Gunakan gambar yang sudah dianonimkan atau data uji yang aman dibagikan.

## Kesimpulan
Miniproject ini membandingkan Grayscale, CLAHE, Sharpening, dan Adaptive Threshold untuk membantu OCR membaca nomor ijazah. Kinerja metode dinilai menggunakan CER; nilai yang lebih rendah menunjukkan lebih sedikit kesalahan karakter. Sistem juga memeriksa indikasi keberadaan tanda tangan berdasarkan piksel tinta pada area yang ditentukan. Kesimpulan akhir harus didasarkan pada hasil pengujian yang sudah diverifikasi.

## Repository GitHub
Setelah membuat repository dan mengunggah notebook, ganti placeholder berikut dengan tautan repository milikmu:

**Link repository:** `https://github.com/USERNAME/NAMA-REPOSITORY`
