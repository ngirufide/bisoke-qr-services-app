<!DOCTYPE html>
<html lang="rw">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BISOKE ICT SOLUTION CENTER</title>
<style>
  :root{
    --navy:#152238;
    --navy-2:#1F3358;
    --amber:#E8A33D;
    --cream:#F7F5EF;
    --ink:#1A1A1A;
    --muted:#6B6B63;
    --line:#E3E0D4;
    --green:#2F8F5B;
    --danger:#C0392B;
    --pending:#B87A1F;
  }
  *{box-sizing:border-box;}
  body{margin:0;font-family:'Segoe UI',system-ui,-apple-system,sans-serif;background:var(--cream);color:var(--ink);}
  header{background:var(--navy);color:#fff;padding:22px 20px 16px;text-align:center;}
  header .mark{display:inline-flex;align-items:center;justify-content:center;width:46px;height:46px;border-radius:12px;background:var(--amber);color:var(--navy);font-weight:700;font-size:18px;margin-bottom:8px;}
  header h1{margin:0;font-size:19px;}
  header p{margin:4px 0 0;font-size:12.5px;color:#C9D2E3;}
  .tabs{display:flex;background:var(--navy-2);}
  .tabs button{flex:1;padding:12px;background:none;border:none;color:#B9C2D6;font-weight:600;font-size:13.5px;cursor:pointer;}
  .tabs button.active{color:#fff;border-bottom:3px solid var(--amber);}
  .tabs button{position:relative;}
  .badge{position:absolute;top:6px;right:24%;background:var(--danger);color:#fff;font-size:10px;font-weight:700;min-width:16px;height:16px;border-radius:8px;display:none;align-items:center;justify-content:center;padding:0 4px;}
  .section-toggle{display:flex;gap:8px;margin-bottom:10px;}
  .section-toggle button{flex:1;padding:8px;border-radius:8px;border:1px solid var(--line);background:#fff;font-size:12.5px;cursor:pointer;color:var(--muted);}
  .section-toggle button.active{background:var(--navy);color:#fff;border-color:var(--navy);}
  .order-card.new-order{border-color:var(--amber);box-shadow:0 0 0 1px var(--amber);}
  main{max-width:520px;margin:0 auto;padding:16px 16px 140px;}
  .view{display:none;}
  .view.active{display:block;}
  .section-title{font-size:12.5px;text-transform:uppercase;letter-spacing:0.5px;color:var(--muted);margin:18px 0 10px;}
  .service{background:#fff;border:1px solid var(--line);border-radius:12px;padding:14px;margin-bottom:10px;}
  .service h3{margin:0 0 3px;font-size:15px;}
  .service p{margin:0;font-size:12.5px;color:var(--muted);}
  .service-top{display:flex;justify-content:space-between;align-items:flex-start;}
  .price{font-size:14px;font-weight:600;color:var(--navy-2);white-space:nowrap;}
  .qty{display:flex;align-items:center;gap:8px;margin-top:10px;}
  .qty button{width:30px;height:30px;border-radius:8px;border:1px solid var(--line);background:var(--cream);font-size:16px;cursor:pointer;}
  .qty span{min-width:20px;text-align:center;font-weight:600;}
  #cartbar{position:fixed;bottom:0;left:0;right:0;background:var(--navy);color:#fff;padding:14px 16px;display:flex;justify-content:space-between;align-items:center;gap:12px;}
  #cartbar .total-label{font-size:11px;color:#B9C2D6;}
  #cartbar .total-amount{font-size:18px;font-weight:700;}
  #cartbar button{background:var(--amber);color:var(--navy);border:none;padding:12px 18px;border-radius:10px;font-weight:700;font-size:14px;cursor:pointer;}
  #cartbar button:disabled{opacity:0.5;cursor:not-allowed;}
  #overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.5);z-index:10;align-items:flex-end;}
  #sheet{background:#fff;width:100%;border-radius:16px 16px 0 0;padding:20px 18px 24px;max-height:88vh;overflow-y:auto;}
  #sheet h2{margin:0 0 4px;font-size:17px;}
  .ref{font-size:12.5px;color:var(--muted);margin-bottom:14px;}
  .order-line{display:flex;justify-content:space-between;font-size:13.5px;padding:5px 0;border-bottom:1px dashed var(--line);}
  .pay-box{background:var(--cream);border:1px solid var(--line);border-radius:12px;padding:13px;margin-top:14px;}
  .pay-box .method{display:flex;justify-content:space-between;font-size:13.5px;margin-bottom:6px;}
  .pay-box .method b{color:var(--navy-2);}
  .field{margin-top:12px;}
  .field label{display:block;font-size:12.5px;color:var(--muted);margin-bottom:4px;}
  .field input,.field select{width:100%;padding:10px;border:1px solid var(--line);border-radius:8px;font-size:14px;}
  .note{font-size:11.5px;color:var(--muted);margin-top:8px;line-height:1.5;}
  #sheet .btn{width:100%;padding:12px;border-radius:10px;border:none;font-weight:700;font-size:14px;margin-top:12px;cursor:pointer;}
  .btn-primary{background:var(--green);color:#fff;}
  .btn-secondary{background:#EFEDE4;color:var(--ink);}
  .error{color:var(--danger);font-size:12px;margin-top:4px;display:none;}
  #done{display:none;text-align:center;padding:6px 0;}
  #done .check{width:52px;height:52px;border-radius:50%;background:var(--green);color:#fff;font-size:26px;display:flex;align-items:center;justify-content:center;margin:0 auto 12px;}
  .order-card{background:#fff;border:1px solid var(--line);border-radius:12px;padding:13px;margin-bottom:10px;}
  .order-card .top{display:flex;justify-content:space-between;align-items:center;margin-bottom:6px;}
  .order-card .top b{font-size:14px;}
  .status{font-size:11px;font-weight:700;padding:3px 9px;border-radius:20px;text-transform:uppercase;}
  .status.pending{background:#FBEED9;color:var(--pending);}
  .status.confirmed{background:#DDF0E4;color:var(--green);}
  .order-card .lines{font-size:12.5px;color:var(--muted);margin:6px 0;}
  .order-card .meta{font-size:12px;color:var(--muted);}
  .order-card .actions{margin-top:8px;}
  .order-card .actions button{width:100%;padding:9px;border-radius:8px;border:none;background:var(--green);color:#fff;font-weight:700;font-size:13px;cursor:pointer;}
  .stats{display:flex;gap:10px;margin-bottom:16px;}
  .stat{flex:1;background:#fff;border:1px solid var(--line);border-radius:12px;padding:12px;text-align:center;}
  .stat .n{font-size:18px;font-weight:700;color:var(--navy-2);}
  .stat .l{font-size:11px;color:var(--muted);margin-top:2px;}
  .lock{text-align:center;padding:60px 20px;}
  .lock input{width:100%;padding:12px;border:1px solid var(--line);border-radius:8px;font-size:15px;text-align:center;margin:14px 0;}
  .lock button{width:100%;padding:12px;border-radius:10px;border:none;background:var(--navy);color:#fff;font-weight:700;cursor:pointer;}
  .empty{text-align:center;color:var(--muted);font-size:13.5px;padding:30px 0;}
</style>
</head>
<body>

<header>
  <div class="mark">B</div>
  <h1>BISOKE ICT SOLUTION CENTER</h1>
  <p>Serivisi za mudasobwa &middot; Ifoto &middot; Impapuro</p>
</header>

<div class="tabs">
  <button id="tab-customer" class="active" onclick="switchTab('customer')">Umukiriya</button>
  <button id="tab-admin" onclick="switchTab('admin')">Admin<span class="badge" id="admin-badge">0</span></button>
</div>

<main>
  <div id="view-customer" class="view active">
    <div class="section-title">Hitamo serivisi ukeneye</div>
    <div id="service-list"></div>
  </div>

  <div id="view-admin" class="view">
    <div id="admin-lock" class="lock">
      <p style="color:var(--muted);font-size:14px;">Injiza ijambo ry'ibanga ry'admin</p>
      <input type="password" id="admin-pass" placeholder="Ijambo ry'ibanga">
      <p class="error" id="admin-error">Ijambo ry'ibanga ntabwo ari ryo.</p>
      <button onclick="checkAdminPass()">Injira</button>
    </div>
    <div id="admin-content" style="display:none;">
      <div class="stats" style="flex-wrap:wrap;">
        <div class="stat" style="min-width:45%;"><div class="n" id="stat-revenue">0</div><div class="l">Ibyacuruzwe (Rwf)</div></div>
        <div class="stat" style="min-width:45%;"><div class="n" id="stat-expenses">0</div><div class="l">Ibyaranguwe (Rwf)</div></div>
        <div class="stat" style="min-width:45%;"><div class="n" id="stat-pending-amount">0</div><div class="l">Ibisigaye (Rwf)</div></div>
        <div class="stat" style="min-width:45%;"><div class="n" id="stat-profit">0</div><div class="l">Inyungu (Rwf)</div></div>
      </div>

      <div class="section-title">Ibyaranguwe (Amafaranga yakoreshejwe)</div>
      <div class="order-card">
        <div class="field">
          <label>Icyaguzwe (urugero: Ipapuro, Ink)</label>
          <input type="text" id="exp-desc" placeholder="Icyo waguze">
        </div>
        <div class="field">
          <label>Amafaranga (Rwf)</label>
          <input type="number" id="exp-amount" placeholder="0">
        </div>
        <p class="error" id="exp-error">Uzuza icyaguzwe n'amafaranga.</p>
        <button class="btn btn-primary" style="margin-top:10px;" onclick="addExpense()">Ongeraho</button>
      </div>
      <div id="expenses-list"></div>

      <div class="section-title">Orders</div>
      <div class="section-toggle">
        <button id="filter-today" class="active" onclick="setFilter('today')">Uyu munsi</button>
        <button id="filter-all" onclick="setFilter('all')">Byose</button>
      </div>
      <div id="orders-list"></div>
    </div>
  </div>
</main>

<div id="cartbar" style="display:none;">
  <div>
    <div class="total-label">Amafaranga yose</div>
    <div class="total-amount" id="total-amount">0 Rwf</div>
  </div>
  <button id="order-btn" disabled onclick="openSheet()">Emeza order</button>
</div>

<div id="overlay">
  <div id="sheet">
    <div id="order-view">
      <h2>Emeza order yawe</h2>
      <div class="ref" id="order-ref"></div>
      <div id="order-lines"></div>
      <div class="pay-box">
        <div class="method"><span>Uburyo bwo kwishyura</span></div>
        <div class="field">
          <select id="pay-method" onchange="renderPayCode()">
            <option value="mtn">MTN Mobile Money</option>
            <option value="airtel">Airtel Money</option>
          </select>
        </div>
        <div class="method" style="margin-top:10px;"><span>Merchant code</span><b id="pay-code">---</b></div>
        <p class="note">Kanda *182*8*1# (MTN) cyangwa *500# (Airtel), wandike iyo code n'amafaranga yose, hanyuma wishyure. Nyuma yo kwishyura, wandike numero ya terefone yawe na transaction ID yagaragaye kuri SMS, hanyuma wemeze hasi.</p>
        <div class="field">
          <label>Numero ya terefone yawe</label>
          <input type="text" id="cust-phone" placeholder="Urugero: 0788123456">
          <p class="error" id="err-phone">Andika numero ya terefone.</p>
        </div>
        <div class="field">
          <label>Transaction ID (kuri SMS wabonye)</label>
          <input type="text" id="cust-txn" placeholder="Urugero: MP240911.1234.A56789">
          <p class="error" id="err-txn">Andika transaction ID.</p>
        </div>
      </div>
      <button class="btn btn-primary" onclick="submitOrder()">Nishyuye - Ohereza order</button>
      <button class="btn btn-secondary" onclick="closeSheet()">Subira inyuma</button>
    </div>
    <div id="done">
      <div class="check">&#10003;</div>
      <h2>Order yawe yakiriwe</h2>
      <p style="color:var(--muted);font-size:14px;">Umukozi azemeza ubwishyu bwawe vuba. Murakoze!</p>
      <button class="btn btn-secondary" onclick="resetAll()">Funga</button>
    </div>
  </div>
</div>

<script>
const SERVICES = [
  {id:1, name:"Service za MTN Mobile Money", desc:"Serivisi", price:100},
  {id:2, name:"Service z'Irembo", desc:"Guhera kuri 500 Rwf", price:500},
  {id:3, name:"Gufotora amafoto magufi y'akokanya", desc:"Ifoto", price:500},
  {id:4, name:"Kohereza ibirego mu nkiko (IECM)", desc:"Buri kirego", price:5000},
  {id:5, name:"Gufasha kugura copy z'urubanza", desc:"Serivisi", price:2000},
  {id:6, name:"Gufasha guteza cash ndangizarubanza", desc:"Serivisi", price:2000},
  {id:7, name:"Gukora invitation na business card", desc:"Buri invitation/card", price:500},
  {id:8, name:"Dactylography", desc:"Buri paji", price:500},
  {id:9, name:"Gufotora impapuro", desc:"Buri paji", price:100},
  {id:10, name:"Gusikana", desc:"Buri paji", price:200},
  {id:11, name:"Gutegura imishinga (bank/umuterankunga)", desc:"Buri mushinga", price:15000},
  {id:12, name:"Kumenyekanisha imisoro", desc:"Uhereye kuri", price:1000},
  {id:13, name:"Kumenyekanisha imitungo (ODAS system)", desc:"Serivisi", price:5000},
  {id:14, name:"Kureba amakuru ku byangombwa by'ubutaka", desc:"Guhera kuri 500 Rwf", price:500},
  {id:15, name:"Kwishyura amazi", desc:"Serivisi", price:500},
  {id:16, name:"Gufasha gusaba guhabwa amazi", desc:"Serivisi", price:1000},
  {id:17, name:"Kugurisha umuriro", desc:"Serivisi", price:500},
  {id:18, name:"Gufasha gusaba akazi kuri MIFOTRA no gukora konti", desc:"Serivisi", price:1000},
  {id:19, name:"Guhugura ku serivisi za online (mudasobwa)", desc:"Ukwezi kumwe", price:50000},
  {id:20, name:"Guhugura ku icungamutungo (QUICKBOOK n'izindi)", desc:"Ukwezi kumwe", price:50000},
  {id:21, name:"Kwigisha Word, Excel, PowerPoint na Internet Explorer", desc:"Amasomo", price:40000},
  {id:22, name:"Service za BK na Equity Bank", desc:"Charge za banki (bitandukanye)", price:0},
];
const MTN_CODE = "---";
const AIRTEL_CODE = "198735";
const ADMIN_PASSWORD = "Bisoke2026";

let cart = {};
let currentOrder = null;
let orderFilter = 'today';
let knownOrderKeys = new Set();
let adminUnlocked = false;
let pollTimer = null;

function isToday(ts){
  const d = new Date(ts);
  const now = new Date();
  return d.getFullYear()===now.getFullYear() && d.getMonth()===now.getMonth() && d.getDate()===now.getDate();
}

function beep(){
  try{
    const ctx = new (window.AudioContext || window.webkitAudioContext)();
    const osc = ctx.createOscillator();
    const gain = ctx.createGain();
    osc.connect(gain); gain.connect(ctx.destination);
    osc.frequency.value = 880;
    gain.gain.value = 0.1;
    osc.start();
    setTimeout(()=>{ osc.stop(); ctx.close(); }, 220);
  }catch(e){}
}

function setFilter(f){
  orderFilter = f;
  document.getElementById('filter-today').classList.toggle('active', f==='today');
  document.getElementById('filter-all').classList.toggle('active', f==='all');
  loadOrders(false);
}

function fmt(n){ return Math.round(n).toLocaleString('en-US') + " Rwf"; }

function switchTab(tab){
  document.getElementById('view-customer').classList.toggle('active', tab==='customer');
  document.getElementById('view-admin').classList.toggle('active', tab==='admin');
  document.getElementById('tab-customer').classList.toggle('active', tab==='customer');
  document.getElementById('tab-admin').classList.toggle('active', tab==='admin');
  document.getElementById('cartbar').style.display = tab==='customer' ? 'flex' : 'none';
  if(tab==='admin' && document.getElementById('admin-content').style.display !== 'none'){
    loadOrders();
  }
}

function startPolling(){
  if(pollTimer) return;
  pollTimer = setInterval(()=>{ pollForNewOrders(); }, 15000);
}

async function pollForNewOrders(){
  try{
    const result = await window.storage.list('order:', true);
    const keys = (result && result.keys) ? result.keys : [];
    const newOnes = keys.filter(k=>!knownOrderKeys.has(k));
    if(newOnes.length > 0 && knownOrderKeys.size > 0){
      beep();
    }
    keys.forEach(k=>knownOrderKeys.add(k));
    updateBadgeCount();
    if(document.getElementById('view-admin').classList.contains('active') && adminUnlocked){
      loadOrders(false);
    }
  }catch(e){}
}

async function updateBadgeCount(){
  try{
    const result = await window.storage.list('order:', true);
    const keys = (result && result.keys) ? result.keys : [];
    let pendingCount = 0;
    for(const k of keys){
      try{
        const r = await window.storage.get(k, true);
        if(r && r.value){
          const o = JSON.parse(r.value);
          if(o.status === 'pending') pendingCount++;
        }
      }catch(e){}
    }
    const badge = document.getElementById('admin-badge');
    if(pendingCount > 0){
      badge.textContent = pendingCount;
      badge.style.display = 'flex';
    } else {
      badge.style.display = 'none';
    }
  }catch(e){}
}

function renderServices(){
  const list = document.getElementById('service-list');
  list.innerHTML = "";
  SERVICES.forEach(s=>{
    const qty = cart[s.id] || 0;
    const div = document.createElement('div');
    div.className = "service";
    div.innerHTML = `
      <div class="service-top">
        <div><h3>${s.name}</h3><p>${s.desc}</p></div>
        <div class="price">${fmt(s.price)}</div>
      </div>
      <div class="qty">
        <button onclick="changeQty(${s.id},-1)">-</button>
        <span>${qty}</span>
        <button onclick="changeQty(${s.id},1)">+</button>
      </div>`;
    list.appendChild(div);
  });
  updateTotal();
}

function changeQty(id, delta){
  const current = cart[id] || 0;
  cart[id] = Math.max(0, current + delta);
  renderServices();
}

function updateTotal(){
  let total = 0;
  Object.keys(cart).forEach(id=>{
    const s = SERVICES.find(x=>x.id==id);
    total += (cart[id]||0) * s.price;
  });
  document.getElementById('total-amount').textContent = fmt(total);
  document.getElementById('order-btn').disabled = !Object.values(cart).some(q=>q>0);
}

function renderPayCode(){
  const method = document.getElementById('pay-method').value;
  document.getElementById('pay-code').textContent = method==='mtn' ? MTN_CODE : AIRTEL_CODE;
}

function openSheet(){
  document.getElementById('order-view').style.display = 'block';
  document.getElementById('done').style.display = 'none';
  document.getElementById('overlay').style.display = 'flex';
  document.getElementById('cust-phone').value = '';
  document.getElementById('cust-txn').value = '';
  document.getElementById('err-phone').style.display = 'none';
  document.getElementById('err-txn').style.display = 'none';

  const ref = "ORD-" + Date.now().toString().slice(-6);
  document.getElementById('order-ref').textContent = "Order No: " + ref;

  const linesDiv = document.getElementById('order-lines');
  linesDiv.innerHTML = "";
  let total = 0;
  const items = [];
  Object.keys(cart).forEach(id=>{
    const qty = cart[id];
    if(qty>0){
      const s = SERVICES.find(x=>x.id==id);
      const lineTotal = qty*s.price;
      total += lineTotal;
      items.push({name:s.name, qty, price:s.price, lineTotal});
      const line = document.createElement('div');
      line.className = "order-line";
      line.innerHTML = `<span>${s.name} x${qty}</span><span>${fmt(lineTotal)}</span>`;
      linesDiv.appendChild(line);
    }
  });
  const totalLine = document.createElement('div');
  totalLine.className = "order-line";
  totalLine.style.fontWeight = "700";
  totalLine.innerHTML = `<span>Amafaranga yose</span><span>${fmt(total)}</span>`;
  linesDiv.appendChild(totalLine);

  currentOrder = {ref, items, total, createdAt: Date.now()};
  renderPayCode();
}

function closeSheet(){
  document.getElementById('overlay').style.display = 'none';
}

async function submitOrder(){
  const phone = document.getElementById('cust-phone').value.trim();
  const txn = document.getElementById('cust-txn').value.trim();
  let ok = true;
  if(!phone){ document.getElementById('err-phone').style.display='block'; ok=false; } else { document.getElementById('err-phone').style.display='none'; }
  if(!txn){ document.getElementById('err-txn').style.display='block'; ok=false; } else { document.getElementById('err-txn').style.display='none'; }
  if(!ok) return;

  const method = document.getElementById('pay-method').value;
  const order = {
    ...currentOrder,
    phone, txn, method,
    status: 'pending'
  };

  try{
    await window.storage.set('order:' + order.ref, JSON.stringify(order), true);
    document.getElementById('order-view').style.display = 'none';
    document.getElementById('done').style.display = 'block';
  }catch(e){
    alert("Ntibyakunze kohereza order. Ongera ugerageze.");
  }
}

function resetAll(){
  cart = {};
  renderServices();
  closeSheet();
}

function checkAdminPass(){
  const val = document.getElementById('admin-pass').value;
  if(val === ADMIN_PASSWORD){
    adminUnlocked = true;
    document.getElementById('admin-lock').style.display = 'none';
    document.getElementById('admin-content').style.display = 'block';
    loadExpenses().then(()=>loadOrders());
    startPolling();
  } else {
    document.getElementById('admin-error').style.display = 'block';
  }
}

async function loadOrders(showLoading){
  const listDiv = document.getElementById('orders-list');
  if(showLoading !== false){
    listDiv.innerHTML = '<p class="empty">Turimo gushakisha orders...</p>';
  }
  try{
    const result = await window.storage.list('order:', true);
    const keys = (result && result.keys) ? result.keys : [];
    keys.forEach(k=>knownOrderKeys.add(k));
    if(keys.length === 0){
      listDiv.innerHTML = '<p class="empty">Nta order irahaba.</p>';
      updateStats([]);
      updateBadgeCount();
      return;
    }
    const orders = [];
    for(const k of keys){
      try{
        const r = await window.storage.get(k, true);
        if(r && r.value) orders.push(JSON.parse(r.value));
      }catch(e){}
    }
    orders.sort((a,b)=> b.createdAt - a.createdAt);
    updateStats(orders);
    const filtered = orderFilter === 'today' ? orders.filter(o=>isToday(o.createdAt)) : orders;
    if(filtered.length === 0){
      listDiv.innerHTML = '<p class="empty">Nta order iri muri iyi gice.</p>';
    } else {
      renderOrders(filtered);
    }
    updateBadgeCount();
  }catch(e){
    listDiv.innerHTML = '<p class="empty">Habaye ikibazo cyo gushakisha orders.</p>';
  }
}

let cachedExpenses = [];

function updateStats(orders){
  const confirmed = orders.filter(o=>o.status==='confirmed');
  const pending = orders.filter(o=>o.status==='pending');
  const revenue = confirmed.reduce((sum,o)=>sum+o.total,0);
  const pendingAmount = pending.reduce((sum,o)=>sum+o.total,0);
  const expensesTotal = cachedExpenses.reduce((sum,e)=>sum+e.amount,0);
  const profit = revenue - expensesTotal;
  document.getElementById('stat-revenue').textContent = Math.round(revenue).toLocaleString('en-US');
  document.getElementById('stat-expenses').textContent = Math.round(expensesTotal).toLocaleString('en-US');
  document.getElementById('stat-pending-amount').textContent = Math.round(pendingAmount).toLocaleString('en-US');
  document.getElementById('stat-profit').textContent = Math.round(profit).toLocaleString('en-US');
}

async function loadExpenses(){
  try{
    const result = await window.storage.list('expense:', true);
    const keys = (result && result.keys) ? result.keys : [];
    const expenses = [];
    for(const k of keys){
      try{
        const r = await window.storage.get(k, true);
        if(r && r.value) expenses.push(JSON.parse(r.value));
      }catch(e){}
    }
    expenses.sort((a,b)=> b.createdAt - a.createdAt);
    cachedExpenses = expenses;
    renderExpenses(expenses);
  }catch(e){
    cachedExpenses = [];
  }
}

function renderExpenses(expenses){
  const listDiv = document.getElementById('expenses-list');
  if(expenses.length === 0){
    listDiv.innerHTML = '<p class="empty">Nta cyaranguwe cyanditswe.</p>';
    return;
  }
  listDiv.innerHTML = '';
  expenses.slice(0,10).forEach(e=>{
    const row = document.createElement('div');
    row.className = 'order-line';
    row.innerHTML = `<span>${e.desc}</span><span>${fmt(e.amount)}</span>`;
    listDiv.appendChild(row);
  });
}

async function addExpense(){
  const desc = document.getElementById('exp-desc').value.trim();
  const amount = parseFloat(document.getElementById('exp-amount').value);
  if(!desc || !amount || amount <= 0){
    document.getElementById('exp-error').style.display = 'block';
    return;
  }
  document.getElementById('exp-error').style.display = 'none';
  const id = 'exp-' + Date.now();
  const expense = {desc, amount, createdAt: Date.now()};
  try{
    await window.storage.set('expense:' + id, JSON.stringify(expense), true);
    document.getElementById('exp-desc').value = '';
    document.getElementById('exp-amount').value = '';
    await loadExpenses();
    loadOrders(false);
  }catch(e){
    alert("Ntibyakunze kubika iki cyaranguwe.");
  }
}

function renderOrders(orders){
  const listDiv = document.getElementById('orders-list');
  listDiv.innerHTML = '';
  orders.forEach(o=>{
    const itemsText = o.items.map(i=>`${i.name} x${i.qty}`).join(', ');
    const methodLabel = o.method === 'mtn' ? 'MTN MoMo' : 'Airtel Money';
    const card = document.createElement('div');
    card.className = 'order-card';
    card.innerHTML = `
      <div class="top"><b>${o.ref}</b><span class="status ${o.status}">${o.status==='pending'?'Bitegereje':'Byishyuwe'}</span></div>
      <div class="lines">${itemsText}</div>
      <div class="meta">Tel: ${o.phone} &middot; ${methodLabel} &middot; Txn: ${o.txn}</div>
      <div class="meta" style="margin-top:4px;font-weight:600;color:var(--navy-2);">${fmt(o.total)}</div>
      ${o.status==='pending' ? `<div class="actions"><button onclick="confirmOrder('${o.ref}')">Emeza ko yishyuye</button></div>` : ''}
    `;
    listDiv.appendChild(card);
  });
}

async function confirmOrder(ref){
  try{
    const r = await window.storage.get('order:' + ref, true);
    if(r && r.value){
      const order = JSON.parse(r.value);
      order.status = 'confirmed';
      await window.storage.set('order:' + ref, JSON.stringify(order), true);
      loadOrders();
    }
  }catch(e){
    alert("Ntibyakunze kuvugurura order.");
  }
}

renderServices();
updateBadgeCount();
startPolling();
</script>

</body>
</html>
