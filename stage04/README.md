# Etapa 04 - Análises com o Segundo Modelo Lógico

## Slides da Apresentação da Etapa

> [Link para a Apresentação Final (pdf)](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/stage04/slides/Apresenta%C3%A7%C3%A3o%20Final%20MC536.pdf) <br>
> [Link para a Apresentação Final (pptx)](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/stage04/slides/Apresenta%C3%A7%C3%A3o%20Final%20MC536.pptx)

## Modelo Conceitual Atualizado

> Coloque aqui a imagem do modelo conceitual atualizado em ER ou UML, como o exemplo a seguir:
> ![ER ModeloConceitual](assets/Modelagem%20conceitual.png)

## Modelos Lógicos Atualizados

> Coloque aqui os dois modelos lógicos dos bancos de dados relacionados aos modelos conceituais. O modelo lógico da etapa anterior pode ser copiado ou apresentado revisado. Para o modelo relacional, sugere-se o formato a seguir. Para outros modelos lógicos o formato é livre, pode ser adotado aqueles apresentados em sala.

> Exemplo de modelo lógico relacional
~~~
PESSOA(_Código_, Nome, Telefone)
ARMÁRIO(_Código_, Tamanho, Ocupante)
  Ocupante chave estrangeira -> PESSOA(Código)
~~~

## Programa de extração e conversão de dados atualizado

> Os arquivos notebooks já contêm ambos a extração de dados dos banco de dados presentes na lista de Arquivos de Dados no final desta página quanto as queries que manipularam e fizeram análises com tais dados.
> Segue abaixo os arquivos notebooks que fizeram extração/relacionamento de dados através do Kernel SQL no Jupyter: <br>
> [Primeiras Análises (Disorders and Weight Problems)](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/stage04/notebooks/ConnectingDatabasesv3.ipynb) <br>
> [Outras Análises (Disorders and Facilities)](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/stage04/notebooks/DisordersAndFacilities.ipynb) <br>
> [Outras análises (Community and IDH)](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/stage04/notebooks/ComunityAndIDH.ipynb) 

## Conjunto de queries de dois modelos

> Acrescente um link para o arquivo do notebook que executa o segundo conjunto de queries. Ele estará dentro da pasta `notebook`. Se por alguma razão o código não for executável no Jupyter, coloque na pasta `src`. Se as queries forem executadas atraves de uma interface de um SGBD não executável no Jupyter, como o Cypher, apresente na forma de markdown.
> O link para queries da etapa 3 também deve aparecer aqui e as queries poderão ser revisadas.
> Link para notebook:
> Queries referentes à análise feita no Cypher:
~~~
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/IucasF/Centro-de-Pesquisas-Asdrubal/main/stage04/data/raw/.csv' AS line
CREATE (:Pais {nome: line. Country, calcio: line.calcio, colesterol: line.colesterol, fibra: line.fibra, fruta: line.fruta, legumes: line.legumes, leite: line.leite, carneVermelha: line.carneVermelha, vegetais: line.vegetais, graos: line.graos})

CREATE INDEX ON :Pais(nome)

MATCH (p1:Pais)
MATCH (p2:Pais)
WHERE toFloat(p1.calcio) - toFloat(p2.calcio) < 0.5 AND p1.nome <> p2.nome
MERGE (p1)-[p:parece]->(p2)
ON CREATE SET p.weight=1
ON MATCH SET p.weight=p.weight+1

MATCH (p1:Pais)
MATCH (p2:Pais)
WHERE toFloat(p1.colesterol) - toFloat(p2.colesterol) < 0.5 AND p1.nome <> p2.nome
MERGE (p1)-[p:parece]->(p2)
ON CREATE SET p.weight=1
ON MATCH SET p.weight=p.weight+1

MATCH (p1:Pais)
MATCH (p2:Pais)
WHERE toFloat(p1.fibra) - toFloat(p2.fibra) < 0.5 AND p1.nome <> p2.nome
MERGE (p1)-[p:parece]->(p2)
ON CREATE SET p.weight=1
ON MATCH SET p.weight=p.weight+1

