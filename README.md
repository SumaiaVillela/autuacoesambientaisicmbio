# Análise da base de dados de autuações ambientais aplicadas pelo ICMBio (Grupo 6)
O conteúdo compõe o trabalho final da disciplina Fundamentos e Ética do Jornalismo de Dados, do Master em Jornalismo de Dados, Automação e Datasotrytelling do Insper.
A base de dados utilizada foi o arquivo com todas as autuações ambientais aplicadas pelo Instituto Chico Mendes de Conservação da Biodiversidade (ICMBio), que passou a ser divulgada pelo instituto em agosto deste ano. COLOCAR HIPERLINK DA PÁGINA

## Arquivos usados nas análises
INSERIR AQUI HIPERLINKS PARA A BASE BRUTA E O ARQUIVOS COM AS PLANILHAS DO TRABALHO

## Por que escolhemos essa base?
Como já dito, o arquivo com todas as autuações ambientais aplicadas pelo ICMBio foi divulgado pela primeira vez no dia 23 de agosto deste ano. Possui registros que datam desde 2008 (o ICMBio foi criado em agosto de 2007), e inclui nomes e CPFs dos autuados, descrição dos autos de infração, dos embargos, fase de julgamento, números dos processos, valor das multas, entre outros dados considerados relevantes para exploração e consulta para casos específicos. É, também, uma base com muitas colunas autoexplicativas e, para nossa análise, havia poucos problemas a serem contornados (que são descritos mais abaixo). Fizemos nossa escolha, portanto, pela relevância, novidade e qualidade dos dados.
## Que plataforma usamos para a análise?
Fizemos todo o processamento dos dados em planilha eletrônica do Excel, com o uso de tabela dinâmica e fórmulas.
## Como analisamos com a base de dados?
O trabalho consistiu em analisar o banco de dados para buscar insights que levassem a investigações relacionadas à degradação ambiental de Unidades de Conservação (UCs) federais, que são protegidas por lei (ver [Lei Nº 9.985/2000] (https://www.planalto.gov.br/ccivil_03/leis/l9985.htm)) e normativas infralegais, conforme classificação de cada uma.
Para iniciar o trabalho, verificamos as colunas das tabelas para entender cada parâmetro e selecionamentos os que nos interessava para análise. Cabe destacar que não identificamos um dicionário para o banco de dados. No entanto, os títulos das colunas e os dados contidos estavam claros o suficiente para os fins que precisávamos – e há similaridade com o banco do Ibama, então é possível fazer algumas comparações para atestar a segurança dos dados (CPFs comuns, por exemplo).
### Excluímos as seguintes colunas antes de começar o processamento:
- ID: número do item
- Número AI: código que identifica o Auto de Infração
- Série: não identificamos a que se refere
- Origem: eletrônico ou papel
- Tipo: se foi multa simples ou advertência e se houve destruição, demolição, embargo. Uma sugestão que poderia ser dada ao ICMBio é desmembrar o campo para que houvesse a classificação inicial em multa ou advertência, e em outra coluna se houve destruição ou demolição (só há campos específicos para apreensão e embargo na tabela). A análise seria facilitada, porque é um dado interessante.
- Embargo: se houve embargo (sim ou não)
- Apreensão: (se houve ou não)
- Data: dia, mês e ano exato em que foi criado o auto de infração. Como há uma coluna somente com o ano, essa foi excluída.
- Artigo 1: artigo do decreto nº 6.514/2008 que aponta o tipo de infração cometida (descobrimos por meio de pesquisa extra tabela).
- Artigo 2: outro artigo do mesmo decreto. Um deles, por exemplo, identifica majoração da multa porque a violação foi cometida dentro de UCs.
- CNUC: Código do Cadastro Nacional de Unidades de Conservação (CNUC).
- Termos Embargo: código do termo de embargo.
- Temos Apreensão: código do termo de apreensão.
- Ordem de fiscalização: código da ordem.
- Processo: número do processo.
- Julgamento: fase ou andamento do processo.
Posteriormente, conforme a análise avançava, fizemos a padronização dos dados e ajuste de dados ausentes onde havia necessidade e nos certificamos de que não havia erro de formatação que causasse alguma distorção nos dados. Explicamos melhor cada limpeza mais abaixo.

## Que perguntas fizemos aos dados?
Inicialmente, optamos identificar quais Unidades de Conservação (UCs) registravam mais infrações ambientais. Portanto:
_Quais as 10 UCs mais "atacadas" do país?_
Uma vez identificada nossa delimitação de pauta, seguimos com outras quatro perguntas:
_Quais os maiores infratores na Flona do Jamanxim?_
_Quais as atividades econômicas ligadas às infrações cometidas na Flona do Jamanxim?_
_Quais as infrações cometidas pela campeã de multas da Flona do Jamanxim?_
_Como as autuações ambientais da Flona do Jamanxim estão distribuídas ano a ano?_

### 1- Quais as 10 UCs mais "atacadas" do país?
- Verificamos que não havia dados ausentes na coluna;
- Montamos uma tabela dinâmica com as colunas Nome da UC, Valor da Multa e contagem de vezes em que aparecia o nome de cada Unidade de Conservação na coluna Nome da UC;
- Ordenamos por quantidade de autuações de cada UC, da maior para a menor. Constatamos que a primeira colocada, a Floresta Nacional do Jamanxim (Flona), era líder isolada do ranking. Testamos com multas, e ela continua na liderança com folga.

A partir daí, pesquisamos a respeito da Flona do Jamanxim e, pelo histórico e simbolismo desse território, unidos ao dado citado anteriormente, escolhemos analisar mais a fundo os números da Flona do Jamanxim.

## Quais os maiores infratores na Flona do Jamanxim?
- Filtramos todas as autuações específicas dessa UC e copiamos como uma nova tabela, para facilitar a reprodução dos passos;
- Verificamos que havia dados ausentes no campo do CPF, que seria usado para realizar a soma das multas em nome dos autuados, a fim de evitar homônimos e erros de grafia. Abrimos uma cópia da planilha filtrada da Flona para realizar exclusões sem afetar as análises seguinte, conforme explicado mais abaixo. Procedemos da seguinte maneira:
COLAR AQUI A LIMPEZA DE DADOS
- Concluídos os ajustes, abrimos uma tabela dinâmica para fazer a contagem do valor das multas por autuados. Usamos as colunas de CPFs para a contagem, e incluímos os nomes como rótulos para identificar os maiores autuados;
- Calculamos o 99 percentil da base de dados com a fórmula =PERCENTIL (matriz;k), ou seja: identificamos o valor de corte para entrar no 1% de valores devidos mais altos, e estabelecemos o ranking de 9 nomes a partir de R$ 17.784.900.
- Constatamos outra liderança isolada, neste caso no ranking de multados: Sandra Mara Silveira, já citada em reportagens sobre desmatamento na Amazônia.

## Quais as atividades econômicas ligadas às infrações cometidas na Flona do Jamanxim?
- Não havia ausência de dados relacionados na coluna Tipo de Infração;
- Abrimos uma tabela dinâmica com a contagem de termos que aparecem na coluna Tipo de Infração e do valor da soma das multas de cada tipo;
- Organizamos por número de infrações em cada tipo, do maior para o menor. Os crimes contra a flora são a tipificação mais comum, com 1.249 dos 1.496 registros.
### Quais as infrações cometidas pela campeã de multas da Flona do Jamanxim?
- Também filtramos as infrações cometidas pela primeira colocada no ranking de multados e separamos os detalhes de cada infração, inscritos na coluna Descrição AI [Auto de Infração].

## Como as autuações ambientais da Flona do Jamanxim estão distribuídas ano a ano?
- Não há dados ausentes na coluna Ano;
- Montamos uma tabela dinâmica para contar a quantidade de infrações por ano. Também somamos o valor das multas por ano. Constatamos que em 2022 houve um aumento vertiginoso da quantidade de autuações – e o valor total de multas também é maior que em outros anos. Foram 613 infrações registradas ano passado;
- Anteriormente, o maior número tinha sido o da 2014, com 194 ocorrências;
- Para 2023, os dados vão até agosto, que é o mês de publicação da base pelo ICMbio. A informação foi verificada na base de dados original, na coluna Data, que conta também com dia e mês de registro. E já são 325 autuações realizadas, o que já torna 2023 o segundo ano com mais infrações registradas.
Os resultados da análise estão na planilha “Autuações por Ano” do arquivo.

## Contato com a equipe
Sumaia Villela (dadosparasumaia@gmail.com)
