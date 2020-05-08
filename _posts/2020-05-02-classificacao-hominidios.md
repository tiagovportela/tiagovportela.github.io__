---
layout: post
title:  Classificação de especies de Hominideos pela dimensão do cranio
excerpt: "Classificação de fossies de hominideos através de metodos de machine learning"
modified: 02/05/2020, 9:00:24
tags: [k-means, human evolution]
comments: true
category: blog
---

Ao assistir a [este](https://www.youtube.com/watch?v=XqX72KvH15E) documentario ocorreu-me a ideia de criar um classificador para fosseis de cranios humanos.

![Cranios](https://anthropologynet.files.wordpress.com/2007/06/fossil-hominid-skulls.jpg) 
*"Fossil hominid skulls. Some of the figures have been modified for ease of comparison (only left-right mirroring or removal of a jawbone). (Images © 2000 Smithsonian Institution.) . - [Cortesia](https://anthropology.net/2007/06/11/fossil-hominid-skulls/fossil-hominid-skulls/)"*


O primeiro desafio foi encontrar um dataset que tivesse as dimenções do cranio, a idade e a especie a que pertence.
Depois de alguma pesquisa encontrei esta [wiki](http://phylo.wikidot.com/fun-with-hominin-cranial-capacity-through-time#toc1) com um excel com a compilação destes dados. Os dados foram recolhidos de um [artigo](https://www.sciencedirect.com/science/article/abs/pii/S0018442X04700025?via%3Dihub) publicado por De Miguela e M.Henneberga em 2001.

O ficheiro contem varias observaçoes mas para esta analise aquenas irei considerar o 'ID', o 'Taxon' a 'Data' a a capacidade craniana media 'mean'.

| ID              | Taxon   |   Date |   mean |
|:----------------|:--------|-------:|-------:|
| AL 288-1 (Lucy) | af      |   3200 |  380   |
| AL 288-1 (Lucy) | af      |   3200 |  410   |
| AL162-28        | af      |   3200 |  400   |
| AL162-28        | af      |   3200 |  375   |
| AL162-28        | af      |   3200 |  387.5 |

Esta tabela contem 603 entrdas mas devido à utilização de varias metodologias para a estimação da capacidade craniana, existem varios fosseis que aparecem duplicados. Assim vou agrupar a tabela por ID e fazer a mediana da capacidade media de cada mediação.

| ID                     |   Date |   mean | Taxon   |
|:-----------------------|-------:|-------:|:--------|
| AL 288-1 (Lucy)        |   3200 |  395   | af      |
| AL333-105 (adult)      |   3200 |  352   | af      |
| AL333-45               |   3200 |  492.5 | af      |
| AL162-28               |   3200 |  387.5 | af      |
| AL333-105 (5 year old) |   3200 |  317.5 | af      |


Esta nova tabela tem 247 entradas.

Assim podemos vizualizar a evolução temporal da capacidade craniana dos ancestrais do Homem.

Como se trata de um problema de classificação não supervisionado irei utilizar o k-means como metodo para classificar as especies.

![cranial capacity evolution](/assets/img/hominid/cc_by_year.png)

Olhando para o plot não é facil verifical o número de clusters que podemos criar. 
Para resolver esta questão irei o utilizar o metodo Elbow para determinal o numero ideal de clusters.

![Elbow Plot](/assets/img/hominid/hominid_Elbow.png)


O curva passa a ser constante a partir do valor 5 assim, o numero ideal de clusters é 5.

![Clusters](/assets/img/hominid/hominid_clusters.png)

Para verificar a validade destes clusters irei construir um grafico de barras com a frequencia das 8 especies mais frequentes em cada cluster.

![Taxon Frequency](/assets/img/hominid/taxon_freq_cluster.png)

Observando o grafico verifica-se que existe uma grande variação de especies dentro de cada cluster, no entanto é possivel vizualizar um clara separação entre 

Assim concluo que a capacidade craniana não é suficiente para determinal a especie a que o fossil pertence 

