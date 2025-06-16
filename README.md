<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CRUD Front-end</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 20px;
    }

    h2 {
      text-align: center;
    }

    .form-control {
      margin-bottom: 10px;
    }

    input[type="text"], input[type="email"] {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
    }

    button {
      padding: 10px 20px;
      background-color: #007bff;
      color: white;
      border: none;
      cursor: pointer;
    }

    button:hover {
      background-color: #0056b3;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }

    th, td {
      padding: 12px;
      border: 1px solid #ccc;
      text-align: center;
    }

    .actions button {
      margin: 0 5px;
    }
  </style>
</head>
<body>

  <h2>CRUD de Usuários (Front-end)</h2>

  <div id="form">
    <div class="form-control">
      <label>Nome:</label>
      <input type="text" id="nome">
    </div>
    <div class="form-control">
      <label>Email:</label>
      <input type="email" id="email">
    </div>
    <button onclick="salvar()">Salvar</button>
  </div>

  <table id="tabela">
    <thead>
      <tr>
        <th>Nome</th>
        <th>Email</th>
        <th>Ações</th>
      </tr>
    </thead>
    <tbody>
      <!-- Conteúdo será gerado via JS -->
    </tbody>
  </table>

  <script>
    let usuarios = [];
    let indexEditando = null;

    function salvar() {
      const nome = document.getElementById('nome').value;
      const email = document.getElementById('email').value;

      if (!nome || !email) {
        alert("Preencha todos os campos!");
        return;
      }

      if (indexEditando === null) {
        // Criar
        usuarios.push({ nome, email });
      } else {
        // Editar
        usuarios[indexEditando] = { nome, email };
        indexEditando = null;
      }

      document.getElementById('nome').value = '';
      document.getElementById('email').value = '';

      renderizarTabela();
    }

    function renderizarTabela() {
      const tbody = document.querySelector('#tabela tbody');
      tbody.innerHTML = '';

      usuarios.forEach((usuario, index) => {
        const tr = document.createElement('tr');

        tr.innerHTML = `
          <td>${usuario.nome}</td>
          <td>${usuario.email}</td>
          <td class="actions">
            <button onclick="editar(${index})">Editar</button>
            <button onclick="excluir(${index})">Excluir</button>
          </td>
        `;

        tbody.appendChild(tr);
      });
    }

    function editar(index) {
      const usuario = usuarios[index];
      document.getElementById('nome').value = usuario.nome;
      document.getElementById('email').value = usuario.email;
      indexEditando = index;
    }

    function excluir(index) {
      if (confirm("Tem certeza que deseja excluir este usuário?")) {
        usuarios.splice(index, 1);
        renderizarTabela();
      }
    }
  </script>

</body>
</html>