MATCH (p1:Pais)
MATCH (p2:Pais)
WHERE toFloat(p1.fruta) - toFloat(p2.fruta) < 0.5 AND p1.nome <> p2.nome
MERGE (p1)-[p:parece]->(p2)
ON CREATE SET p.weight=1
ON MATCH SET p.weight=p.weight+1

MATCH (p1:Pais)
MATCH (p2:Pais)
WHERE toFloat(p1.legumes) - toFloat(p2.legumes) < 0.5 AND p1.nome <> p2.nome
MERGE (p1)-[p:parece]->(p2)
ON CREATE SET p.weight=1
ON MATCH SET p.weight=p.weight+1

MATCH (p1:Pais)
MATCH (p2:Pais)
WHERE toFloat(p1.leite) - toFloat(p2.leite) < 0.5 AND p1.nome <> p2.nome
MERGE (p1)-[p:parece]->(p2)
ON CREATE SET p.weight=1
ON MATCH SET p.weight=p.weight+1

MATCH (p1:Pais)
MATCH (p2:Pais)
WHERE toFloat(p1.carneVermelha) - toFloat(p2.carneVermelha) < 0.5 AND p1.nome <> p2.nome
MERGE (p1)-[p:parece]->(p2)
ON CREATE SET p.weight=1
ON MATCH SET p.weight=p.weight+1

MATCH (p1:Pais)
MATCH (p2:Pais)
WHERE toFloat(p1.vegetais) - toFloat(p2.vegetais) < 0.5 AND p1.nome <> p2.nome
MERGE (p1)-[p:parece]->(p2)
ON CREATE SET p.weight=1
ON MATCH SET p.weight=p.weight+1

MATCH (p1:Pais)
MATCH (p2:Pais)
WHERE toFloat(p1.graos) - toFloat(p2.graos) < 0.5 AND p1.nome <> p2.nome
MERGE (p1)-[p:parece]->(p2)
ON CREATE SET p.weight=1
ON MATCH SET p.weight=p.weight+1

match (p1)-[l:parece]->(p2)
where l.weight > 6
create (p1)-[:semelhante]->(p2)

match (p1)-[l:parece]->(p2)
delete l

CALL gds.graph.create(
  'prGraph',
  'Pais',
  'semelhante'
)

CALL gds.pageRank.stream('prGraph')
YIELD nodeId, score
RETURN gds.util.asNode(nodeId).nome AS name, score
ORDER BY score DESC, name ASC

CALL gds.graph.create(
  'relacaoDieta',
  'Pais',
  {
    semelhante: {
      orientation: 'UNDIRECTED'
    }
  }
)

CALL gds.louvain.stream('relacaoDieta')
YIELD nodeId, communityId
RETURN gds.util.asNode(nodeId).nome AS name, communityId
ORDER BY communityId ASC

CALL gds.louvain.stream('relacaoDieta')
YIELD nodeId, communityId
MATCH (p:Pais {name: gds.util.asNode(nodeId).nome})
SET p.community = communityId

match (source)-[semelhante]->(target)
WHERE source.nome <> target.nome
return source.nome,target.nome
~~~

## Bases de Dados
> Elencar as bases de dados utilizadas no projeto. Trata-se de uma atualização daquelas apresentadas na Etapa 3.

