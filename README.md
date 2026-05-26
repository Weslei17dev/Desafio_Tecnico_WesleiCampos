# Desafio Técnico - Analista de Dados | ROQT DATA & AI

Este repositório contém a solução para o Desafio Técnico Prático do processo seletivo para a vaga de Analista de Dados (Assistente/Júnior) na ROQT DATA & AI.

## 📋 Contexto do Projeto

O projeto simula o dia a dia de um analista numa construtora de médio porte. O objetivo é processar dados exportados de um ERP em planilhas Excel e construir um relatório no Power BI que responda a perguntas estratégicas fundamentais sobre receitas, despesas e comportamento de fornecedores.

O desafio avalia habilidades práticas de raciocínio lógico, organização, e domínio técnico de ponta a ponta: desde a limpeza dos dados até à apresentação visual.

---

## 📁 Estrutura do Repositório

Com base na organização dos arquivos, o repositório contém:

* **Backgrounds/**: Imagens e recursos visuais utilizados para compor o layout do dashboard.
* **Dados/**: Arquivos originais em Excel (tabelas dimensão e fato) utilizados como fonte de dados.
* **Desafio_Tecnico_Power_BI_v2.docx**: Documento original com as instruções e requisitos do projeto.
* **Desafio_Tecnico_WesleiCampos.pbix**: Arquivo final do Power BI contendo o modelo de dados, ETL, medidas DAX e dashboards construídos.

---

## 🛠️ Etapas de Desenvolvimento

A solução foi desenvolvida seguindo as melhores práticas de Business Intelligence, dividida em quatro pilares principais:

### 1. Extração, Transformação e Carga (Power Query)
As bases de dados transacionais (Fato) apresentavam diversos problemas de qualidade que foram tratados:
* Conversão de valores monetários importados como texto com vírgula para formato numérico.
* Tratamento de datas armazenadas em formato de *string* (dd/mm/yyyy) para o tipo *Date*.
* Padronização de chaves identificadoras (IDs), removendo espaços extras e ajustando caracteres para maiúsculo (utilizando lógicas como `Text.Trim` e `Text.Upper`).
* Tratamento de registros duplicados e de IDs de fornecedores inválidos/inexistentes (como F099 e F999) e valores nulos.
* As tabelas de Dimensão (`d_Plano_de_Contas`, `d_Centro_de_Custo`, `d_Fornecedores`) foram utilizadas como referência limpa.

### 2. Modelagem de Dados (Star Schema)
O modelo foi construído no formato *Star Schema* (Estrela), posicionando as tabelas de movimentação (Fato) no centro e as tabelas de cadastro (Dimensão) ao redor. 
* **Relacionamentos:** Foram estabelecidos relacionamentos de "Muitos para Um (*:1)" entre as tabelas Fato (`f_Lancamentos`, `f_Notas_Fiscais`) e as tabelas Dimensão.

### 3. Cálculos e Regras de Negócio (DAX)
Criação de medidas explícitas para garantir flexibilidade analítica, evitando o uso excessivo de colunas calculadas. O destaque técnico é o cálculo do **Prazo Médio de Pagamento (PMP)** de 2026, que exigiu a elaboração de uma média ponderada baseada no valor da nota, e não uma média simples:

`PMP = Σ (Valor_NF × Prazo_em_Dias) / Σ (Valor_NF)`

*Regras aplicadas ao PMP:* Foram considerados apenas os dados de 2026, excluindo fornecedores sem cadastro, valores nulos e datas de vencimento vazias.

### 4. Visualização de Dados
O dashboard foi projetado para responder visualmente e de forma clara às seguintes perguntas de negócio estipuladas pelo desafio:
1. Qual plano de contas gerou a maior despesa total em janeiro de 2025?
2. Qual plano de contas gerou a maior receita total em janeiro de 2025?
3. Qual fornecedor apresenta o maior Prazo Médio de Pagamento (PMP) ao longo de todo o ano de 2026?
4. Qual o total de despesas por Centro de Custo em 2025?
5. Quantas notas fiscais foram emitidas por status de pagamento em 2026?
6. Qual segmento de fornecedor concentra mais despesas em 2025?
7. Qual UF de fornecedor possui mais notas fiscais em atraso em 2026?
8. Como evoluiu a receita vs. despesa mês a mês ao longo de 2025?

---

## 🚀 Como Executar

1. Faça o clone ou o download deste repositório.
2. Certifique-se de ter o **Power BI Desktop** gratuito instalado na sua máquina.
3. Abra o arquivo `Desafio_Tecnico_WesleiCampos.pbix` para interagir com os relatórios e visualizar as transformações no Power Query e medidas DAX.

---
*Desenvolvido por Weslei Campos.*
