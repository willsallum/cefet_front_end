<!-- {"layout": "title"} -->
# Introdução a **servidores Web**
## Apache, PHP, MySQL e os piratas :crown: x2

---
<!-- {"layout": "centered"} -->
# O que veremos hoje

1. [O que é um servidor](#servidor-web)
	 - [O servidor Apache](#servidor-apache)
1. [PHP: PHP Hypertext Preprocessor](#php)
1. [Bancos de dados](#bancos-de-dados) e o MySQL
1. [Piratas e seus Tesouros](#tesouros-de-piratas-dinamicos) :crown: x2

*[PHP]: PHP Hypertext Preprocessor*

---
<!-- {"layout": "section-header", "hash": "servidor-web"} -->
# Servidor Web
## O que come, onde vive

- Como fizemos até hoje?
- O que faz um servidor Web?
- Página estática vs página dinâmica
- Servidor Apache
<!-- {ul:.content} -->

---
## Como fizemos até agora

- Nas práticas
	- Foram criados arquivos (HTML, CSS, etc) e, os mesmos, foram exibidos no
    navegador
	- Os arquivos de um computador não podiam ser visualizados em outro
- Para disponibilizar para demais computadores, precisamos de um serviço que:
	- **Mantenha** os arquivos
	- A partir de um **requisiçäo**, **envie** os arquivos solicitados
	- **Controle** os determinados erros que poderiam ocorrer
		- Página inexistente, falta de permissão
- Para isso, usaremos um **servidor Web** e nos comunicaremos por meio do
  **protocolo HTTP**

---
<!-- {"embedSVG": "img[src$='.svg']", "styles": ["../../styles/classes/http-diagram.min.css"], "backdrop": "oldtimes"} -->
## Relembrando, o protocolo **HTTP**

- É um **protocolo** na camada de aplicação
  > Conjunto de regras bem definidas descrevendo como
  > entidades se comunicam.
  - É a **"língua falada" pelo navegador e pelo servidor web**
- Modelo requisição &rarr; resposta

::: figure .http-diagram.flex-align-center.figure-slides.clean.no-margin
![](../../images/http-diagram-informal.svg) <!-- {.step-1 style="height: 280px"} --> <!-- {p:.bullet.figure-step.bullet-no-anim} -->

![](../../images/http-diagram-informal.svg) <!-- {.step-2 style="height: 280px"} --> <!-- {p:.bullet.figure-step.bullet-no-anim} -->

![](../../images/http-diagram-informal.svg) <!-- {.step-3 style="height: 280px"} --> <!-- {p:.bullet.figure-step.bullet-no-anim} -->
:::

---
<!-- {"layout": "2-column-content", "embedSVG": "img[src$='.svg']", "backdrop": "oldtimes"} -->
### **Navegador requisita** algo e **Servidor responde**

- ![](../../images/http-diagram-informal.svg) <!-- {.full-width.centered.step-3} --> <!-- {ul:.http-diagram.no-bullets.no-padding.bullet} -->
  Requisição:
  ```http
  GET /index.html HTTP/1.1
  Host: www.twitter.com
  ```

1. Resposta: <!-- {ol:.bullet.no-bullets.no-padding.compact-code} -->
   ```http
   HTTP/1.1 200 OK
   Date: Mon, 23 May 2005 22:38:34 GMT
   Server: Apache/1.3.3.7 (Unix) (Red-Hat/Linux)
   Content-Type: text/html; charset=UTF-8
   Content-Length: 131

   <!DOCTYPE html>
   <html>
   <head>
     <title>Twitter</title>
   </head>
   <body>
     Olá mundo, este é um tweet.
   </body>
   </html>
   ```


---
::: figure .figure-slides.full-width-slides
![Carregando uma página com um servidor vs sem](../../images/carregando-pagina-servidor-vs-local-1.png) <!-- {.bullet.figure-step.bullet-no-anim} -->
![Carregando uma página com um servidor vs sem](../../images/carregando-pagina-servidor-vs-local-2.png) <!-- {.bullet.figure-step.bullet-no-anim} -->
![Carregando uma página com um servidor vs sem](../../images/carregando-pagina-servidor-vs-local-3.png) <!-- {.bullet.figure-step.bullet-no-anim} -->
![Carregando uma página com um servidor vs sem](../../images/carregando-pagina-servidor-vs-local-4.png) <!-- {.bullet.figure-step.bullet-no-anim} -->
:::

---
## O que faz um servidor Web?

- O servidor Web **precisa**:
  1. Saber "falar" o protocolo HTTP para atender as requisições
  1. Conhecer o sistema de arquivos do SO para entregar arquivos solicitados
		 (JS, HTML, CSS, imagens etc.)
- O servidor Web **pode** (opcional... alguns fazem, outros não):
  1. Executar algum arquivo escrito em alguma linguagem de programação
  1. Permitir a geração dinâmica de arquivos HTML (_e.g._, usando PHP)
  1. Permitir a recepção de arquivos (_e.g._, cliente fazendo _upload_)
  1. Entender outros protocolos além de HTTP: HTTPS, FTP, etc.
  1. Gerenciar conexões simultâneas de vários "solicitantes"

*[SO]: Sistema Operacional*

---
## Páginas HTML **estáticas** vs páginas **dinâmicas** <!-- {.alternate-color} -->

Pág. **estáticas**
	~ O servidor simplesmente entrega um arquivo .html da forma como ele foi
		criado pelo programador
	~ É o que temos feito

Pág. **dinâmicas** <!-- {.alternate-color} -->
	~ Podem exibir um conteúdo diferente, dependendo:
		- Usuário que está logado
		- Parâmetros de entrada
		- Além disso, elas podem exibir conteúdo que está armazenado
			em um **banco de dados**
	~ É o que vamos fazer hoje!

---
<!-- {"layout": "2-column-content"} -->
## Site das ovelhas: páginas **estáticas**

![Exemplo de uma página estática](../../images/pag-estatica.png)<!-- {style="height: 50vh;"} -->

- Exemplo:
	- Existe um arquivo `index.html` para a página inicial
	- +1 arquivo `.html` para cada raça
		- `algodovelha.html`
		- `piratovelha.html`
		- `ovelho-pixel.html`
	- Problema: precisa-se <u>repetir muito código</u> HTML entre uma página e outra

---
## Site das ovelhas: páginas **dinâmicas** <!-- {.alternate-color} -->

::: figure .figure-slides.clean
![Páginas dinâmicas](../../images/pag-dinamica-1.png) <!-- {.bullet.figure-step.bullet-no-anim style="max-width: 100%"} -->
![Páginas dinâmicas](../../images/pag-dinamica-2.png) <!-- {.bullet.figure-step.bullet-no-anim style="max-width: 100%"} -->
![Páginas dinâmicas](../../images/pag-dinamica-3.png) <!-- {.bullet.figure-step.bullet-no-anim style="max-width: 100%"} -->
![Páginas dinâmicas](../../images/pag-dinamica-4.png) <!-- {.bullet.figure-step.bullet-no-anim style="max-width: 100%"} -->
![Páginas dinâmicas](../../images/pag-dinamica-5.png) <!-- {.bullet.figure-step.bullet-no-anim style="max-width: 100%"} -->
:::

---
## O que é uma **URL**? <small>Unique Resource Locator </small>

![As partes de uma URL](../../images/url-parts.svg) <!-- {.block.full-width} -->
  
domínio <!-- {dl.bulleted} -->
~ Em que computador estão os arquivos

porta
~ Qual endereço do programa dentro do computador

caminho
~ Qual o endereço até o arquivo

**_query string_**
~ Identificar o que se deseja mostrar - por exemplo, o código identificador da ovelha

O _back-end_ pode usar a _query string_ para fazer uma busca no
banco de dados e retornar informações sobre algo específico. <!-- {p:.note.info} -->


*[URL]: Unique Resource Locator*

---
## Servidores Web

- Exemplos de Servidores Web:
	1. **Apache**
	1. Tomcat
	1. JBoss
	1. IIS
	1. Nginx
	1. **http-server** <!-- {strong:.alternate-color} --> <!-- {ol:.multi-column-list-3} -->
- Vejamos um exemplo de servidor web que simplesmente envia arquivos
	estáticos (`.html`, `.js`, `.css`, imagens etc.):
	```
	http-server .
	```
- Além de servir arquivos estáticos, eles podem executar _scripts_ (programas)
	em diversas outras linguagens:
	- PHP, Python, Java, ASP .NET etc.
- A esses programas, que executam em um servidor web, damos o nome de
	**_back-end_** (digamos, a "parte oculta" de um site)

---
<!-- {"hash": "servidor-apache"} -->
## **Apache**

- O servidor web mais utilizado desde 1995
- Tipicamente (mas não exclusivamente) associado à linguagem PHP
- Motivos para seu sucesso:
  1. Projeto altamente modularizado e configurável
  1. Gratuito
  1. Extensível
  1. Bom desempenho
  1. Multi-plataforma (Linux, Windows, OSX)

---
<!-- {"layout": "section-header", "hash": "php"} -->
# PHP
## Hypertext Preprocessor

- Sintaxe Básica
- Condicionais
- Estrutura de Repetição
- Vetores
<!-- {ul:.content} -->

---
## PHP - Hypertext Preprocessor

- É uma linguagem amplamente usada
- É executada **no servidor** para preprocessar e gerar HTML dinamicamente
- O código PHP é tipicamente mesclado ao HTML
	- Mas existem formas mais organizadas
- Assim, todo código PHP deve iniciar por `<?php` e finalizar com `?>`

```php
...
<body>
  <h1>Produto: <?php echo produto["nome"]; ?></h1>
</body>
</html>
```

---
<!-- {"layout": "2-column-content", "hash": "for-formas-preferiveis"} -->
## PHP - Sintaxe Básica

1. `echo`: exibe no HTML o que for passado como parametro. Exemplo, arquivo `index.php`:
```php
<html>
<head>...</head>
<body>
  <?php echo "<p>Olá Mundo</p>"; ?>
</body>
</html>
```
- O servidor irá ler `index.php`, processá-lo e enviar ao navegador o
	seguinte código HTML:
```html
<!DOCTYPE html>
<html>
<head>...</head>
<body>
  <p>Olá Mundo</p>
</body>
</html>
```

---
## PHP - **Variáveis**

- Variáveis não precisam ser declaradas
- Toda a variável inicia-se com o caractere `$`
- Exibir a variável no HTML: `echo` (tipo `printf` do C)
- Para concatenação de strings, usa-se o ponto `.`
- Com aspas duplas, o PHP faz substituição das variáveis na string:
  ```php
  <?php
    $a = 1;
    echo $a; //imprime: 1
    echo "resultado: " . $a;  // imprime: resultado: 1
    echo "resultado: $a";     // imprime: resultado: 1
    echo 'resultado: $a';     // imprime: resultado: $a
  ?>
  ```

---
## PHP - **Condicionais**

- Condicionais possuem a sintaxe similar ao JavaScript:
  ```php
  <?php
    $a = 1;
    $b = rand(); // rand(): retorna um número inteiro aleatório
    echo "b: $b";  
    if ($a > $b) {
      echo "'a' é maior que 'b'!";
    } else {
      echo "'b' é maior ou igual a 'a'!";
    }
  ?>
  ```

---
## PHP - Estrutura de repetição - **for**

- Também possui a sintaxe similar ao JavaScript
  ```php
  <?php $numero = rand(2,9); 			// aleatório entre 2 e 9 	?>
  <h1>Tabuada do <?php echo $numero ?></h1>
  <ul>
  <?php
    for($i = 1; $i < 10; $i++) {
      $resultado = $i * $numero;
      echo "<li>$i x $numero = $resultado</li>";
    }
  ?>
  </ul>
  ```

---
## PHP - Estrutura de repetição - **while**

```php
<?php $numero = rand(2,9); 			// aleatório entre 2 e 9 	?>
<h1>Tabuada do <?php echo $numero ?></h1>
<ul>
<?php
  $i = 1;
  while($i < 10) {
    $resultado = $i * $numero;
    echo "<li>$i x $numero = $resultado</li>";
    $i++;
  }
?>
</ul>
```

---
<!-- {"classes": "compact-code"} -->
## PHP - **Vetores** (_Arrays_) <small>(1/2)</small>

- Inicialização:
  ```php
  <?php $frutas =  array("kiwi", "morango", "uva"); ?>
  ```
- Percorrendo o _array_:
  ```php
  <?php
    echo("<ul>");
    for ($i = 0; i < count($frutas); $i++) {
      echo("<li>{$frutas[$i]}</li>");
    }
    echo("</ul>");
  ?>
  ```
	- para imprimirmos um valor do _array_ em uma string, colocar chaves
- A função `count` retorna o tamanho do _array_

---
<!-- {"classes": "compact-code"} -->
## PHP - Vetores <small>(2/2)</small>

- _Arrays_ em PHP são, na verdade, **mapas ordenados**:
	- mapeiam uma *chave* a um *valor*
- Exemplo:
  ```php
  <?php
    $personagem = array(nome => "luke",
                        pontos => 123);

    $personagem["pontos"] += 100;

    echo("O personagem {$personagem['nome']} possui {$personagem['pontos']}");
  ?>
  ```
	- São parecidos com os objetos em JavaScript!

---
<!-- {"layout": "section-header", "hash": "bancos-de-dados"} -->
# Bancos de Dados

- Por que centralizar dados?
- SGBDs
- Entidades e Relacionamentos
- Tabelas e Registros
- Cláusula SELECT
- PHP e MySQL
<!-- {ul:.content} -->

---
## Centralizando dados

- Servidores são úteis para **centralizar dados**, para, por exemplo:
	- salvar/ler mensagens de um bate-papo;
	- apresentar/escrever e-mails;
	- exibir/escrever posts de um blog;
	- exibir e registrar compras de produtos de um site de compra.
- Para centralizar, temos que armazenar estes dados em:
	- Arquivos ou
	- Bancos de Dados
- Bancos de dados armazenam os seus dados de uma forma:
	- mais **estruturada**
	- favorecendo o **uso por muitos usuários**

---
## **S**istema de **G**erenciamento de **B**anco de **D**ados

- **SGBD**: É um conjunto de ferramentas para gerenciar *bancos de dados*
- São exemplos de SGBDs:
	- **MySQL**
	- Postgres
	- Oracle
	- MS SQL Server <!-- {ul:.multi-column-list-4} -->
- Usaremos o **MySQL** por ser gratuito, multiplataforma
	e popular
	![Site oficial do MySQL](../../images/mysql-com.png) <!-- {style="max-width: 100%"} -->

*[SGBD]: Sistema de Gerenciamento de Banco de Dados

---
## **Entidades** e **Relacionamentos** <!-- {.alternate-color} -->

- Um banco de dados é formado por um conjunto de *entidades* com *relacionamentos* <!-- {ul:.bulleted-0} -->
- **Entidades** podem ser abstratas ou concretas:
	- **Pessoa**, **Carro**, **Alimento**, **Pedido**, **Transação Bancária**
- Cada entidade pode ter **relacionamentos** <!-- {.alternate-color} --> com outras:
	- Uma **pessoa** **faz** <!-- {.alternate-color} --> diversas **transações bancárias**
	- Um **carro** **possui** <!-- {.alternate-color} --> uma **pessoa** que é seu dono
	- Uma **pessoa** pode **fazer** <!-- {.alternate-color} --> diversos **pedidos de compra**
- Em SGBDs, *entidades* são representadas por _tabelas_ <!-- {.underline.upon-activation.delay-1600} -->

---
## Tabelas e registros <small>(ou "linhas")</small>

- Uma entidade é representada por uma ou mais **tabelas** em um SGBD
- Tais tabelas possuem um conjunto de **registros**
- Na tabela, cada linha é um **registro** e cada coluna é um **campo**
	que descreve aquela entidade

![Tabela de ovelhas](../../images/sql-tabela-e-registros.png) <!-- {p:.centered} -->

Para interagir com um SGBD, precisamos de uma linguagem...<!-- {p:.note.info} -->

---
## SQL - Structured Query Language

- Tendo um conjunto de tabelas, precisamos de uma linguagem para:
	1. Manipular e pesquisar nos registros
	1. Criar, alterar a estrutura das tabelas
	1. Conceder e retirar permissões de usuários, etc.
- Para isso, foi criado o **SQL** que é uma linguagem padrão que a maioria dos SGBDs adotam (com algumas adaptações)
- Na aula de hoje, iremos aprender a consultar os registros que uma tabela possui usando a cláusula SQL **SELECT**

*[SQL]: Structured Query Language

---
<!-- {"layout": "centered"} -->
# SQL - Cláusula **SELECT**

![Formato da clausula SELECT](../../images/sql-formato.png)

---
## SQL - Cláusula **SELECT** - Exemplo <small>(1/3)</small>

- Seleciona todas as colunas e registros da tabela `RACA_OVELHA`

![Seleciona todos os registros e colunas](../../images/sql-exemplo1.png) <!-- {p:.centered} -->

---
## SQL - Cláusula **SELECT** - Exemplo <small>(2/3)</small>

- Seleciona o nome de todas as raças de ovelha (i.e. tabela `RACA_OVELHA`)

![Seleciona o nome de todas as raças de ovelha](../../images/sql-exemplo2.png) <!-- {p:.centered} -->

---
## SQL - Cláusula **SELECT** - Exemplo <small>(3/3)</small>

- Seleciona o nome e alimento preferido de todas as raças de ovelha (i.e. tabela `RACA_OVELHA`) em que a expectativa de vida é menor que 5 anos

![Seleciona o nome e o alimento preferido de todas as raças de ovelha com expectativa de vida menor que 5](../../images/sql-exemplo3.png) <!-- {p:.centered} -->

---
## PHP e MySQL - Exemplo <small>(1/2)</small>

- Para usarmos o MySQL no PHP precisamos conectar ao MySQL: <!-- {ul:.full-width.compact-code} -->
  ```php
  <?php
    // faz a conexão com o banco de dados
    $db = mysqli_connect("localhost", "root", "123456", "piratas");
    $db->set_charset("utf8");
    // verifica se a conexão funcionou...
    if (!$db) {
      // encerra a execução do script php, dando um erro
      $descricaoErro = "Erro! Detalhes: " . mysqli_connect_error();
      die($descricaoErro);
    }
  ?>
  <!DOCTYPE html>
  <html>
  <head>
    ⋮
  ```

---
## PHP e MySQL - Exemplo <small>(2/2)</small>

- Logo após, podemos fazer uma consulta, por exemplo, exibindo todas as raças de ovelha: <!-- {ul:.full-width.compact-code} -->
  ```php
  <?php
    $sql = "SELECT nome, alimento_preferido FROM raca_ovelha";
    $result = $db->query($sql); // $db é a conexão obtida
    if ($result->num_rows > 0) {
      echo("<ul>");
      while($linha = $result->fetch_assoc()) {
        $html = "<li>Ovelhas da raça <strong>{linha['nome']}</strong>";
        $html .= "gostam de {linha['alimento_preferido']} </li>"
        echo($html);
      }	  
      echo("</ul>");
    } else {
      echo("<p>Não existem ovelhas cadastradas</p>");
    }
  ?>
  ```


---
<!-- {"layout": "section-header", "hash": "tesouros-de-piratas-dinamicos"} -->
# Piratas Dinâmicos
## Barba-Ruiva + Apache, PHP e MySQL

- Instalando Apache, PHP e MySQL
- Atividade de hoje
<!-- {ul:.content} -->

---
<!-- {"backdrop": "piratas-php"} -->

---
## Instalando Apache, PHP e MySQL

- **<u>Pergunte ao professor</u> se é necessário instalar algo** nos
  laboratórios
  - É provável que já esteja tudo funcionando... de qualquer forma, leia sobre
    como fazê-lo
- Podemos instalar (a) cada software separadamente ou (b) um pacote que
  instala todos de uma vez _(mais fácil)_
  - (a) Visite os sites oficiais: [Apache][apache], [MySQL][mysql], [PHP][php]
  - (b) [WAMP][wamp] (para Windows), [LAMP][lamp] (para Linux)
    ou [XAMPP][xampp] (ambos)
- Ao instalar, lembre-se apenas de **<u>anotar o usuário</u> (normalmente
  'root') <u>e senha</u> escolhidos para o MySQL**

*[WAMP]: Windows, Apache, MySQL e PHP*
*[LAMP]: Linux, Apache, MySQL e PHP*

[apache]: https://httpd.apache.org/download.cgi
[mysql]: https://www.mysql.com/downloads/
[php]: http://php.net/downloads.php
[wamp]: http://www.wampserver.com/en/
[lamp]: https://howtoubuntu.org/how-to-install-lamp-on-ubuntu
[xampp]: https://www.apachefriends.org/pt_br/index.html

---
<!-- {"layout": "2-column-content"} -->
## Atividade de hoje

![](../../images/piratas-php-inicial.jpg) <!-- {.full-width} -->

![](../../images/piratas-php.jpg) <!-- {.full-width} -->

- Torne a página dos tesouros do Barba-Ruiva uma página dinâmica usando
  o Apache, PHP e um banco de dados MySQL <!-- {ul:.span-columns} -->
- Veja o [enunciado completo][enunciado-pirates] no Github

[enunciado-pirates]: https://github.com/fegemo/cefet-front-end-pirates/tree/master-php

---
<!-- {"layout": "centered"} -->
# Referências

1. [Site do Apache](http://apache.org)
1. [Guia PHP](http://php.net/manual/pt_BR/langref.php)
2. [Guia MySQL](https://dev.mysql.com/doc/refman/5.7/)
