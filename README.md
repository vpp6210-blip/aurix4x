<h2>Aurix4x AI Gold Analyzer</h2>

<input id="pair" placeholder="Search XAUUSD">
<button onclick="analyze()">Analyze</button>

<div id="result"></div>

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
