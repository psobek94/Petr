# Petr
Portfolio tracker
<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Moje investiční portfolio</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f5f5f5;
      color: #333;
    }
    header {
      background-color: #222;
      color: white;
      padding: 1rem;
      text-align: center;
    }
    .container {
      padding: 1rem;
      max-width: 1200px;
      margin: 0 auto;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 1rem;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 0.5rem;
      text-align: left;
    }
    th {
      background-color: #eee;
    }
    .toggle {
      float: right;
    }
  </style>
</head>
<body>
  <header>
    <h1>Moje investiční portfolio</h1>
  </header>

  <div class="container">
    <label for="currency">Měna:</label>
    <select id="currency">
      <option value="USD">USD</option>
      <option value="CZK">CZK</option>
    </select>

    <input type="text" id="search" placeholder="Hledat akcie..." style="float:right;"/>

    <table id="portfolio">
      <thead>
        <tr>
          <th>Logo</th>
          <th>Název</th>
          <th>Ticker</th>
          <th>Počet</th>
          <th>Cena (USD)</th>
          <th>Hodnota</th>
          <th>Div. výnos</th>
          <th>Dividenda ročně</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><img src="https://logo.clearbit.com/apple.com" alt="Apple" width="32" /></td>
          <td>Apple</td>
          <td>AAPL</td>
          <td>5</td>
          <td>180</td>
          <td class="value" data-usd="900">900</td>
          <td>0.5%</td>
          <td>4.5</td>
        </tr>
        <tr>
          <td><img src="https://logo.clearbit.com/microsoft.com" alt="Microsoft" width="32" /></td>
          <td>Microsoft</td>
          <td>MSFT</td>
          <td>3</td>
          <td>350</td>
          <td class="value" data-usd="1050">1050</td>
          <td>0.8%</td>
          <td>8.4</td>
        </tr>
        <!-- Další řádky zde -->
      </tbody>
    </table>
  </div>

  <script>
    const currencySelect = document.getElementById("currency");
    const values = document.querySelectorAll(".value");
    const exchangeRate = 23.5;

    currencySelect.addEventListener("change", () => {
      const currency = currencySelect.value;
      values.forEach(cell => {
        const usd = parseFloat(cell.dataset.usd);
        if (currency === "CZK") {
          cell.textContent = (usd * exchangeRate).toFixed(2);
        } else {
          cell.textContent = usd.toFixed(2);
        }
      });
    });

    const searchInput = document.getElementById("search");
    searchInput.addEventListener("input", () => {
      const filter = searchInput.value.toLowerCase();
      const rows = document.querySelectorAll("#portfolio tbody tr");
      rows.forEach(row => {
        const text = row.textContent.toLowerCase();
        row.style.display = text.includes(filter) ? "" : "none";
      });
    });
  </script>
</body>
</html>
