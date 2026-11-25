# AdventureWorks — Dashboard Analítico com Power BI

Projeto acadêmico desenvolvido para a **Demonstração de Competência**, com foco na construção de um dashboard analítico utilizando o **AdventureWorks Data Warehouse**, Microsoft SQL Server e Power BI.

O projeto aplica conceitos de:

- construção de KPIs;
- modelagem dimensional;
- análise de dados;
- dashboards interativos;
- Data Storytelling;
- interpretação de indicadores para apoio à tomada de decisão.

---

## Objetivo

Desenvolver um dashboard no **Power BI** utilizando a base **AdventureWorksDW2025**, contendo no mínimo **10 indicadores de negócio relevantes** para acompanhar o desempenho das vendas e apoiar análises sobre produtos, clientes, períodos e territórios.

O dashboard foi estruturado para permitir uma navegação do panorama geral para análises específicas de produtos, clientes e geografia, mantendo filtros sincronizados entre as páginas analíticas.

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

O projeto utiliza diretamente o Data Warehouse AdventureWorks armazenado no SQL Server.

```text
AdventureWorksDW2025
        │
        ▼
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

A tabela fato principal utilizada no projeto é:

```text
dbo.FactInternetSales
```

Ela contém os registros das vendas realizadas pela Internet e fornece as medidas utilizadas nos principais indicadores do dashboard.

---

# Modelo analítico

O escopo do projeto está concentrado no processo de **vendas pela Internet**.

A tabela fato principal é:

```text
FactInternetSales
```

Ela registra os itens dos pedidos e contém informações como:

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

As dimensões fornecem contexto para análises por período, cliente, produto e território.

---

## Tabelas utilizadas no modelo final

### Tabela fato

```text
FactInternetSales
```

Responsável pelos eventos de venda e pelas medidas utilizadas nos indicadores.

### Dimensão de tempo

```text
DimDate
```

Permite análises por ano, trimestre, mês e dia.

### Dimensão de clientes

```text
DimCustomer
```

Contém informações utilizadas nas análises de clientes, incluindo país, ocupação e dados de identificação do cliente.

### Dimensão de produtos

```text
DimProduct
```

Concentra os atributos utilizados nas análises de produto, incluindo produto, categoria e subcategoria.

### Dimensão de território de vendas

```text
DimSalesTerritory
```

Fornece contexto territorial para as análises geográficas e comerciais.

---

# Estrutura dimensional

O modelo final foi organizado com a tabela `FactInternetSales` no centro das análises e as dimensões relacionadas diretamente à fato.

```text
                     DimDate
                        │
                        │
                        ▼
DimCustomer ───── FactInternetSales ───── DimProduct
                        │
                        ▼
                DimSalesTerritory
```

Essa organização facilita o uso das medidas DAX e mantém uma estrutura dimensional simples para as análises realizadas no Power BI.

---

# KPIs e medidas desenvolvidas

O requisito do trabalho era possuir no mínimo **10 indicadores relevantes**.

A versão final utiliza os seguintes indicadores principais:

1. **Receita Total**
2. **Lucro Bruto**
3. **Margem Bruta %**
4. **Ticket Médio**
5. **Crescimento da Receita YoY %**
6. **Itens Vendidos**
7. **Receita Média por Item**
8. **Clientes Ativos**
9. **Receita por Cliente**
10. **Quantidade de Pedidos**

Também foram utilizadas medidas auxiliares, como:

- **Receita Ano Anterior**
- **Estado/Província Líder**

A medida de Receita Média por Item foi definida como:

```DAX
Receita Média por Item =
DIVIDE(
    [Receita Total],
    [Itens Vendidos],
    0
)
```

---

# Estrutura final do dashboard

O relatório foi organizado em cinco páginas.

## 1. Capa

Página inicial com identidade visual do projeto e identificação do aluno.

## 2. Visão Geral

Apresenta uma visão executiva do desempenho comercial.

### KPIs

- Receita Total
- Ticket Médio
- Crescimento YoY
- Margem Bruta
- Lucro Bruto

### Análises

- Evolução da Receita
- Receita Atual x Ano Anterior
- Receita por Categoria
- Receita por País

A análise temporal possui drill-down:

```text
Ano → Trimestre → Mês → Dia
```

---

## 3. Análise de Produtos

Página dedicada ao desempenho de categorias, subcategorias e produtos.

### KPIs

- Receita Total
- Lucro Bruto
- Margem Bruta
- Itens Vendidos

### Análises

- Receita por Categoria
- Principais Subcategorias por Receita
- Principais Produtos por Receita
- Receita Média por Item x Margem Bruta

O gráfico de dispersão utiliza:

```text
Eixo X  → Receita Média por Item
Eixo Y  → Margem Bruta %
Tamanho → Itens Vendidos
Detalhe → Produto
```

Também foram adicionadas linhas médias nos dois eixos para facilitar a identificação de produtos com:

- alto valor médio e alta margem;
- alto valor médio e baixa margem;
- baixo valor médio e alta margem;
- baixo valor médio e baixa margem.

O segmentador de Categoria utiliza o filtro:

```text
Receita Total > 0
```

Isso impede a exibição de categorias sem vendas no contexto analisado.

---

## 4. Análise de Clientes

Página dedicada ao perfil e comportamento da base de clientes.

### KPIs

- Ticket Médio
- Clientes Ativos
- Receita por Cliente
- Quantidade de Pedidos

### Análises

- Principais Clientes por Receita
- Receita por Ocupação

Os eixos foram formatados de acordo com a escala de cada análise para evitar unidades inadequadas.

---

## 5. Análise Geográfica

Página voltada à análise territorial das vendas.

### KPIs

- Estado/Província Líder
- Receita Total

### Análises

- Principais Cidades por Receita
- Receita x Lucro por Estado/Província
- Receita por Região

O mapa utiliza hierarquia geográfica e informações adicionais em tooltip, como:

- Receita Total
- Lucro Bruto
- Margem Bruta %
- Clientes Ativos

---

# Interatividade

O dashboard utiliza segmentadores sincronizados entre as páginas analíticas.

Os principais filtros globais são:

- **Ano**
- **País**

Também há sincronização de **Categoria** entre as páginas em que esse filtro é relevante.

Dessa forma, uma seleção realizada em uma página pode ser mantida durante a navegação pelo relatório, preservando o mesmo contexto de análise.

Além disso, o dashboard utiliza:

- drill-down temporal;
- tooltips;
- filtros entre visuais;
- segmentadores;
- formatação condicional;
- linhas médias em gráfico de dispersão.

---

# Data Storytelling

A estrutura das páginas foi organizada para construir uma sequência analítica:

```text
Visão Geral
    ↓
