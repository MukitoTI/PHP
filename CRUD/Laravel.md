# 🟦 PARTE 2: Laravel


🧰 PRÉ-REQUISITOS
Antes de começar, você precisa ter instalado:
1. **PHP** (versão 8 ou superior)
2. **Composer** (gerenciador de pacotes PHP) → https://getcomposer.org/
3. **Laravel Installer** (opcional) ou usar via composer create-project
4. **MySQL ou MariaDB** (via XAMPP, WAMP ou nativo)
5. **Terminal (CMD, PowerShell ou Git Bash)**

Se ainda não tiver o Composer ou PHP instalado, posso te guiar na instalação.

# 🛠️ ETAPA 1: Criar o Projeto Laravel
Abra o terminal e digite:

```bash

composer create-project laravel/laravel crud-laravel

```
Isso criará uma pasta chamada `crud-laravel` com o projeto pronto.


# 📦 ETAPA 2: Subir o servidor
Dentro da pasta do projeto, rode:
```bash

cd crud-laravel
php artisan serve

```
Acesse o navegador:

```arduino

http://localhost:8000

```
Você verá a tela padrão do Laravel.

### ⚙️ ETAPA 3: Configurar o Banco de Dados
1. Crie um banco no phpMyAdmin chamado `crud_laravel`
2. No projeto, abra `.env` e configure:
```env

DB_DATABASE=crud_laravel
DB_USERNAME=root
DB_PASSWORD=

```

### 🧱 ETAPA 4: Criar o Model + Migration + Controller
Vamos criar um CRUD de usuários com `nome` e `email`.

```bash

php artisan make:model Usuario -mc

```
Isso cria:

  * `app/Models/Usuario.php`
  * `app/Http/Controllers/UsuarioController.php`
  * `database/migrations/xxxx_create_usuarios_table.php`


**Edite a migration** (`database/migrations/...usuarios_table.php`):
```php

public function up()
{
    Schema::create('usuarios', function (Blueprint $table) {
        $table->id();
        $table->string('nome');
        $table->string('email')->unique();
        $table->timestamps();
    });
}

```

Execulte a migration:
```bash

php artisan migrate

```

### ✏️ ETAPA 5: Criar rotas no** `web.php`
Abra `routes/web.php` e adicione:
```php

use App\Http\Controllers\UsuarioController;

Route::get('/', [UsuarioController::class, 'index']);
Route::get('/usuarios/create', [UsuarioController::class, 'create']);
Route::post('/usuarios', [UsuarioController::class, 'store']);
Route::get('/usuarios/{id}/edit', [UsuarioController::class, 'edit']);
Route::put('/usuarios/{id}', [UsuarioController::class, 'update']);
Route::delete('/usuarios/{id}', [UsuarioController::class, 'destroy']);

```

### 🖥️ ETAPA 6: Criar as views Blade
Crie a pasta `resources/views/usuarios/` e os arquivos:
 * `index.blade.php`
 * `create.blade.php`
 * `edit.blade.php`

Posso gerar o conteúdo de cada um para você, com Bootstrap incluído. Quer que eu envie agora?

🚀 RESUMO
Você agora tem:

✅ Laravel instalado <br>
✅ Banco de dados configurado <br>
✅ Model, Controller e Migration criados <br>
✅ Rotas funcionando <br>
⏳ Próximo: criar as telas Blade com formulários e listagem <br>