título da base | link | breve descrição
----- | ----- | -----
Instalações | https://apps.who.int/gho/data/node.main.MHFAC | Instalações para tratamento de problemas mentais por país (JSON) 
Transtornos | https://ourworldindata.org/mental-health | Transtornos mentais por país (CSV)
Suicídio/Felicidade | https://www.kaggle.com/rblcoder/mental-health-happiness-economics-human-freedom/notebook | Dados sobre Suicídio e níveis de felicidade por país (CSV)
Peso | https://data.unicef.org/dv_index/ | Taxa de obesidade, desnutrição entre outros por país (CSV)
Peso2 | https://www.who.int/data/nutrition/nlis/data-search | Taxa de obesidade e desnutrição por país (CSV)
Dieta | https://www.globaldietarydatabase.org/gdd-2015-beta-version | Informações sobre o tipo de dieta mais comum por país
Saúde_Geral | https://data.oecd.org/searchresults/?q=mental+health | Dados diversos relacionados à saúde, além de dados sobre índices de suicídio e de obesidade (CSV)
Países | https://data.world/badosa/uneces-country-overview | Dados geográficos gerais de países (JSON)
IDH | http://hdr.undp.org/en/composite/HDI | Valores do IDH de cada país
Geral | https://wiki.dbpedia.org/ | Dados gerais de países (grafo)


## Arquivos de Dados
> Elencar os arquivos usados no projeto que estão disponíveis no Github do projeto (manter os da Etapa 3 e acrescentar os da Etapa 4).

Título da Base | Arquivo
----- | -----
Transtornos(1) | [Esquizofrenia](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/data/databasse5_prevalence-of-schizophrenia-in-males-vs-femalesv3.csv)
Transtornos(2) | [Ansiedade](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/data/anxiety_disorders_mh.csv)
Transtornos(3) | [Depressão](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/data/depression_mh.csv)
Instalações | [Instalações](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/data/mental_health_facilities_gho.csv)
Peso 2 | [Sobrepeso/Subnutrição](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/data/database2_overweight_underweight.csv)
Dieta | [Dieta Simplificada](https://raw.githubusercontent.com/IucasF/Centro-de-Pesquisas-Asdrubal/main/stage04/data/external/dieta.csv)
Dieta(1) | [Dieta calcio](https://raw.githubusercontent.com/IucasF/Centro-de-Pesquisas-Asdrubal/main/stage04/data/raw/dietary%20calcium.tsv)
Dieta(2) | [Dieta colesterol](https://raw.githubusercontent.com/IucasF/Centro-de-Pesquisas-Asdrubal/main/stage04/data/raw/dietary%20cholesterol.csv)
Dieta(3) | [Dieta fibra](https://raw.githubusercontent.com/IucasF/Centro-de-Pesquisas-Asdrubal/main/stage04/data/raw/dietary%20fiber.csv)
Dieta(4) | [Dieta frutas](https://raw.githubusercontent.com/IucasF/Centro-de-Pesquisas-Asdrubal/main/stage04/data/raw/dietary%20fruit.csv)
Dieta(5) | [Dieta grãos](https://raw.githubusercontent.com/IucasF/Centro-de-Pesquisas-Asdrubal/main/stage04/data/raw/dietary%20grains.csv)
Dieta(6) | [Dieta leite](https://raw.githubusercontent.com/IucasF/Centro-de-Pesquisas-Asdrubal/main/stage04/data/raw/dietary%20milk.csv)
Dieta(7) | [Dieta carne vermelha](https://raw.githubusercontent.com/IucasF/Centro-de-Pesquisas-Asdrubal/main/stage04/data/raw/dietary%20red%20meat.csv)
Dieta(8) | [Dieta vegetais](https://raw.githubusercontent.com/IucasF/Centro-de-Pesquisas-Asdrubal/main/stage04/data/raw/dietary%20vegetables.csv)
Comunidades Dieta | [Países e suas comunidades de dieta](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/stage04/data/processed/community.csv)
Source - Target | [Países com semelhanças nas dietas](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/stage04/data/interim/source-target.csv)

> Os arquivos devem ser colocados na pasta `data`, em subpasta conforme seu papel (externo, interim, processado, raw). A diferença entre externo e raw é que o raw é em formato não adaptado para uso. A pasta `raw` é opcional, pois pode ser substituída pelo link para a base original da seção anterior.
> Coloque arquivos relacionais (usualmente CSV), XML ou JSON que não estejam disponíveis online e sejam acessados pelo notebook.
