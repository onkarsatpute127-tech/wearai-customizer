
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>WearAI Customizer</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f6f5f1;color:#171717}
header{background:#111;color:white;padding:18px 6%;display:flex;justify-content:space-between;align-items:center}
main{max-width:1050px;margin:auto;padding:22px}
.hero{background:#e8e3da;padding:38px 20px;text-align:center;border-radius:16px}
button{background:#171717;color:white;padding:12px 16px;border:0;border-radius:8px;cursor:pointer}
input,select,textarea{width:100%;padding:12px;border:1px solid #ccc;border-radius:8px;margin:7px 0 14px;font:inherit}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(190px,1fr));gap:14px}
.card,.panel{background:white;padding:18px;border:1px solid #e4e4e4;border-radius:12px}
.shirt{height:190px;background:#eee;display:grid;place-items:center;border-radius:10px;position:relative;overflow:hidden}
.shirt svg{width:150px;height:160px}
#shirtText{position:absolute;top:85px;max-width:100px;text-align:center;font-size:14px;font-weight:bold;overflow-wrap:anywhere}
.layout{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:18px}
h2{margin-top:30px}
small{color:#666}
</style>
</head>
<body>
<header><b>WearAI ✦</b><span>Custom Clothing Studio</span></header>
<main>
<div class="hero">
<h1>Your Idea. Your Style.</h1>
<p>Choose a product, personalize your look and submit your design request.</p>
<button onclick="document.getElementById('customize').scrollIntoView()">Start Customizing</button>
</div>

<h2>Explore Collections</h2>
<input id="search" placeholder="Search T-shirts, hoodies, shirts..." oninput="filterProducts()">
<div class="grid" id="products">
<div class="card" data-search="t-shirt tshirt graphic streetwear">
<h3>Graphic T-shirt</h3><p>Everyday custom streetwear</p>
<button onclick="choose('T-shirt')">Customize</button></div>
<div class="card" data-search="hoodie oversized sweatshirt">
<h3>Oversized Hoodie</h3><p>Your style, your idea</p>
<button onclick="choose('Hoodie')">Customize</button></div>
<div class="card" data-search="shirt casual formal">
<h3>Custom Shirt</h3><p>Create your own look</p>
<button onclick="choose('Shirt')">Customize</button></div>
</div>

<h2 id="customize">Customize Your Product</h2>
<div class="layout">
<div class="panel">
<h3>Live Preview</h3>
<div class="shirt" id="preview">
<svg viewBox="0 0 200 200" aria-label="T-shirt preview">
<path id="shirtShape" d="M65 25 L82 15 Q100 35 118 15 L135 25 L175 55 L150 85 L135 72 L135 185 L65 185 L65 72 L50 85 L25 55 Z" fill="#222" stroke="#555" stroke-width="2"/>
</svg>
<div id="shirtText"></div>
</div>
<label>Clothing colour</label>
<select id="color" onchange="updatePreview()">
<option value="#222222">Black</option><option value="#ffffff">White</option>
<option value="#173c75">Blue</option><option value="#8b2635">Maroon</option>
<option value="#777777">Grey</option>
</select>
<label>Text on clothing</label>
<input id="printText" maxlength="45" placeholder="Example: MY STYLE" oninput="updatePreview()">
<label>Choose product</label>
<select id="product" onchange="updatePreview()">
<option>T-shirt</option><option>Hoodie</option><option>Shirt</option><option>Sweatshirt</option>
</select>
</div>

<div class="panel">
<h3>AI Design Idea</h3>
<small>This demo collects your idea; AI image generation is not connected yet.</small>
<label>Describe your design</label>
<textarea id="idea" placeholder="Example: Futuristic blue tiger on a black oversized T-shirt"></textarea>
<label>Preferred design style</label>
<select id="style"><option>Streetwear</option><option>Minimalist</option><option>Anime-inspired</option><option>Nature</option><option>Sports</option><option>Indian-inspired</option></select>
<label>Your contact</label>
<input id="contact" placeholder="Email or mobile number">
<button onclick="downloadRequest()">Download Design Request</button>
<p id="message" role="status"></p>
</div>
</div>
<footer><p>WearAI Customizer · Your idea, your style.</p></footer>
</main>
<script>
function choose(p){document.getElementById('product').value=p;updatePreview();document.getElementById('customize').scrollIntoView({behavior:'smooth'})}
function filterProducts(){let q=document.getElementById('search').value.toLowerCase();document.querySelectorAll('[data-search]').forEach(c=>c.style.display=c.dataset.search.includes(q)?'block':'none')}
function updatePreview(){let c=document.getElementById('color').value;document.getElementById('shirtShape').setAttribute('fill',c);document.getElementById('shirtText').textContent=document.getElementById('printText').value;document.getElementById('shirtText').style.color=c==='#ffffff'?'#111':'#fff'}
function downloadRequest(){let contact=document.getElementById('contact').value.trim();let idea=document.getElementById('idea').value.trim();if(!contact||!idea){document.getElementById('message').textContent='Please enter your design idea and contact details.';return}let text='WearAI Design Request\nProduct: '+document.getElementById('product').value+'\nColour: '+document.getElementById('color').selectedOptions[0].text+'\nText: '+document.getElementById('printText').value+'\nStyle: '+document.getElementById('style').value+'\nDesign idea: '+idea+'\nContact: '+contact+'\n';let a=document.createElement('a');a.href=URL.createObjectURL(new Blob([text],{type:'text/plain'}));a.download='wearai-design-request.txt';a.click();URL.revokeObjectURL(a.href);document.getElementById('message').textContent='Request file downloaded to this device. It has not been sent to the owner.'}
updatePreview();
</script>
</body>
</html>
