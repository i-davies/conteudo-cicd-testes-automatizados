# Gabarito Privado - Dissertativas de Revisão PW1 (2º Bimestre)

Este arquivo é de apoio do professor e não deve ser publicado para os alunos.

## Dissertativa 1 - Estrutura semântica básica

Resposta sugerida:

```html
<header>
  <h1>Clube de Leitura</h1>
  <p>Espaço para trocar ideias sobre livros.</p>
</header>

<main>
  <section>
    <h2>Encontros da semana</h2>
    <p>A turma discute capítulos e compartilha resumos.</p>
  </section>

  <section>
    <h2>Próxima atividade</h2>
    <p>Cada grupo vai apresentar uma recomendação de leitura.</p>
  </section>
</main>

<footer>
  <p>Nome do aluno - 1B-T1</p>
</footer>
```

## Dissertativa 2 - Seletores por classe e id

Resposta sugerida:

```html
<h2 id="titulo-principal">Agenda Cultural</h2>
<p class="destaque">Atividade na quarta-feira.</p>
<p class="destaque">Atividade na sexta-feira.</p>

<style>
  #titulo-principal {
    color: #1d4ed8;
  }

  .destaque {
    background-color: #eaf2ff;
    padding: 8px;
  }
</style>
```

## Dissertativa 3 - Box Model

Resposta sugerida:

```css
.bloco {
  padding: 16px;
  border: 2px solid #666666;
  margin-bottom: 12px;
  background-color: #f5f5f5;
}
```

```html
<div class="bloco">Primeiro aviso</div>
<div class="bloco">Segundo aviso</div>
```

## Dissertativa 4 - Banner com gradiente

Resposta sugerida:

```html
<header class="banner">
  <h1>Mostra Cultural</h1>
  <p>Arte e criatividade da turma.</p>
</header>

<style>
  .banner {
    background: linear-gradient(135deg, #2563eb, #0ea5e9);
    color: white;
    padding: 24px;
  }
</style>
```

## Dissertativa 5 - Float com texto

Resposta sugerida:

```css
.materia img {
  float: left;
  width: 180px;
  margin-right: 12px;
}
```

## Dissertativa 6 - Inline-block com tags

Resposta sugerida:

```css
.tag {
  display: inline-block;
  border: 1px solid #333333;
  padding: 4px 8px;
  margin-right: 6px;
}
```

## Observações de correção

- Aceitar variações de texto, desde que a estrutura pedida exista.
- Aceitar cores diferentes, mantendo a lógica do exercício.
- Aceitar pequenas variações de indentação e ordem de blocos.
- Priorizar a compreensão de semântica e propriedades CSS estudadas nas aulas 07 a 12.
