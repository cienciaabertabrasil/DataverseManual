# Manual do Dataverse
Manual do Dataverse


## Contribuidores

[Lista completa de contribuidores](./contribs.md){:target="_blank" rel="noopener"}.



# Instalação

O Sistema Operacional utilizado neste tutorial de instalação foi o Linux, distribuição **Debian 10**. 
Esse sistema operacional foi escolhido por ser um dos mais utilizado em servidores de instituições acadêmicas. 
Os programas são instalados utilizando o programa gestor de pacotes _APT_, 
 contudo, por conta de problemas de compatibilidade, alguns programas serão instalados manualmente.

>O procedimento de instalação do Dataverse descrito a seguir exige noções básicas de redes de computadores e comandos executados no terminal do Sistema Operacional Linux.

## Pré-requisitos

É necessário a autorização de administrador ou de _superusuário_ em algumas etapas da instalação, 
com isso, recomenda-se estar logado como `root` durante a instalação, ou possuir usuário com `sudo` configurado. 
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
$ sudo apt install git postgresql jq curl
```

Crie um usuário de nome _dataverse_ para vinculá-lo aos pacotes baixados e à instalação da instância do Dataverse:

```linux
$ sudo useradd -m dataverse
```

Ao se criar o usuário, também será criada uma pasta no diretório `/home/` como o nome `dataverse`.  É necessário mudar as permissões da pasta `/home/dataverse` para que o usuário que executa a instalação possa salvar arquivos e realizar modificações neste diretório. Substitua `user` pelo nome do usuário que executa a instalação e proceda com o seguinte comando:

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

O pacote _Java_ 8 pode ser instalado utilizando o programa _APT_, contudo, por questão de compatibilidade, recomendamos baixar este pacote diretamente do sítio da _Oracle_. Acesse a página de downloads:

> [https://www.oracle.com/java/technologies/javase-jdk8-downloads.html](https://www.oracle.com/java/technologies/javase-jdk8-downloads.html)

 Faça o download da versão mais recente do pacote `jdk-8uxxx-linux-x64.tar.gz` e transfira-o para a pasta recém-criada `/home/dataverse/temp`.

> Infelizmente, é necessário ter uma conta de acesso configurada na _Oracle_ para concluir o download.

Descompacte o arquivo `jdk-8uxxx-linux-x64.tar.gz` transferido (lembre-se de substituir _xxx_ pelo número correto da versão baixada.

```linux
$ cd temp
$ tar -vzxf jdk-8uxxx-linux-x64.tar.gz
```

Crie a pasta de instalação da JDK.

```linux
$ sudo mkdir /usr/java
```

Mova a pasta criada da descompactação do arquivo (`jdk1.8.xxx/`) para dentro da pasta recém-criada (`/usr/java`).

```linux
$ sudo mv jdk1.8.xxx/ /usr/java/
```

Ative o pacote JDK 8 por meio dos comandos:

```linux
$sudo update-alternatives --install /usr/bin/java java /usr/java/jdk1.8.xxx/bin/java 100

$ sudo update-alternatives --install /usr/bin/javac javac /usr/java/jdk1.8.xxx/bin/javac 100
```



### Glassfish

Para instalar o servidor web _Glassfish_ é necessário proceder com o roteiro dado a seguir.

Primeiro, baixe o programa _Glassfish_,  versão 4.1, dentro da pasta `/home/dataverse/temp`.

```linux
$ cd /home/dataverse/temp/

$ wget http://download.oracle.com/glassfish/4.1/release/glassfish-4.1.zip
```

Descompacte o arquivo baixado.

```linux
$ unzip glassfish-4.1.zip
```

Mova a pasta automaticamente criada `glassfish4` para `/home/dataverse`.

```linux
$ mv glassfish4 /home/dataverse/
```

Remova o arquivo `weld-osgi-bundle.jar`, localizado no diretório `/home/dataverse/glassfish4/glassfish/modules/`.

```linux
$ rm /home/dataverse/glassfish4/glassfish/modules/weld-osgi-bundle.jar
```

Baixe a nova versão do arquivo removido dentro de `/home/dataverse/temp`.

```linux
$ curl -L -O https://search.maven.org/remotecontent?filepath=org/jboss/weld/weld-osgi-bundle/2.2.10.Final/weld-osgi-bundle-2.2.10.Final-glassfish4.jar
```

Copie o novo arquivo baixado `weld-osgi-bundle-2.2.10.Final-glassfish4.jar` para dentro do diretório `/home/dataverse/glassfish4/glassfish/modules/`.

```linux
$ cp weld-osgi-bundle-2.2.10.Final-glassfish4.jar /home/dataverse/glassfish4/glassfish/modules/
```

Edite o arquivo  `domain.xml` localizado na pasta `/home/dataverse/glassfish4/glassfish/domains/domain1/config/`, alterando de `-client` para `-server` a tag `<jvm-options>-client</jvm-options>`.

```linux
$ nano /home/dataverse/glassfish4/glassfish/domains/domain1/config/domain.xml
```

Alterar de:

```xml
        <jvm-options>-client</jvm-options>
```

Para:

```xml
        <jvm-options>-server</jvm-options>
```

Copie os certificados de segurança atualizados no pacote _JDK_ 8 baixado para dentro da pasta `/home/dataverse/glassfish4/glassfish/domains/domain1/config/`.

```linux
$ cp /usr/java/jdk1.8.xxx/jre/lib/security/cacerts /home/dataverse/glassfish4/glassfish/domains/domain1/config/cacerts.jks
```

Inicie a execução do _Glassfish_.

```linux
$ /home/dataverse/glassfish4/bin/asadmin start-domain
```

Verifique a versão do progrma _Weld_ em execução,

```linux
$ /home/dataverse/glassfish4/bin/asadmin osgi lb | grep 'Weld OSGi Bundle'
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