Produtos
    ↓
Clientes
    ↓
Geografia
```

A narrativa busca responder às seguintes perguntas:

- Como está o desempenho geral das vendas?
- Como a receita evolui ao longo do tempo?
- Quais categorias, subcategorias e produtos apresentam maior desempenho?
- Como valor médio, margem e volume se relacionam entre os produtos?
- Quem são os principais clientes?
- Quais perfis de clientes concentram maior receita?
- Quais países, estados e cidades apresentam maior desempenho comercial?

O objetivo é transformar os dados em informações úteis para apoiar a tomada de decisão.

---

# Etapas do projeto

## Fase 1 — Ambiente e entendimento do AdventureWorksDW

**Status:** ✅ Concluída

- restauração e validação do AdventureWorksDW2025;
- validação da `FactInternetSales`;
- conexão do Power BI ao SQL Server;
- seleção inicial das tabelas;
- análise das dimensões e fato.

## Fase 2 — Modelagem de Dados no Power BI

**Status:** ✅ Concluída

- tratamento das tabelas no Power Query;
- revisão dos tipos de dados;
- validação dos relacionamentos;
- organização do modelo dimensional;
- configuração da dimensão de tempo;
- criação de hierarquias;
- validação do modelo final.

## Fase 3 — Definição dos KPIs

**Status:** ✅ Concluída

- definição dos indicadores;
- validação da relevância de cada KPI;
- organização das medidas de negócio.

## Fase 4 — Medidas DAX

**Status:** ✅ Concluída

- criação das medidas;
- testes dos cálculos;
- validação dos resultados;
- criação de comparativos temporais e medidas auxiliares.

## Fase 5 — Dashboard

**Status:** ✅ Concluída

- criação das cinco páginas;
- definição da identidade visual;
- construção dos gráficos;
- criação dos segmentadores;
- sincronização de filtros;
- configuração de drill-down;
- configuração de tooltips;
- revisão de escalas, unidades e formatação.

## Fase 6 — Análise e Data Storytelling

**Status:** ✅ Concluída

- organização da sequência analítica das páginas;
- análise de produtos, clientes e geografia;
- criação de comparativos;
- refinamento do gráfico de dispersão;
- revisão da experiência de navegação.

---

# Estrutura do repositório

```text
adventureworks-powerbi-dashboard/
│
├── docs/
│   └── documentação e evidências do projeto
│
├── powerbi/
│   └── AdventureWorks_Dashboard.pbix
│
├── screenshots/
│   └── evidências das etapas e páginas do dashboard
│
└── README.md
```

---

# Critérios do trabalho

O projeto foi desenvolvido considerando os seguintes aspectos:

- construção de KPIs relevantes;
- qualidade visual e organização do dashboard;
- usabilidade e interatividade;
- análise dos dados;
- geração de insights;
- aplicação de Data Storytelling.

A versão final possui mais de 10 métricas e indicadores, identidade visual consistente e quatro perspectivas analíticas principais: visão geral, produtos, clientes e geografia.

---

# Entrega

Principal arquivo do projeto:

```text
AdventureWorks_Dashboard.pbix
```

Status atual:

```text
Projeto concluído e pronto para entrega.
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
