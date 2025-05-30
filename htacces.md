# ✅ PARTE 1: Rotas Amigáveis com .htaccess no Projeto Atual
### 🎯 Objetivo
Transformar isso:

```
http://localhost/crud_php/editar.php?id=3

```
 Nisso:
```
http://localhost/crud_php/editar.php?id=3

```

### 🧰 Etapa 1: Habilitar mod_rewrite no XAMPP
1. Vá até o XAMPP Control Panel
2. Clique no botão **Config** (do lado do Apache) → escolha `httpd.conf`
3. Procure (Ctrl+F) por esta linha:


```apache

#LoadModule rewrite_module modules/mod_rewrite.so

```
4. **Remova** o # (descomente a linha):

```apache

LoadModule rewrite_module modules/mod_rewrite.so

```

5. Agora, procure esta outra linha:

```
AllowOverride None
```apache
Mude para:

```apache
AllowOverride All
```

#### 🔁 Salve o arquivo e reinicie o Apache.

### Etapa 2: Criar um arquivo `.htaccess`
Na pasta do seu projeto (`C:\xampp\htdocs\crud_php`), crie um arquivo chamado `.htaccess` com este conteúdo:
```apache

RewriteEngine On
RewriteBase /crud_php/

RewriteRule ^editar/([0-9]+)$ editar.php?id=$1 [L]
RewriteRule ^deletar/([0-9]+)$ deletar.php?id=$1 [L]
RewriteRule ^adicionar$ adicionar.php [L]
RewriteRule ^$ index.php [L]

```

Esse arquivo define que:
  * `editar/3` → vai para `editar.php?id=3`
  * `deletar/5` → vai para `deletar.php?id=5`
  * `adicionar` → vai para `adicionar.php`
  * / → vai para `index.php`

### ✏️ Etapa 3: Ajustar os links nos seus arquivos PHP
Exemplo em `index.php`:

```php

<a href="editar/<?= $row['id'] ?>" class="btn btn-warning btn-sm">Editar</a>
<a href="deletar/<?= $row['id'] ?>" class="btn btn-danger btn-sm" onclick="return confirm('Tem certeza?')">Excluir</a>

```

**Exemplo no botão “Novo usuário”:**

```php

<a href="adicionar" class="btn btn-primary mb-3">Novo Usuário</a>

```

### 🚀 Etapa 4: Acessar no navegador
Agora, no navegador, use:
```arduino

http://localhost/crud_php/

```

E clique nos botões para ver as rotas amigáveis funcionando!

