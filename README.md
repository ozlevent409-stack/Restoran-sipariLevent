<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Restoran Sipariş Hesaplama</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: #f2f2f2;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 600px;
    margin: auto;
}

h1 {
    text-align: center;
    font-size: 24px;
}

.card {
    background: white;
    padding: 18px;
    margin-bottom: 15px;
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

label {
    display: block;
    font-weight: bold;
    margin-bottom: 6px;
}

select,
input {
    width: 100%;
    padding: 12px;
    box-sizing: border-box;
    margin-bottom: 12px;
    border: 1px solid #ccc;
    border-radius: 8px;
    font-size: 16px;
}

button {
    width: 100%;
    padding: 15px;
    background: #007aff;
    color: white;
    border: none;
    border-radius: 10px;
    font-size: 17px;
    font-weight: bold;
}

.product {
    border-top: 1px solid #ddd;
    padding-top: 15px;
    margin-top: 15px;
}

.result {
    background: #eaf7ea;
    padding: 12px;
    border-radius: 8px;
    margin-top: 10px;
    font-weight: bold;
}
</style>
</head>

<body>

<div class="container">

<h1>🍗 Restoran Sipariş Hesaplama</h1>

<div class="card">

<label>Sipariş Günü</label>

<select id="orderDay">
    <option value="Pazartesi">Pazartesi</option>
    <option value="Çarşamba">Çarşamba</option>
    <option value="Cuma">Cuma</option>
</select>

<label>Sipariş Saati</label>

<input type="time" id="orderTime">

</div>

<div class="card">

<h2>Ürün Stokları</h2>

<div class="product">
    <h3>Klasik Drop</h3>

    <label>Mevcut Stok</label>
    <input type="number" id="dropStock" value="59">

    <label>Minimum Stok</label>
    <input type="number" id="dropMin" value="30">
</div>

<div class="product">
    <h3>Kanat</h3>

    <label>Mevcut Stok</label>
    <input type="number" id="wingStock" value="1318">

    <label>Minimum Stok</label>
    <input type="number" id="wingMin" value="110">
</div>

<div class="product">
    <h3>Golden But</h3>

    <label>Mevcut Stok</label>
    <input type="number" id="butStock" value="66">

    <label>Minimum Stok</label>
    <input type="number" id="butMin" value="38">
</div>

</div>

<div class="card">

<button onclick="calculateOrder()">
    📦 Sipariş Miktarını Hesapla
</button>

<div id="result"></div>

</div>

</div>

<script>

function calculateOrder() {

    const day = document.getElementById("orderDay").value;

    const dropStock = Number(document.getElementById("dropStock").value);
    const dropMin = Number(document.getElementById("dropMin").value);

    const wingStock = Number(document.getElementById("wingStock").value);
    const wingMin = Number(document.getElementById("wingMin").value);

    const butStock = Number(document.getElementById("butStock").value);
    const butMin = Number(document.getElementById("butMin").value);

    /*
    Teslimat günleri:

    Pazartesi sipariş → Perşembe teslimat
    Çarşamba sipariş → Cumartesi teslimat
    Cuma sipariş → Salı teslimat
    */

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

    const dropOrder = Math.max(0, dropMin - dropStock);
    const wingOrder = Math.max(0, wingMin - wingStock);
    const butOrder = Math.max(0, butMin - butStock);

    document.getElementById("result").innerHTML = `

        <h3>📋 Sipariş Sonucu</h3>

        <p>
        <strong>Sipariş:</strong> ${day}
        </p>

        <p>
        <strong>Teslimat:</strong> ${deliveryDay}
        </p>

        <hr>

        <p>
        Klasik Drop: <strong>${dropOrder} adet</strong>
        </p>

        <p>
        Kanat: <strong>${wingOrder} adet</strong>
        </p>

        <p>
        Golden But: <strong>${butOrder} adet</strong>
        </p>

    `;
}

</script>

</body>
</html>
