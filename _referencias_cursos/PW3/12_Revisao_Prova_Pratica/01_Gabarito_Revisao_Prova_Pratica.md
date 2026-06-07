# Gabarito da Revisão para Prova Prática - PW3

> Material de apoio do professor. Não publicar para os alunos.

---

## Contexto

Este gabarito corresponde à revisão prática de PW3 com a funcionalidade `Oficina` em Laravel, com criação de Model, migration, Controller, View e rotas.

## Comandos esperados

```bash
php artisan make:model Oficina -m
php artisan make:controller OficinaController
php artisan migrate
```

---

## Migration sugerida

Arquivo sugerido: `database/migrations/...create_oficinas_table.php`

```php
public function up(): void
{
    Schema::create('oficinas', function (Blueprint $table) {
        $table->id();
        $table->string('nome_oficina');
        $table->string('professor_responsavel');
        $table->integer('carga_horaria');
        $table->string('turno');
        $table->timestamps();
    });
}
```

---

## Model sugerido

Arquivo sugerido: `app/Models/Oficina.php`

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Oficina extends Model
{
    protected $fillable = [
        'nome_oficina',
        'professor_responsavel',
        'carga_horaria',
        'turno',
    ];
}
```

---

## Controller sugerido

Arquivo sugerido: `app/Http/Controllers/OficinaController.php`

```php
<?php

namespace App\Http\Controllers;

use App\Models\Oficina;
use Illuminate\Http\Request;

class OficinaController extends Controller
{
    public function index()
    {
        $oficinas = Oficina::orderBy('nome_oficina')->get();
        return view('oficinas.index', compact('oficinas'));
    }

    public function store(Request $request)
    {
        $dados = $request->validate([
            'nome_oficina' => 'required|min:4',
            'professor_responsavel' => 'required|min:4',
            'carga_horaria' => 'required|integer|min:20|max:120',
            'turno' => 'required',
        ]);

        Oficina::create($dados);

        return redirect('/oficinas')->with('sucesso', 'Oficina cadastrada com sucesso.');
    }
}
```

---

## View sugerida

Arquivo sugerido: `resources/views/oficinas/index.blade.php`

```blade
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de Oficinas</title>
</head>
<body>
    <h1>Cadastro de Oficinas</h1>

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

    <form action="/oficinas" method="post">
        @csrf

        <label for="nome_oficina">Nome da oficina</label><br>
        <input type="text" id="nome_oficina" name="nome_oficina" value="{{ old('nome_oficina') }}" required><br><br>

        <label for="professor_responsavel">Professor responsável</label><br>
        <input type="text" id="professor_responsavel" name="professor_responsavel" value="{{ old('professor_responsavel') }}" required><br><br>

        <label for="carga_horaria">Carga horária</label><br>
        <input type="number" id="carga_horaria" name="carga_horaria" value="{{ old('carga_horaria') }}" required><br><br>

        <label for="turno">Turno</label><br>
        <input type="text" id="turno" name="turno" value="{{ old('turno') }}" required><br><br>

        <button type="submit">Salvar</button>
    </form>

    <h2>Oficinas cadastradas</h2>

    @if ($oficinas->isEmpty())
        <p>Nenhuma oficina cadastrada.</p>
    @else
        <table border="1" cellpadding="6">
            <thead>
                <tr>
                    <th>Oficina</th>
                    <th>Professor responsável</th>
                    <th>Carga horária</th>
                    <th>Turno</th>
                </tr>
            </thead>
            <tbody>
                @foreach ($oficinas as $oficina)
                    <tr>
                        <td>{{ $oficina->nome_oficina }}</td>
                        <td>{{ $oficina->professor_responsavel }}</td>
                        <td>{{ $oficina->carga_horaria }}</td>
                        <td>{{ $oficina->turno }}</td>
                    </tr>
                @endforeach
            </tbody>
        </table>
    @endif
</body>
</html>
```

---

## Rotas esperadas

Arquivo sugerido: `routes/web.php`

```php
use App\Http\Controllers\OficinaController;

Route::get('/oficinas', [OficinaController::class, 'index']);
Route::post('/oficinas', [OficinaController::class, 'store']);
```

---

## Checklist rápido de correção

- Comandos Artisan executados corretamente.
- Migration ajustada com os campos da revisão.
- Model com `fillable` completo.
- Controller com validação simples e persistência.
- View com formulário, erros e listagem.
- Rotas `GET` e `POST` funcionando.
