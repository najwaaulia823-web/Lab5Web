<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kalkulator Nilai Mahasiswa</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            background-color: #f4f4f9;
        }
        .container {
            max-width: 400px;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input[type="number"] {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #0056b3;
        }
        .result {
            margin-top: 20px;
            padding: 15px;
            background-color: #e9ecef;
            border-radius: 4px;
            display: none;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Kalkulator Nilai</h2>
    
    <!-- Input Form untuk ketiga komponen nilai -->
    <div class="form-group">
        <label for="tugas">Nilai Tugas (0-100):</label>
        <input type="number" id="tugas" min="0" max="100" required>
    </div>
    
    <div class="form-group">
        <label for="uts">Nilai UTS (0-100):</label>
        <input type="number" id="uts" min="0" max="100" required>
    </div>
    
    <div class="form-group">
        <label for="uas">Nilai UAS (0-100):</label>
        <input type="number" id="uas" min="0" max="100" required>
    </div>
    
    <button onclick="prosesKalkulasi()">Hitung Nilai</button>

    <!-- Tempat menampilkan hasil di halaman HTML -->
    <div id="hasil" class="result"></div>
</div>

<script>
    // Fungsi 1: Menghitung Nilai Akhir (Proses Perhitungan)
    function hitungNilaiAkhir(tugas, uts, uas) {
        return (tugas * 0.30) + (uts * 0.30) + (uas * 0.40);
    }

    // Fungsi 2: Menentukan Predikat (Proses Perhitungan)
    function tentukanPredikat(nilai) {
        if (nilai >= 85) return "A";
        if (nilai >= 75) return "B";
        if (nilai >= 60) return "C";
        if (nilai >= 50) return "D";
        return "E";
    }

    // Fungsi Utama: Memisahkan proses perhitungan dari tampilan (DOM Manipulation)
    function prosesKalkulasi() {
        // Mengambil elemen input
        const inputTugas = document.getElementById('tugas').value;
        const inputUts = document.getElementById('uts').value;
        const inputUas = document.getElementById('uas').value;
        const elHasil = document.getElementById('hasil');

        // Mengubah string input menjadi angka float
        const tugas = parseFloat(inputTugas);
        const uts = parseFloat(inputUts);
        const uas = parseFloat(inputUas);

        // Validasi rentang nilai 0 - 100
        if (isNaN(tugas) || isNaN(uts) || isNaN(uas)) {
            alert("Semua kolom nilai harus diisi dengan angka!");
            return;
        }
        if (tugas < 0 || tugas > 100 || uts < 0 || uts > 100 || uas < 0 || uas > 100) {
            alert("Validasi Gagal: Nilai harus berada dalam rentang 0 hingga 100!");
            return;
        }

        // Memanggil fungsi perhitungan
        const akhir = hitungNilaiAkhir(tugas, uts, uas);
        const predikat = tentukanPredikat(akhir);
        const status = akhir >= 60 ? "Lulus" : "Belum Lulus";

        // Menampilkan nilai akhir, predikat, dan status ke halaman HTML
        elHasil.style.display = "block";
        elHasil.innerHTML = `
            <strong>Hasil Kelulusan:</strong><br>
            Nilai Akhir: ${akhir.toFixed(2)}<br>
            Predikat: ${predikat}<br>
            Status: <strong>${status}</strong>
        `;
    }
</script>

</body>
</html>
