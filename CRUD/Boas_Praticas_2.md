# Vamos **melhorar o CRUD em PHP com boas práticas e visual mais bonito**, usando:
 * ✅ **Validação de formulários**
 * ✅ **Segurança com prepared statements**
 * ✅ **Interface com Bootstrap**


# 🛠️ 1. Adicionar o Bootstrap (visual moderno)
Adicione este trecho no `<head>` do seu `index.php`, `adicionar.php`, e `editar.php`:

```html

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

```

E se quiser, coloque o conteúdo dentro de um container:

```html

<div class="container mt-5">
  <!-- seu conteúdo PHP aqui -->
</div>

```
### 🧱 2. Conexão segura (conexao.php)
Atualize `conexao.php` para usar **PDO (PHP Data Objects)** — mais seguro:

```php

<?php
try {
  $conn = new PDO("mysql:host=localhost;dbname=crud_php", "root", "");
  $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
  die("Erro na conexão: " . $e->getMessage());
}
?>

```

### ➕ 3. adicionar.php com validação + segurança

```php

<?php include "conexao.php"; ?>
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

<div class="container mt-5">
  <h2>Adicionar Usuário</h2>
  <form method="POST">
    <div class="mb-3">
      <label>Nome:</label>
      <input type="text" name="nome" class="form-control" required>
    </div>
    <div class="mb-3">
      <label>Email:</label>
      <input type="email" name="email" class="form-control" required>
    </div>
    <button type="submit" class="btn btn-primary">Salvar</button>
  </form>

<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $nome = trim($_POST["nome"]);
  $email = trim($_POST["email"]);

  if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
    echo "<div class='alert alert-danger mt-3'>Email inválido!</div>";
  } else {
    $stmt = $conn->prepare("INSERT INTO usuarios (nome, email) VALUES (:nome, :email)");
    $stmt->bindParam(":nome", $nome);
    $stmt->bindParam(":email", $email);
    $stmt->execute();
    echo "<div class='alert alert-success mt-3'>Usuário adicionado com sucesso!</div>";
    echo "<a href='index.php' class='btn btn-secondary mt-2'>Voltar</a>";
  }
}
?>
</div>

```
### ✏️ 4. editar.php com segurança
```php

<?php include "conexao.php"; ?>
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<div class="container mt-5">

<?php
$id = $_GET["id"];
$stmt = $conn->prepare("SELECT * FROM usuarios WHERE id = :id");
$stmt->bindParam(":id", $id, PDO::PARAM_INT);
$stmt->execute();
$usuario = $stmt->fetch(PDO::FETCH_ASSOC);

if (!$usuario) {
  echo "<div class='alert alert-danger'>Usuário não encontrado.</div>";
  exit;
}

if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $nome = trim($_POST["nome"]);
  $email = trim($_POST["email"]);

  if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
    echo "<div class='alert alert-danger'>Email inválido.</div>";
  } else {
    $stmt = $conn->prepare("UPDATE usuarios SET nome = :nome, email = :email WHERE id = :id");
    $stmt->bindParam(":nome", $nome);
    $stmt->bindParam(":email", $email);
    $stmt->bindParam(":id", $id);
    $stmt->execute();
    header("Location: index.php");
    exit;
  }
}
?>

<h2>Editar Usuário</h2>
<form method="POST">
  <div class="mb-3">
    <label>Nome:</label>
    <input type="text" name="nome" class="form-control" value="<?= $usuario['nome'] ?>" required>
  </div>
  <div class="mb-3">
    <label>Email:</label>
    <input type="email" name="email" class="form-control" value="<?= $usuario['email'] ?>" required>
  </div>
  <button type="submit" class="btn btn-success">Atualizar</button>
</form>
</div>


```

### ❌ 5. deletar.php com segurança
```php

<?php
include "conexao.php";
$id = $_GET["id"];

$stmt = $conn->prepare("DELETE FROM usuarios WHERE id = :id");
$stmt->bindParam(":id", $id, PDO::PARAM_INT);
$stmt->execute();

header("Location: index.php");
exit;

```

### 📋 6. index.php com Bootstrap
Você pode deixar sua lista mais bonita assim:

```php

<?php include "conexao.php"; ?>
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<div class="container mt-5">
  <h2>Lista de Usuários</h2>
  <a href="adicionar.php" class="btn btn-primary mb-3">Novo Usuário</a>

  <table class="table table-bordered">
    <thead>
      <tr><th>ID</th><th>Nome</th><th>Email</th><th>Ações</th></tr>
    </thead>
    <tbody>
      <?php
        $stmt = $conn->query("SELECT * FROM usuarios");
        while($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
          echo "<tr>
            <td>{$row['id']}</td>
            <td>{$row['nome']}</td>
            <td>{$row['email']}</td>
            <td>
              <a href='editar.php?id={$row['id']}' class='btn btn-warning btn-sm'>Editar</a>
              <a href='deletar.php?id={$row['id']}' class='btn btn-danger btn-sm' onclick=\"return confirm('Tem certeza?')\">Excluir</a>
            </td>
          </tr>";
        }
      ?>
    </tbody>
  </table>
</div>

```

### ✅ Resultado
Você terá um CRUD:
  * Responsivo com Bootstrap
  * Seguro com PDO e validação
  * Visualmente organizado


