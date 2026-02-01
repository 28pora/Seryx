<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ABB Crêpes</title>

<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
/* ====== STYLE ORIGINAL ABB CRÊPES (INCHANGÉ) ====== */
*{margin:0;padding:0;box-sizing:border-box}
:root{
 --bg:#0a0a0f;
 --card:rgba(20,15,35,.9);
 --purple:#8b5cf6;
 --purple-dark:#6d28d9;
 --green:#10b981;
 --orange:#f59e0b;
 --red:#ef4444;
 --text:#f1f5f9;
 --text2:#94a3b8;
 --border:rgba(139,92,246,.2);
}
body{
 font-family:'Rajdhani',sans-serif;
 background:var(--bg);
 color:var(--text);
 min-height:100vh;
}
.login-overlay{
 position:fixed;inset:0;
 background:rgba(0,0,0,.95);
 display:flex;
 align-items:center;
 justify-content:center;
 z-index:9999;
}
.login-box{
 background:var(--card);
 padding:40px;
 width:380px;
 border-radius:18px;
 text-align:center;
 border:1px solid var(--border);
}
.login-box h1{
 font-family:'Orbitron',sans-serif;
 margin-bottom:10px;
}
.login-tabs{
 display:flex;
 gap:10px;
 margin:15px 0;
}
.login-tab{
 flex:1;
 padding:10px;
 border-radius:10px;
 border:1px solid var(--border);
 background:transparent;
 color:var(--text2);
 cursor:pointer;
 font-weight:600;
}
.login-tab.active{
 background:linear-gradient(135deg,var(--purple),var(--purple-dark));
 color:#fff;
}
.login-box input,select{
 width:100%;
 padding:14px;
 margin-top:10px;
 background:#0a0a15;
 border:1px solid var(--border);
 border-radius:10px;
 color:#fff;
}
.login-box button{
 margin-top:15px;
 width:100%;
 padding:14px;
 border:none;
 border-radius:10px;
 background:linear-gradient(135deg,var(--purple),var(--purple-dark));
 color:#fff;
 font-family:'Orbitron',sans-serif;
 cursor:pointer;
}
.login-error{
 margin-top:10px;
 color:var(--red);
 display:none;
}
.app{display:none}
header{
 background:var(--card);
 padding:15px 20px;
 display:flex;
 justify-content:space-between;
 align-items:center;
 border-bottom:1px solid var(--border);
}
.sidebar{
 width:240px;
 background:var(--card);
 padding:15px;
 border-right:1px solid var(--border);
}
.nav-item{
 padding:12px;
 border-radius:8px;
 cursor:pointer;
 color:var(--text2);
}
.nav-item.active{
 background:rgba(139,92,246,.15);
 color:#fff;
}
.main{
 flex:1;
 padding:20px;
}
.layout{
 display:flex;
 min-height:calc(100vh - 70px);
}
.section{
 background:var(--card);
 border:1px solid var(--border);
 border-radius:14px;
 margin-bottom:20px;
}
.section-header{
 padding:15px 20px;
 border-bottom:1px solid var(--border);
 font-family:'Orbitron',sans-serif;
}
.section-body{
 padding:20px;
}
.btn{
 padding:10px 16px;
 border:none;
 border-radius:8px;
 cursor:pointer;
 font-weight:600;
}
.btn-primary{
 background:linear-gradient(135deg,var(--purple),var(--purple-dark));
 color:#fff;
}
.item{
 padding:12px;
 border-bottom:1px solid var(--border);
}
.item:last-child{border-bottom:none}
.badge{
 padding:4px 10px;
 border-radius:20px;
 font-size:12px;
}
.online{background:rgba(16,185,129,.2);color:var(--green)}
.offline{background:rgba(100,116,139,.2);color:var(--text2)}
</style>
</head>

<body>

