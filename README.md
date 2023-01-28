# Projeto BI Status Construções

Esta documentação irá detalhar as etapas a serem executadas para o desenvolvimento do projeto de BI dentro da Empresa Status Construções como projeto piloto para serem replicadas para as outras empresas que compõe o Grupo Status.

## A empresa
A Status Construções é uma construtora e incorporadora que atua desde 2002 no mercado imobiliária da região metropolitana de Belém.

## Sistemas utilizados
* ERP - Sienge
* CRM - Construtor de vendas

## Objetivo do projeto
Utilizar estrategicamente os dados da Status Construções a partir da coleta, tratamento e análise de todo e qualquer tipo de informação relevante, possibilitando as melhores decisões para os negócios da empresa.

## Etapa 1 – Coleta dos dados e área a ser analisada
A primeira etapa será coletar e analisar os dados que são gerados com a utilização do Sienge no almoxarifado do canteiro de obras, onde há um grande volume de entrada e saída de material para execução das obras da empresa.

## API Sienge
O Sienge possuí APIs que são baseadas em HTTP RESTful, sendo assim, o body e resposta das requisições são formatadas em JSON.

## URL E requisições

Além de realizar a autenticação com o usuário e senha no momento da requisição às APIs, é necessário informar o seu sub domínio que identifica qual será o cliente Sienge que receberá a requisição. Essa informação irá complementar a url para qual será realizada chamada na API.

Exemplo:

`https://api.sienge.com.br/{subdonimio-do-cliente}/public/api/{versão-da-api}/{recurso}`

Exemplo:

* Subdomínio do Cliente: minhaempresa.sienge.com.br
* Versão da API: v1
* Recurso: examples

URL Final: `https://api.sienge.com.br/minhaempresa/public/api/v1/examples`

## APIs a serem analisadas
`/stock-inventories/{costCenterId}/items`

* Esta API retorna um array contendo informações atuais de todos os insumos que estão no estoque do centro de custo em que é requisitado.

`/building-cost-estimations/{buildingId}/resource-units-of-movement`

* Retona um array com as unidades de movimentos dos insumos da obra.

## Como será feita a extração e consulta dos dados

Iremos criar fluxos de dados dentro do Workspace no serviço do Power Bi que irá armazenas os dados que serão extraídos das APIs acima citadas.

https://learn.microsoft.com/pt-br/power-bi/transform-model/dataflows/dataflows-create#create-a-dataflow-by-using-linked-tables
