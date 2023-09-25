# Análise da base de dados de autuações ambientais aplicadas pelo ICMBio (Grupo 6)
O conteúdo compõe o trabalho final da disciplina Fundamentos e Ética do Jornalismo de Dados, do Master em Jornalismo de Dados, Automação e Datasotrytelling do Insper.

A base de dados utilizada foi o arquivo com todas as autuações ambientais aplicadas pelo Instituto Chico Mendes de Conservação da Biodiversidade (ICMBio), que passou a ser divulgada pelo instituto em agosto deste ano.

## Arquivos usados nas análises
Subimos neste repositório os [dados brutos](https://github.com/SumaiaVillela/autuacoesambientaisicmbio/blob/b6a1886fa7a639cee1ac4858220d96f66b248352/autos_infracao_icmbio_atualizado_25082023.xlsx), sem nenhum ajuste, mas ele pode ser baixado [aqui](https://www.gov.br/icmbio/pt-br/assuntos/dados_geoespaciais/mapa-tematico-e-dados-geoestatisticos-das-unidades-de-conservacao-federais).

A base com as colunas selecionadas para análise, as construídas a partir dela com as filtragens necessárias e as tabelas dinâmicas onde chegamos aos resultados estão [neste arquivo](https://github.com/SumaiaVillela/autuacoesambientaisicmbio/blob/main/autos_infracao_icmbio_25-08-2023_PLANILHAS%20FILTRADAS%20E%20TABELAS%20DIN%C3%82MICAS.xlsx).

[Neste outro arquivo](https://github.com/SumaiaVillela/autuacoesambientaisicmbio/blob/main/Termos%20comuns%20nas%20descri%C3%A7%C3%B5es%20de%20infra%C3%A7%C3%A3o%20-%20base%20do%20ICMBio%20de%2025-08-2023.xlsx), temos os termos mais comuns encontrados nas descrições dos autos de infração separados por tipo de infração (contra a fauna, contra a flora, etc), o que nos auxiliou a identificar as principais atividades econômicas envolvidas nas infrações ambientais.

## Por que escolhemos essa base?
Como já dito, o arquivo com todas as autuações ambientais aplicadas pelo ICMBio foi divulgado pela primeira vez no dia 23 de agosto deste ano. Possui registros que datam desde 2008 (o ICMBio foi criado em agosto de 2007), e inclui nomes e CPFs dos autuados, descrição dos autos de infração, dos embargos, fase de julgamento, números dos processos, valor das multas, entre outros dados considerados relevantes para exploração e consulta para casos específicos. É, também, uma base com muitas colunas autoexplicativas e, para nossa análise, havia poucos problemas a serem contornados (que são descritos mais abaixo). Fizemos nossa escolha, portanto, pela relevância, novidade e qualidade dos dados.
## Que plataforma usamos para a análise?
Fizemos todo o processamento dos dados em planilha eletrônica do Excel, com o uso de tabela dinâmica e fórmulas.
## Como analisamos a base de dados?
O trabalho consistiu em analisar o banco de dados para buscar insights que levassem a investigações relacionadas à degradação ambiental de Unidades de Conservação (UCs) federais, que são protegidas por lei (ver [Lei Nº 9.985/2000](https://www.planalto.gov.br/ccivil_03/leis/l9985.htm)) e normativas infralegais, conforme classificação de cada uma.

Para iniciar o trabalho, verificamos as colunas das tabelas para entender cada parâmetro e selecionamentos os que nos interessava para análise. Cabe destacar que não identificamos um dicionário para o banco de dados. No entanto, os títulos das colunas e os dados contidos estavam claros o suficiente para os fins que precisávamos – e há similaridade com o banco do Ibama, então é possível fazer algumas comparações para atestar a segurança dos dados (CPFs comuns, por exemplo).
### Excluímos as seguintes colunas antes de começar o processamento:
- `ID`: número do item
- `Número AI`: código que identifica o Auto de Infração
- `Série`: não identificamos a que se refere
- `Origem`: eletrônico ou papel
- `Tipo`: se foi multa simples ou advertência e se houve destruição, demolição, embargo. Uma sugestão que poderia ser dada ao ICMBio é desmembrar o campo para que houvesse a classificação inicial em multa ou advertência, e em outra coluna se houve destruição ou demolição (só há campos específicos para apreensão e embargo na tabela). A análise seria facilitada, porque é um dado interessante.
- `Embargo`: se houve embargo (sim ou não)
- `Apreensão`: (se houve ou não)
- `Data`: dia, mês e ano exato em que foi criado o auto de infração. Como há uma coluna somente com o ano, essa foi excluída.
- `Artigo 1`: artigo do decreto nº 6.514/2008 que aponta o tipo de infração cometida (descobrimos por meio de pesquisa extra tabela).
- `Artigo 2`: outro artigo do mesmo decreto. Um deles, por exemplo, identifica majoração da multa porque a violação foi cometida dentro de UCs.
- `CNUC`: Código do Cadastro Nacional de Unidades de Conservação (CNUC).
- `Termos Embargo`: código do termo de embargo.
- `Temos Apreensão`: código do termo de apreensão.
- `Ordem de fiscalização`: código da ordem.
- `Processo`: número do processo.
- `Julgamento`: fase ou andamento do processo.
   
Posteriormente, conforme a análise avançava, fizemos a padronização dos dados e ajuste de dados ausentes onde havia necessidade e nos certificamos de que não havia erro de formatação que causasse alguma distorção nos dados. Explicamos melhor cada limpeza mais abaixo.

## Quais perguntas fizemos aos dados?
Inicialmente, optamos identificar quais Unidades de Conservação (UCs) registravam mais infrações ambientais. Portanto:
- _Quais as 10 UCs mais "atacadas" do país?_
  
Uma vez identificada nossa delimitação de pauta, seguimos com outras quatro perguntas:

- _Quais os maiores infratores na Flona do Jamanxim?_
- _Quais as atividades econômicas ligadas às infrações cometidas na Flona do Jamanxim?_
- _Quais as infrações cometidas pela campeã de multas da Flona do Jamanxim?_
- _Como as autuações ambientais da Flona do Jamanxim estão distribuídas ano a ano?_

### Quais as 10 UCs mais "atacadas" do país?
- Verificamos que não havia dados ausentes na coluna;
- Montamos uma tabela dinâmica com as colunas `Nome da UC`, `Valor da Multa` e contagem de vezes em que aparecia o nome de cada Unidade de Conservação na coluna `Nome da UC`;
- Ordenamos por quantidade de autuações de cada UC, da maior para a menor. Constatamos que a primeira colocada, a Floresta Nacional do Jamanxim (Flona), era líder isolada do ranking. Testamos com a soma do valor das multas, e ela continua na liderança com folga.

`PRINCIPAL DADO: A Flona do Jamanxim possui 1.496 autuações ambientais`

A partir daí, pesquisamos a respeito da Flona do Jamanxim e, pelo histórico e simbolismo desse território (por exemplo, ela fica em Novo Progresso, Pará, onde investigações de jornalistas ambientais identificaram ter começado a ação coordenada de incêndios florestais conhecida como Dia do Fogo, em 2019), unidos ao dado citado anteriormente, escolhemos analisar mais a fundo os números da Flona do Jamanxim.

Os resultados da análise estão na planilha `Ranking UC - qnt de autuações` do arquivo.

## Quais os maiores infratores na Flona do Jamanxim?
- Filtramos todas as autuações específicas dessa UC e copiamos como uma nova tabela, para facilitar a reprodução dos passos;
- Verificamos que havia dados ausentes na coluna `CPF/CNPJ`, que seria usado para realizar a soma das multas em nome dos autuados, a fim de evitar homônimos e erros de grafia. **Abrimos uma cópia da planilha filtrada da Flona para realizar exclusões sem afetar as análises seguintes**, conforme explicado mais abaixo. Procedemos da seguinte maneira:
  - Havia pessoas sem CPF. Foram identificados todos os espaços em branco, e o tratamento foi dividido em dois grupos.
    - Para multas com valor menor que R$ 1 milhão, foi feita busca pelo nome no banco de dados. Quando não havia outra multa com o mesmo nome (ou muito semelhante) e, portanto, não geraria agregação para um valor maior, a pessoa era excluída da base de dados, pois ela não seria relevante para esta análise específica.
    - Quando havia multa de mais de R$ 1 milhão, foi atribuído um CPF fictício (e que não pudesse se confundir com nenhum outro). Caso o mesmo nome tivesse mais de uma multa, o mesmo CPF fictício era atribuído. Nenhum caso desses alcançou o corte do ranqueamento.
  - Há 75 “infratores não identificados” num universo de 1946 autuações. Estão, portanto, sem CPF. 39 deles não tinham recebido multa (há possibilidade de receber somente advertência). Outros 15 possuíam multa abaixo de R$ 100 mil. Outros oito estão acima disso e com limite de R$ 1 milhão. Hipoteticamente, seria possível que várias dessas multas pertencessem à mesma pessoa, mas se não há identificado, o objeto da nossa análise, que são os infratores apontados pelo ICMBio, se perde. De todo modo, Atribuímos CPFs fictícios aos não identificados acima de R$ 1 milhão, e nenhum alcançava o corte do ranking.
  - Havia alguns CPFs faltando um dígito. Procuramos na base de dados o mesmo nome de autuado, a mesma sequência numérica e o CPF completo (casos em que há mais de uma multa), e fizemos a substituição. Para quem só tinha uma multa, buscamos no banco de autuações do IBAMA com a mesma lógica. Não houve caso em que não foi encontrado o registro para substituição, mas seria possível buscar por outros meios o preenchimento desse CPF corretamente, caso fosse necessário para a análise.
- Concluídos os ajustes, abrimos uma tabela dinâmica para fazer a contagem do valor das multas por autuados. Usamos as colunas `CPF/CNPJ` para a contagem, e incluímos a coluna `Autuados` como rótulos para identificar os maiores multados;
- Calculamos o 99 percentil da base de dados com a fórmula `=PERCENTIL (matriz;k)`, ou seja: identificamos o valor de corte para entrar no 1% de valores devidos mais altos, e estabelecemos o ranking de 9 nomes a partir de R$ 17.784.900.
- Constatamos outra liderança isolada, neste caso no ranking de multados: Sandra Mara Silveira, já citada em reportagens sobre desmatamento na Amazônia.
- Também fizemos o ranking por ano. Para isso, inserimos, em outra tabela dinâmica, a coluna `Ano` e retiramos a coluna `Autuados` (porque a tabela dinâmica cria uma hierarquização entre CPF e autuado que polui a tabela quando ela é exportada para virar uma nova base de dados). O resultado dessa nova tabela dinâmica foi copiado e colado apenas como dados, para que pudéssemos usar mais facilmente o filtro em cada ano. Usamos a fórmula `=PROCV(valor_procurado;matriz_tabela; núm_índice_coluna; [procurar_intervalo])`para inserir os nomes dos multados na nova base e ativamos os filtros. Assim, é possível navegar por ordem decrescente em cada ano. 

`PRINCIPAL DADO: Sandra Mara Silveira já foi multada em R$ 101,37 milhões. Sua última multa é de 2022`

 `PRINCPAL DADO 2: Marco Tulio Pires Franco é o primeiro da lista de 2023, com valor em multa de R$ 12,88 milhões`
 
  `PRINCIPAL DADO 3: Jaime Zaminham é o primeiro da lista de 2022, com valor em multa de R$ 27,25 milhões`
  
Os resultados da análise estão nas planilhas `Ranking maiores multados` e `Ranking multados por ano` do arquivo.

## Quais as atividades econômicas ligadas às infrações cometidas na Flona do Jamanxim?
- Não havia ausência de dados relacionados na coluna `Tipo de Infração`;
- Abrimos uma tabela dinâmica com a contagem de termos que aparecem na coluna `Tipo de Infração` e do valor da soma das multas de cada tipo, expressas na coluna `Valor da Multa`;
- Organizamos por número de infrações em cada tipo, do maior para o menor. As infrações contra a flora são a tipificação mais comum, de novo em liderança absoluta.

`PRINCPAL DADO: Das Infrações Contra a Flora é o tipo mais comum de infração, com 1.249 dos 1.496 registros.`

- Em um conjunto de planilhas específico (linkado no início deste READ-ME, separamos a coluna `Descrição AI` para cada parâmetro que consta na coluna `Tipo de Infração`, de modo a identificar as atividades econômicas ligadas a cada uma. Para fazer a contagem dos termos, usamos a fórmula `=CONT.SE(intervalo;critérios)`, colocando o `*`ao início e fim de cada critério, para abarcar todas as construções frasais possíveis. Identificamos, por exemplo, que a palavra "gado" aparece 565 vezes quando o tipo de infração é contra a flora, ou que as variações de minério aparecem 70 vezes em 90 ocorrências relacionadas a poluição e outras infrações ambientais.

`PRINCIPAL DADO: Termos ligados a desmatamento e pecuária são comuns em infrações contra a flora, que é a líder entre os tipos de autuação.`
### Quais as infrações cometidas pela campeã de multas da Flona do Jamanxim?
- Também filtramos as infrações cometidas pela primeira colocada no ranking de multados e separamos os detalhes de cada infração, inscritos na coluna `Descrição AI` (Auto de Infração).

Os resultados da análise estão na planilha `Atividades ligadas às infrações` do arquivo.

## Como as autuações ambientais da Flona do Jamanxim estão distribuídas ano a ano?
- Não há dados ausentes na coluna Ano;
- Montamos uma tabela dinâmica para contar a quantidade de infrações por ano. Para isso, naturalmente usamos a coluna `Ano`. Também usamos a coluna `Valor da Multa` para somar o total das multas por ano. Constatamos que em 2022 houve um aumento vertiginoso da quantidade de autuações – e o valor total de multas também é maior que em outros anos.

`DADO PRINCIPAL: Foram 613 infrações registradas ano passado. Anteriormente, o maior número tinha sido o de 2014, com 194 ocorrências`

- Para 2023, os dados vão até agosto, que é o mês de publicação da base pelo ICMbio. A informação foi verificada na base de dados original, na coluna Data, que conta também com dia e mês de registro. E já são 325 autuações realizadas, o que já torna 2023 o segundo ano com mais infrações registradas.

Os resultados da análise estão na planilha `Autuações por Ano` do arquivo.

## Contato com a equipe
Sumaia Villela (dadosparasumaia@gmail.com)
