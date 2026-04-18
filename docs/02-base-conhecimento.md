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

Os dados foram expandidos para separar gastos Pessoais (PF) de gastos do Negócio (PJ). Adicionei um campo de "Categoria MEI" no perfil para que o agente saiba exatamente qual imposto aplicar e quais deduções são permitidas por lei.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Os arquivos JSON de regras fiscais e o CSV de fluxo de caixa são carregados no início da sessão. O sistema realiza uma leitura prévia para calcular o saldo disponível para "pro-labore" antes de iniciar a interação com o usuário.

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Os dados são inseridos dinamicamente no system prompt. Se o saldo de caixa estiver próximo do valor do DAS (imposto), o agente recebe uma instrução de prioridade para alertar o usuário sobre esse compromisso antes de qualquer outra sugestão de gasto.

---

## Exemplo de Contexto Montado

> Aqui está como o "Mestre Fortunato" enxerga a situação antes de falar com o empreendedor:

```
Dados do Microempreendedor:
- Nome: Ricardo (Marceneiro)
- Categoria: MEI - Serviços
- Saldo em Conta PJ: R$ 3.200,00
- Meta: Comprar Serra de Bancada (R$ 1.500,00)

Últimas Movimentações:
- 10/04: Entrada - Venda Armário Planejado: + R$ 1.200,00
- 12/04: Saída - Material de Madeira: - R$ 450,00
- 15/04: Saída - Conta de Luz Residencial (ALERTA PF): - R$ 180,00

Lembretes Fiscais:
- Vencimento DAS: Dia 20 (R$ 70,60) - Status: Pendente.
...
```
