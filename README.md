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
    padding: 15px;
    margin: 0;
}

.container {
    max-width: 500px;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 15px;
}

h1 {
    text-align: center;
}

.urun {
    background: #f5f5f5;
    padding: 15px;
    margin-top: 15px;
    border-radius: 10px;
}

label {
    display: block;
    font-weight: bold;
    margin-top: 12px;
}

input, select {
    width: 100%;
    box-sizing: border-box;
    padding: 12px;
    margin-top: 5px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 8px;
}

button {
    width: 100%;
    padding: 16px;
    margin-top: 25px;
    background: #222;
    color: white;
    border: 0;
    border-radius: 10px;
    font-size: 18px;
    font-weight: bold;
}

#sonuc {
    margin-top: 25px;
}

.sonuc-kutu {
    background: #eee;
    padding: 15px;
    border-radius: 10px;
    margin-top: 10px;
}

.siparis {
    font-size: 24px;
    font-weight: bold;
}
</style>
</head>

<body>

<div class="container">

<h1>🍗 Restoran Sipariş Hesaplama</h1>

<label>Sipariş Günü</label>

<select id="gun">
    <option value="Pazartesi">Pazartesi</option>
    <option value="Çarşamba">Çarşamba</option>
    <option value="Cuma">Cuma</option>
</select>

<label>Sipariş Saati</label>
<input type="time" id="saat">


<div class="urun">

<h2>Klasik Drop</h2>

<label>Mevcut Stok</label>
<input type="number" id="dropMevcut" placeholder="Örn: 59">

<label>Gelen</label>
<input type="number" id="dropGelen" placeholder="Yoksa 0">

<label>Kullanım</label>
<input type="number" id="dropKullanim" placeholder="Bu haftaki kullanım">

<p>Minimum stok: <b>30</b></p>

</div>


<div class="urun">

<h2>Kanat</h2>

<label>Mevcut Stok</label>
<input type="number" id="kanatMevcut" placeholder="Örn: 1318">

<label>Gelen</label>
<input type="number" id="kanatGelen" placeholder="Yoksa 0">

<label>Kullanım</label>
<input type="number" id="kanatKullanim" placeholder="Bu haftaki kullanım">

<p>Minimum stok: <b>110</b></p>

</div>


<div class="urun">

<h2>Golden But</h2>

<label>Mevcut Stok</label>
<input type="number" id="butMevcut" placeholder="Örn: 66">

<label>Gelen</label>
<input type="number" id="butGelen" placeholder="Yoksa 0">

<label>Kullanım</label>
<input type="number" id="butKullanim" placeholder="Bu haftaki kullanım">

<p>Minimum stok: <b>38</b></p>

</div>


<button onclick="hesapla()">
📦 Sipariş Miktarını Hesapla
</button>


<div id="sonuc"></div>

</div>


<script>

function hesapla() {

    let gun = document.getElementById("gun").value;

    let teslimGun = "";

    if (gun === "Pazartesi") {
        teslimGun = "Perşembe";
    }

    if (gun === "Çarşamba") {
        teslimGun = "Cumartesi";
    }

    if (gun === "Cuma") {
        teslimGun = "Salı";
    }


    // KLASİK DROP

    let dropMevcut =
        Number(document.getElementById("dropMevcut").value) || 0;

    let dropGelen =
        Number(document.getElementById("dropGelen").value) || 0;

    let dropKullanim =
        Number(document.getElementById("dropKullanim").value) || 0;

    let dropKalan =
        dropMevcut + dropGelen - dropKullanim;

    let dropSiparis =
        Math.max(0, 30 - dropKalan);


    // KANAT

    let kanatMevcut =
        Number(document.getElementById("kanatMevcut").value) || 0;

    let kanatGelen =
        Number(document.getElementById("kanatGelen").value) || 0;

    let kanatKullanim =
        Number(document.getElementById("kanatKullanim").value) || 0;

    let kanatKalan =
        kanatMevcut + kanatGelen - kanatKullanim;

    let kanatSiparis =
        Math.max(0, 110 - kanatKalan);


    // GOLDEN BUT

    let butMevcut =
        Number(document.getElementById("butMevcut").value) || 0;

    let butGelen =
        Number(document.getElementById("butGelen").value) || 0;

    let butKullanim =
        Number(document.getElementById("butKullanim").value) || 0;

    let butKalan =
        butMevcut + butGelen - butKullanim;

    let butSiparis =
        Math.max(0, 38 - butKalan);


    // SONUÇ

    document.getElementById("sonuc").innerHTML = `

    <div class="sonuc-kutu">

        <h2>📦 Sipariş Sonucu</h2>

        <p>
        Sipariş günü: <b>${gun}</b>
        </p>

        <p>
        Teslim günü: <b>${teslimGun}</b>
        </p>

        <hr>

        <h3>Klasik Drop</h3>
        <p>Kalan stok: ${dropKalan}</p>
        <p class="siparis">
        Sipariş: ${dropSiparis} adet
        </p>

        <h3>Kanat</h3>
        <p>Kalan stok: ${kanatKalan}</p>
        <p class="siparis">
        Sipariş: ${kanatSiparis} adet
        </p>

        <h3>Golden But</h3>
        <p>Kalan stok: ${butKalan}</p>
        <p class="siparis">
        Sipariş: ${butSiparis} adet
        </p>

    </div>

    `;
}

</script>

</body>
</html>
