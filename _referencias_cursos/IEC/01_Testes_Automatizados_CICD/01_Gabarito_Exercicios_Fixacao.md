## Gabarito - Exercícios de Fixação

### Fácil - Unitário
```python
@pytest.mark.unit
def test_nao_subiu_de_nivel_no_mesmo_nivel():
    assert subiu_de_nivel(1000, 1000) is False
```

### Moderado - Integração
```python
import time


@pytest.mark.integration
def test_desafio_inexistente_retorna_incorreta(client):
    response = client.post(
        "/responder",
        data={
            "resposta": "qualquer_resposta",
            "desafio_id": 9999,
            "timestamp": str(time.time()),
        },
    )

    assert response.status_code == 200
    assert "Incorreta" in response.text
    assert "+" not in response.text
    assert "XP" not in response.text
```

### Difícil - E2E
```python
@pytest.mark.e2e
def test_fluxo_erro_e_retorno_para_novo_desafio(page):
    pg, url = page

    pg.goto(url)
    assert pg.locator("#pergunta").is_visible()
    assert pg.locator("#resposta").is_visible()
    assert pg.locator("#enviar").is_visible()

    pg.fill("#resposta", "resposta_totalmente_errada_xyz")
    pg.click("#enviar")

    pg.wait_for_selector("#resultado")
    conteudo = pg.text_content("#resultado")
    assert "Incorreta" in conteudo

    pg.click("a.next-btn")
    pg.wait_for_selector("#pergunta")
    assert pg.locator("#resposta").is_visible()
    assert pg.locator("#enviar").is_visible()
```
