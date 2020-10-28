# Etapa 02 - Descrição da Proposta

## Slides da Proposta
 
> [Link para a Apresentação](https://github.com/IucasF/Centro-de-Pesquisas-Asdrubal/blob/main/stage02/slides/Apresenta%C3%A7%C3%A3o%20MC536.pdf)


## Motivação e Contexto

> O coronavírus atingiu o mundo em cheio neste ano de 2020, desde interações sociais entre indivíduos até o desempenho da economia dos países. Com ele, a ideia de Quarentena, o famoso 'lock down', cresceu muito neste ano e suas consequências para a população estão ainda a ser descobertas. Uma das mais predominantes que podemos destacar é o decaimento da saúde mental, uma vez que muitas pessoas estão (quase) sempre confinadas em casa, impedidas de sair, criando espaço para a ansiedade, preocupação e até pensamentos depressivos. Pensando ainda no contexto da quarentena, vemos que a dieta das pessoas, que muitas vezes almoçavam fora, teve de mudar bastante para se adaptar à nova situação, onde fazer comida em casa ou pedir por aplicativo se tornaram as duas principais opções hoje em dia. Há já diversos estudos que apontam para a existência de uma forte relação entre o que comemos e nosso humor, como na existência de alimentos promotores de estresse (como açúcar, café, chocolate) e em outros que melhoram o estado mental (como água, verduras e frutas).  
O objetivo então é de tentar analisar dados coletados em anos passados em diversos países com informações da dieta de seus habitantes que nos possibilite correlacionar aspectos nutricionais com a saúde mental de uma certa população com dados do mundo real.

## Método

> Quais são as análises a ser realizadas, quais os resultados esperados e qual o papel de cada modelo lógico no processo. Proposta de metodologia incluindo o que se pretende analisar e como será feita a análise.  
> Primeiramente, pegaremos os dados básicos dos países através do banco de dados da DBPedia; Em seguida, através do Nome de cada país, uma vez que sabemos que não existem dois países com o mesmo nome, poderemos estabelecer relações entre as diversas tabelas.  
Com elas se relacionando entre si, oalgumas das ideias primordiais seriam a de analisar o nível de desnutrição e obesidade (Database 4/5) e comparar com os índices de transtornos mentais (Database 2), comparar a quantidade de transtornos e a quantidade de instalações para tratamento da saúde e a pobreza/riqueza do referido país, e, mais para frente, tentar comparar o tipo de dieta de cada país com tabelas de doenças/transtornos e de felicidade.  
Sabemos que o assunto é complexo por se tratar do ser humano e é multivariável, dependente de fatores que não entraram na análise e que não estão a nosso alcance. Dito isso, esperamos encontrar uma relação pequena, porém presente nas associações previamente descritas.

## Bases de Dados
> Elencar as bases de dados candidatas a serem utilizadas no projeto.

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
Geral | https://wiki.dbpedia.org/ | Dados gerais de países (grafo)

