# 🛒 Sistema de Recomendação — Regras de Associação (Apriori)

Sistema de recomendação de produtos baseado em **Market Basket Analysis** (Análise de Cesta de Compras), utilizando o algoritmo **Apriori** para descobrir padrões de associação entre itens frequentemente comprados juntos.

> Desenvolvido como trabalho de Engenharia da Informação — aplica um dos algoritmos clássicos de sistemas de recomendação, usado até hoje por varejistas (o clássico exemplo "quem compra X também compra Y").

---

## 📌 O problema

Dado um histórico de transações de um supermercado (cada linha representa os itens comprados por um cliente em uma única compra), o objetivo é identificar **regras de associação** — padrões do tipo:

> *"Clientes que compram **pão** e **manteiga** também tendem a comprar **leite**, com 40% de confiança."*

Essas regras podem ser usadas para recomendação de produtos, otimização de layout de loja, ou campanhas de cross-sell.

## 🧠 Como funciona o algoritmo Apriori

O Apriori encontra **itemsets frequentes** (conjuntos de produtos que aparecem juntos com frequência mínima) e, a partir deles, gera **regras de associação** com duas métricas principais:

- **Suporte**: com que frequência o conjunto de itens aparece no total de transações.
- **Confiança**: dado que o cliente comprou o item A, qual a probabilidade de também comprar o item B.

O algoritmo funciona de forma iterativa: começa encontrando itens individuais frequentes, depois combina pares, depois trios, e assim por diante — descartando a cada passo combinações que não atingem o suporte mínimo (princípio de poda que torna o algoritmo eficiente mesmo com muitos produtos).

## 📂 Dataset

O projeto utiliza o dataset **Groceries** (`groceries.csv`), contendo transações reais de compras de supermercado, onde cada linha é uma cesta de compras com múltiplos itens.

## 🚀 Como executar

```bash
python3 main.py -f groceries.csv -c 0.3 -s 0.01
```

| Parâmetro | Significado |
|---|---|
| `-f` | Caminho do arquivo CSV com as transações |
| `-c` | Confiança mínima para gerar uma regra (ex: `0.3` = 30%) |
| `-s` | Suporte mínimo para considerar um itemset frequente (ex: `0.01` = 1% das transações) |

**Pré-requisitos:** Python 3.x

## 📊 Saída esperada

O programa imprime as regras de associação encontradas, no formato:

```
{item_A, item_B} -> {item_C}   suporte: 0.015   confiança: 0.42
```

Cada regra indica que clientes que compraram os itens do lado esquerdo tendem a comprar também o item do lado direito, com a confiança e suporte calculados.

## 🛠️ Stack

- Python
- Implementação própria do algoritmo Apriori (`apriori.py`)

## 🔭 Possíveis evoluções

- Migrar para bibliotecas otimizadas (`mlxtend`, `efficient-apriori`) para datasets maiores
- Adicionar métrica de **lift** além de suporte/confiança, para medir a força real da associação (não só a co-ocorrência)
- Construir uma interface simples para consulta interativa das regras
- Aplicar o mesmo princípio a dados de e-commerce reais para recomendação em tempo real
