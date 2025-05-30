# 🛠️ Etapa 1: Instalando o ambiente PHP
### ✅ Opção recomendada: XAMPP
**XAMPP** é um pacote que inclui:

 * **Apache** (servidor web)
 * **MySQL/MariaDB** (banco de dados)
 * **PHP**
 * **phpMyAdmin** (interface para gerenciar bancos de dados)

### 🔽 Como instalar:
1. Acesse https://www.apachefriends.org/pt_br/index.html
2. Baixe o XAMPP para o seu sistema operacional (Windows, Linux ou macOS)
3. Instale e abra o painel de controle do XAMPP
4. Inicie os módulos **Apache** e **MySQL**

📁 Os arquivos do seu site PHP devem ir para a pasta:
`C:\xampp\htdocs\` (no Windows)

**Exemplo**: crie a pasta `meusite`, e dentro dela, crie um arquivo chamado `index.php`.

### 🧪 Etapa 2: Seu primeiro script PHP
No arquivo `index.php` dentro da pasta `htdocs/meusite`, digite:
```php

<?php
  echo "Olá, mundo!";
?>
```
Agora acesse no navegador:
📎 `http://localhost/meusite`

### 📘 Etapa 3: Conceitos básicos de PHP
### 🔹 **Variáveis**
```php

<?php
  $nome = "João";
  $idade = 25;
  echo "Meu nome é $nome e eu tenho $idade anos.";
?>

```

### 🔹 **Condições**
```php

<?php
  $idade = 18;
  if ($idade >= 18) {
    echo "Maior de idade";
  } else {
    echo "Menor de idade";
  }
?>

```
### 🔹 **Laços (loops)**
```php

<?php
  for ($i = 1; $i <= 5; $i++) {
    echo "Número: $i<br>";
  }
?>

```
### 🔹 **Funções**
```php

<?php
  function saudacao($nome) {
    return "Olá, $nome!";
  }

  echo saudacao("Ana");
?>

```

### 🔗 Etapa 4: Banco de dados com PHP + MySQL
1. Acesse `http://localhost/phpmyadmin`
2. Crie um novo banco de dados, por exemplo: `teste`
3. Crie uma tabela chamada `usuarios` com os campos: `id`, `nome`, `email`

### 🔸 Conectando ao banco com PHP
```php

<?php
$conn = new mysqli("localhost", "root", "", "teste");

if ($conn->connect_error) {
  die("Falha na conexão: " . $conn->connect_error);
}

echo "Conectado com sucesso!";
?>

```
### 🔄 Etapa 5: Próximos passos
Se quiser, posso te mostrar:
 * Como **inserir, listar, editar e deletar** dados no banco
 * Criar um **formulário de login**
 * Usar **rotas simples com .htaccess**
 * Introduzir um **framework moderno como Laravel**

