# Pr-dicateur-rng
<!DOCTYPE html>
<html>
<head>
<title>Prédicteur RNG</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body { font-family: Arial; padding: 20px; }
h1, h2 { text-align: center; }
#tirage { font-weight: bold; font-size: 1.2em; margin-top: 10px; }
button { padding: 10px; margin-top: 15px; background-color: blue; color: white; border: none; border-radius: 5px; width: 100%; }
#liste, #stats { margin-top: 10px; text-align: center; }
</style>
</head>
<body>
<h1>Prédicteur RNG</h1>

<h2>100 derniers numéros :</h2>
<div id="liste"></div>

<h2>Statistiques :</h2>
<div id="stats"></div>

<h2>Tirage aléatoire de 15 numéros :</h2>
<div id="tirage"></div>

<button onclick="genererTirage()">Générer 15 numéros</button>

<script>
// Génère 100 numéros aléatoires 0-36 (simule les derniers tirages)
let derniersNumeros = [];
for(let i=0; i<100; i++){
    derniersNumeros.push(Math.floor(Math.random()*37));
}
document.getElementById('liste').innerText = derniersNumeros.join(' – ');

// Calcul statistiques
let freq = {};
for(let n=0; n<37; n++) freq[n]=0;
derniersNumeros.forEach(n => freq[n]++);
let top = Object.entries(freq).sort((a,b)=>b[1]-a[1]).slice(0,5);
let low = Object.entries(freq).sort((a,b)=>a[1]-b[1]).slice(0,5);
document.getElementById('stats').innerHTML = 
    "Top 5 : " + top.map(x=>x[0]+" ("+x[1]+")").join(", ") + "<br>" +
    "Moins fréquents : " + low.map(x=>x[0]+" ("+x[1]+")").join(", ");

// Tirage aléatoire 15 numéros
function genererTirage(){
    let shuffle = derniersNumeros.sort(()=>0.5-Math.random());
    let tirage15 = shuffle.slice(0,15);
    document.getElementById('tirage').innerText = tirage15.join(' – ');
}
</script>

</body>
</html>