<!-- LOGIN -->
<div class="login-overlay" id="loginOverlay">
 <div class="login-box">
  <h1>🥞 ABB CRÊPES</h1>

  <div class="login-tabs">
   <button class="login-tab active" onclick="setMode('admin')">Admin</button>
   <button class="login-tab" onclick="setMode('livreur')">Livreur</button>
  </div>

  <select id="livreurSelect" style="display:none"></select>
  <input type="password" id="password" placeholder="Mot de passe">
  <button onclick="login()">Connexion</button>
  <div class="login-error" id="loginError">Erreur</div>
 </div>
</div>

<!-- APP -->
<div class="app" id="app">
<header>
 <strong id="userTitle">ADMIN</strong>
 <button class="btn btn-primary" onclick="logout()">Déconnexion</button>
</header>

<div class="layout">
 <div class="sidebar">
  <div class="nav-item active" onclick="show('dashboard')">📊 Dashboard</div>
  <div class="nav-item" onclick="show('livreurs')">🚴 Livreurs</div>
 </div>

 <div class="main" id="main"></div>
</div>
</div>

<script>
/* ====== DONNÉES VIDES (IMPORTANT) ====== */
const ADMIN_PASS="admin";
const LIVREUR_PASS="livreur";

let mode="admin";
let currentUser=null;

let data={
 livreurs:[],
 settings:{adminName:"Admin"}
};

/* ====== LOGIN ====== */
function setMode(m){
 mode=m;
 document.querySelectorAll(".login-tab").forEach(b=>b.classList.remove("active"));
 event.target.classList.add("active");
 livreurSelect.style.display = m==="livreur"?"block":"none";
 populateLivreurs();
}

function populateLivreurs(){
 if(data.livreurs.length===0){
  livreurSelect.innerHTML="<option>Aucun livreur</option>";
  return;
 }
 livreurSelect.innerHTML=data.livreurs
  .map(l=>`<option value="${l.id}">${l.name}</option>`)
  .join("");
}

function login(){
 loginError.style.display="none";

 if(mode==="admin"){
  if(password.value!==ADMIN_PASS){
   loginError.textContent="Mot de passe incorrect";
   loginError.style.display="block";
   return;
  }
  currentUser={type:"admin"};
 }
 else{
  if(data.livreurs.length===0){
   loginError.textContent="Aucun livreur créé";
   loginError.style.display="block";
   return;
  }
  if(password.value!==LIVREUR_PASS){
   loginError.textContent="Mot de passe incorrect";
   loginError.style.display="block";
   return;
  }
  const id=+livreurSelect.value;
  currentUser={type:"livreur",id};
 }

 loginOverlay.style.display="none";
 app.style.display="block";
 show("dashboard");
}

/* ====== NAV ====== */
function show(view){
 document.querySelectorAll(".nav-item").forEach(n=>n.classList.remove("active"));
 event.target?.classList.add("active");

 if(view==="dashboard")renderDashboard();
 if(view==="livreurs")renderLivreurs();
}

/* ====== DASHBOARD ====== */
function renderDashboard(){
 main.innerHTML=`
 <div class="section">
  <div class="section-header">📊 Dashboard</div>
  <div class="section-body">
   Livreurs : ${data.livreurs.length}
  </div>
 </div>`;
}

/* ====== LIVREURS ====== */
function renderLivreurs(){
 if(currentUser.type!=="admin"){renderDashboard();return;}

 main.innerHTML=`
 <div class="section">
  <div class="section-header">🚴 Livreurs</div>
  <div class="section-body">
   <input id="lname" placeholder="Nom du livreur">
   <button class="btn btn-primary" onclick="addLivreur()">Ajouter</button>
  </div>
 </div>
 ${data.livreurs.map(l=>`
  <div class="section">
   <div class="section-body item">
    ${l.name}
    <span class="badge ${l.status}">${l.status}</span>
   </div>
  </div>
 `).join("")}
 `;
}

function addLivreur(){
 const name=lname.value.trim();
 if(!name)return;
 data.livreurs.push({id:Date.now(),name,status:"offline"});
 lname.value="";
 populateLivreurs();
 renderLivreurs();
}

/* ====== LOGOUT ====== */
function logout(){
 location.reload();
}
</script>

</body>
</html>
