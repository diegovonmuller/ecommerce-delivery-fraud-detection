# Detecção de Fraudes em Entregas — Walmart E-commerce (Flórida Central)

Projeto final do curso de Data Science — análise de fraude em entregas de e-commerce.

## Contexto

O Walmart identificou um crescimento nas perdas por furto vindas de compras feitas via e-commerce, em que consumidores relatam não receber todos os itens de seus pedidos — mesmo com a entrega marcada como concluída no sistema. Este projeto analisa dados de entregas na região Central da Flórida para identificar padrões e anomalias que ajudem a apontar a origem do problema.

Três hipóteses foram testadas:

1. **Fraude do entregador (motorista)** — item não entregue, mas registrado como entregue
2. **Erro de sistema ou processo** — falha no registro, não necessariamente fraude intencional
3. **Fraude do consumidor** — cliente declara não ter recebido item que na verdade recebeu, buscando reembolso

## Metodologia

- **10.000 pedidos** analisados
- **1.502 fraudes** identificadas — taxa geral de **15,02%**
- Workbook Excel com 9 abas de análise (`ecommerce_fraud_sheets_v2.xlsx`), incluindo teste qui-quadrado de significância estatística
- Dashboard interativo construído no Tableau Public com 5 visualizações

## Principais achados

### Região — não é um fator relevante
A variação entre as 7 regiões analisadas é pequena (13,89% a 16,20%). Altamonte Springs tem a maior taxa, Sanford a menor, mas a diferença de apenas ~2,3 pontos percentuais não sustenta a região como driver de fraude.

### Horário — não é um fator relevante
Existe um pico visível às 22h (19,16%) e um vale às 16h (11,72%), mas a oscilação ao longo do dia não é estatisticamente significativa isoladamente.

### Motoristas — nenhum outlier estatístico
A taxa de fraude individual máxima é de 36,36%, mas **227 motoristas diferentes** empatam nesse valor — sinal claro de baixo volume de entregas (efeito de amostra pequena), não de comportamento fraudulento isolado. O z-score máximo observado na base é **1,98**, abaixo do limiar de 3,0 usado para classificar um outlier. A fraude está distribuída de forma homogênea entre os ~1.247 motoristas analisados — não concentrada em "maçãs podres".

### Idade do motorista — o único fator estatisticamente significativo
**χ² = 79,78, p < 0,000001**

A taxa de fraude sobe de forma quase linear conforme a idade do motorista aumenta:

| Faixa etária | Taxa de fraude |
|---|---|
| 18 anos | 9,17% |
| 19-25 | 13,03% |
| 26-35 | 17,19% |
| 36-50 | 17,34% |
| 50+ | 18,13% |

Esse achado contraria a intuição comum de que motoristas mais jovens representariam maior risco — os dados mostram o oposto. Cruzando idade com horário do dia (heatmap), confirmamos que esse padrão se repete em todos os turnos, descartando a hipótese de que o efeito seria apenas reflexo de motoristas mais velhos trabalharem nos horários de pico.

### Produtos — impacto financeiro concentrado em eletrônicos
Itens como fones Bose QuietComfort, PlayStation 5 e Beats Studio Pro representam uma fração pequena do volume total de furtos, mas concentram a maior parte do valor financeiro perdido (mais de $8.000 só em fones Bose).

## Conclusão

Os dados sustentam a hipótese de **fraude do entregador** como o fator mais relevante para explicar as perdas em entregas de e-commerce nesta região, com a **idade do motorista** como variável preditiva central. Região, horário do dia e perfil individual de motoristas específicos não se mostraram fatores relevantes.

## Dashboard

Dashboard interativo disponível no Tableau Public: https://public.tableau.com/app/profile/diego.von.muller/viz/DetecodeFraudesEntregas/DetecodeFraudesemEntregas-10_000pedidos#1

## Dados

Workbook completo com as 9 abas de análise: `ecommerce_fraud_sheets_v2.xlsx`
