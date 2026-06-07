# Gabarito - Revisão para Prova Prática

> Este gabarito apresenta uma solução possível para o relatório da revisão.

---

## Solução do desafio 2: consulta integradora principal

Consulta única solicitada no enunciado:

```sql
USE bd2_revisao_prova_pratica;

SELECT
    tecnico_responsavel,
    setor,
    status_chamado,
    canal_abertura,
    modalidade_atendimento,
    prioridade,
    horas_execucao,
    custo_pecas,
    data_abertura
FROM chamados_revisao
WHERE setor IN ('Infraestrutura', 'Desenvolvimento', 'Dados', 'Suporte')
  AND status_chamado <> 'Cancelado'
  AND horas_execucao BETWEEN 2 AND 14
  AND prioridade IN ('Alta', 'Media')
  AND (
      canal_abertura IN ('Portal', 'Email')
      OR (canal_abertura = 'Telefone' AND prioridade = 'Alta')
  )
  AND (
      (modalidade_atendimento = 'Remoto' AND sla_horas <= 12)
      OR (modalidade_atendimento = 'Presencial' AND custo_pecas <= 350)
  )
ORDER BY
    setor ASC,
    data_abertura DESC,
    horas_execucao DESC;
```

---

## Validação opcional do resultado final

```sql
USE bd2_revisao_prova_pratica;

SELECT COUNT(*) AS total_linhas
FROM chamados_revisao
WHERE setor IN ('Infraestrutura', 'Desenvolvimento', 'Dados', 'Suporte')
  AND status_chamado <> 'Cancelado'
  AND horas_execucao BETWEEN 2 AND 14
  AND prioridade IN ('Alta', 'Media')
  AND (
      canal_abertura IN ('Portal', 'Email')
      OR (canal_abertura = 'Telefone' AND prioridade = 'Alta')
  )
  AND (
      (modalidade_atendimento = 'Remoto' AND sla_horas <= 12)
      OR (modalidade_atendimento = 'Presencial' AND custo_pecas <= 350)
  );
```

Resultado esperado do relatório: `9` linhas.

---

## Checklist de conferência

- [x] Executei a base da revisão sem erros.
- [x] Montei a consulta integradora principal com todas as regras.
- [x] Apliquei corretamente as duas regras compostas.
- [x] Usei parênteses para controlar a precedência lógica.
- [x] Apliquei `ORDER BY` com mais de um critério.
- [x] Conferi se o resultado final retorna `9` linhas.
