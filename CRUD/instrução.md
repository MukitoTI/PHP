# CRUD
Vamos criar um pequeno sistema **CRUD com PHP e MySQL** passo a passo. CRUD significa:
  * **C** – Criar (inserir dados)
  * **R** – Ler (listar dados)
  * **U** – Atualizar (editar dados)
  * **D** – Deletar (excluir dados)

### 🧰 Etapa 1: Preparar o ambiente
#### 1.1 Criar banco de dados e tabela
1. Acesse `http://localhost/phpmyadmin`
2. Crie um banco de dados chamado `crud_php`
3. Execute o seguinte SQL para criar a tabela `usuarios`:

```sql

CREATE TABLE usuarios (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(100) NOT NULL,
  email VARCHAR(100) NOT NULL
);

```

### 📁 Etapa 2: Estrutura de arquivos
Crie uma pasta em `C:\xampp\htdocs\crud_php` com os seguintes arquivos:
```lua

crud_php/
├── conexao.php
├── index.php       ← Lista os usuários
├── adicionar.php   ← Formulário de novo usuário
├── editar.php      ← Editar usuário existente
├── deletar.php     ← Excluir usuário
```
### 🔌 conexao.php
```php
<?php
$servidor = "localhost";
$usuario = "root";
$senha = "";
$banco = "crud_php";

$conn = new mysqli($servidor, $usuario, $senha, $banco);

if ($conn->connect_error) {
  die("Erro na conexão: " . $conn->connect_error);
}
?>

```

### 📄 index.php – Listar usuários
```php

<?php include "conexao.php"; ?>
<h2>Lista de Usuários</h2>
<a href="adicionar.php">Adicionar Novo</a><br><br>

<table border="1" cellpadding="10">
  <tr><th>ID</th><th>Nome</th><th>Email</th><th>Ações</th></tr>

<?php
$result = $conn->query("SELECT * FROM usuarios");
while($row = $result->fetch_assoc()) {
  echo "<tr>
    <td>{$row['id']}</td>
    <td>{$row['nome']}</td>
    <td>{$row['email']}</td>
    <td>
      <a href='editar.php?id={$row['id']}'>Editar</a> |
      <a href='deletar.php?id={$row['id']}'>Excluir</a>
    </td>
  </tr>";
}
?>
</table>

```

### ➕ adicionar.php – Inserir novo usuário
```php

<?php include "conexao.php"; ?>

<h2>Adicionar Usuário</h2>
<form method="POST">
  Nome: <input type="text" name="nome" required><br>
  Email: <input type="email" name="email" required><br>
  <button type="submit">Salvar</button>
</form>

<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $nome = $_POST["nome"];
  $email = $_POST["email"];
  $conn->query("INSERT INTO usuarios (nome, email) VALUES ('$nome', '$email')");
  echo "Usuário adicionado!";
  echo "<br><a href='index.php'>Voltar</a>";
}
?>

```

### ✏️ editar.php – Editar usuário
```php

<?php
include "conexao.php";
$id = $_GET["id"];
$usuario = $conn->query("SELECT * FROM usuarios WHERE id=$id")->fetch_assoc();

if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $nome = $_POST["nome"];
  $email = $_POST["email"];
  $conn->query("UPDATE usuarios SET nome='$nome', email='$email' WHERE id=$id");
  header("Location: index.php");
  exit;
}
?>

<h2>Editar Usuário</h2>
<form method="POST">
  Nome: <input type="text" name="nome" value="<?= $usuario['nome'] ?>"><br>
  Email: <input type="email" name="email" value="<?= $usuario['email'] ?>"><br>
  <button type="submit">Salvar</button>
</form>

```

### ❌ deletar.php – Excluir usuário
```php

<?php
include "conexao.php";
$id = $_GET["id"];
$conn->query("DELETE FROM usuarios WHERE id=$id");
header("Location: index.php");
exit;

```

### 🚀 Como testar
1. Coloque a pasta `crud_php` em `C:\xampp\htdocs\`
2. Inicie o Apache e MySQL no XAMPP
3. Acesse `http://localhost/crud_php/index.php`


