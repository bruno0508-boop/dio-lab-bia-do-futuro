# Base de Conhecimento

## Dados Utilizados

Descreva se usou os arquivos da pasta `data`, por exemplo:

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores, ou seja, dar continuidade ao atendimento de forma mais eficiente.|
| `perfil_investidor.json` | JSON | Personalizar as explicações sobre as dúvidas e necessidades de aprendizado do cliente.|
| `produtos_financeiros.json` | JSON | Conhecer os produtos disponíveis para que eles possam ser ensinados ao cliente.|
| `transacoes.csv` | CSV |Analisar padrão de gastos do cliente e usar essas informações de forma didática. |

> [!TIP]
> **Quer um dataset mais robusto?** Você pode utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

A base de dados original de produtos financeiros foi expandida para incluir opções de crédito estruturado: Financiamento Imobiliário (SFH) e Financiamento de Veículo (CDC). A inclusão desses ativos permite que o motor de recomendação avalie não apenas oportunidades de investimento, mas também soluções de crédito personalizadas, baseando-se no perfil de risco, fluxo de caixa e histórico de gastos do investidor.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.
Existem duas possibilidades, injetar os dados diretamente no prompt (Ctrl + C, Ctrl + V) ou carregar os arquivos via código, como no exemplo abaixo:
```

import pandas as pd
import json

# =========== CARREGAR DADOS ===========
perfil = json.load(open('./data/perfil_investidor.json'))
transacoes = pd.read_csv('./data/transacoes.csv')
historico = pd.read_csv('./data/historico_atendimento.csv')
produtos = json.load(open('./data/produtos_financeiros.json'))
```

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Para simplificar, podemos simplesmente "injetar" os dados em nosso prompt, garantindo que o Agente tenha o melhor contexto possível. Lembrando que, em soluções mais robustas, o ideal é que essas informações sejam carregadas dinamicamente para que possamos ganhar flexibilidade
```
{
  "nome": "João Silva",
  "idade": 32,
  "profissao": "Analista de Sistemas",
  "renda_mensal": 5000.00,
  "perfil_investidor": "moderado",
  "objetivo_principal": "Construir reserva de emergência",
  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "aceita_risco": false,
  "metas": [
    {
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06"
    },
    {
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12"
    }
  ]
}
```
---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

O exemplo de contexto montado abaixo se baseia nos dados originais da base de conhecimento, mas os sintetiza deixando apenas as informações mais relevantes, otimizando assim o consumo de tokens. Entretanto, vale lembrar que mais importante do que economizar tokens, é ter todas as informações relevantes disponíveis em seu contexto
```
DADOS DO CLIENTE:
- Nome: João Silva
- Perfil: Moderado
- Objetivo: Construir reserva de emergência
- Reserva atual: R$ 10.000 (meta: R$ 15.000)

RESUMO DE GASTOS:
- Moradia: R$ 1.380
- Alimentação: R$ 570
- Transporte: R$ 295
- Saúde: R$ 188
- Lazer: R$ 55,90
- Total de saídas: R$ 2.488,90

PRODUTOS DISPONÍVEIS PARA EXPLICAR:
- Tesouro Selic (risco baixo)
- CDB Liquidez Diária (risco baixo)
- LCI/LCA (risco baixo)
- Fundo Imobiliário - FII (risco médio)
- Fundo de Ações (risco alto)
- Financiamento Imobiliário - SFH (Crédito)
- Financiamento de Veículo - CDC (Crédito)
...
```
