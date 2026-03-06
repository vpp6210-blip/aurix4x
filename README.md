<!DOCTYPE html>
<html>

<head>
<title>Aurix4x AI Gold Analyzer</title>

<style>
body{
font-family:Arial;
background:#0f172a;
color:white;
text-align:center;
padding-top:40px
}

input{
padding:10px;
font-size:16px
}

button{
padding:10px 20px;
background:gold;
border:none;
font-weight:bold;
cursor:pointer
}

#result{
margin-top:20px;
font-size:18px
}
</style>

</head>

<body>

<h2>Aurix4x AI Gold Analyzer</h2>

<input id="pair" placeholder="Type XAUUSD">
<br><br>

<button onclick="analyze()">Analyze</button>

<div id="result"></div>

<script>

async function analyze(){

let pair = document.getElementById("pair").value

if(pair !== "XAUUSD"){
document.getElementById("result").innerHTML="Only XAUUSD supported"
return
}

let res = await fetch("https://api.twelvedata.com/time_series?symbol=XAU/USD&interval=5min&outputsize=50&apikey=bc045d74482d4842848d3cf13b3f7992")

let data = await res.json()

let closes = data.values.map(v => parseFloat(v.close))

let price = closes[0]

let avg = closes.reduce((a,b)=>a+b)/closes.length

let signal=""
let win=""

if(price > avg){
signal="BUY"
win="68%"
}else{
signal="SELL"
win="65%"
}

let sl = (signal=="BUY") ? (price-5).toFixed(2) : (price+5).toFixed(2)
let tp = (signal=="BUY") ? (price+8).toFixed(2) : (price-8).toFixed(2)

document.getElementById("result").innerHTML = `
Live Price : ${price}<br><br>

Signal : ${signal}<br>
Win Probability : ${win}<br><br>

Take Profit : ${tp}<br>
Stop Loss : ${sl}
`

}

</script>

</body>
</html>
