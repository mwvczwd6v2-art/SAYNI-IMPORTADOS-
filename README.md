# SAYNI-IMPORTADOS-
tienda web
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SAYNI IMPORTADOS</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600&family=Montserrat:wght@300;400;500&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Montserrat',sans-serif;background:#fffafc;color:#4a2a35}
.header{padding:30px 20px;text-align:center;background:#fff;border-bottom:1px solid #f8d7e2}
.header h1{font-family:'Cormorant Garamond',serif;font-size:42px;letter-spacing:6px;font-weight:600;color:#b03a5b}
.header p{margin-top:8px;letter-spacing:3px;font-size:12px;color:#c48a9c}
.filters{display:flex;gap:10px;justify-content:center;flex-wrap:wrap;padding:25px 15px;background:#fff}
.filters button{border:1px solid #f3c2d1;background:#fff;padding:10px 18px;border-radius:25px;cursor:pointer;font-size:13px;transition:.3s}
.filters button.active,.filters button:hover{background:#b03a5b;color:#fff;border-color:#b03a5b}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(170px,1fr));gap:18px;padding:20px;max-width:1200px;margin:0 auto}
.card{background:#fff;border-radius:18px;padding:12px;border:1px solid #fde2ea;transition:.3s;text-align:center}
.card:hover{transform:translateY(-4px);box-shadow:0 10px 25px rgba(176,58,91,.12)}
.card img{width:100%;height:210px;object-fit:contain;background:#fff9fb;border-radius:12px}
.card h3{font-size:13px;margin:10px 0 4px;font-weight:500;line-height:1.2;height:32px;overflow:hidden}
.card .price{font-weight:600;color:#b03a5b;margin:6px 0;font-size:15px}
.card button{width:100%;background:#b03a5b;color:#fff;border:none;padding:9px;border-radius:20px;cursor:pointer;font-size:12px;margin-top:6px}
.cart-btn{position:fixed;bottom:20px;right:20px;background:#b03a5b;color:#fff;border:none;width:60px;height:60px;border-radius:50%;font-size:24px;cursor:pointer;box-shadow:0 6px 20px rgba(0,0,0,.2);z-index:100}
.cart-count{position:absolute;top:-5px;right:-5px;background:#000;color:#fff;width:22px;height:22px;border-radius:50%;font-size:12px;display:flex;align-items:center;justify-content:center}
#cartModal{position:fixed;inset:0;background:rgba(0,0,0,.5);display:none;z-index:200;justify-content:flex-end}
#cartModal.open{display:flex}
.cart-panel{background:#fff;width:100%;max-width:400px;height:100%;overflow:auto;padding:20px;display:flex;flex-direction:column}
.cart-item{display:flex;gap:10px;align-items:center;border-bottom:1px solid #fde2ea;padding:10px 0}
.cart-item img{width:50px;height:50px;object-fit:contain}
.qty{display:flex;align-items:center;gap:8px;margin-left:auto}
.qty button{width:26px;height:26px;border:1px solid #f3c2d1;background:#fff;border-radius:50%;cursor:pointer}
.form input, .form textarea{width:100%;padding:12px;margin:6px 0;border:1px solid #f3c2d1;border-radius:10px;font-family:inherit}
.form button.submit{width:100%;background:#b03a5b;color:#fff;padding:14px;border:none;border-radius:12px;margin-top:10px;cursor:pointer;font-size:14px;letter-spacing:1px}
</style>
</head>
<body>
<div class="header">
<h1>SAYNI IMPORTADOS</h1>
<p>VICTORIA'S SECRET & KARSEELL ORIGINALES</p>
</div>

<div class="filters">
<button class="active" data-filter="all">Todos</button>
<button data-filter="clasicos">Clásicos $29.500</button>
<button data-filter="shimmer">Shimmer $30.000</button>
<button data-filter="limitada">Ed. Limitada $32.000</button>
<button data-filter="karseell">Karseell</button>
</div>

<div class="grid" id="grid"></div>

<button class="cart-btn" onclick="openCart()">🛒<span class="cart-count" id="cartCount">0</span></button>

<div id="cartModal" onclick="if(event.target==this)closeCart()">
<div class="cart-panel">
<h3 style="font-family:'Cormorant Garamond';font-size:26px;margin-bottom:15px">Tu Carrito</h3>
<div id="cartItems" style="flex:1"></div>
<div id="cartTotal" style="font-weight:600;margin:15px 0;font-size:18px"></div>

<form class="form" action="https://formsubmit.co/naylaeroldan@icloud.com" method="POST" onsubmit="return prepareOrder()">
<input type="hidden" name="_subject" value="Nuevo pedido - SAYNI IMPORTADOS">
<input type="hidden" name="_captcha" value="false">
<input type="hidden" name="_template" value="table">
<input type="hidden" name="pedido" id="pedidoField">
<input type="hidden" name="_next" value="https://gracias.html">

<input type="text" name="nombre" placeholder="Nombre y apellido" required>
<input type="tel" name="telefono" placeholder="WhatsApp / Teléfono" required>
<input type="text" name="direccion" placeholder="Dirección + Localidad" required>
<textarea name="nota" placeholder="Nota (ej: horario de entrega)"></textarea>

<button type="submit" class="submit">FINALIZAR PEDIDO POR MAIL</button>
<p style="font-size:11px;text-align:center;margin-top:10px;color:#999">Te llegará a naylaeroldan@icloud.com</p>
</form>
<button onclick="closeCart()" style="margin-top:10px;background:none;border:none;color:#999;cursor:pointer">Seguir comprando</button>
</div>
</div>

<script>
const products=[
{name:"Velvet Petals",cat:"clasicos",price:29500,img:"images/velvet-petals.jpg"},
{name:"Midnight Bloom",cat:"clasicos",price:29500,img:"images/midnight-bloom.jpg"},
{name:"Bare Vanilla",cat:"clasicos",price:29500,img:"images/bare-vanilla.jpg"},
{name:"Temptation",cat:"clasicos",price:29500,img:"images/temptation.jpg"},
{name:"Aqua Kiss",cat:"clasicos",price:29500,img:"images/aqua-kiss.jpg"},
{name:"Pure Seduction",cat:"clasicos",price:29500,img:"images/pure-seduction.jpg"},
{name:"Love Spell",cat:"clasicos",price:29500,img:"images/love-spell.jpg"},
{name:"Coconut Passion",cat:"clasicos",price:29500,img:"images/coconut-passion.jpg"},

{name:"Velvet Petals Shimmer",cat:"shimmer",price:30000,img:"images/velvet-petals-shimmer.jpg"},
{name:"Aqua Kiss Shimmer",cat:"shimmer",price:30000,img:"images/aqua-kiss-shimmer.jpg"},
{name:"Coconut Passion Shimmer",cat:"shimmer",price:30000,img:"images/coconut-passion-shimmer.jpg"},
{name:"Bare Vanilla Shimmer",cat:"shimmer",price:30000,img:"images/bare-vanilla-shimmer.jpg"},
{name:"Temptation Shimmer",cat:"shimmer",price:30000,img:"images/temptation-shimmer.jpg"},
{name:"Midnight Bloom Shimmer",cat:"shimmer",price:30000,img:"images/midnight-bloom-shimmer.jpg"},
{name:"Love Spell Shimmer",cat:"shimmer",price:30000,img:"images/love-spell-shimmer.jpg"},
{name:"Pure Seduction Shimmer",cat:"shimmer",price:30000,img:"images/pure-seduction-shimmer.jpg"},

{name:"Seashell Shimmer",cat:"limitada",price:32000,img:"images/seashell-shimmer.jpg"},
{name:"Tidal Shimmer",cat:"limitada",price:32000,img:"images/tidal-shimmer.jpg"},
{name:"Beach Shimmer",cat:"limitada",price:32000,img:"images/beach-shimmer.jpg"},
{name:"Bikini Shimmer",cat:"limitada",price:32000,img:"images/bikini-shimmer.jpg"},
{name:"Cherry Milkshake",cat:"limitada",price:32000,img:"images/cherry-milkshake.jpg"},
{name:"Cherry Bite",cat:"limitada",price:32000,img:"images/cherry-bite.jpg"},
{name:"Forbidden Cherry",cat:"limitada",price:32000,img:"images/forbidden-cherry.jpg"},
{name:"Merry Delights",cat:"limitada",price:32000,img:"images/merry-delights.jpg"},
{name:"Midnight Magic",cat:"limitada",price:32000,img:"images/midnight-magic.jpg"},
{name:"Radiant Wings Shimmer",cat:"limitada",price:32000,img:"images/radiant-wings.jpg"},
{name:"Runway Pose Shimmer",cat:"limitada",price:32000,img:"images/runway-pose.jpg"},
{name:"Sundrenched Blooms",cat:"limitada",price:32000,img:"images/sundrenched-blooms.jpg"},
{name:"Iconic Glam Shimmer",cat:"limitada",price:32000,img:"images/iconic-glam.jpg"},
{name:"Vanilla Rebel",cat:"limitada",price:32000,img:"images/vanilla-rebel.jpg"},
{name:"Love Spell Brûlée",cat:"limitada",price:32000,img:"images/love-spell-brulee.jpg"},
{name:"Love Spell Bliss",cat:"limitada",price:32000,img:"images/love-spell-bliss.jpg"},
{name:"Canyon Blooms",cat:"limitada",price:32000,img:"images/canyon-blooms.jpg"},

{name:"Karseell Aceite 50ml",cat:"karseell",price:20000,img:"images/karseell-aceite.jpg"},
{name:"Karseell Mascarilla 500ml",cat:"karseell",price:20000,img:"images/karseell-mascarilla.jpg"},
{name:"Kit Karseell (Mascarilla + Aceite)",cat:"karseell",price:37500,img:"images/karseell-kit.jpg"},
];

let cart=[];
const grid=document.getElementById('grid');
function render(filter='all'){
grid.innerHTML='';
products.filter(p=> filter=='all' || p.cat==filter).forEach((p,i)=>{
let idx=products.indexOf(p);
grid.innerHTML+=`
<div class="card">
<img src="${p.img}" onerror="this.src='https://via.placeholder.com/200x300?text=${encodeURIComponent(p.name)}'">
<h3>${p.name}</h3>
<div class="price">$${p.price.toLocaleString('es-AR')}</div>
<button onclick="addToCart(${idx})">Agregar al carrito</button>
</div>`;
});
}
render();
document.querySelectorAll('.filters button').forEach(b=>{
b.onclick=()=>{
document.querySelectorAll('.filters button').forEach(x=>x.classList.remove('active'));
b.classList.add('active');
render(b.dataset.filter);
}
});

function addToCart(idx){
let item=cart.find(c=>c.idx==idx);
if(item) item.q++;
else cart.push({idx,q:1});
updateCart();
openCart();
}
function updateCart(){
document.getElementById('cartCount').innerText=cart.reduce((a,c)=>a+c.q,0);
let html=''; let total=0;
cart.forEach(c=>{
let p=products[c.idx];
total+=p.price*c.q;
html+=`<div class="cart-item">
<img src="${p.img}">
<div><div style="font-size:13px">${p.name}</div><div style="font-size:12px;color:#b03a5b">$${p.price.toLocaleString('es-AR')}</div></div>
<div class="qty"><button onclick="changeQty(${c.idx},-1)">-</button><span>${c.q}</span><button onclick="changeQty(${c.idx},1)">+</button></div>
</div>`;
});
document.getElementById('cartItems').innerHTML=html||'<p style="color:#999;text-align:center;margin-top:20px">Carrito vacío</p>';
document.getElementById('cartTotal').innerText= total?`Total: $${total.toLocaleString('es-AR')}`:'';
}
function changeQty(idx,d){
let c=cart.find(x=>x.idx==idx);
c.q+=d;
if(c.q<=0) cart=cart.filter(x=>x.idx!=idx);
updateCart();
}
function openCart(){document.getElementById('cartModal').classList.add('open')}
function closeCart(){document.getElementById('cartModal').classList.remove('open')}
function prepareOrder(){
if(cart.length==0){alert('Carrito vacío');return false;}
let detalle=cart.map(c=>`${products[c.idx].name} x${c.q} - $${(products[c.idx].price*c.q).toLocaleString('es-AR')}`).join('\n');
let total=cart.reduce((a,c)=>a+products[c.idx].price*c.q,0);
document.getElementById('pedidoField').value= detalle + `\n\nTOTAL: $${total.toLocaleString('es-AR')}`;
return true;
}
</script>
</body>
</html>
