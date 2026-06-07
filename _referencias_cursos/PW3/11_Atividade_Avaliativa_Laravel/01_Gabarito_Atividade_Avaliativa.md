# Gabarito da Atividade Avaliativa - Laravel

> Material de apoio do professor. Não publicar para os alunos.

---

## Contexto

Este gabarito corresponde à atividade de cadastro e listagem de livros em Laravel, com foco em completar Model, Controller e View no padrão MVC.

## Implementação sugerida

### Model

Arquivo sugerido: `app/Models/Livro.php`

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Livro extends Model
{
    protected $fillable = [
        'titulo',
        'autor',
        'ano_publicacao',
    ];
}
```

### Controller

Arquivo sugerido: `app/Http/Controllers/LivroController.php`

```php
<?php

namespace App\Http\Controllers;

use App\Models\Livro;
use Illuminate\Http\Request;

class LivroController extends Controller
{
    public function index()
    {
        $livros = Livro::orderBy('titulo')->get();
        return view('livros.index', compact('livros'));
    }

    public function store(Request $request)
    {
        $dados = $request->validate([
            'titulo' => 'required|min:3',
            'autor' => 'required|min:3',
            'ano_publicacao' => 'required|integer|min:1|max:' . date('Y'),
        ]);

        Livro::create($dados);

        return redirect('/livros')->with('sucesso', 'Livro cadastrado com sucesso.');
    }
}
```

### View

Arquivo sugerido: `resources/views/livros/index.blade.php`

```blade
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de Livros</title>
</head>
<body>
    <h1>Cadastro de Livros</h1>

    @if (session('sucesso'))
        <p>{{ session('sucesso') }}</p>
    @endif

    @if ($errors->any())
        <ul>
            @foreach ($errors->all() as $erro)
                <li>{{ $erro }}</li>
            @endforeach
        </ul>
    @endif

    <form action="/livros" method="post">
        @csrf

        <label for="titulo">Título</label><br>
        <input type="text" id="titulo" name="titulo" value="{{ old('titulo') }}" required><br><br>

        <label for="autor">Autor</label><br>
        <input type="text" id="autor" name="autor" value="{{ old('autor') }}" required><br><br>

        <label for="ano_publicacao">Ano de publicação</label><br>
        <input type="number" id="ano_publicacao" name="ano_publicacao" value="{{ old('ano_publicacao') }}" required><br><br>

        <button type="submit">Salvar</button>
    </form>

    <h2>Livros cadastrados</h2>

    @if ($livros->isEmpty())
        <p>Nenhum livro cadastrado.</p>
    @else
        <table border="1" cellpadding="6">
            <thead>
                <tr>
                    <th>Título</th>
                    <th>Autor</th>
                    <th>Ano</th>
                </tr>
            </thead>
            <tbody>
                @foreach ($livros as $livro)
                    <tr>
                        <td>{{ $livro->titulo }}</td>
                        <td>{{ $livro->autor }}</td>
                        <td>{{ $livro->ano_publicacao }}</td>
                    </tr>
                @endforeach
            </tbody>
        </table>
    @endif
</body>
</html>
```

### Rotas esperadas

Arquivo sugerido: `routes/web.php`

```php
use App\Http\Controllers\LivroController;

Route::get('/livros', [LivroController::class, 'index']);
Route::post('/livros', [LivroController::class, 'store']);
```

---

## Checklist rápido de correção

- Model com `fillable` correto.
- Controller com validação, persistência e redirecionamento.
- View com formulário, mensagens de erro e listagem.
- Fluxo de cadastro funcionando no navegador.
