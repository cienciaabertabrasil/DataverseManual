# Manual do Dataverse
Manual do Dataverse


## Contribuidores

[Lista completa de contribuidores](./contribs.md){:target="_blank" rel="noopener"}.



# Instalação

O Sistema Operacional utilizado neste tutorial de instalação foi o Linux, distribuição **Debian 10**. 
Esse sistema operacional foi escolhido por ser um dos mais utilizado em servidores de instituições acadêmicas. 
Os programas são instalados utilizando o programa gestor de pacotes _APT_, 
 contudo, por conta de problemas de compatibilidade, alguns programas serão instalados manualmente.

## Pré-requisitos

É necessário a autorização de administrador ou de _superusuário_ em algumas etapas da instalação, 
com isso, recomenda-se estar logado como _root_ durante a instalação, ou possuir usuário com _sudo_ configurado. 
Todos os comandos com permissão especial serão executados com _sudo_ a frente. Exemplo:

```linux
$ sudo apt update
```

Uma forma alternativa de execução de comandos como _superusuário_ é, tendo conhecimento da senha de _root_, executar o comando: 

```linux
$ su -
```

Para retornar ao usuário comum, basta executar:

```linux
# exit
```

A primeira coisa a se fazer, depois de acessar como superusuário, é atualizar a base de dados do gestor de pacotes:

```linux
$ sudo apt update
$ sudo apt upgrade
```



Em seguida, devem ser instalados alguns pacotes e programas básicos, que serão utilizados durante a instalação, como o descompactador _unzip_,  o programa para versionamento de código _git_:

```linux
$ sudo apt install git postgresql jq 
```



Crie um usuário de nome _dataverse_ para vinculá-lo aos pacotes baixados e à instalação da instância do Dataverse:

```linux
$ sudo useradd -m dataverse
```



Ao se criar o usuário, também será criada uma pasta no diretório _/home/_ como o nome _dataverse_.  É necessário mudar as permissões da pasta _/home/dataverse_ para que o usuário que executa a instalação possa salvar arquivos e realizar modificações neste diretório. Substitua _user_ pelo nome do usuário que executa a instalação e proceda com o seguinte comando:

```linux
$ chown -R user:user /home/dataverse
```

Acesse a pasta _/home/dataverse_ e crie um diretório temporário _temp_, onde serão baixados alguns dos programas e pacotes necessários para a instalação.

```linux
$ cd /home/dataverse
$ mkdir temp 
$ cd temp
```



### Java Oracle (JDK 8)

O pacote _Java_ 8 pode ser instalado utilizando o programa _apt_, contudo, por questão de compatibilidade, recomendamos baixar este pacote diretamente do sítio da _Oracle_. Acesse a página de downloads:

> [https://www.oracle.com/java/technologies/javase-jdk8-downloads.html](https://www.oracle.com/java/technologies/javase-jdk8-downloads.html)

 Faça o download da versão mais recente do pacote _jdk-8uxxx-linux-x64.tar.gz_ e transfira-o para a pasta recém-criada _/home/dataverse/temp_.

> Infelizmente, é necessário ter uma conta de acesso configurada na _Oracle_ para concluir o download.

Descompacte o arquivo _jdk-8uxxx-linux-x64.tar.gz_ transferido (lembre-se de substituir _xxx_ pelo número correto da versão baixada.

```linux
$ cd temp
$ tar -vzxf jdk-8uxxx-linux-x64.tar.gz
```

Crie a pasta de instalação da JDK.

```linux
$ sudo mkdir /usr/java
```

Mova a pasta criada da descompactação do arquivo (_jdk1.8.xxx/_) para dentro da pasta recém-criada (_/usr/java_).

```linux
$ sudo mv jdk1.8.xxx/ /usr/java/
```





Text can be **bold**, _italic_, or ~~strikethrough~~.

There should be whitespace between paragraphs.

There should be whitespace between paragraphs. We recommend including a README, or a file with information about your project.

This is a normal paragraph following a header. GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

## Header 2

> This is a blockquote following a header.
>
> When something is important enough, you do it even if the odds are not in your favor.

### Header 3

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```


```

```