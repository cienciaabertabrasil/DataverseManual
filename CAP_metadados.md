<a href="http://www.ibict.br" target="_blank"><img src="./imagens/ibict.jpeg" alt="Ibict" style="zoom:40%;" /></a> <a href="https://dataverse.org" target="_blank"><img src="./imagens/dataverse.png" alt="Dataverse" style="zoom:55%;" /></a>

> Este manual foi elaborado inicialmente pela equipe de bolsistas do [**Instituto Brasileiro de Informação em Ciência e Tecnologia (Ibict)**](http://www.ibict.br/){:target="_blank" rel="noopener"}, e aberto à comunidade brasileiro de usuários do [Dataverse](https://dataverse.org/){:target="_blank" rel="noopener"}.

# Contribuidores

[Lista completa de contribuidores](./contribs.md){:target="_blank" rel="noopener"}.

# Configuração de Metadados

-Opções 

* name
  Nome que será atribuido ao metadado e ao bloco de metadados
* title
  Nome do  
* dataverseAlias
  
* displayName
* blockURI
* fieldType
* displayOrder
* displayFormat
* advancedSearchField	
* allowControlledVocabulary	
* allowmultiples	
* facetable	
* displayoncreate	
* required	
* parent	
* metadatablock_id	
* termURI

```shell
# curl http://localhost:8080/api/admin/datasetfield/load -H "Content-type: text/tab-separated-values" -X POST --upload-file /tmp/new-metadata-block.tsv
```
Atualização do bloco de metadados Citation Metadata(citation.tsv)

```shell
# curl http://localhost:8080/api/admin/datasetfield/load -H "Content-type: text/tab-separated-values" -X POST --upload-file citation.tsv
```

```shell
# curl http://localhost:8080/api/admin/index/solr/schema
```
