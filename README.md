<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Kalkulator Reward</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 700px; margin: auto; padding: 20px; }
    label { display: block; margin-top: 10px; }
    input, select { width: 100%; padding: 8px; margin-top: 5px; }
    .result { margin-top: 20px; background: #f0f0f0; padding: 15px; border-radius: 8px; }
  </style>
</head>
<body>
  <h2>Kalkulator Reward</h2>

  <label for="balance">Balance (Rp):</label>
  <input type="text" id="balance" placeholder="Contoh: 100.000.000">

  <label for="rate">Rate Reward (%):</label>
  <input type="number" id="rate" step="0.1" min="0.1" max="3.5" placeholder="Contoh: 1.5">

  <label for="start">Penempatan Awal:</label>
  <input type="date" id="start">

  <label for="end">Akhir Penempatan:</label>
  <input type="date" id="end">

  <button onclick="hitung()">Hitung</button>

  <div class="result" id="hasil" style="display:none">
    <p><strong>Jumlah Hari:</strong> <span id="hari"></span> hari</p>
    <p><strong>Reward:</strong> Rp <span id="reward"></span></p>
    <p><strong>Penalty (1%):</strong> Rp <span id="penalty"></span></p>
  </div>

  <script>
    function parseRupiah(str) {
      return parseFloat(str.replaceAll('.', '').replace(',', '.')) || 0;
    }

    function formatRupiah(angka) {
      return new Intl.NumberFormat('id-ID').format(angka);
    }

    function hitung() {
      const balanceInput = document.getElementById('balance').value;
      const rate = parseFloat(document.getElementById('rate').value) / 100;
      const startDate = new Date(document.getElementById('start').value);
      const endDate = new Date(document.getElementById('end').value);

      const balance = parseRupiah(balanceInput);

      if (isNaN(balance) || isNaN(rate) || !startDate || !endDate || endDate <= startDate) {
        alert("Pastikan semua input valid dan tanggal akhir setelah tanggal awal.");
        return;
      }

      const diffTime = endDate - startDate;
      const days = diffTime / (1000 * 60 * 60 * 24);

      const reward = balance * rate * (days / 365);
      const penalty = balance * 0.001 * days / 365;

      document.getElementById('hari').textContent = days;
      document.getElementById('reward').textContent = formatRupiah(reward.toFixed(2));
      document.getElementById('penalty').textContent = formatRupiah(penalty.toFixed(2));
      document.getElementById('hasil').style.display = 'block';
    }
  </script>
</body>
</html>
