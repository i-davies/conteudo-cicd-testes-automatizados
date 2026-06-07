# Gabarito da Revisão para Prova Prática

> Material de apoio do professor. Não publicar para os alunos.

## Implementação sugerida

Arquivo sugerido: `app/atendimento/pontuacao.py`

```python
def calcular_pontuacao_atendimento(tempo_minutos, resolvido_primeiro_contato, reincidencia):
    if tempo_minutos <= 0:
        return 0

    if resolvido_primeiro_contato:
        if tempo_minutos <= 10:
            base = 10
        elif tempo_minutos <= 20:
            base = 8
        else:
            base = 6
    else:
        if tempo_minutos <= 10:
            base = 5
        elif tempo_minutos <= 20:
            base = 3
        else:
            base = 1

    if reincidencia:
        base -= 2

    return max(base, 0)


def classificar_atendimento(pontuacao):
    if pontuacao >= 9:
        return "Excelente"
    if pontuacao >= 7:
        return "Bom"
    if pontuacao >= 4:
        return "Regular"
    return "Crítico"
```

## Testes sugeridos

Arquivo sugerido: `tests/atendimento/test_pontuacao.py`

```python
from app.atendimento.pontuacao import (
    calcular_pontuacao_atendimento,
    classificar_atendimento,
)


def test_retorna_zero_para_tempo_invalido_zero():
    assert calcular_pontuacao_atendimento(0, True, False) == 0


def test_retorna_zero_para_tempo_invalido_negativo():
    assert calcular_pontuacao_atendimento(-3, False, True) == 0


def test_resolvido_ate_10_sem_reincidencia():
    assert calcular_pontuacao_atendimento(10, True, False) == 10


def test_resolvido_entre_11_e_20_sem_reincidencia():
    assert calcular_pontuacao_atendimento(11, True, False) == 8


def test_resolvido_limite_20_sem_reincidencia():
    assert calcular_pontuacao_atendimento(20, True, False) == 8


def test_resolvido_acima_20_com_reincidencia():
    assert calcular_pontuacao_atendimento(21, True, True) == 4


def test_nao_resolvido_ate_10_sem_reincidencia():
    assert calcular_pontuacao_atendimento(10, False, False) == 5


def test_nao_resolvido_entre_11_e_20_com_reincidencia():
    assert calcular_pontuacao_atendimento(15, False, True) == 1


def test_nao_resolvido_limite_20_sem_reincidencia():
    assert calcular_pontuacao_atendimento(20, False, False) == 3


def test_nao_resolvido_acima_20_com_reincidencia_minimo_zero():
    assert calcular_pontuacao_atendimento(25, False, True) == 0


def test_classificacao_excelente():
    assert classificar_atendimento(10) == "Excelente"


def test_classificacao_bom():
    assert classificar_atendimento(8) == "Bom"


def test_classificacao_regular():
    assert classificar_atendimento(5) == "Regular"


def test_classificacao_critico():
    assert classificar_atendimento(2) == "Crítico"


def test_fluxo_completo_resultado_excelente():
    pontuacao = calcular_pontuacao_atendimento(10, True, False)
    resultado = classificar_atendimento(pontuacao)
    assert resultado == "Excelente"


def test_fluxo_completo_resultado_bom():
    pontuacao = calcular_pontuacao_atendimento(11, True, False)
    resultado = classificar_atendimento(pontuacao)
    assert resultado == "Bom"


def test_fluxo_completo_resultado_regular():
    pontuacao = calcular_pontuacao_atendimento(10, False, False)
    resultado = classificar_atendimento(pontuacao)
    assert resultado == "Regular"


def test_fluxo_completo_resultado_critico():
    pontuacao = calcular_pontuacao_atendimento(25, False, True)
    resultado = classificar_atendimento(pontuacao)
    assert resultado == "Crítico"
```

## Resultado esperado

- Todos os testes devem passar com `uv run pytest -v`.
- Os alunos podem variar nomes dos testes, desde que cubram todos os caminhos de decisão.
- Recomenda-se validar também o fluxo completo: calcular pontuação e depois classificar o resultado.
