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
.siparis-listesi {
    margin-top: 25px;
    background: #eeeeee;
    padding: 20px;
    border-radius: 15px;
}
.siparis-baslik {
    text-align: center;
    font-size: 28px;
    font-weight: bold;
    margin-bottom: 15px;
}
.teslim {
    text-align: center;
    font-size: 18px;
    margin-bottom: 20px;
}
.siparis-urun {
    background: white;
    padding: 18px;
    margin-top: 12px;
    border-radius: 12px;
    text-align: center;
}
.urun-adi {
    font-size: 20px;
    font-weight: bold;
}
.koli {
    font-size: 32px;
    font-weight: bold;
    margin-top: 8px;
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
📦 SİPARİŞ MİKTARINI HESAPLA
</button>
<div id="sonuc"></div>
</div>
<script>
function sayi(id) {
    return Number(
        document.getElementById(id).value
    ) || 0;
}
function hesapla() {
    const gun =
        document.getElementById("gun").value;
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
    */
    const dropKapanis =
        sayi("dropKapanis");
    const dropGelen =
        sayi("dropGelen");
    const dropKullanim =
        sayi("dropKullanim");
    const dropKalan =
        dropKapanis +
        (dropGelen * 35) -
        dropKullanim;
    const dropIhtiyac =
        Math.max(
            0,
            30 - dropKalan
        );
    const dropSiparis =
        Math.ceil(
            dropIhtiyac / 35
        );
    /*
    KANAT
    */
    const kanatKapanis =
        sayi("kanatKapanis");
    const kanatGelen =
        sayi("kanatGelen");
    const kanatKullanim =
        sayi("kanatKullanim");
    const kanatKalan =
        kanatKapanis +
        (kanatGelen * 110) -
        kanatKullanim;
    const kanatIhtiyac =
        Math.max(
            0,
            110 - kanatKalan
        );
    const kanatSiparis =
        Math.ceil(
            kanatIhtiyac / 110
        );
    /*
    GOLDEN BUT
    */
    const butKapanis =
        sayi("butKapanis");
    const butGelen =
        sayi("butGelen");
    const butKullanim =
        sayi("butKullanim");
    const butKalan =
        butKapanis +
        (butGelen * 38) -
        butKullanim;
    const butIhtiyac =
        Math.max(
            0,
            38 - butKalan
        );
    const butSiparis =
        Math.ceil(
            butIhtiyac / 38
        );
    /*
    BÜYÜK SİPARİŞ LİSTESİ
    */
    document.getElementById("sonuc").innerHTML = `
    <div class="siparis-listesi">
        <div class="siparis-baslik">
            📦 SİPARİŞ LİSTESİ
        </div>
        <div class="teslim">
            Teslim Günü:
            <strong>${teslimGun}</strong>
        </div>
        <div class="siparis-urun">
            <div class="urun-adi">
                🍗 KLASİK DROP
            </div>
            <div class="koli">
                ${dropSiparis} KOLİ
            </div>
        </div>
        <div class="siparis-urun">
            <div class="urun-adi">
                🍗 KANAT
            </div>
            <div class="koli">
                ${kanatSiparis} KOLİ
            </div>
        </div>
        <div class="siparis-urun">
            <div class="urun-adi">
                🍗 GOLDEN BUT
            </div>
            <div class="koli">
                ${butSiparis} KOLİ
            </div>
        </div>
    </div>
    `;
}
</script>
</body>
</html>
