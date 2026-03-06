<!DOCTYPE html>
<html>
<head>
<title>Aurix4x AI Gold Analyzer</title>
</head>

<body style="background:#0b1320;color:white;font-family:Arial;text-align:center">

<h2>Aurix4x AI Gold Analyzer</h2>

<input id="pair" placeholder="Search XAUUSD">
<button onclick="analyze()">Analyze</button>

<h3 id="result"></h3>

<script>

async function analyze(){

let pair = document.getElementById("pair").value

if(pair !== "XAUUSD"){
document.getElementById("result").innerHTML="Only XAUUSD supported"
return
}

let res = await fetch("https://api.twelvedata.com/time_series?symbol=XAU/USD&interval=5min&apikey=bc045d74482d4842848d3cf13b3f7992")

let data = await res.json()

let price = data.values[0].close

document.getElementById("result").innerHTML =
"Live XAUUSD Price : " + price

}

</script>

</body>
</html>
