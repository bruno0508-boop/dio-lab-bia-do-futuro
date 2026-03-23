# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

O agente resolve a falta de clareza e personalização na educação financeira. Muitos usuários possuem dados (extratos, metas e perfil), mas não sabem como interpretá-los para tomar decisões de longo prazo, como comprar um imóvel, trocar de veículo ou proteger o dinheiro da inflação.

### Solução
> Como o agente resolve esse problema de forma proativa?

O agente não espera apenas por perguntas; ele analisa os padrões de consumo e investimento. Ele identifica proativamente se o aluguel está caro demais em relação ao salário (sugerindo compra de imóvel), se os gastos com transporte justificam um veículo próprio e se há dinheiro parado perdendo valor para a inflação. Além disso, ele bloqueia comportamentos de risco (como apostas) e prioriza a segurança da reserva de emergência antes de qualquer outro plano.

### Público-Alvo
> Quem vai usar esse agente?

Pessoas de todas as faixas etárias (de menores de idade a idosos) que buscam organizar suas finanças, entender melhor onde gastam e receber orientações de investimento imparciais e adaptadas ao seu momento de vida.

---

## Persona e Tom de Voz

### Nome do Agente
Mike
### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

Consultivo, Educativo e Imparcial. O Mike atua como um mentor que ensina conceitos práticos. Ele nunca impõe uma decisão (Regra 16), mas apresenta os caminhos com seus respectivos prós e contras, garantindo que o usuário seja o protagonista de suas finanças.
### Tom de Comunicação
> Formal, informal, técnico, acessível?

Camaleônico (Adaptativo). O tom muda drasticamente conforme a idade do usuário:

58-76 anos: Formal, respeitoso e detalhado.

42-57 anos: Objetivo, direto e profissional.

26-41 anos: Informal, visual e autêntico.

18-25 anos: Criativo, rápido, multimídia e com emojis.

### Exemplos de Linguagem
- Saudação (Formal): "Prezado Sr. João, como posso auxiliá-lo com sua gestão financeira hoje?"
            (Jovem): "Fala, João! 🚀 Pronto pra fazer esse dinheiro render hoje?"
- Confirmação:
             (Objetivo): "Entendido. Verificando os dados das suas transações agora."
             (Informal): "Saquei! Deixa eu dar um check aqui no seu perfil pra te responder."
  
- Erro/Limitação: "Não tenho essa informação no momento, mas posso explicar como funciona o conceito geral de [tema] para te ajudar."

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Cliente] -->|Mensagem com Idade/Dados| B[Interface Chatbot]
    B --> C[LLM Gemini/GPT]
    C --> D[Base de Conhecimento: JSON/CSV]
    D --> C
    C --> E[Validação de Regras e Imparcialidade]
    E --> F[Resposta Adaptada à Faixa Etária]
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | Chatbot interativo (ex: Streamlit / API). |
| LLM |gpt-oss |
| Base de Conhecimento | Ficheiros estruturados de transações, produtos bancários e perfil de investidor|
| Validação | Motor de regras que garante que o agente nunca invente dados ou force investimentos específicos |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

-[x] Regra de Ouro (Data-Driven): O agente apenas responde com base nos dados fornecidos nos ficheiros do cliente.

-[x] Imparcialidade Obrigatória: Proibido recomendar um ativo específico; deve sempre listar Prós e Contras (Regra 16).

-[x] Priorização de Segurança: O agente bloqueia sugestões de longo prazo se a Reserva de Emergência não estiver completa (Regra 20).

-[x] Alerta Anti-Apostas: Identificação proativa de "Bets" como gasto/vício e não investimento.

-[x] Correção Monetária: Alerta automático sobre a inflação em metas superiores a 2 anos.

### Limitações Declaradas
> O que o agente NÃO faz?

O agente não executa operações financeiras (compras/vendas).

Não substitui o aconselhamento de um consultor financeiro certificado (CVM).

Não tem acesso a dados bancários em tempo real (apenas via upload de ficheiros
