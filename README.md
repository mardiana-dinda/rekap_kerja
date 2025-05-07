<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Rekap Pekerjaan PT. INKA</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
  <style>
    body {
      font-family: sans-serif;
      margin: 2rem;
      max-width: 600px;
    }
    input, textarea, button, select {
      width: 100%;
      margin-top: 5px;
      margin-bottom: 15px;
      padding: 8px;
      font-size: 1rem;
    }
    label {
      font-weight: bold;
    }
  </style>
</head>
<body>

  <h2>Form Rekap Pekerjaan - PT. INKA (Persero)</h2>
  <form id="rekapForm">
    <label for="nama">Nama Pekerja:</label>
    <input type="text" id="nama" name="nama" required />

    <label for="tanggal">Tanggal Pekerjaan:</label>
    <input type="date" id="tanggal" name="tanggal" required />

    <label for="jamMulai">Jam Mulai:</label>
    <input type="time" id="jamMulai" name="jamMulai" required />

    <label for="jamSelesai">Jam Selesai:</label>
    <input type="time" id="jamSelesai" name="jamSelesai" required />

    <label for="lembur">Perlu Lembur?</label>
    <select id="lembur" name="lembur">
      <option value="Tidak">Tidak</option>
      <option value="Ya">Ya</option>
    </select>

    <label for="bahan">Bahan Tidak Ada/Kurang:</label>
    <textarea id="bahan" name="bahan" rows="4"></textarea>

    <button type="submit">Simpan Data</button>
  </form>

  <button onclick="exportToExcel()">Export ke Excel</button>

  <script>
    const dataRekap = [];

    document.getElementById('rekapForm').addEventListener('submit', function(e) {
      e.preventDefault();

      const nama = document.getElementById('nama').value;
      const tanggal = document.getElementById('tanggal').value;
      const jamMulai = document.getElementById('jamMulai').value;
      const jamSelesai = document.getElementById('jamSelesai').value;
      const lembur = document.getElementById('lembur').value;
      const bahan = document.getElementById('bahan').value;

      const record = {
        "Nama Pekerja": nama,
        "Tanggal": tanggal,
        "Jam Mulai": jamMulai,
        "Jam Selesai": jamSelesai,
        "Perlu Lembur": lembur,
        "Bahan Kurang": bahan
      };

      dataRekap.push(record);

      // Reset form
      document.getElementById('rekapForm').reset();

      alert("Data berhasil disimpan!");
    });

    function exportToExcel() {
      if (dataRekap.length === 0) {
        alert("Belum ada data yang bisa diexport.");
        return;
      }

      const worksheet = XLSX.utils.json_to_sheet(dataRekap);
      const workbook = XLSX.utils.book_new();
      XLSX.utils.book_append_sheet(workbook, worksheet, "Rekap");

      XLSX.writeFile(workbook, "Rekap_Pekerjaan_PT_INKA.xlsx");
    }
  </script>

</body>
</html>
