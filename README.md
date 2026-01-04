<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Blox Main</title>

<style>
body {
  font-family: Arial, sans-serif;
  background:#0a1e3f;
  color:#fff;
  margin:0;
  display:flex;
  justify-content:center;
}
.container {
  width:100%;
  max-width:420px;
  padding:20px;
}
header { text-align:center; }
header h1 { color:#4da3ff; margin:0; }

.card {
  background:#102c5a;
  padding:20px;
  border-radius:10px;
  margin-top:20px;
}
.produto-img {
  width:100%;
  border-radius:8px;
  margin-bottom:10px;
}
.badges {
  display:flex;
  gap:8px;
  flex-wrap:wrap;
  margin-bottom:10px;
}
.badge {
  background:#1e90ff;
  padding:6px 10px;
  border-radius:20px;
  font-size:12px;
}
label { margin-top:10px; display:block; }
input, textarea, button {
  width:100%;
  margin-top:6px;
  padding:10px;
  border-radius:6px;
  border:none;
}
textarea { height:90px; resize:none; }
button {
  background:#1e90ff;
  color:white;
  font-weight:bold;
  cursor:pointer;
  margin-top:12px;
}
button:hover { background:#187bcd; }
.valor { margin-top:10px; color:#00ffae; font-weight:bold; }
.status { margin-top:10px; font-size:14px; }
.hidden { display:none; }
footer {
  margin-top:20px;
  font-size:12px;
  text-align:center;
  color:#ccc;
}
hr { border:1px solid #1e90ff; margin:20px 0; }
</style>
</head>

<body>
<div class="container">

<header>
  <h1>Blox Main</h1>
  <p>Contas Blox Fruits • Entrega segura</p>
</header>

<!-- ===== PRODUTO ===== -->
<div class="card" id="loja">
  <img src="images/bloxfruits.jpg" class="produto-img" alt="Blox Fruits">

  <h2>Conta Blox Fruits FULL</h2>

  <div class="badges">
    <div class="badge">🐯 Tiger</div>
    <div class="badge">🥋 God Human</div>
    <div class="badge">⭐ Level Máx</div>
  </div>

  <p>
    Conta pronta para PvP e Farm.<br>
    Entrega segura após confirmação do Pix.
  </p>

  <label>Nome completo (igual ao banco)</label>
  <input id="nome">

  <label>Cupom de desconto</label>
  <input id="cupom">
  <button onclick="aplicarCupom()">Aplicar cupom</button>

  <div class="valor" id="valorTexto">Valor: R$ 18,00</div>

  <label>Pix para pagamento</label>
  <textarea id="pixArea" readonly></textarea>

  <button onclick="finalizarPedido()">Confirmar pedido</button>
  <div class="status" id="status"></div>
</div>

<!-- ===== ENTREGA CLIENTE ===== -->
<div class="card hidden" id="entregaCliente">
  <h2>🎉 Pedido entregue</h2>
  <p><strong>Login:</strong> <span id="loginCli"></span></p>
  <p><strong>Senha:</strong> <span id="senhaCli"></span></p>
</div>

<!-- ===== PAINEL ===== -->
<div class="card">
  <h2>Painel do vendedor</h2>

  <label>Senha do painel</label>
  <input type="password" id="senhaPainel">
  <button onclick="abrirPainel()">Entrar</button>

  <div id="painel" class="hidden">
    <hr>
    <p id="infoPedido"></p>

    <label>Login da conta</label>
    <input id="loginConta">

    <label>Senha da conta</label>
    <input id="senhaConta">

    <button onclick="enviarConta()">ENVIAR CONTA</button>
  </div>
</div>

<footer>
⚠️ Após receber a conta, troque a senha imediatamente.
</footer>

</div>

<script>
let valorAtual = 18;

const pix18 = `00020126490014BR.GOV.BCB.PIX0127arrecadando.ajuda@gmail.com520400005303986540518.005802BR5925David Luiz Turani Bechene6009SAO PAULO621405106cxvu46bR36304EB65`;
const pix12 = `00020126490014BR.GOV.BCB.PIX0127arrecadando.ajuda@gmail.com520400005303986540512.005802BR5925David Luiz Turani Bechene6009SAO PAULO62140510Pk1ZSdC6Ll6304B422`;

document.getElementById("pixArea").value = pix18;

function aplicarCupom(){
  if(document.getElementById("cupom").value.trim() === "stream"){
    valorAtual = 12;
    document.getElementById("valorTexto").innerText = "Valor: R$ 12,00";
    document.getElementById("pixArea").value = pix12;
    document.getElementById("status").innerText = "✅ Cupom aplicado";
  }
}

function finalizarPedido(){
  const nome = document.getElementById("nome").value.trim();
  if(!nome){ alert("Preencha o nome."); return; }

  localStorage.setItem("pedido", JSON.stringify({nome, valor:valorAtual}));
  document.getElementById("status").innerText =
    "⏳ Pedido registrado. Aguarde confirmação.";
}

function abrirPainel(){
  if(document.getElementById("senhaPainel").value !== "admin123"){
    alert("Senha incorreta"); return;
  }

  const pedido = JSON.parse(localStorage.getItem("pedido"));
  if(!pedido){ alert("Nenhum pedido"); return; }

  document.getElementById("painel").classList.remove("hidden");
  document.getElementById("infoPedido").innerText =
    `Cliente: ${pedido.nome} | Valor: R$ ${pedido.valor},00`;
}

function enviarConta(){
  const login = document.getElementById("loginConta").value;
  const senha = document.getElementById("senhaConta").value;

  if(!login || !senha){ alert("Preencha login e senha"); return; }

  document.getElementById("loginCli").innerText = login;
  document.getElementById("senhaCli").innerText = senha;
  document.getElementById("entregaCliente").classList.remove("hidden");
}
</script>

</body>
</html>
