# Sobre
Serviço SAAS dinâmico de acordo com o produto.

## Baixar o projeto
Vá até a pasta desejada e digite:

```bash
git clone https://github.com/nanicas/<projeto>.git
```

## Instalação e Configuração
No terminal, execute:
```bash
docker-compose up -d --build
```

> Como estamos usando a rede `database-network-nanicas`, verifique se a mesma foi criada. Caso contrário, use o auxílio do projeto: https://github.com/nanicas/database-mysql

### Autenticação Laravel UI com Bootstrap
Dentro do container, execute o comando para incluir como dependência:
```bash
composer require laravel/ui
```

Execute o comando para gerar o scaffolding:
```bash
php artisan ui bootstrap --auth
```

```bash
INFO  Authentication scaffolding generated successfully.  

INFO  Bootstrap scaffolding installed successfully.  

WARN  Please run [npm install && npm run build] to compile your fresh scaffolding.
```

Conforme aviso anterior, precisamos então executar dois comandos para atualizar nosso gerenciador de dependências JavaScript. Como teremos alguns passos a seguir que envolvem adição de novos arquivos a serem compilados, então iremos executar somente um por ora.

E, por fim, execute:
```bash
npm install
```

### Toolkits

Referências para instalação e configuração dos *Toolkits*:
- Lógica: https://github.com/nanicas/legacy-laravel-toolkit-library
- Visual: https://github.com/nanicas/legacy-laravel-toolkit-view-library

### Copiar arquivos base
- Ao utilizar `legacy-laravel-toolkit-library`, teremos os arquivos base no seguinte caminho: `/vendor/nanicas/legacy-laravel-toolkit-library/_to_copy`. Copie-os para sua pasta `/app` em seus respectivos diretórios e renomeio-os conforme sua necessidade/vontade. (obs: sugestão é apenas remover o `Example` do prefíxo para ter menos trabalho em questão de renomeamento futuro)

    > Ponto de atenção: Não se esqueça se alterar o arquivo `/config/nanicas_legacy_laravel_toolkit.php` para garantir a integridade.
    ---

- Ao utilizar `legacy-laravel-toolkit-view-library`, teremos os arquivos base no seguinte caminho: `/resources/views/vendor/legacy_laravel_toolkit_view_library/_to_copy`. Copie-os para sua pasta `/resources/views` em seus respectivos diretórios mantendo os mesmos nomes.

    > Ponto de atenção: Caso já existam arquivos criados previamente, tome cuidado ao substituí-los.

### Configurar leitura de funções globais
Abra seu arquivo `composer.json` e adicione as seguintes linhas:

```json
"autoload": {
    "files": [
        "app/Functions/global.php"
    ]
},
```

Dentro do container, execute:
```bash
composer dump-autoload
```

### Migrar/Criar tabelas
Dentro do container, execute:
```bash
php artisan migrate
```

### Compilar assets
Dentro do container, execute:
```bash
npm run build
```

```bash
> build
> vite build

vite v4.5.3 building for production...
✓ 482 modules transformed.
public/build/manifest.json                         1.04 kB │ gzip:   0.30 kB
public/build/assets/app-a6b74ef6.css             261.43 kB │ gzip:  35.35 kB
public/build/assets/purify.es-d6eec8ab.js         21.87 kB │ gzip:   8.69 kB
public/build/assets/index.es-18e47ed2.js         149.69 kB │ gzip:  51.12 kB
public/build/assets/html2canvas.esm-e0a7d97b.js  201.43 kB │ gzip:  48.04 kB
public/build/assets/app-aaa5687b.js              948.88 kB │ gzip: 315.51 kB

(!) Some chunks are larger than 500 kBs after minification. Consider:
- Using dynamic import() to code-split the application
- Use build.rollupOptions.output.manualChunks to improve chunking: https://rollupjs.org/configuration-options/#output-manualchunks
- Adjust chunk size limit for this warning via build.chunkSizeWarningLimit.
[vite-plugin-static-copy] Copied 4 items.
✓ built in 7.17s
```

## Integrações
- Aplicação de autenticação: https://github.com/nanicas/authentication-laravel
    - Biblioteca de autenticação: https://github.com/nanicas/authentication-library

## Observações

### Chamada da view

- Link do código sobre `beforeView`: https://github.com/nanicas/legacy-laravel-toolkit-library/blob/main/app/Http/Controllers/Controller.php#L50

Caso esteja usando o pacote de autenticação do Laravel juntamente com `legacy-laravel-toolkit-view-library` + `legacy-laravel-toolkit-library`, antes de chamar qualquer `view`, precisará executar o seguinte método `beforeView`.

Exemplo de uso em `HomeController`:
```php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Http\Controllers\Controller;

class HomeController extends Controller
{
    /**
     * Show the application dashboard.
     * 
     * @param Request $request
     * @return \Illuminate\Contracts\Support\Renderable
     */
    public function index(Request $request)
    {
        parent::beforeView($request);

        return view('home');
    }
}
```

#### Laravel Authentication

- Link documentação: https://laravel.com/docs/10.x/authentication

Exemplo de uso em `LoginController`:
```php
namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;

class LoginController extends Controller
{
    /**
     * @param Request $request
     */
    public function showLoginForm(Request $request)
    {
        parent::beforeView($request);

        return view('auth.login');
    }
}
```

Exemplo de uso em `RegisterController`:
```php
namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;

class RegisterController extends Controller
{
    /**
     * @param Request $request
     */
    public function showRegistrationForm(Request $request)
    {
        parent::beforeView($request);

        return view('auth.register');
    }
}
```

## Usar a aplicação
Abra o navegador e digite: http://localhost:{port}

## Tecnologias e Bibliotecas
- [PHP] - https://www.php.net
- [Laravel] - https://laravel.com/docs/10.x
- [Bootstrap] - https://getbootstrap.com/docs/5.2/getting-started/introduction
- [MySQL] - https://www.mysql.com
- [Jquery] - https://jquery.com
- [GitHub] - https://github.com
- [Git] - https://git-scm.com

## Pendências
- Adicionar instalação sobre o `DataTables Yajra`;
