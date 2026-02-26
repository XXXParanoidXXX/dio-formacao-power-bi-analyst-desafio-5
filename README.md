📊 Power BI – Modelo Star Schema (Financial Sample)
Este repositório contém a implementação de um modelo dimensional em estrela (Star Schema) desenvolvido no Power BI, a partir da tabela única Financial Sample, conforme proposto no desafio de projeto.
O objetivo principal é demonstrar boas práticas de modelagem dimensional, separação entre tabelas fato e dimensões, criação de uma dimensão de tempo robusta via DAX e organização do modelo para garantir escalabilidade e performance.

🧠 Visão Geral do Projeto
Fonte de dados: Financial Sample (tabela única)
Ferramenta: Power BI Desktop
Modelo: Star Schema (Esquema em Estrela)
Foco:

Estruturação da Fact Table e Dimensions
Redução de redundância e consistência de atributos
Uso de DAX para construção de tabelas auxiliares
Boa arquitetura de dados para Dashboards profissionais
Inclusão de uma Dimensão de Tempo completa (D_Tempo)


🗂️ Estrutura do Modelo Dimensional
A partir da tabela única original, foram criadas as seguintes tabelas:

🔹 Tabela de Origem (Backup)
financials_origem

Cópia da tabela Financial Sample
Mantida oculta
Utilizada como base de derivação para Fato e Dimensões


🔹 Tabela Fato
F_Vendas
Tabela central do modelo, contendo os registros de vendas.
Campos principais:

SK_ID
ID_Produto
Produto
Units Sold
Sale Price
Discount Band
Segment
Country
Sales
Profit
Date

Essa tabela se relaciona com todas as dimensões segundo o formato tradicional do Star Schema.

🔹 Tabelas Dimensão

D_Produtos
Dimensão agregada de produtos, construída por agrupamento.
Campos:

ID_Produto
Produto
Média de Unidades Vendidas
Média do Valor de Vendas
Mediana do Valor de Vendas
Valor Máximo de Venda
Valor Mínimo de Venda


D_Produtos_Detalhes
Dimensão com atributos descritivos dos produtos.
Campos:

ID_Produto
Discount Band
Sale Price
Units Sold
Manufacturing Price


D_Descontos
Dimensão de descontos.
Campos:

ID_Produto
Discount
Discount Band


D_Detalhes
Dimensão complementar para campos adicionais da origem.
Inclui, por exemplo:

Sales
COGS
Country
Date
Gross Sales
Product
Segment
Profit
Units Sold
Year
Month Name / Number


⭐ D_Tempo (Nova Dimensão de Tempo Completa)
A antiga D_Calendario foi substituída por uma tabela de tempo muito mais completa e aderente às boas práticas de Data Warehousing.
📅 O que é a D_Tempo?
É a dimensão de calendário utilizada para análises temporais e cálculos de time intelligence.
Ela é construída totalmente em DAX utilizando CALENDAR() + colunas derivadas.
✔ Principais atributos:

Date (chave natural)
DateKey no formato AAAAMMDD
Ano, Semestre, Trimestre
Mês (nome, número, abreviação)
Ano-Mês (chave e texto)
Dia do mês
Dia da semana (nome e número)
Início e fim de períodos (mês, trimestre, ano)
Flags (EhFimDeSemana, EhHoje)
Semana ISO (sem uso de ISOWEEKNUM, implementada manualmente)

SemanaISO
AnoISO
AnoSemanaISO (AAAAWW)



🛠 Como a tabela é criada?
A tabela é construída por meio de DAX, via:

Power BI → Modelagem → Nova Tabela

E inclui lógica customizada para suportar ambientes que não possuem a função ISOWEEKNUM.

🧩 Ajustes recomendados após criação:

Classificar colunas

MesNome → por MesNumero
MesNomeAbrev → por MesNumero
DiaSemanaNome → por DiaSemanaNumero
AnoMes → por AnoMesKey


Marcar como Tabela de Datas

Modelagem → Marcar como tabela de datas → selecionar Date



Essa tabela substitui completamente a antiga D_Calendario e atende padrões profissionais de BI.

🔗 Relacionamentos

Estrutura em estrela com F_Vendas no centro
Relacionamentos 1:N entre cada dimensão e a Fato
Direção de filtro: única (Dimensões → Fato)
Tabela de origem permanece desconectada


🧮 Funcionalidades e Recursos DAX Utilizados
✔ Criação de tabelas calculadas via DAX

CALENDAR
Campos derivados com YEAR, MONTH, FORMAT, etc.
Lógica avançada de Semana ISO sem ISOWEEKNUM

✔ Agregações

SUM, AVERAGE, MEDIAN, MAX, MIN

✔ Recursos adicionais

Colunas condicionais
Índices lógicos
Separação entre medidas e colunas calculadas


🖼️ Evidências do Projeto

📁 Arquivo .pbix
🖼️ Imagem do modelo Star Schema
📝 Este README atualizado


🎯 Objetivo Educacional
O projeto foi desenvolvido para reforçar:

Práticas sólidas de modelagem dimensional
Construção de modelos profissionais para portfólio
Uso avançado de DAX
Boas práticas em análise de dados corporativa


🚀 Considerações Finais
A inclusão da tabela D_Tempo torna o modelo muito mais robusto, escalável e aderente aos padrões modernos de BI.
Este repositório serve como:

Referência para estudo
Base para novos modelos
Portfólio profissional para recrutadores


📌 Sugestões e melhorias são bem‑vindas!
