# Project6-Statistical-Analysis-Taxi-InChicago-SQL

## Deskripsi Proyek

Anda bekerja sebagai seorang analis untuk Zuber, sebuah perusahaan berbagi tumpangan (*ride-sharing*) baru yang diluncurkan di Chicago. Tugas Anda adalah untuk menemukan pola pada informasi yang tersedia. Anda ingin memahami preferensi penumpang dan dampak faktor eksternal terhadap perjalanan.

Dengan menggunakan basis data, Anda akan menganalisis data dari kompetitor dan menguji hipotesis terkait pengaruh cuaca terhadap frekuensi perjalanan.

### Deskripsi Data

Basis data yang memuat informasi perjalanan taksi di Chicago:

Tabel `neighborhoods`: data terkait wilayah di kota Chicago

- `name`: nama wilayah
- `neighborhood_id`: kode wilayah

Tabel `cabs`: data terkait taksi

- `cab_id`: kode kendaraan
- `vehicle_id`: ID teknis kendaraan
- `company_name`: nama perusahaan yang memiliki kendaraan

Tabel `trips`: data terkait perjalanan

- `trip_id`: kode perjalanan
- `cab_id`: kode kendaraan yang beroperasi
- `start_ts`: tanggal dan waktu perjalanan dimulai (waktu dibulatkan dalam satuan jam)
- `end_ts`: tanggal dan waktu perjalanan berakhir (waktu dibulatkan dalam satuan jam)
- `duration_seconds`: durasi perjalanan dalam satuan detik
- `distance_miles`: jarak perjalanan dalam satuan mil
- `pickup_location_id`: kode wilayah penjemputan
- `dropoff_location_id`: kode wilayah pengantaran

Tabel `weather_records`: data terkait cuaca

- `record_id`: kode pencatatan cuaca
- `ts`: tanggal dan waktu saat pencatatan cuaca dilakukan (waktu dibulatkan dalam satuan jam)
- `temperature`: suhu saat pencatatan cuaca dilakukan
- `description`: deskripsi singkat tentang kondisi cuaca, seperti "*light rain*" (hujan ringan) atau "*scattered clouds*" (berawan).

## Skema Tabel

!https://pictures.s3.yandex.net/resources/Untitled_1_1585510727.png

Catatan: tidak ada hubungan langsung antara tabel `trips` dan `weather_records` pada basis data. Namun, Anda tetap bisa menggunakan **JOIN** dan menghubungkan kedua tabel dengan menggunakan data waktu perjalanan dimulai (`trips.start_ts`) dan waktu pencatatan cuaca (`weather_records.ts`).

### Step pada project Ini

**Tahap 1. Tuliskan sebuah kode untuk menguraikan data cuaca di Chicago pada bulan November 2017 dari situs web:**

https://code.s3.yandex.net/data-analyst-eng/chicago_weather_2017.html

**Tahap 2. Analisis Data Eksploratif**

1. Temukan jumlah perjalanan taksi untuk masing-masing perusahaan taksi pada tanggal 15 - 16 November 2017. Namai kolom yang dihasilkan dengan `trips_amount` dan tampilkanlah kolom tersebut bersama dengan kolom `company_name`. Urutkan hasilnya secara turun berdasarkan `trips_amount`.
2. Temukan jumlah perjalanan untuk setiap perusahaan taksi yang namanya memuat unsur kata "*Yellow*" atau "*Blue*" pada tanggal 1-7 November 2017. Namai variabel yang dihasilkan dengan `trips_amount`. Kelompokan hasilnya berdasarkan kolom `company_name`.
3. Pada bulan November 2017, perusahaan taksi yang paling populer adalah Flash Cab dan Taxi Affiliation Services. Temukan jumlah perjalanan untuk kedua perusahaan tersebut dan namai variabel yang dihasilkan dengan `trips_amount`. Gabungkan perjalanan dari semua perusahaan lainnya dalam satu kelompok: "*Other*". Kelompokkan data berdasarkan nama perusahaan taksi. Namai kolom yang memuat nama perusahaan taksi dengan `company`. Urutkan hasilnya dalam urutan turun berdasarkan `trips_amount`.

**Tahap 3. Uji hipotesis yang menyatakan bahwa durasi perjalanan dari Loop ke Bandara Internasional O'Hare berubah pada hari-hari Sabtu yang hujan.**

1. Ambil data tentang ID wilayah O'Hare dan Loop dari tabel `neighborhoods`.
2. Untuk setiap jam, ambil catatan kondisi cuaca dari tabel `weather_records`. Dengan menggunakan operator CASE, bagi semua jam menjadi dua kelompok: "*Bad*" jika kolom `description` memuat kata "*rain*" (hujan) atau "*storm*" (badai), dan "*Good*" untuk sisanya yang tidak memuat kedua kata tersebut. Namai kolom yang dihasilkan dengan `weather_conditions`. Tabel akhir harus memuat dua kolom: tanggal dan jam (*ts*), serta `weather_conditions`.
3. Ambil dari tabel `trips` data semua perjalanan yang dimulai dari wilayah Loop (`neighborhood_id`: 50) dan berakhir di wilayah O'Hare (`neighborhood_id`: 63) pada hari Sabtu. Dapatkan kondisi cuaca untuk setiap perjalanan. Gunakan metode yang Anda terapkan di tugas sebelumnya. Ambil juga durasi untuk setiap perjalanan. Abaikan perjalanan yang data kondisi cuacanya tidak tersedia.

**Tahap 4. Analisis Data Eksploratif (Python)**

Selain data yang Anda peroleh dalam tugas sebelumnya, Anda telah diberikan *file* kedua. Sekarang, Anda memiliki dua *file* CSV berikut:

`project_sql_result_01.csv`. *File* ini memuat data berikut:

- `company_name`: nama perusahaan taksi
- `trips_amount`: jumlah perjalanan untuk setiap perusahaan taksi pada tanggal 15-16 November 2017.

`project_sql_result_04.csv`. *File* ini memuat data berikut:

- `dropoff_location_name`: nama wilayah di Chicago tempat perjalanan berakhir
- `average_trips`: jumlah rata-rata perjalanan yang berakhir di setiap wilayah pada bulan November 2017.

Untuk kedua *dataset* tersebut, sekarang Anda perlu untuk:

- mengimpor kedua *file*
- mempelajari isi datanya
- memastikan tipe datanya sudah benar
- mengidentifikasi 10 wilayah teratas yang dijadikan sebagai titik pengantaran
- membuat grafik: perusahaan taksi dan jumlah perjalanannya, 10 wilayah teratas berdasarkan jumlah pengantaran
- menarik kesimpulan berdasarkan grafik yang telah dibuat dan menjelaskan hasilnya

**Tahap 5. Menguji Hipotesis (Python)**

`project_sql_result_07.csv` — hasil dari kueri terakhir. *File* ini memuat data perjalanan dari Loop ke Bandara Internasional O'Hare. Ingat, berikut adalah nilai kolom-kolom yang ada di tabel ini:

- `start_ts` - tanggal dan waktu penjemputan
- `weather_conditions` - kondisi cuaca saat perjalanan dimulai
- `duration_seconds` - durasi perjalanan dalam satuan detik

Uji hipotesis berikut:

"Durasi rata-rata perjalanan dari Loop ke Bandara Internasional O'Hare berubah pada hari-hari Sabtu yang hujan.”

Atur tingkat signifikansi (*alpha*) secara mandiri.

Jelaskan:

- Bagaimana Anda merumuskan hipotesis nol dan hipotesis alternatif
- Kriteria apa yang Anda gunakan untuk menguji hipotesis dan alasan Anda menggunakannya
