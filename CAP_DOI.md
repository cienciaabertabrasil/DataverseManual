<a href="http://www.ibict.br" target="_blank"><img src="./imagens/ibict.jpeg" alt="Ibict" style="zoom:40%;" /></a> <a href="https://dataverse.org" target="_blank"><img src="./imagens/dataverse.png" alt="Dataverse" style="zoom:55%;" /></a>

> Este manual foi elaborado inicialmente pela equipe de bolsistas do [**Instituto Brasileiro de Informação em Ciência e Tecnologia (Ibict)**](http://www.ibict.br/){:target="_blank" rel="noopener"}, e aberto à comunidade brasileiro de usuários do [Dataverse](https://dataverse.org/){:target="_blank" rel="noopener"}.


# Serviço DOI


# Configurar Dataverse 

A configuração seguirá a implementação para o identificador persistente utilizando o serviço DataCite. As configurações serão realizadas via terminal, utilizando comando pro URL(curl).

A escolha do provedor Doi deve ser explicitado como "DataCite" ou "Handle", nesse caso vamos utilizar a o "Datacite". Como apresentado no comando abaixo, é atribuido o termo "DataCite" à variavel DoiProvider.

```shell
# curl -X PUT -d DataCite http://localhost:8080/api/admin/settings/:DoiProvider
```

O protocolo "doi" ou "hdl" são os possíveis protocolos utilizado no Dataverse. O comando abaixo atribui o valor "doi" a variável Protocol.

```shell
# curl -X PUT -d doi http://localhost:8080/api/admin/settings/:Protocol
```


```shell
# ./asadmin delete-jvm-options '-Ddoi.mdcbaseurlstring=https\://api.test.datacite.org'
```

```shell
# ./asadmin create-jvm-options '-Ddoi.mdcbaseurlstring=https\://api.datacite.org'
```
A autorização do serviço é número prefix selecionado no serviço Datacite. O prefixo inicia com "10.", seguindo por mais digitos, o comando logo abaixo mostra como deve ser atribuido o valor "10.xxxx" à varrável Authority, lembrando que o "10.xxxx" deve ser substituido pelo o prefix individual do repositório.

```shell
# curl -X PUT -d 10.xxxx http://localhost:8080/api/admin/settings/:Authority
```

Os arquivos depositados no Dataverse carregam no registro DOI um endereço inicial, denominado shoulder. O shoulder é escolhido de forma arbitrairia, no exemplo abaixo o shoulder seria "Sigla"

```shell
# curl -X PUT -d "Sigla/" http://localhost:8080/api/admin/settings/:Shoulder
```


```shell
# ./asadmin delete-jvm-options '-Ddoi.username=YOUR_USERNAME_HERE'
```

```shell
# ./asadmin create-jvm-options '-Ddoi.username=YOUR_USERNAME_HERE'
```


Primeiro é necessário verificar se já há alguma configuração 
```shell
# ./asadmin delete-jvm-options '-Ddoi.password=YOUR_PASSWORD_HERE'
```

```shell
# ./asadmin create-jvm-options '-Ddoi.password=YOUR_PASSWORD_HERE'
```



- reiniciar o glassfish

# Depositar e publicar
