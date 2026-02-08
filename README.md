djfelisbertomixmixx<!DOCTYPE html>
<html lang="pt">
<head>
<meta charset="UTF-8">
<title>AfroDelivers | Serviço de Entregas</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
  margin:0;
  font-family:'Segoe UI', Arial, sans-serif;
  background:linear-gradient(160deg,#0f2027,#203a43,#2c5364);
  color:#fff;
}
header{
  padding:30px 20px;
  text-align:center;
}
header h1{
  margin:0;
  font-size:32px;
}
header p{
  opacity:0.9;
}

.container{
  padding:15px;
  max-width:500px;
  margin:auto;
}

.grid{
  display:grid;
  grid-template-columns:1fr;
  gap:20px;
}

.card{
  background:rgba(255,255,255,0.08);
  backdrop-filter: blur(10px);
  border-radius:18px;
  padding:20px;
  box-shadow:0 10px 25px rgba(0,0,0,0.3);
}

.card h3{
  margin-top:0;
  font-size:20px;
}

input, textarea{
  width:100%;
  padding:12px;
  margin-top:10px;
  border-radius:10px;
  border:none;
  font-size:15px;
}

textarea{resize:none;}

button{
  width:100%;
  padding:14px;
  margin-top:15px;
  border:none;
  border-radius:12px;
  font-size:16px;
  cursor:pointer;
  font-weight:bold;
}

.btn-primary{
  background:linear-gradient(135deg,#ff512f,#dd2476);
  color:white;
}

.btn-secondary{
  background:linear-gradient(135deg,#00c6ff,#0072ff);
  color:white;
}

.hidden{display:none;}

footer{
  text-align:center;
  font-size:13px;
  opacity:0.7;
  padding:20px 10px;
}
</style>
</head>

<body>

<header>
  <h1>🚚 AfroDelivers</h1>
  <p>Plataforma de ligação entre restaurantes e entregadores</p>
</header>

<div class="container">
  <div class="grid">

    <!-- CARD PEDIDO -->
    <div class="card">
      <h3>📦 Chamar Entregador</h3>
      <input id="restaurante" placeholder="Nome do restaurante">
      <input id="cliente" placeholder="Nome do cliente">
      <input id="recolha" placeholder="Local de recolha">
      <input id="entrega" placeholder="Local de entrega">
      <textarea id="descricao" placeholder="Descrição da encomenda"></textarea>
      <button class="btn-primary" onclick="enviarPedido()">🚀 Enviar Pedido</button>
    </div>

    <!-- CARD ADMIN -->
    <div class="card">
      <h3>👑 Área do Administrador</h3>
      <button class="btn-secondary" onclick="mostrarLogin()">Acessar Painel</button>
    </div>

  </div>
</div>

<!-- LOGIN ADMIN -->
<div class="container hidden" id="login">
  <div class="card">
    <h3>🔐 Login Administrador</h3>
    <input type="password" id="senha" placeholder="Senha de administrador">
    <button class="btn-secondary" onclick="entrar()">Entrar</button>
  </div>
</div>

<!-- PAINEL ADMIN -->
<div class="container hidden" id="admin">
  <div class="card">
    <h3>📋 Pedidos Recebidos</h3>
    <div id="listaPedidos"></div>
    <button class="btn-primary" onclick="limpar()">Limpar Pedidos</button>
  </div>
</div>

<footer>
  © 2026 AfroDelivers • Serviço de Entregas
</footer>

<script>
const WHATSAPP="244939513462";
const SENHA_ADMIN="afro123";

let pedidos=JSON.parse(localStorage.getItem("pedidos"))||[];

function enviarPedido(){
  let r=restaurante.value;
  let c=cliente.value;
  let rec=recolha.value;
  let ent=entrega.value;
  let d=descricao.value;
  if(!r||!c||!rec||!ent) return alert("Preencha todos os campos");

  let pedido={r,c,rec,ent,d};
  pedidos.push(pedido);
  localStorage.setItem("pedidos",JSON.stringify(pedidos));

  let msg=`🚚 NOVO PEDIDO DE ENTREGA - AfroDelivers
🏪 Restaurante: ${r}
👤 Cliente: ${c}
📍 Recolha: ${rec}
📦 Entrega: ${ent}
📝 Descrição: ${d}`;

  window.open(`https://wa.me/${WHATSAPP}?text=${encodeURIComponent(msg)}`);
}

function mostrarLogin(){
  login.classList.toggle("hidden");
}

function entrar(){
  if(senha.value===SENHA_ADMIN){
    admin.classList.remove("hidden");
    login.classList.add("hidden");
    listar();
  } else alert("Senha incorreta");
}

function listar(){
  listaPedidos.innerHTML="";
  pedidos.forEach(p=>{
    listaPedidos.innerHTML+=`
      <p>🏪 <b>${p.r}</b><br>➡️ ${p.ent}</p><hr>`;
  });
}

function limpar(){
  if(confirm("Apagar todos os pedidos?")){
    pedidos=[];
    localStorage.removeItem("pedidos");
    listar();
  }
}
</script>

</body>
</html>
