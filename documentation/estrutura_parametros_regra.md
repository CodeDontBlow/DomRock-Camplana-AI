# Estrutura de Parâmetros da Regra (Task A6-16)

Documentação de contrato de dados entre Frontend, Backend e Agente de IA para a extração, edição e validação dos parâmetros das regras de comissionamento.

---

## 1. Dicionário de Metadados

| Campo (key) | Rótulo (label) | Tipo (type) | Valores Aceitos |
| :--- | :--- | :--- | :--- |
| `periodo` | Prazo da Campanha | `date_range` | Formato `YYYY-MM-DD` |
| `pct_acrescimo` | Acréscimo de Comissão (%) | `percentage` | Decimal (ex: `1.0` = +1%) |
| `marcas_alvo` | Marcas Participantes | `multi_select` | Tabela marca (`10`, `20`, `30`, `40`, `50`, `60`, `ALL`) |
| `cargos_alvo` | Cargos Elegíveis | `multi_select` | Tabela cargo (`100`, `150_LOJA`, `150_QUIOSQUE`, `200`, `300`) |
| `canal` | Canal de Venda | `select` | `TODOS`, `LOJA`, `BALCAO` |
| `meta_vendas` | Meta Financeira (R$) | `currency` | Valor monetário em R$ |
| `orcamento_limite` | Orçamento Máximo (R$) | `currency` | Teto financeiro em R$ |

---

## 2. MOCK JSON

```json
{
  "rule_id": "draft-bf-2025-11",
  "raw_prompt": "Todas as vendas no período de 24/11 a 30/11 terão um acréscimo no % de comissão de +1%.",
  "status": "DRAFT_PENDING_REVIEW",
  "rule_parameters": [
    {
      "key": "periodo",
      "label": "Prazo da Campanha",
      "type": "date_range",
      "value": {
        "data_inicio": "2025-11-24",
        "data_fim": "2025-11-30"
      },
      "required": true
    },
    {
      "key": "pct_acrescimo",
      "label": "Acréscimo de Comissão (%)",
      "type": "percentage",
      "value": 1.0,
      "required": true
    },
    {
      "key": "marcas_alvo",
      "label": "Marcas Participantes",
      "type": "multi_select",
      "value": ["ALL"],
      "options": [
        { "id": "ALL", "label": "Todas as Marcas" },
        { "id": "10", "label": "PRETO (10)" },
        { "id": "20", "label": "BRANCO (20)" },
        { "id": "30", "label": "AZUL (30)" },
        { "id": "40", "label": "VERMELHO (40)" }
      ],
      "required": true
    },
    {
      "key": "cargos_alvo",
      "label": "Cargos Elegíveis",
      "type": "multi_select",
      "value": ["100", "200", "300"],
      "options": [
        { "id": "100", "label": "VENDEDOR LOJA" },
        { "id": "150_LOJA", "label": "GERENTE DE LOJA" },
        { "id": "150_QUIOSQUE", "label": "GERENTE QUIOSQUE" },
        { "id": "200", "label": "VENDEDOR BALCAO" },
        { "id": "300", "label": "ASSISTENTE DE VENDAS" }
      ],
      "required": true
    },
    {
      "key": "canal",
      "label": "Canal de Venda",
      "type": "select",
      "value": "TODOS",
      "options": [
        { "id": "TODOS", "label": "Todos os Canais" },
        { "id": "LOJA", "label": "Loja Física" },
        { "id": "BALCAO", "label": "Balcão" }
      ],
      "required": true
    }
  ],
  "simulation_constraints": [
    {
      "key": "meta_vendas",
      "label": "Meta Financeira da Campanha (R$)",
      "type": "currency",
      "value": null,
      "required": true
    },
    {
      "key": "orcamento_limite",
      "label": "Orçamento Máximo de Incentivo (R$)",
      "type": "currency",
      "value": null,
      "required": true
    }
  ]
}