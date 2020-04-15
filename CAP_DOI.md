<a href="http://www.ibict.br" target="_blank"><img src="./imagens/ibict.jpeg" alt="Ibict" style="zoom:40%;" /></a> <a href="https://dataverse.org" target="_blank"><img src="./imagens/dataverse.png" alt="Dataverse" style="zoom:55%;" /></a>

> Este manual foi elaborado inicialmente pela equipe de bolsistas do [**Instituto Brasileiro de Informação em Ciência e Tecnologia (Ibict)**](http://www.ibict.br/){:target="_blank" rel="noopener"}, e aberto à comunidade brasileiro de usuários do [Dataverse](https://dataverse.org/){:target="_blank" rel="noopener"}.

# Contribuidores

[Lista completa de contribuidores](./contribs.md){:target="_blank" rel="noopener"}.

# Identificador Persistente e Publicação de Dataset


# Configurar dataverse 
```shell
# curl -X PUT -d DataCite http://localhost:8080/api/admin/settings/:DoiProvider
```

```shell
# curl -X PUT -d 10.xxxx http://localhost:8080/api/admin/settings/:Authority
```
```shell
# curl -X PUT -d doi http://localhost:8080/api/admin/settings/:Protocol
```

```shell
# curl -X PUT -d "MyShoulder/" http://localhost:8080/api/admin/settings/:Shoulder
```
```shell
# ./asadmin create-jvm-options '-Ddoi.mdcbaseurlstring=https\://api.datacite.org'
```

```shell
# ./asadmin create-jvm-options '-Ddoi.username=YOUR_USERNAME_HERE'
```

```shell
# ./asadmin create-jvm-options '-Ddoi.password=YOUR_PASSWORD_HERE'
```



- reiniciar o glassfish

# Depositar e publicar
