<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Restoran Sipariş Hesaplama</title>
<style>
body {
    font-family: Arial, sans-serif;
    background: #f3f3f3;
    margin: 0;
    padding: 15px;
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
h2 {
    margin-top: 25px;
}
label {
    display: block;
    margin-top: 12px;
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
.product {
    margin-top: 20px;
    padding: 15px;
    background: #f7f7f7;
    border-radius: 10px;
}
.product h3 {
    margin-top: 0;
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
    background: #eeeeee;
    border-radius: 10px;
}
.order {
    font-size: 24px;
    font-weight: bold;
}
.delivery {
    font-size: 18px;
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
<!-- KLASİK DROP -->
<div class="product">
<h3>🍗 Klasik Drop</h3>
<label>Mevcut Stok</label>
<input type="number" id="dropStock" min="0" placeholder="Örn: 59">
<label>Gelen Ürün</label>
<input type="number" id="dropIncoming" min="0" placeholder="Yoksa 0">
<label>Kullanım</label>
<input type="number" id="dropUsage" min="0" placeholder="Manuel kullanım">
<p>Minimum Stok: <strong>30</strong></p>
</div>
<!-- KANAT -->
<div class="product">
<h3>🍗 Kanat</h3>
<label>Mevcut Stok</label>
<input type="number" id="wingStock" min="0" placeholder="Örn: 1318">
<label>Gelen Ürün</label>
<input type="number" id="wingIncoming" min="0" placeholder="Yoksa 0">
<label>Kullanım</label>
<input type="number" id="wingUsage" min="0" placeholder="Manuel kullanım">
<p>Minimum Stok: <strong>110</strong></p>
</div>
<!-- GOLDEN BUT -->
<div class="product">
<h3>🍗 Golden But</h3>
<label>Mevcut Stok</label>
<input type="number" id="goldenStock" min="0" placeholder="Örn: 66">
<label>Gelen Ürün</label>
<input type="number" id="goldenIncoming" min="0" placeholder="Yoksa 0">
<label>Kullanım</label>
<input type="number" id="goldenUsage" min="0" placeholder="Manuel kullanım">
<p>Minimum Stok: <strong>38</strong></p>
</div>
<button onclick="calculateOrder()">
📦 Sipariş Miktarını Hesapla
</button>
<div id="result"></div>
</div>
<script>
function calculateOrder() {
    const day = document.getElementById("orderDay").value;
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
    KLASİK DROP
    */
    const dropStock =
        Number(document.getElementById("dropStock").value) || 0;
    const dropIncoming =
        Number(document.getElementById("dropIncoming").value) || 0;
    const dropUsage =
        Number(document.getElementById("dropUsage").value) || 0;
    const dropMinimum = 30;
    const dropRemaining =
        dropStock + dropIncoming - dropUsage;
    const dropOrder =
        Math.max(0, dropMinimum - dropRemaining);
    /*
    KANAT
    */
    const wingStock =
        Number(document.getElementById("wingStock").value) || 0;
    const wingIncoming =
        Number(document.getElementById("wingIncoming").value) || 0;
    const wingUsage =
        Number(document.getElementById("wingUsage").value) || 0;
    const wingMinimum = 110;
    const wingRemaining =
        wingStock + wingIncoming - wingUsage;
    const wingOrder =
        Math.max(0, wingMinimum - wingRemaining);
    /*
    GOLDEN BUT
    */
    const goldenStock =
        Number(document.getElementById("goldenStock").value) || 0;
    const goldenIncoming =
        Number(document.getElementById("goldenIncoming").value) || 0;
    const goldenUsage =
        Number(document.getElementById("goldenUsage").value) || 0;
    const goldenMinimum = 38;
    const goldenRemaining =
        goldenStock + goldenIncoming - goldenUsage;
    const goldenOrder =
        Math.max(0, goldenMinimum - goldenRemaining);
    /*
    SONUÇ
    */
    document.getElementById("result").innerHTML = `
        <div class="result">
            <h2>📦 Sipariş Sonucu</h2>
            <p>
            Sipariş Günü:
            <strong>${day}</strong>
            </p>
            <p class="delivery">
            Teslim Günü:
            ${deliveryDay}
            </p>
            <hr>
            <h3>🍗 Klasik Drop</h3>
            <p>
            Teslimat öncesi kalan:
            <strong>${dropRemaining}</strong>
            </p>
            <p class="order">
            Sipariş: ${dropOrder} adet
            </p>
            <h3>🍗 Kanat</h3>
            <p>
            Teslimat öncesi kalan:
            <strong>${wingRemaining}</strong>
            </p>
            <p class="order">
            Sipariş: ${wingOrder} adet
            </p>
            <h3>🍗 Golden But</h3>
            <p>
            Teslimat öncesi kalan:
            <strong>${goldenRemaining}</strong>
            </p>
            <p class="order">
            Sipariş: ${goldenOrder} adet
            </p>
        </div>
    `;
}
</script>
</body>
</html>
