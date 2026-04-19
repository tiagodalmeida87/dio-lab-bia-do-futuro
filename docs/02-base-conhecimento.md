# Base de Conhecimento

## Dados Utilizados

Para o Mestre Fortunato ser assertivo, ele precisa olhar para a saúde do negócio de forma holística, identificando padrões de comportamento e obrigações fiscais do MEI.

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `fluxo_caixa_mei.csv` | CSV | Analisar entradas, saídas e identificar o lucro real do mês |
| `guia_servicos_das.json` | JSON | Consultar alíquotas e vencimentos do imposto DAS conforme a categoria (Comércio/Serviço) |
| `metas_crescimento.json` | JSON | Personalizar conselhos sobre quando investir em novos equipamentos ou estoque |
| `historico_mentorias.csv` | CSV | Contextualizar conversas anteriores e lembretes de pendências financeiras |



---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Os dados foram significativamente expandidos para simular o cenário real de um MEI prestador de serviços (marcenaria) durante um período de dois meses. Foram inseridos intencionalmente "ruídos" financeiros, como o pagamento de gastos pessoais (iFood, Netflix, Conta de Água Residencial) utilizando a conta da empresa (PJ), para testar a capacidade do agente de alertar sobre confusão patrimonial. Além disso, o arquivo fiscal foi enriquecido com regras sobre limite de faturamento e a declaração anual (DASN-SIMEI), e as metas passaram a incluir a construção contínua de uma "Reserva de Emergência".

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Os arquivos JSON e CSV são carregados e pré-processados na inicialização da sessão. O sistema realiza um cruzamento prévio: soma os valores já reservados no metas_crescimento.json e os subtrai do saldo positivo gerado no fluxo_caixa_mei.csv, calculando o verdadeiro "caixa livre" antes de o agente iniciar a interação com o usuário.

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

O contexto processado é injetado dinamicamente no system prompt. O histórico de mentorias atua como um "gatilho" de atenção: se o historico_mentorias.csv relata um alerta recente sobre mistura de contas e o fluxo_caixa_mei.csv mostra uma nova transação suspeita, o Mestre Fortunato recebe uma instrução de prioridade para abordar essa falha logo na saudação inicial, antes de responder a outras dúvidas.

---

## Exemplo de Contexto Montado

> Aqui está como o "Mestre Fortunato" enxerga a situação antes de falar com o empreendedor:

```
Dados do Microempreendedor:
- Nome: Ricardo (Marceneiro)
- Categoria: MEI - Serviços
- Status Financeiro Atual: Caixa Positivo, mas com indícios de confusão patrimonial recente.

Metas em Andamento:
- Parafusadeira Profissional: R$ 350,00 guardados (Meta: R$ 850,00) - Status: Quase na metade!
- Reserva de Emergência: R$ 100,00 guardados (Meta: R$ 3.000,00) - Status: Iniciado.

Últimas Movimentações (Maio/2024):
- 20/05: Entrada - Parcela Gabinete de Banheiro: + R$ 600,00 (Conta PJ)
- 22/05: Saída - Reserva para Meta (Parafusadeira): - R$ 200,00 (Conta PJ)
- 28/05: Saída - Compra de EPI: - R$ 65,00 (Conta PJ)
- 30/05: Saída - Fundo de Emergência: - R$ 100,00 (Conta PJ)

Histórico e Alertas Críticos (Baseado no histórico de mentorias):
- ALERTA COMPORTAMENTAL: Usuário utilizou cartão PJ para iFood e Netflix recentemente. Reforçar necessidade de Pró-labore.
- ALERTA FISCAL: O prazo da Declaração Anual (DASN-SIMEI) encerra dia 31 de maio. Perguntar se ele já somou o faturamento.
...
```
