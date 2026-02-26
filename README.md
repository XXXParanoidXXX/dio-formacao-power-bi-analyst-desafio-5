# 📊 Power BI – Modelo Star Schema (Financial Sample)

Este repositório contém a implementação de um **modelo dimensional em estrela (Star Schema)** desenvolvido no **Power BI**, a partir da tabela única **Financial Sample**, conforme proposto no desafio de projeto.

O objetivo principal é demonstrar **boas práticas de modelagem dimensional**, organização de tabelas fato e dimensões, além do uso de **DAX** para criação de tabelas de apoio e métricas analíticas.

---

## 🧠 Visão Geral do Projeto

* Fonte de dados: **Financial Sample** (tabela única)
* Ferramenta: **Power BI Desktop**
* Modelo: **Star Schema (Esquema em Estrela)**
* Foco:

  * Separação entre fatos e dimensões
  * Redução de redundância
  * Melhor desempenho analítico
  * Base sólida para criação de dashboards

---

## 🗂️ Estrutura do Modelo Dimensional

A partir da tabela original, foram criadas as seguintes tabelas:

### 🔹 Tabela de Origem (Backup)

* **financials_origem**

  * Cópia da tabela Financial Sample
  * Mantida em modo *oculto*
  * Usada como base para construção das demais tabelas

---

### 🔹 Tabela Fato

#### **F_Vendas**

Tabela central do modelo, responsável por armazenar os eventos de negócio (vendas).

Campos principais:

* SK_ID
* ID_Produto
* Produto
* Units Sold
* Sale Price
* Discount Band
* Segment
* Country
* Sales
* Profit
* Date

Essa tabela concentra os valores numéricos analisáveis e se relaciona com todas as dimensões.

---

### 🔹 Tabelas Dimensão

#### **D_Produtos**

Dimensão agregada de produtos, criada por meio de agrupamentos.

Campos:

* ID_Produto
* Produto
* Média de Unidades Vendidas
* Média do Valor de Vendas
* Mediana do Valor de Vendas
* Valor Máximo de Venda
* Valor Mínimo de Venda

---

#### **D_Produtos_Detalhes**

Dimensão com atributos descritivos dos produtos.

Campos:

* ID_Produto
* Discount Band
* Sale Price
* Units Sold
* Manufacturing Price

---

#### **D_Descontos**

Dimensão voltada às informações de descontos.

Campos:

* ID_Produto
* Discount
* Discount Band

---

#### **D_Detalhes**

Dimensão complementar criada para armazenar informações que **não foram contempladas nas demais dimensões**, mas que enriquecem a análise de vendas.

Campos incluem:

* Sales
* COGS
* Country
* Date
* Discount Band
* Discounts
* Gross Sales
* Manufacturing Price
* Month Name / Number
* Product
* Profit
* Segment
* Units Sold
* Year

---

#### **D_Calendário**

Tabela de datas criada utilizando **DAX**, essencial para análises temporais.

Exemplo de criação:

```DAX
D_Calendario = CALENDAR ( DATE(2013,1,1), DATE(2015,12,31) )
```

A partir dessa tabela, podem ser derivados:

* Ano
* Mês
* Nome do mês
* Trimestre
* Indicadores de tempo (YTD, MTD, YoY)

---

## 🔗 Relacionamentos

* Modelo em estrela com a **F_Vendas** no centro
* Relacionamentos do tipo **1 : N** entre dimensões e fato
* Direção de filtro simples (Dimensão → Fato)
* Tabela de origem mantida desconectada

---

## 🧮 Funcionalidades e Recursos DAX Utilizados

Durante o projeto, foram aplicados os seguintes conceitos e funções DAX:

* Criação de tabelas calculadas (`CALENDAR`)
* Agregações:

  * `SUM`
  * `AVERAGE`
  * `MEDIAN`
  * `MAX`
  * `MIN`
* Uso de colunas condicionais
* Criação de índices por lógica condicional
* Separação clara entre **medidas** e **colunas calculadas**

Esses recursos permitem análises dinâmicas e dashboards mais robustos.

---

## 🖼️ Evidências do Projeto

O repositório inclui:

* 📁 Arquivo **.pbix** do Power BI
* 🖼️ Imagem do **modelo Star Schema**
* 📝 Este **README**, documentando o processo de construção

---

## 🎯 Objetivo Educacional

Este projeto foi desenvolvido com foco em:

* Aprendizado de **modelagem dimensional**
* Organização de projetos Power BI para portfólio
* Aplicação prática de **DAX**
* Boas práticas para ambientes analíticos e corporativos

---

## 🚀 Considerações Finais

O modelo em estrela facilita a leitura, manutenção e escalabilidade do projeto, além de ser amplamente utilizado em ambientes profissionais de BI.

Este repositório pode servir como:

* Referência de estudo
* Base para novos projetos
* Demonstração técnica para recrutadores

---

📌 *Sugestões e melhorias são bem-vindas!*
