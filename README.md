<!DOCTYPE html>
<html lang="pt-br">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Busca de Pacientes</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        /* Customização de cores e fontes */
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f7fc;
        }

        .container {
            max-width: 800px;
            padding: 40px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        h2 {
            color: #4a90e2;
            text-align: center;
            margin-bottom: 30px;
        }

        .form-control {
            border-radius: 10px;
            padding: 15px;
            font-size: 16px;
        }

        .btn-primary {
            background-color: #4a90e2;
            border-color: #4a90e2;
            padding: 12px 30px;
            font-size: 16px;
            border-radius: 5px;
        }

        .btn-primary:hover {
            background-color: #357ab7;
            border-color: #357ab7;
        }

        .btn-success {
            background-color: #28a745;
            border-color: #28a745;
            padding: 12px 30px;
            font-size: 16px;
            border-radius: 5px;
        }

        .btn-success:hover {
            background-color: #218838;
            border-color: #1e7e34;
        }

        .input-group {
            margin-bottom: 15px;
        }

        .form-label {
            font-weight: 600;
            color: #555;
        }

        .input-group-text {
            background-color: #f1f1f1;
        }

        .form-select {
            padding: 15px;
            border-radius: 10px;
            font-size: 16px;
        }
    </style>
</head>

<body>

    <div class="container">
        <h2>Sistema de Busca de Pacientes do Ambulatório Municipal de Psiquiatria</h2>

        <!-- Formulário para adicionar e buscar prontuários -->
        <form>
            <div class="input-group">
                <span class="input-group-text" id="basic-addon1">🔍</span>
                <input type="text" class="form-control" id="nomePaciente" placeholder="Nome do Paciente" aria-label="Nome do Paciente" aria-describedby="basic-addon1">
            </div>

            <div class="input-group">
                <span class="input-group-text" id="basic-addon2">👩‍👦</span>
                <input type="text" class="form-control" id="nomeMae" placeholder="Nome da Mãe" aria-label="Nome da Mãe" aria-describedby="basic-addon2">
            </div>

            <div class="input-group">
                <span class="input-group-text" id="basic-addon3">📋</span>
                <input type="number" class="form-control" id="numeroProntuario" placeholder="Número do Prontuário" aria-label="Número do Prontuário" aria-describedby="basic-addon3">
            </div>

            <div class="input-group">
                <span class="input-group-text" id="basic-addon4">📦</span>
                <select class="form-select" id="caixa">
                    <option value="">Escolha a Caixa</option>
                    <option value="A1">Caixa A1</option>
                    <option value="A2">Caixa A2</option>
                    <option value="A3">Caixa A3</option>
                    <option value="A4">Caixa A4</option>
                    <option value="B1">Caixa B1</option>
                    <option value="B2">Caixa B2</option>
                    <option value="B3">Caixa B3</option>
                    <option value="B4">Caixa B4</option>
                </select>
            </div>

            <div class="mb-3">
                <button type="button" class="btn btn-primary" onclick="adicionarProntuario()">Adicionar Prontuário</button>
            </div>

            <hr>

            <!-- Carregar Arquivo Word -->
            <div class="input-group">
                <input type="file" class="form-control" id="uploadWord" accept=".docx">
            </div>

            <div class="mb-3 mt-3">
                <button type="button" class="btn btn-success" onclick="pesquisarPaciente()">Pesquisar Paciente</button>
            </div>

        </form>

        <!-- Resultados da Busca -->
        <div class="result-container" id="resultados">
            <!-- Resultados serão inseridos aqui -->
        </div>

    </div>

    <script>
        let prontuarios = [];

        function adicionarProntuario() {
            const nomePaciente = document.getElementById('nomePaciente').value;
            const nomeMae = document.getElementById('nomeMae').value;
            const numeroProntuario = document.getElementById('numeroProntuario').value;
            const caixa = document.getElementById('caixa').value;

            if (nomePaciente && nomeMae && numeroProntuario && caixa) {
                const prontuario = {
                    nomePaciente,
                    nomeMae,
                    numeroProntuario,
                    caixa
                };
                prontuarios.push(prontuario);
                alert('Prontuário adicionado com sucesso!');
                limparFormulario();
            } else {
                alert('Por favor, preencha todos os campos!');
            }
        }

        function limparFormulario() {
            document.getElementById('nomePaciente').value = '';
            document.getElementById('nomeMae').value = '';
            document.getElementById('numeroProntuario').value = '';
            document.getElementById('caixa').value = '';
        }

        function pesquisarPaciente() {
            const nomePacienteBusca = document.getElementById('nomePaciente').value;
            const resultados = prontuarios.filter(prontuario => prontuario.nomePaciente.toLowerCase().includes(nomePacienteBusca.toLowerCase()));
            exibirResultados(resultados);
        }

        function exibirResultados(resultados) {
            const divResultados = document.getElementById('resultados');
            divResultados.innerHTML = '';
            if (resultados.length > 0) {
                let html = '<ul>';
                resultados.forEach(prontuario => {
                    html += `<li><strong>Nome do Paciente:</strong> ${prontuario.nomePaciente} <br><strong>Caixa:</strong> ${prontuario.caixa} <br><strong>Número do Prontuário:</strong> ${prontuario.numeroProntuario} </li><hr>`;
                });
                html += '</ul>';
                divResultados.innerHTML = html;
            } else {
                divResultados.innerHTML = 'Nenhum prontuário encontrado.';
            }
        }
    </script>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>

</body>

</html>
