# Pipeline de Dados para Análise de Transações Bancárias

Este repositório contém o desenvolvimento de um *Minimum Viable Product (MVP)* de engenharia de dados voltado à análise de transações bancárias, realizado como parte da pós-graduação em Ciência de Dados na PUC-Rio.

O trabalho tem como foco a construção de um pipeline de dados em nuvem, contemplando as etapas de busca, coleta, modelagem, carga e análise dos dados, utilizando a plataforma Databricks e o formato Delta Lake, seguindo a arquitetura Bronze–Silver–Gold.

---

## Objetivo do Projeto

O objetivo do projeto é desenvolver um pipeline analítico completo e reprodutível para dados transacionais bancários, permitindo a exploração de padrões de comportamento financeiro e operacional.

A partir do dataset utilizado, o trabalho busca responder perguntas como:
- Como os valores das transações se distribuem ao longo do tempo?
- Existem padrões distintos de acordo com o tipo de transação e o canal utilizado?
- Quais variáveis operacionais estão mais associadas ao volume financeiro movimentado?
- Há indícios de risco operacional observáveis a partir das características das transações?

Mais do que responder a essas perguntas, o projeto busca demonstrar a aplicação de boas práticas de engenharia de dados em ambiente de nuvem.

---

## Conjunto de Dados

O dataset utilizado é público e está disponível neste repositório:

- **Arquivo:** `bank_transactions_data_2.csv`
- **Formato:** CSV
- **Conteúdo:** registros de transações bancárias com atributos financeiros, temporais, operacionais e demográficos.

O conjunto de dados não contém informações sensíveis ou identificáveis de indivíduos reais e é utilizado exclusivamente para fins educacionais.

---

## Arquitetura do Pipeline

O pipeline foi estruturado seguindo a arquitetura **Bronze–Silver–Gold**:

### 🔹 Bronze (Raw)
- Ingestão dos dados brutos exatamente como fornecidos pela fonte.
- Persistência em formato Delta Lake.
- Preservação da integridade e rastreabilidade dos dados.

### 🔹 Silver (Curated)
- Padronização de tipos de dados.
- Tratamento de datas, valores numéricos e colunas categóricas.
- Criação de atributos derivados.
- Preparação dos dados para análise e modelagem dimensional.

### 🔹 Gold (Analytics)
- Modelagem dimensional em esquema estrela.
- Estruturação de tabelas fato e dimensões.
- Base pronta para análises analíticas e exploração de indicadores.

---

## Modelagem de Dados

A modelagem foi realizada no formato **Esquema Estrela**, composta por:
- Tabela fato de transações;
- Dimensões de tempo, tipo de transação, canal, categoria e usuário.

Além da modelagem, foi construído um **Catálogo de Dados**, contendo:
- descrição dos atributos;
- tipos e domínios esperados;
- linhagem dos dados desde a fonte até as camadas analíticas.

---

## Análises Realizadas

A etapa de análise foi dividida em dois grandes blocos:

### Qualidade de Dados
- Avaliação de valores nulos, tipos inconsistentes e faixas inválidas.
- Discussão dos impactos desses problemas nas análises.
- Validação da consistência dos dados após o tratamento.

### Solução do Problema
- Análises exploratórias orientadas às perguntas de negócio.
- Interpretação dos resultados à luz do contexto transacional.
- Discussão integrada dos achados, destacando o papel de variáveis operacionais e temporais.

---

## Desafios

Durante o desenvolvimento do projeto, foram identificadas restrições técnicas no **Databricks Community Edition**, tais como:
- Limitação na leitura direta de arquivos via HTTP/HTTPS usando `spark.read.csv()`;
- Bloqueio de acesso ao sistema de arquivos local do driver;
- Desativação do DBFS público (`/FileStore`).

Diante dessas restrições, foi adotada uma solução técnica baseada no uso de **Volumes (Unity Catalog)** como área de aterrissagem (*landing zone*) dos dados. Essa abordagem permitiu manter o armazenamento em nuvem, garantir governança e assegurar a execução consistente do pipeline, transformando uma limitação da plataforma em uma decisão arquitetural consciente.

---

## Tecnologias Utilizadas:

- Databricks Community Edition
- Apache Spark
- Delta Lake
- Python (PySpark)
- GitHub

---

## Considerações Finais e Autoavaliação

O MVP desenvolvido atende aos requisitos propostos, contemplando de forma consistente todas as etapas exigidas para a construção de um pipeline de dados em nuvem: busca, coleta, modelagem, carga e análise. A solução implementada permitiu transformar um conjunto de dados bruto em uma base analítica estruturada, documentada e alinhada às boas práticas de engenharia de dados, utilizando a arquitetura Bronze–Silver–Gold.

Durante o desenvolvimento, um dos principais desafios enfrentados esteve relacionado às **limitações técnicas do Databricks Community Edition**, especialmente no que diz respeito à ingestão de dados diretamente a partir de fontes externas em nuvem. Foram realizadas tentativas de importação do dataset a partir de um **bucket no Amazon S3** e também via **Google Cloud Storage**, porém ambas as abordagens apresentaram restrições na versão Community da plataforma, impedindo a leitura direta dos dados por meio de URLs ou conectores nativos sem o uso de credenciais ou recursos pagos.

Essas limitações impactaram a estratégia inicial de ingestão, exigindo um maior aprofundamento na compreensão do ambiente do Databricks e levando à adoção de uma solução alternativa baseada no uso de **Volumes (Unity Catalog)** como área de aterrissagem dos dados. Essa decisão permitiu manter o armazenamento em nuvem, garantir governança, rastreabilidade e reprodutibilidade do pipeline, transformando uma restrição da plataforma em uma escolha arquitetural consciente.

Outro aspecto desafiador foi equilibrar o **rigor técnico da implementação** com a **clareza documental exigida pelo trabalho**, uma vez que o projeto demandou não apenas a execução do pipeline, mas também a explicitação das decisões de modelagem, dos processos de transformação e das análises realizadas. Esse esforço contribuiu significativamente para o amadurecimento da visão prática sobre engenharia de dados aplicada.

Apesar das dificuldades encontradas, os objetivos centrais do trabalho foram atingidos, e as perguntas de negócio definidas inicialmente puderam ser exploradas de forma coerente a partir das análises desenvolvidas. Como extensões futuras, o projeto poderia ser enriquecido com a integração de ferramentas de visualização (como Power BI ou Databricks SQL), automação do pipeline e aplicação de modelos analíticos ou preditivos sobre a camada Gold.

De forma geral, o desenvolvimento deste MVP consolidou o entendimento prático sobre pipelines de dados em nuvem e evidenciou a importância de adaptar soluções técnicas às restrições reais das plataformas utilizadas, reforçando a relevância de decisões arquiteturais bem fundamentadas no contexto de projetos de dados.


---

## Autor

**Júlio Cioffi**  
Projeto desenvolvido como parte da pós-graduação em Ciência de Dados – PUC-Rio.

