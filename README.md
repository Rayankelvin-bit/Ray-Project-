<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Ponto Virtual Acessível</title>

<style>
body {
    font-family: Arial, sans-serif;
    background-color: #000;
    color: #FFF;
    text-align: center;
    font-size: 22px;
}

button {
    width: 300px;
    height: 60px;
    font-size: 22px;
    margin: 10px;
    background-color: #FFD700;
    border: none;
    border-radius: 10px;
    cursor: pointer;
}

button:focus {
    outline: 4px solid #00FFFF;
}

#historico {
    margin-top: 30px;
}
</style>

</head>
<body>

<h1>Ponto Virtual</h1>

<button onclick="registrar('Entrada')">Registrar Entrada</button>
<button onclick="registrar('Saída Almoço')">Saída para Almoço</button>
<button onclick="registrar('Volta Almoço')">Volta do Almoço</button>
<button onclick="registrar('Saída Final')">Registrar Saída</button>

<div id="historico" aria-live="polite"></div>

<script>

function registrar(tipo) {
    const agora = new Date();
    const horario = agora.toLocaleString();

    const registro = tipo + " - " + horario;

    let dados = JSON.parse(localStorage.getItem("ponto")) || [];

    dados.push(registro);

    localStorage.setItem("ponto", JSON.stringify(dados));

    mostrarHistorico();
}

function mostrarHistorico() {
    let dados = JSON.parse(localStorage.getItem("ponto")) || [];

    const div = document.getElementById("historico");

    div.innerHTML = "<h2>Histórico</h2>";

    dados.forEach(item => {
        div.innerHTML += "<p>" + item + "</p>";
    });
}

mostrarHistorico();

</script>

</body>
</html>
