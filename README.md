# lab2_web

Nama: Muhamad Farras Jasir

Kelas: TI.22.A5

Nim: 312210361

## Belajar PHP Dasar
![Screenshot (492)](https://github.com/muhamadfarrasjasir12/lab2_web/assets/150880443/a63ad72c-1afa-4d1d-b222-ae3e870d2c19)



Hasil:


![324307416-bc3adfcf-c6b5-44bd-85bc-a0cf7da6cf47](https://github.com/muhamadfarrasjasir12/lab2_web/assets/150880443/2422655c-cccd-4895-bcae-92fc73f6807e)


## Menggunakan Variable
![Screenshot (492)](https://github.com/muhamadfarrasjasir12/lab2_web/assets/150880443/cbcd8a48-411e-43ed-b678-c82117c8d94a)


Hasil:

![Screenshot (490)](https://github.com/muhamadfarrasjasir12/lab2_web/assets/150880443/adca07c4-b9d9-4d69-9d34-3e0fe5c1db24)


## Form Input
![Screenshot (493)](https://github.com/muhamadfarrasjasir12/lab2_web/assets/150880443/a7224cc3-42db-45fd-aa28-e5501f23745e)


Hasil:


![Screenshot (491)](https://github.com/muhamadfarrasjasir12/lab2_web/assets/150880443/b1d4f792-48a7-435a-ab10-9f02db439af9)


## Tugas
![Screenshot (494)](https://github.com/muhamadfarrasjasir12/lab2_web/assets/150880443/50f0265b-025e-49b2-97be-f7583c2d55ec)

![Screenshot (495)](https://github.com/muhamadfarrasjasir12/lab2_web/assets/150880443/c19ca1ca-c631-4d0c-bc4d-2a6b9c6cd809)



Hasil:


![Screenshot (496)](https://github.com/muhamadfarrasjasir12/lab2_web/assets/150880443/b6cd3112-830a-4190-b6b0-8c96807e9e80)


## Penjelasan
1. Struktur HTML
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>PHP Dasar</title>
</head>
<body>
    <h2>Form Input</h2>
    <form method="post">
        <label>Nama: </label>
        <input type="text" name="nama">
        <label>Tanggal Lahir: </label>
        <input type="date" name="tanggal_lahir">
        <label>Pekerjaan: </label>
        <select name="pekerjaan">
            <option value="Operator">Operator</option>
            <option value="Developer">Developer</option>
            <option value="Manager">Manager</option>
        </select>
        <input type="submit" value="Kirim">
    </form>
```
**Input Nama:** Pengguna memasukkan nama mereka.

**Input Tanggal Lahir:** Pengguna memilih tanggal lahir menggunakan kontrol input tanggal.

**Pilihan Pekerjaan:** Pengguna memilih pekerjaan dari dropdown, yang akan mempengaruhi perhitungan gaji.

2. Logika PHP, Proses Formulir
```
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_POST['nama']) && isset($_POST['tanggal_lahir']) && isset($_POST['pekerjaan'])) {
    $nama = htmlspecialchars($_POST['nama']);
    $tanggal_lahir = $_POST['tanggal_lahir'];
    $pekerjaan = $_POST['pekerjaan'];
```
**Pengecekan Metode dan Data:** Memeriksa apakah formulir telah dikirim menggunakan metode POST dan semua data yang diperlukan ada.

**Sanitisasi Input:** Fungsi htmlspecialchars digunakan untuk menghindari serangan XSS (Cross-Site Scripting) dengan membersihkan input nama dari tag HTML atau karakter khusus.

3. Kalkulasi Umur
```
    $birthdate = new DateTime($tanggal_lahir);
    $today = new DateTime('today');
    $age = $birthdate->diff($today)->y;
```
**Objek DateTime:** Digunakan untuk memanipulasi tanggal dengan mudah.

**Perhitungan Selisih Tahun:** Menghitung selisih tahun antara tanggal lahir dan hari ini untuk mendapatkan umur.

4. Perhitungan Gaji dan Pajak
```
    $salaries = [
        "Operator" => 1000000,
        "Developer" => 3000000,
        "Manager" => 5000000
    ];
    $taxRates = [
        "Operator" => 0.1,
        "Developer" => 0.15,
        "Manager" => 0.2
    ];
    $gaji = isset($salaries[$pekerjaan]) ? $salaries[$pekerjaan] : 0;
    $pajak = isset($taxRates[$pekerjaan]) ? $taxRates[$pekerjaan] : 0;
    $thp = $gaji - ($gaji * $pajak);
```

**Array:** Menyimpan nilai gaji dan pajak berdasarkan jenis pekerjaan.

**Kalkulasi Gaji Bersih:** Menghitung gaji bersih dengan mengurangkan pajak dari gaji kotor.

5. Menampilkan Hasil
```
    echo "Selamat Datang $nama<br>";
    echo "Usia Anda: $age tahun<br>";
    echo "Pekerjaan: $pekerjaan<br>";
    echo "Gaji sebelum pajak = Rp. " . number_format($gaji, 0, ',', '.') . "<br>";
    echo "Gaji yang dibawa pulang = Rp. " . number_format($thp, 0, ',', '.');
}
?>
</body>
</html>
```
**Output:** Menggunakan echo untuk menampilkan teks dan data yang diproses ke pengguna.
