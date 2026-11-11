# Prediksi Dini Mahasiswa Non-Aktif

Kode pendamping naskah **"Parsimonious Logistic Regression versus XGBoost untuk Prediksi Dini Mahasiswa Non-Aktif dengan Rolling-Origin Validation"** (UTS Advanced Machine Learning, Magister Ilmu Komputer, Universitas Nusa Mandiri, 2026).

Penelitian ini membandingkan Logistic Regression 3 fitur, Logistic Regression 28 fitur, Logistic Regression dengan *nested feature selection* (SHAP dan Lasso), dan XGBoost 28 fitur untuk memprediksi mahasiswa yang akan berstatus non-aktif pada semester berikutnya. Semua model diuji dengan *rolling-origin validation* pada tujuh semester uji (2022-2 sampai 2025-2) dan dibandingkan dengan *random cross-validation*.

## Isi repositori

| File | Keterangan |
|---|---|
| `Prediksi_NonAktif.ipynb` | Seluruh tahapan CRISP-DM, dari *data understanding* sampai pembuatan tabel dan gambar naskah |
| `requirements.txt` | Daftar pustaka Python |
| `.gitignore` | Mencegah file data ikut terunggah |

## Data

Data mentah **tidak disertakan** karena memuat catatan akademik mahasiswa sebuah perguruan tinggi swasta di Indonesia. Identitas mahasiswa sudah diganti dengan `kode_mhs`, tetapi kombinasi atribut akademik tetap berpotensi dikenali sehingga data tidak dipublikasikan.

Notebook membaca file `tabel_target1_nonaktif_v2.csv` (format *person-period*: satu baris = satu mahasiswa pada satu semester). Semua fitur diambil dari semester sebelumnya (*t*−1) agar tidak ada kebocoran informasi.

### Kamus data (28 fitur dasar)

| Kolom | Keterangan |
|---|---|
| `angkatan` | Tahun masuk mahasiswa |
| `kode_prodi` | Kode program studi (kategori) |
| `semester_ke` | Semester ke-berapa pada semester *t* |
| `status_l1` | Status semester *t*−1: Aktif atau Kampus Merdeka (kategori) |
| `mbkm_l1` | 1 jika semester *t*−1 mengikuti MBKM |
| `sks_diambil_l1` | SKS yang diambil pada semester *t*−1 |
| `batas_sks_l1` | Batas SKS yang boleh diambil pada semester *t*−1 |
| `ips_l1`, `ips_l2` | IPS semester *t*−1 dan *t*−2 |
| `ips_delta` | `ips_l1` − `ips_l2` |
| `ipk_l1` | IPK sampai semester *t*−1 |
| `ipk_delta` | Perubahan IPK dari *t*−2 ke *t*−1 |
| `sks_tempuh_kum` | SKS kumulatif yang pernah ditempuh |
| `sks_lulus_kum` | SKS kumulatif yang lulus |
| `sks_gagal_kum` | `sks_tempuh_kum` − `sks_lulus_kum` |
| `rasio_lulus` | `sks_lulus_kum` / `sks_tempuh_kum` |
| `sks_lulus_smt_l1` | SKS yang lulus pada semester *t*−1 |
| `sks_gagal_smt_l1` | SKS yang tidak lulus pada semester *t*−1 |
| `laju_sks` | Rata-rata SKS lulus per semester |
| `sisa_sks` | Sisa SKS menuju 148 SKS |
| `sisa_sem` | Sisa semester menuju batas 14 semester |
| `margin_sks` | 24 × `sisa_sem` − `sisa_sks` (kelonggaran waktu studi) |
| `na_berturut_l1` | Jumlah semester non-aktif berturut-turut sampai *t*−1 |
| `na_total` | Jumlah semester non-aktif sampai *t*−1 |
| `mbkm_total` | Jumlah semester MBKM sampai *t*−1 |
| `ips0_total` | Jumlah semester aktif dengan IPS 0 |
| `ips0_l1` | 1 jika semester *t*−1 aktif tetapi IPS 0 |
| `n_aktif` | Jumlah semester aktif sampai *t*−1 |

Kolom lain: `kode_mhs` (kode anonim), `periode` (semester *t*), `y_nonaktif` (label: 1 jika non-aktif pada semester *t*), serta 11 kolom berakhiran `_riwayat` yang hanya dipakai pada analisis tambahan.

## Cara menjalankan

1. Buka notebook di Google Colab atau Jupyter.
2. Di komputer lokal, pasang pustaka: `pip install -r requirements.txt`.
3. Letakkan file data di folder yang sama dengan notebook atau di `data/`. Di Colab, notebook akan meminta unggah file.
4. Jalankan semua sel (Runtime → Run all). Waktu jalan sekitar 15 menit; bagian *nested feature selection* paling lama.

Notebook tidak menampilkan baris data individual. Keluarannya berupa ringkasan, tabel metrik, gambar (`gambar3_prauc.png` sampai `gambar7_kalibrasi.png`), dan file Excel `hasil_penelitian_crispdm.xlsx`.

## Kaitan dengan naskah

| Naskah | Bagian notebook |
|---|---|
| Tabel 2 dan Tabel 3 | 3.1–3.3, 4.1 |
| Tabel 4 | 5.2, 5.14 |
| Tabel 5 | 5.6 |
| Tabel 6 | 5.11 |
| Tabel 7 | 5.12 |
| Gambar 3 | 5.4, 5.6, 5.6b |
| Gambar 4 | 5.15 |
| Gambar 5 dan Gambar 6 | 5.16 |
| Gambar 7 | 5.9 |
