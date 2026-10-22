# AdventureWorks — Dashboard Analítico com Power BI

Projeto acadêmico desenvolvido para a **Demonstração de Competência**, com foco na construção de um dashboard analítico utilizando o **AdventureWorks Data Warehouse**, Microsoft SQL Server e Power BI.

O projeto tem como objetivo aplicar conceitos de:

- construção de KPIs;
- modelagem dimensional;
- análise de dados;
- dashboards interativos;
- Data Storytelling;
- interpretação de indicadores para apoio à tomada de decisão.

---

## Objetivo

Desenvolver um dashboard no **Power BI** utilizando a base **AdventureWorksDW2025**, contendo no mínimo **10 indicadores de negócio relevantes**, capazes de apresentar o desempenho das vendas e apoiar análises sobre produtos, clientes, períodos e territórios.

Além da construção do dashboard, o projeto contempla a identificação de insights e a preparação de uma apresentação individual utilizando conceitos de **Data Storytelling**.

---

## Tecnologias utilizadas

- **Microsoft SQL Server 2025**
- **SQL Server Management Studio — SSMS**
- **AdventureWorksDW2025**
- **Microsoft Power BI Desktop**
- **Power Query**
- **DAX**
- **Git**
- **GitHub**

---

## Arquitetura

O projeto utiliza diretamente o Data Warehouse oficial do AdventureWorks armazenado no SQL Server.

```text
AdventureWorksDW2025
      SQL Server
          │
          │ Importação
          ▼
      Power Query
          │
          │ Tratamento
          ▼
     Modelo Power BI
          │
          ├── Relacionamentos
          ├── Medidas DAX
          ├── KPIs
          └── Hierarquias
          │
          ▼
       Dashboard
          │
          ▼
  Insights e Storytelling
```

---

## Fonte de dados

A base utilizada é:

```text
AdventureWorksDW2025
```

O banco foi restaurado localmente no SQL Server e validado antes da conexão com o Power BI.

Durante a validação foi confirmado que a tabela principal de vendas:

```text
dbo.FactInternetSales
```

possui:

```text
60.398 registros
```

---

# Modelo analítico

O escopo do projeto está concentrado no processo de **vendas pela Internet**.

A tabela fato principal é:

```text
FactInternetSales
```

Ela registra os itens dos pedidos realizados pela Internet e contém medidas importantes como:

```text
OrderQuantity
UnitPrice
ExtendedAmount
DiscountAmount
ProductStandardCost
TotalProductCost
SalesAmount
TaxAmt
Freight
```

Também possui chaves para relacionamento com as dimensões de produto, cliente, tempo e território.

---

## Tabelas utilizadas

Foram selecionadas oito tabelas do AdventureWorksDW2025.

### Tabela fato

```text
FactInternetSales
```

Responsável por armazenar os eventos de venda e os valores utilizados para os principais indicadores.

### Dimensão de tempo

```text
DimDate
```

Permite análises por data, mês, trimestre, ano e ano fiscal.

### Dimensão de clientes

```text
DimCustomer
```

Contém informações sobre gênero, renda, estado civil, educação, ocupação, número de filhos, quantidade de veículos e data da primeira compra.

### Dimensão geográfica

```text
DimGeography
```

Permite analisar clientes por país, estado ou província, cidade, código postal e território comercial.

### Dimensão de produtos

```text
DimProduct
```

Contém informações sobre produto, custo, preço, cor, tamanho, modelo e subcategoria.

### Subcategoria de produtos

```text
DimProductSubcategory
```

Permite organizar os produtos em níveis intermediários, como Mountain Bikes, Road Bikes, Touring Bikes, Helmets e Tires and Tubes.

### Categoria de produtos

```text
DimProductCategory
```

As principais categorias presentes no banco são Bikes, Components, Clothing e Accessories.

### Território de vendas

```text
DimSalesTerritory
```

Permite analisar o desempenho comercial por região, país e agrupamento territorial.

---

# Estrutura dimensional

```text
                           DimDate
                              │
                              │
                              ▼
DimCustomer ──────── FactInternetSales ──────── DimProduct
     │                        │                       │
     │                        │                       ▼
     ▼                        ▼             DimProductSubcategory
DimGeography          DimSalesTerritory              │
                                                    ▼
                                           DimProductCategory
```

A estrutura combina características de **Star Schema** e **Snowflake Schema**.

A tabela `FactInternetSales` permanece no centro das análises, enquanto as dimensões fornecem contexto para responder perguntas como quando ocorreu a venda, quem realizou a compra, onde o cliente está localizado, qual produto foi comprado, a qual categoria ele pertence e em qual território ocorreu a venda.

---

# Indicadores planejados

O dashboard deverá possuir pelo menos dez KPIs:

1. **Receita Total**
2. **Lucro Bruto**
3. **Margem Bruta %**
4. **Quantidade de Pedidos**
5. **Ticket Médio**
6. **Unidades Vendidas**
7. **Clientes Únicos**
8. **Taxa de Clientes Recorrentes**
9. **Crescimento de Receita YoY**
10. **Prazo Médio de Envio**

