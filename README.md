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
    box-shadow: 0 3px 12px rgba(0,0,0,0.15);
}
h1 {
    text-align: center;
    font-size: 24px;
}
h2 {
    margin-bottom: 10px;
}
.urun {
    background: #f7f7f7;
    padding: 15px;
    margin-top: 18px;
    border-radius: 12px;
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
    margin-top: 6px;
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
    border: none;
    border-radius: 10px;
    font-size: 18px;
    font-weight: bold;
}
#sonuc {
    margin-top: 25px;
}
.sonuc-kutu {
    background: #eeeeee;
    padding: 15px;
    border-radius: 12px;
}
.siparis {
    font-size: 25px;
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
<!-- KLASİK DROP -->
<div class="urun">
<h2>🍗 Klasik Drop</h2>
<p>1 koli = <strong>35 adet</strong></p>
<label>Kapanış (adet)</label>
<input
type="number"
id="dropKapanis"
min="0"
placeholder="Örn: 59">
<label>Gelen (koli)</label>
<input
type="number"
id="dropGelen"
min="0"
placeholder="Örn: 2">
<label>Kullanım (adet)</label>
<input
type="number"
id="dropKullanim"
min="0"
placeholder="Örn: 45">
<p>Minimum stok: <strong>30 adet</strong></p>
</div>
<!-- KANAT -->
<div class="urun">
<h2>🍗 Kanat</h2>
<p>1 koli = <strong>110 adet</strong></p>
<label>Kapanış (adet)</label>
<input
type="number"
id="kanatKapanis"
min="0"
placeholder="Örn: 1318">
<label>Gelen (koli)</label>
<input
type="number"
id="kanatGelen"
min="0"
placeholder="Örn: 2">
<label>Kullanım (adet)</label>
<input
type="number"
id="kanatKullanim"
min="0"
placeholder="Örn: 500">
<p>Minimum stok: <strong>110 adet</strong></p>
</div>
<!-- GOLDEN BUT -->
<div class="urun">
<h2>🍗 Golden But</h2>
<p>1 koli = <strong>38 adet</strong></p>
<label>Kapanış (adet)</label>
<input
type="number"
id="butKapanis"
min="0"
placeholder="Örn: 66">
<label>Gelen (koli)</label>
<input
type="number"
id="butGelen"
min="0"
placeholder="Örn: 2">
<label>Kullanım (adet)</label>
<input
type="number"
id="butKullanim"
min="0"
placeholder="Örn: 30">
<p>Minimum stok: <strong>38 adet</strong></p>
</div>
<button onclick="hesapla()">
📦 Sipariş Miktarını Hesapla
</button>
<div id="sonuc"></div>
</div>
<script>
function sayi(id) {
    return Number(document.getElementById(id).value) || 0;
}
function hesapla() {
    // SİPARİŞ GÜNÜ
    const gun =
        document.getElementById("gun").value;
    // TESLİMAT GÜNÜ
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
    /*
    KLASİK DROP
    1 koli = 35 adet
    Minimum = 30 adet
    */
    const dropKapanis =
        sayi("dropKapanis");
    const dropGelenKoli =
        sayi("dropGelen");
    const dropKullanim =
        sayi("dropKullanim");
    const dropGelenAdet =
        dropGelenKoli * 35;
    const dropKalan =
        dropKapanis +
        dropGelenAdet -
        dropKullanim;
    const dropIhtiyac =
        Math.max(
            0,
            30 - dropKalan
        );
    const dropSiparisKoli =
        Math.ceil(
            dropIhtiyac / 35
        );
    /*
    KANAT
    1 koli = 110 adet
    Minimum = 110 adet
    */
    const kanatKapanis =
        sayi("kanatKapanis");
    const kanatGelenKoli =
        sayi("kanatGelen");
    const kanatKullanim =
        sayi("kanatKullanim");
    const kanatGelenAdet =
        kanatGelenKoli * 110;
    const kanatKalan =
        kanatKapanis +
        kanatGelenAdet -
        kanatKullanim;
    const kanatIhtiyac =
        Math.max(
            0,
            110 - kanatKalan
        );
    const kanatSiparisKoli =
        Math.ceil(
            kanatIhtiyac / 110
        );
    /*
    GOLDEN BUT
    1 koli = 38 adet
    Minimum = 38 adet
    */
    const butKapanis =
        sayi("butKapanis");
    const butGelenKoli =
        sayi("butGelen");
    const butKullanim =
        sayi("butKullanim");
    const butGelenAdet =
        butGelenKoli * 38;
    const butKalan =
        butKapanis +
        butGelenAdet -
        butKullanim;
    const butIhtiyac =
        Math.max(
            0,
            38 - butKalan
        );
    const butSiparisKoli =
        Math.ceil(
            butIhtiyac / 38
        );
    /*
    SONUÇ
    */
    document.getElementById("sonuc").innerHTML = `
    <div class="sonuc-kutu">
        <h2>📦 Sipariş Sonucu</h2>
        <p>
        Sipariş günü:
        <strong>${gun}</strong>
        </p>
        <p>
        Teslim günü:
        <strong>${teslimGun}</strong>
        </p>
        <hr>
        <h3>🍗 Klasik Drop</h3>
        <p>
        Teslimat öncesi kalan:
        <strong>${dropKalan} adet</strong>
        </p>
        <p>
        İhtiyaç:
        <strong>${dropIhtiyac} adet</strong>
        </p>
        <p class="siparis">
        Sipariş: ${dropSiparisKoli} koli
        </p>
        <h3>🍗 Kanat</h3>
        <p>
        Teslimat öncesi kalan:
        <strong>${kanatKalan} adet</strong>
        </p>
        <p>
        İhtiyaç:
        <strong>${kanatIhtiyac} adet</strong>
        </p>
        <p class="siparis">
        Sipariş: ${kanatSiparisKoli} koli
        </p>
        <h3>🍗 Golden But</h3>
        <p>
        Teslimat öncesi kalan:
        <strong>${butKalan} adet</strong>
        </p>
        <p>
        İhtiyaç:
        <strong>${butIhtiyac} adet</strong>
        </p>
        <p class="siparis">
        Sipariş: ${butSiparisKoli} koli
        </p>
    </div>
    `;
}
</script>
</body>
</html>
