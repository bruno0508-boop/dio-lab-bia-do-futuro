# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação pode ser feita de duas formas complementares:

1. **Testes estruturados:** Você define perguntas e respostas esperadas;
2. **Feedback real:** Pessoas testam o agente e dão notas.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu o que foi perguntado? | Perguntar o saldo e receber o valor correto |
| **Segurança** | O agente evitou inventar informações? | Perguntar algo fora do contexto e ele admitir que não sabe |
| **Coerência** | A resposta faz sentido para o perfil do cliente? | Sugerir investimento conservador para cliente conservador |

> [!TIP]
> Peça para 3-5 pessoas (amigos, família, colegas) testarem seu agente e avaliarem cada métrica com notas de 1 a 5. Isso torna suas métricas mais confiáveis! Caso use os arquivos da pasta `data`, lembre-se de contextualizar os participantes sobre o **cliente fictício** representado nesses dados.

---

## Exemplos de Cenários de Teste

Crie testes simples para validar seu agente:

### Teste 1: Consulta de gastos
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** Valor baseado no `transacoes.csv`
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 2: Recomendação de produto
- **Pergunta:** "Qual investimento você recomenda para mim?"
- **Resposta esperada:** Produto compatível com o perfil do cliente
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual a previsão do tempo?"
- **Resposta esperada:** Agente informa que só trata de finanças
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 4: Informação inexistente
- **Pergunta:** "Quanto rende o produto XYZ?"
- **Resposta esperada:** Agente admite que produtos de renda variável onde o rendimento depende diretamente da performance das empresas que compõem a carteira do fundo. Diferente da renda fixa, ele não possui uma taxa de retorno definida no momento da compra.
- **Resultado:** [x] Correto  [ ] Incorreto

---

## Resultados

Após os testes, registre suas conclusões:

**O que funcionou bem:**
- Adoção de Termos de Cautela: A transição para uma linguagem baseada em estimativas foi imediata. Agora, o modelo utiliza consistentemente termos como "é estimado", "com base nos atuais rendimentos" e "projeções", evitando afirmações deterministas sobre lucros futuros.

- Contextualização de Risco: O modelo passou a enfatizar que os valores podem aumentar ou diminuir devido às oscilações do mercado, cumprindo a regra de não garantir rentabilidade em ativos variáveis.

- Cruzamento de Dados Silencioso: A integração entre os arquivos enviados (perfil_investidor.json, produtos_financeiros.json) e o conhecimento técnico ocorreu de forma fluida, permitindo alertar sobre a inadequação de produtos de alto risco (como Fundo de Ações) para quem busca reserva de emergência, sem precisar citar explicitamente o nome do arquivo.

- Identidade do Usuário: O modelo respeitou a persona estabelecida nos arquivos (João Silva), mantendo a coerência com os objetivos financeiros descritos.

**O que pode melhorar:**
- Aprofundamento de Cenários: Embora a cautela tenha sido aplicada, o modelo pode detalhar um pouco mais quais fatores de mercado causam essas oscilações (como Selic, inflação ou resultados corporativos) para educar o usuário enquanto mantém a linguagem estimativa.

-Comparativos de Volatilidade: Poderíamos incluir exemplos históricos de oscilação (quedas e altas passadas) para materializar o conceito de que "os valores podem diminuir", tornando o alerta de risco menos abstrato.

---

## Métricas Avançadas (Opcional)

Para quem quer explorar mais, algumas métricas técnicas de observabilidade também podem fazer parte da sua solução, como:

- Latência e tempo de resposta;
- Consumo de tokens e custos;
- Logs e taxa de erros.

Ferramentas especializadas em LLMs, como [LangWatch](https://langwatch.ai/) e [LangFuse](https://langfuse.com/), são exemplos que podem ajudar nesse monitoramento. Entretanto, fique à vontade para usar qualquer outra que você já conheça!
