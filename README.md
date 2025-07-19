<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Samgasi Market</title>
  <style>
    body { font-family: Arial; background: #f8f8f8; margin: 0; padding: 20px; }
    h1 { color: #2a7ae2; }
    .product { background: white; border-radius: 10px; padding: 10px; margin: 10px 0; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
  </style>
</head>
<body>
  <h1>Samgasi Market</h1>
  <div id="products">Yuklanmoqda...</div>

  <script>
    const sheetURL = "https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID/gviz/tq?tqx=out:json";

    fetch(sheetURL)
      .then(res => res.text())
      .then(data => {
        const json = JSON.parse(data.substr(47).slice(0, -2));
        const rows = json.table.rows;
        let html = "";
        rows.forEach(row => {
          const name = row.c[0]?.v || "";
          const price = row.c[1]?.v || "";
          const desc = row.c[2]?.v || "";
          html += `<div class="product">
                    <strong>${name}</strong><br>
                    Narxi: ${price} so‘m<br>
                    <small>${desc}</small>
                  </div>`;
        });
        document.getElementById("products").innerHTML = html;
      })
      .catch(err => {
        document.getElementById("products").innerText = "Xatolik yuz berdi!";
        console.error(err);
      });
  </script>
</body>
</html>