Os indicadores poderão ser refinados durante a etapa de implementação das medidas DAX.

---

# Estrutura planejada do dashboard

## 1. Visão Executiva

Principais indicadores: Receita, Lucro, Margem, Pedidos e Ticket médio.

Análises: evolução temporal, receita por categoria e desempenho por território.

## 2. Produtos e Clientes

Análises previstas: produtos com maior receita, categorias e subcategorias, quantidade vendida, clientes únicos, perfil dos clientes, comportamento de compra e distribuição geográfica.

## 3. Tendências e Desempenho

Análises previstas: crescimento anual, comparação entre períodos, evolução de receita, evolução de margem, desempenho territorial e prazo de envio.

---

# Data Storytelling

Além de apresentar os indicadores, o dashboard será utilizado para construir uma narrativa baseada nos dados, buscando responder perguntas como:

- Como está o desempenho geral da empresa?
- As vendas estão crescendo?
- Quais produtos geram mais receita?
- Quais categorias apresentam maior participação?
- Quais territórios apresentam melhor desempenho?
- Quem são os principais clientes?
- Existem oportunidades de crescimento?
- Quais decisões podem ser tomadas a partir desses dados?

O objetivo não é apenas apresentar gráficos, mas transformar os resultados em **insights capazes de apoiar decisões de negócio**.

---

# Etapas do projeto

## Fase 1 — Ambiente e entendimento do AdventureWorksDW

**Status:** ✅ Concluída

Atividades realizadas:

- restauração e validação do AdventureWorksDW2025;
- confirmação do banco no SQL Server;
- validação da `FactInternetSales`;
- conexão do Power BI ao SQL Server;
- seleção das tabelas;
- análise inicial das dimensões e fato.

## Fase 2 — Modelagem de Dados no Power BI

**Status:** 🚧 Em desenvolvimento

Atividades:

- revisar e preparar as tabelas no Power Query;
- carregar os dados;
- validar relacionamentos;
- organizar o modelo dimensional;
- configurar cardinalidades e filtros;
- preparar dimensão de tempo;
- criar hierarquias;
- validar o modelo final.

## Fase 3 — Definição dos KPIs

**Status:** ⬜ Não iniciada

- revisar os indicadores;
- definir fórmulas;
- justificar cada KPI;
- relacionar indicadores às necessidades do negócio.

## Fase 4 — Medidas DAX

**Status:** ⬜ Não iniciada

- criação das medidas;
- testes dos cálculos;
- validação dos resultados.

## Fase 5 — Dashboard

**Status:** ⬜ Não iniciada

- construção das páginas;
- definição da identidade visual;
- filtros;
- segmentações;
- interatividade;
- drill-down.

## Fase 6 — Análise e Data Storytelling

**Status:** ⬜ Não iniciada

- identificação de padrões;
- geração de insights;
- análise de oportunidades;
- elaboração das recomendações;
- construção da narrativa.

## Fase 7 — Apresentação e defesa

**Status:** ⬜ Não iniciada

- preparação da apresentação;
- roteiro de Data Storytelling;
- revisão dos conceitos;
- preparação para arguição.

---

# Estrutura do repositório

```text
adventureworks-powerbi-dashboard/
│
├── docs/
│   └── Ambiente e entendimento do AdventureWorksDW/
│       ├── relatórios/
│       └── documentação/
│
├── powerbi/
│   └── AdventureWorks_Dashboard.pbix
│
├── screenshots/
│   └── evidências das etapas
│
└── README.md
```

A estrutura poderá ser ampliada conforme o desenvolvimento das próximas fases.

---

# Critérios avaliativos

| Critério | Pontuação |
|---|---:|
| Construção dos KPIs | 6,0 |
| Desenvolvimento do Dashboard | 6,0 |
| Análise e Insights | 5,0 |
| Data Storytelling e Apresentação | 5,0 |
| Defesa do Projeto | 3,0 |
| **Total** | **25,0** |

---

# Entrega

Prazo considerado para o projeto:

```text
25/11/2026 — 18:00
```

Principal arquivo de entrega:

```text
AdventureWorks_Dashboard.pbix
```

---

# Referências

- Microsoft Learn — AdventureWorks Sample Databases  
  https://learn.microsoft.com/sql/samples/adventureworks-install-configure

- Microsoft Learn — Star Schema no Power BI  
  https://learn.microsoft.com/power-bi/guidance/star-schema

- Microsoft Learn — Conector SQL Server no Power Query  
  https://learn.microsoft.com/power-query/connectors/sql-server

- Microsoft Learn — Power BI  
  https://learn.microsoft.com/power-bi/

- Microsoft SQL Server Samples — AdventureWorks  
  https://github.com/microsoft/sql-server-samples

---

## Autor

**Phablo Correia**

Projeto desenvolvido para fins acadêmicos utilizando o AdventureWorks Data Warehouse, SQL Server e Microsoft Power BI.
