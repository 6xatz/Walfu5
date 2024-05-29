## Mata Kuliah

Sebagai tugas praktikum: [5] Basis Data | Universitas Pelita Bangsa.

## Laporan Praktikum

- Bagian 1:

  > Membuat Tabel untuk KRS, Dosen, dan Mahasiswa.

  <p align="left">
    <img src="/ss/TabelKRS.jpg" width="500">
  </p>
  <p align="left">
    <img src="/ss/TabelDosen.jpg" width="500">
  </p>
  <p align="left">
    <img src="/ss/TabelMahasiswa.jpg" width="500">
  </p>

```sql
-- Membuat Tabel Dosen
CREATE TABLE Dosen (
    kd_ds VARCHAR(5) PRIMARY KEY,
    nama VARCHAR(50)
);

-- Membuat Tabel MataKuliah
CREATE TABLE MataKuliah (
    kd_mk VARCHAR(5) PRIMARY KEY,
    nama VARCHAR(100),
    sks INT
);

-- Membuat Tabel Jadwal
CREATE TABLE Jadwal (
    kd_mk VARCHAR(5),
    kd_ds VARCHAR(5),
    hari VARCHAR(10),
    jam TIME,
    ruang VARCHAR(10),
    PRIMARY KEY (kd_mk, kd_ds, hari, jam),
    FOREIGN KEY (kd_mk) REFERENCES MataKuliah(kd_mk),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
);

-- Membuat Tabel KRS
CREATE TABLE KRS (
    nim VARCHAR(10),
    kd_mk VARCHAR(5),
    kd_ds VARCHAR(5),
    semester INT,
    nilai CHAR(2),
    PRIMARY KEY (nim, kd_mk),
    FOREIGN KEY (kd_mk) REFERENCES MataKuliah(kd_mk),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
);

-- Membuat Tabel Mahasiswa
CREATE TABLE Mahasiswa (
    nim VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(50),
    jk CHAR(1),
    tgl_lahir DATE,
    jalan VARCHAR(100),
    kota VARCHAR(50),
    kodepos VARCHAR(10),
    no_hp VARCHAR(15),
    kd_ds VARCHAR(5),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
);

-- Mengisi Tabel Dosen
INSERT INTO Dosen (kd_ds, nama) VALUES
('DS001', 'Nofal Arianto'),
('DS002', 'Ario Talib'),
('DS003', 'Ayu Rahmadina'),
('DS004', 'Ratna Kumala'),
('DS005', 'Vika Prasetyo');

-- Mengisi Tabel MataKuliah
INSERT INTO MataKuliah (kd_mk, nama, sks) VALUES
('MK001', 'Algoritma Dan Pemrograman', 3),
('MK002', 'Praktikum Algoritma Dan Pemrograman', 1),
('MK003', 'Teknologi Basis Data', 3),
('MK004', 'Praktikum Teknologi Basis Data', 1),
('MK005', 'Pemrograman Dasar', 3),
('MK006', 'Pemrograman Berorientasi Objek', 3),
('MK007', 'Struktur Data', 3),
('MK008', 'Arsitektur Komputer', 2);

-- Mengisi Tabel Jadwal
INSERT INTO Jadwal (kd_mk, kd_ds, hari, jam, ruang) VALUES
('MK001', 'DS002', 'Senin', '13:00:00', '102'),
('MK002', 'DS002', 'Senin', '10:00:00', 'Lab. 01'),
('MK003', 'DS001', 'Selasa', '13:00:00', '201'),
('MK004', 'DS001', 'Rabu', '09:00:00', 'Lab. 02'),
('MK005', 'DS003', 'Kamis', '13:00:00', '101'),
('MK006', 'DS005', 'Kamis', '09:00:00', '102'),
('MK007', 'DS005', 'Rabu', '10:00:00', '201'),
('MK008', 'DS005', 'Kamis', '13:00:00', '201');

-- Mengisi Tabel KRS
INSERT INTO KRS (nim, kd_mk, kd_ds, semester, nilai) VALUES
('1823456', 'MK001', 'DS002', 3, NULL),
('1823456', 'MK002', 'DS002', 3, NULL),
('1823456', 'MK003', 'DS001', 3, NULL),
('1823456', 'MK004', 'DS001', 3, NULL),
('1823456', 'MK007', 'DS005', 3, NULL),
('1823456', 'MK008', 'DS005', 3, NULL);

-- Mengisi Tabel Mahasiswa
INSERT INTO Mahasiswa (nim, nama, jk, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds) VALUES
('1812345', 'Ari Santoso', 'L', '1999-10-11', NULL, 'Bekasi', NULL, NULL, 'DS002'),
('1823456', 'Dina Marlina', 'P', '1998-11-20', NULL, 'Jakarta', NULL, NULL, 'DS002'),
('1834567', 'Rahmat Hidayat', 'L', '1999-05-10', NULL, 'Bekasi', NULL, NULL, 'DS001'),
('1845678', 'Jaka Sampurna', 'L', '2000-10-19', NULL, 'Cikarang', NULL, NULL, 'DS003'),
('1856789', 'Tia Lestari', 'P', '1999-02-15', NULL, 'Karawang', NULL, NULL, 'DS004'),
('1867890', 'Anton Sinaga', 'L', '1998-06-22', NULL, 'Bekasi', NULL, NULL, 'DS002'),
('1912345', 'Listia Nastiti', 'P', '2001-10-23', NULL, 'Jakarta', NULL, NULL, 'DS002'),
('1923456', 'Amira Jarisa', 'P', '2001-01-24', NULL, 'Karawang', NULL, NULL, 'DS004'),
('1934567', 'Laksana Mardito', 'L', '1999-04-14', NULL, 'Cikarang', NULL, NULL, 'DS003'),
('1945678', 'Jura Marsina', 'P', '2000-05-10', NULL, 'Cikarang', NULL, NULL, 'DS003'),
('1956789', 'Dadi Martani', 'L', '2001-08-29', NULL, 'Bekasi', NULL, NULL, 'DS005'),
('1967890', 'Bayu Laksono', 'L', '1999-07-22', NULL, 'Cikarang', NULL, NULL, 'DS004');
```

  <p align="left">
    <img src="/ss/TabelNV.jpg" width="700">
  </p>

