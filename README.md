<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Restoran Sipariş Hesaplama</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: #f4f4f4;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 500px;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 3px 12px rgba(0,0,0,0.15);
}

h1 {
    text-align: center;
    font-size: 24px;
}

label {
    display: block;
    margin-top: 15px;
    font-weight: bold;
}

select,
input {
    width: 100%;
    box-sizing: border-box;
    padding: 12px;
    margin-top: 6px;
    border: 1px solid #ccc;
    border-radius: 8px;
    font-size: 16px;
}

button {
    width: 100%;
    padding: 15px;
    margin-top: 25px;
    border: none;
    border-radius: 10px;
    background: #222;
    color: white;
    font-size: 18px;
    font-weight: bold;
}

.result {
    margin-top: 25px;
    padding: 15px;
    background: #f1f1f1;
    border-radius: 10px;
}

.product {
    background: white;
    padding: 12px;
    margin-top: 10px;
    border-radius: 8px;
    border-left: 5px solid #222;
}

.order {
    font-size: 22px;
    font-weight: bold;
}
</style>
</head>

<body>

<div class="container">

<h1>🍗 Restoran Sipariş Hesaplama</h1>

<label>Sipariş Günü</label>

<select id="orderDay">
    <option value="Pazartesi">Pazartesi</option>
    <option value="Çarşamba">Çarşamba</option>
    <option value="Cuma">Cuma</option>
</select>

<label>Sipariş Saati</label>

<input type="time" id="orderTime">

<h2>Mevcut Stok</h2>

<label>Klasik Drop</label>
<input type="number" id="dropStock" placeholder="Mevcut adet">

<label>Kanat</label>
<input type="number" id="wingStock" placeholder="Mevcut adet">

<label>Golden But</label>
<input type="number" id="goldenStock" placeholder="Mevcut adet">

<button onclick="calculateOrder()">
📦 Sipariş Miktarını Hesapla
</button>

<div id="result"></div>

</div>

<script>

function calculateOrder() {

    const day = document.getElementById("orderDay").value;

    const dropStock = Number(document.getElementById("dropStock").value) || 0;
    const wingStock = Number(document.getElementById("wingStock").value) || 0;
    const goldenStock = Number(document.getElementById("goldenStock").value) || 0;

    let deliveryDay = "";

    if (day === "Pazartesi") {
        deliveryDay = "Perşembe";
    }

    if (day === "Çarşamba") {
        deliveryDay = "Cumartesi";
    }

    if (day === "Cuma") {
        deliveryDay = "Salı";
    }

    /*
       9 günlük kullanım verileri
    */

    const dropDaily = 166 / 9;
    const wingDaily = 4246 / 9;
    const goldenDaily = 102 / 9;

    /*
       Minimum stoklar
    */

    const dropMin = 30;
    const wingMin = 110;
    const goldenMin = 38;

    /*
       Teslimata kadar 3 günlük tüketim
    */

    const dropNeeded = Math.ceil(dropDaily * 3);
    const wingNeeded = Math.ceil(wingDaily * 3);
    const goldenNeeded = Math.ceil(goldenDaily * 3);

    /*
       Sipariş hesabı

       Mevcut stok
       - teslimata kadar kullanılacak miktar
       - minimum stok

       eksikse sipariş miktarı
    */

    const dropOrder = Math.max(
        0,
        Math.ceil(dropNeeded + dropMin - dropStock)
    );

    const wingOrder = Math.max(
        0,
        Math.ceil(wingNeeded + wingMin - wingStock)
    );

    const goldenOrder = Math.max(
        0,
        Math.ceil(goldenNeeded + goldenMin - goldenStock)
    );

    document.getElementById("result").innerHTML = `

        <div class="result">

            <h2>📦 Sipariş Sonucu</h2>

            <p>
            <strong>Sipariş günü:</strong> ${day}
            </p>

            <p>
            <strong>Teslim günü:</strong> ${deliveryDay}
            </p>

            <div class="product">
                <strong>Klasik Drop</strong><br>
                Mevcut stok: ${dropStock}<br>
                Sipariş:
                <span class="order">${dropOrder} adet</span>
            </div>

            <div class="product">
                <strong>Kanat</strong><br>
                Mevcut stok: ${wingStock}<br>
                Sipariş:
                <span class="order">${wingOrder} adet</span>
            </div>

            <div class="product">
                <strong>Golden But</strong><br>
                Mevcut stok: ${goldenStock}<br>
                Sipariş:
                <span class="order">${goldenOrder} adet</span>
            </div>

        </div>
    `;
}

</script>

</body>
</html>
