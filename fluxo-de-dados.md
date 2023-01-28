# Criação de Fluxo de Dados com Tabela Vinculada

Ao criarmos um fluxo de dados usando tabelas vinculadas permite fazer referência a uma tabela existente, definida em outro fluxo de dados, de forma somente leitura.

Desta forma iremos ganhar na eficiência na requisição dos dados evitando a criação de várias atualizações em uma fonte de dados, será melhor usar tabelas vinculadas para armazenar os dados e servir como um cache. Isso permite que todos os consumidores subsequentes usem essa tabela, reduzindo a carga para a fonte de dados subjacente.

> ***Obs: As tabelas vinculadas só estão disponíveis no Power BI Premium.***

Ao final do processo de criação do fluxo de dados a linhagem dos dados ficará conforme a imagem a seguir.

![image](https://user-images.githubusercontent.com/82005568/215267234-2ca99951-2909-4821-9094-6bce1a7009bc.png)

## Veja na prática como fazer:

Dentro do Workspace do projeto você irá clicar em **Novo > Fluxo de dados**

![image](https://user-images.githubusercontent.com/82005568/215260742-b35d4460-94f3-4500-a9ac-841823b3fef6.png)

Na página a seguir você irá visualizar o quandro Definir novas tabelas e você irá clicar em **Adicionar nova tebal**

![image](https://user-images.githubusercontent.com/82005568/215260988-3e4d97ac-124e-47bd-9dc1-ecf27e7ea6ab.png)

Agora chegamos na etapa onde irá escolher a fonte de dados para realizar a conexão. Você irá clicar em **Outro > Consulta em branco**.

![image](https://user-images.githubusercontent.com/82005568/215261444-c6b2a043-5243-4126-9528-220488b1fbd2.png)

Agora na tela a seguir iremos realizar a conexão na API do Sienge para extrair os dados e logo em seguida convertermos em tabela.

No repositório [Conexão API Sienge](https://github.com/gleydsonms2/conexoes-power-bi/blob/main/api_sienge.md) disponibilizo os códigos prontos de algumas APIs que já realizam todo o processo de conexão, extração e tratamento dos dados.

![image](https://user-images.githubusercontent.com/82005568/215262868-8ffe1b68-0338-4f6f-9d44-94e98f360146.png)

Após copiar o código da conexão desejada em [Conexão API Sienge](https://github.com/gleydsonms2/conexoes-power-bi/blob/main/api_sienge.md), você irá apagar o código inicial que você viu na imagem anterior e colará o código da API que você irá realizar a conexão ficando examente conforme a imagem a seguir e após, cliar em **Próximo**.

![image](https://user-images.githubusercontent.com/82005568/215263018-33909903-37f7-4ae0-9bef-830e4f87f790.png)

Agora entramos na etapa em que é necessário configurar nossa conexão com a API informando as credenciais de Login e Senha e para isso você irá clicar em **Configurar conexão**.

![image](https://user-images.githubusercontent.com/82005568/215263798-53c59f44-9bd3-4428-b237-e625309dfed4.png)

Na tela **Digitar as credenciais** você irá selecionar o Tipo de autenticação que será Básica, Login e Senha de acesso a logo em seguida irá clicar em **Conectar**.
![image](https://user-images.githubusercontent.com/82005568/215263920-73b7eedf-22ec-4893-8197-dc568d578a0f.png)

Após conexão ter sido estabelecida e as informações virem em formato de tabela, Faz necessário renomearmos a tabela para que o projeto fique organizadas e de fácil edificação.

Será necessário clicar com o botão direito do mouse e clicar em renomear.

![image](https://user-images.githubusercontent.com/82005568/215264697-09de6137-4cb7-48c3-9769-1c1ca560c1da.png)

Observe que nesta primeira etapa do processo, iremos somente carregar os dados da API dentro do dataflow e certificarmos de transformar todas as colunas em texto. Nesta etapa, aplicamos o mínimo de transformações possíveis, assim exigimos da API somente o carregamento de dados.
```
Obs: É importante transformar em texto todas as colunas, pois o Power Query do dataflow não entende direito os campos do tipo any.
```
Após certificarmos de que todas as colunas foram transformadas em texto, você irá licar em **Salvar e fechar**.

![image](https://user-images.githubusercontent.com/82005568/215265051-c3960ae2-df9c-4cf6-b9a1-aa3b7b9681e5.png)

## Vincular tabelas de outro fluxo de dados

Agora iremos partir para a segunda etapa do processo que é vincular tabelas de outro fluxo de dados.

Conforme descrito no início deste tutorial, você irá criar um novo fluxo de dados no Worksapce do projeto, só que desta vez você irá clicar em **Adicionar tabelas vinculadas**

![image](https://user-images.githubusercontent.com/82005568/215265562-9ae7132b-21cf-4ecc-a733-fc72dc6df235.png)

Na próxima imagem teremos no lado esquerdo o fluxo de dados que temos disponível para realizarmos a nossa conexão e as credenciais por padrão já veio a autenticação com o Power BI, agora basta clicar em **Próximo**.

![image](https://user-images.githubusercontent.com/82005568/215265926-5d3cf65e-564c-4199-a6e7-13bf0b357100.png)

Após selecionar os dados que estão no dataflow criado anteriormente, esles serão carregados na coluna da direta para visualização e você irá clicar em **Transformar dados**.

![image](https://user-images.githubusercontent.com/82005568/215266095-e7705a0a-4b6b-4aff-95cf-b8d9ce2fdf80.png)

Quando a tabela do dataflow de cache for carregado neste segundo dataflow, terá uma marca de uma corrente ao lado da tabela, dizendo que é uma tabela vinculada. Tabelas vinculadas são somente leitura e não pode ser feita nenhuma transformação diretamente nelas.

![image](https://user-images.githubusercontent.com/82005568/215266825-5c40da4e-a7b8-4a4a-b168-e92a770a6cc6.png)

Por esse motivo, iremos clicar com o botão direito em cima da tabela vinculada e iremos fazer uma referência dela para podermos aplicar as transformações.

![image](https://user-images.githubusercontent.com/82005568/215266856-be766f8e-4f11-4606-96cb-3327b1ab0c57.png)

Perceba que essa tabela, agora tem a marca de um raio, isso quer dizer que ela é uma tabela computada, ou seja, ela "executa cálculos em armazenamento para transformações de dados avançadas", fazendo com que o desempenho seja muito superior.

![image](https://user-images.githubusercontent.com/82005568/215267046-cc94323a-40bd-4948-aa37-0503428ce1d0.png)

Nessa tabela computada, ponde ser feito todas as transformações necessária.

Na hora da atualização, basta atualizar ou agendar somente a atualização do dataflow de Cache, pois o Power BI fará a atualização em cascata, como se fosse um efeito dominó, atualizando todo os outros dafalows que estão abaixo dele.