### Pertanyaan dari Praktikum 5

1. Lakukan Join pada Table Mahasiswa dan Dosen:
```sql
SELECT Mahasiswa.nim, Mahasiswa.nama AS nama_mahasiswa, Mahasiswa.jk AS jenis_kelamin, Dosen.nama AS nama_dosen
FROM Mahasiswa
JOIN Dosen ON Mahasiswa.kd_ds = Dosen.kd_ds;
```

  <p align="left">
    <img src="/ss/LL1.jpg" width="700">
  </p>
  
2. Lakukan Join pada Table MataKuliah dan Dosen:
```sql
SELECT MataKuliah.kd_mk, MataKuliah.nama AS nama_matakuliah, MataKuliah.sks, Dosen.nama AS nama_dosen
FROM MataKuliah
LEFT JOIN Jadwal ON MataKuliah.kd_mk = Jadwal.kd_mk
LEFT JOIN Dosen ON Jadwal.kd_ds = Dosen.kd_ds;
```

  <p align="left">
    <img src="/ss/LL2.jpg" width="700">
  </p>

3. Lakukan Join pada Table Jadwal, MataKuliah, dan Dosen:
```sql
SELECT Jadwal.kd_mk, MataKuliah.nama AS nama_matakuliah, Dosen.nama AS nama_dosen, Jadwal.hari, Jadwal.jam, Jadwal.ruang
FROM Jadwal
JOIN Dosen ON Jadwal.kd_ds = Dosen.kd_ds
JOIN MataKuliah ON Jadwal.kd_mk = MataKuliah.kd_mk;
```

  <p align="left">
    <img src="/ss/LL3.jpg" width="700">
  </p>

4. Lakukan Join pada Table KRS, MataKuliah, Mahasiswa, dan Dosen:
```sql
SELECT KRS.nim, Mahasiswa.nama AS nama_mahasiswa, Mahasiswa.jk AS jenis_kelamin, Mahasiswa.tgl_lahir, MataKuliah.nama AS nama_matakuliah, Dosen.nama AS nama_dosen, KRS.semester, KRS.nilai
FROM KRS
JOIN Mahasiswa ON KRS.nim = Mahasiswa.nim
JOIN MataKuliah ON KRS.kd_mk = MataKuliah.kd_mk
JOIN Dosen ON KRS.kd_ds = Dosen.kd_ds;
```

  <p align="left">
    <img src="/ss/LL4.jpg" width="700">
  </p>

## Documentation

All associated resources. are licensed under the [MIT License](https://mit-license.org/).
