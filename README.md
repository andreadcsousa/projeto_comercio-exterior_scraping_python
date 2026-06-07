# 📊 Automação e Análise de Dados do Comércio Exterior

Este projeto consiste em uma solução automatizada para a coleta, extração e análise preliminar de dados brutos sobre **Importação e Exportação** do comércio exterior brasileiro. Utilizando técnicas de *web scraping* e manipulação de dados com Python, o pipeline faz a ingestão direta de bases governamentais e as consolida em estruturas prontas para consumo analítico.

## 🎯 Objetivo de Negócio e Engenharia

Muitas análises estratégicas de comércio exterior dependem do portal oficial de dados abertos. No entanto, o download manual frequente dessas planilhas e bases brutas gera gargalos e erros operacionais. 

Esta solução automatiza o processo ao:
1. Mapear dinamicamente a página de estatísticas de base de dados bruta do governo.
2. Identificar e extrair os arquivos de dados mais recentes de movimentações comerciais (`.csv`).
3. Fazer o download automatizado e salvar diretamente em um ambiente de nuvem integrado (Google Drive).
4. Padronizar, tipar e enriquecer os conjuntos de dados para facilitar a criação posterior de dashboards (como Power BI ou Tableau).

## 🏗️ Arquitetura do Pipeline

O fluxo de dados segue uma estrutura linear e resiliente:
`Portal Gov.br (HTML) ➔ Web Scraping (BeautifulSoup) ➔ Ingestão Automática (.csv) ➔ Armazenamento Nuvem (Google Drive) ➔ Processamento & Padronização (Pandas DataFrame)`

## 💻 Tecnologias e Bibliotecas Utilizadas

* **Python 3.10+** (Linguagem base do projeto)
* **Requests:** Para realizar requisições HTTP seguras e baixar as bases de dados volumosas.
* **BeautifulSoup4:** Para analisar a estrutura HTML das páginas web e capturar os links dinâmicos de download de forma automatizada.
* **Pandas:** Para manipulação estruturada das tabelas, aplicação de filtros, conversão de tipos e criação de colunas derivadas.
* **OS & Google Colab Suite:** Para automação e integração de diretórios locais e em nuvem.

## 📁 Estrutura dos Dados Coletados

Os arquivos baixados e lidos de forma estruturada contam com as seguintes informações-chave do Siscomex/eSocial:

* `CO_ANO` / `CO_MES`: Período de referência da movimentação.
* `CO_NCM`: Código da Nomenclatura Comum do Mercosul (identificação do produto).
* `SG_UF_NCM`: Unidade Federativa (Estado) de origem/destino da carga.
* `KG_LIQUIDO`: Peso total das mercadorias.
* `VL_FOB`: Valor da mercadoria em Dólar Comercial (Free on Board).
* `VL_FRETE` / `VL_SEGURO`: Indicadores de custos logísticos (específicos de Importação).
* `TP_CARGA`: Atributo derivado criado via código para segmentar os registros (`Importação` ou `Exportação`).

## ▶️ Como Reproduzir o Projeto

### Pré-requisitos
Certifique-se de ter instalado as dependências necessárias listadas em seu ambiente local ou utilize o Google Colab:

```bash
pip install requests beautifulsoup4 pandas
```

### Passos de Execução

- **Montar o Drive (Opcional):** Caso use o ambiente do Google Colab, execute a primeira célula para vincular seu armazenamento.
- **Mapeamento e Download:** O script acessa a URL oficial de dados brutos e realiza a busca pelos seletores CSS para encontrar os arquivos desejados (Ex: EXP_2022.csv e IMP_2022.csv).
- **Tratamento de Dados:** Os dados salvos são convertidos em estruturas Pandas através da definição correta do delimitador (no caso, sep=";"), e recebem a inserção da coluna discriminatória de carga.

### Próximos Passos (Roadmap)

[ ] Unificar os DataFrames de importação e exportação utilizando junções adequadas via Pandas (pd.concat / merge).  
[ ] Criar um dicionário de dados cruzando as tabelas auxiliares do eSocial e da NCM para traduzir os códigos numéricos em descrições textuais amigáveis.  
[ ] Desenvolver um dashboard interativo integrado para visualização de balança comercial e análise espacial por estado (SG_UF_NCM).
