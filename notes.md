#08/11/2025


```
cd curso-react-alurabooks
npm start
cd api-alurabooks
npm run start-auth
```

Curso de HTTP: entendendo a web por baixo dos panos

@01-Conhecendo o protocolo HTTP 

@@01
Apresentação

Boas-vindas a este curso sobre HTTP ministrado pelo Geovane Fedrecheski!
Autodescrição: Geovane é um homem de pele clara, barba e cabelos curtos. Ele usa óculos e está à frente de uma parede iluminada por uma luz azul-clara.
Para aprendermos como o HTTP funciona, usaremos o projeto do AluraBooks, um e-commerce de livros sobre programação. O projeto está dividido entre Back-End e Front-End. Vamos instalá-lo e usá-lo como um pano de fundo para compreender o funcionamento do HTTP.

Ao longo do curso, abordaremos:

A relação entre Back e Front-End;
Como os domínios funcionam e qual a sua relação com o HTTP;
Segurança com HTTPS.
Usaremos o navegador para inspecionar a página e usaremos o inspetor para fazer requisições HTTP (requests), ou seja, conversas entre o nosso navegador e o servidor.

Também compreenderemos cada um dos campos exibidos (Status Code, Request Method e assim por diante). Aprenderemos a configurá-los com parâmetros adequados para enviar do cliente para o servidor e, por fim, aprenderemos a deixar o nosso sistema seguro. Como garantimos que o seu login e senha no AluraBooks ficam protegidos de hackers, por exemplo?

Também investigaremos as novas versões do HTTP, já que este é um protocolo que está em constante desenvolvimento.

Pré-requisitos
Para aproveitar bem este curso, é interessante você ter noções em:

Terminal;
Noções em Node.js.
Ainda assim, se você não tiver esses conhecimentos, não tem problema, pois o foco do curso é o HTTP.

Caso você tenha alguma dúvida, aproveite os recursos da nossa plataforma: utilize o Fórum, faça as atividades extras e participe da comunidade no Discord.

@@02
Preparando o ambiente

Para aproveitar melhor o curso, recomendamos que instale o projeto AluraBooks na sua máquina, conforme as instruções abaixo.
O projeto está dividido em duas partes: o backend e o frontend. Para executá-los, vamos precisar de uma versão atualizada do NodeJS. Confira como fazer isso no nosso artigo: Como instalar o Node.js no Windows, Linux e macOS.

Baixando e executando o backend
Abra um terminal (em caso de dúvidas, confira nossos cursos de Linux e CMD do Windows e execute os comandos abaixo:

# baixa nosso backend
git clone https://github.com/alura-cursos/api-alurabooks.git

# entra na pasta do backend
cd api-alurabooks

# instala as dependências que estão listadas no arquivo package.json
npm install

# executa o backend e o disponibiliza através de um servidor no endereço http://localhost:8000
npm run start-auth
COPIAR CÓDIGO
Baixando e executando o frontend
Abra outro terminal e execute os comandos abaixo:

# baixa nosso frontend
git clone https://github.com/alura-cursos/curso-react-alurabooks.git

# entra na pasta do frontend
cd curso-react-alurabooks

# seleciona a versão correta
git checkout aula-5

# instala as dependências
npm install

# compila o frontend e o disponibiliza através de um servidor no endereço http://localhost:3000
npm start
COPIAR CÓDIGO
Prontinho!

Agora você já está preparado para acompanhar todo o nosso curso na prática.

Basta abrir o navegador, e acessar o endereço http://localhost:3000.

https://www.alura.com.br/artigos/como-instalar-node-js-windows-linux-macos

https://cursos.alura.com.br/formacao-comecando-linux

https://cursos.alura.com.br/course/windows-prompt-utilizando-cmd

http://localhost:3000/

@@03
Conhecendo o protocolo HTTP

Transcrição

No vídeo passado, conhecemos o projeto AluraBooks e os tópicos que abordaremos neste curso.
Você sabia que provavelmente já usou o protocolo HTTP várias vezes, apenas hoje? Se você acessou o site da Alura para assistir a este vídeo, você usou o HTTP. Não só o da Alura, mas todos os sites do mundo, usam este protocolo.

Mas como o HTTP funciona? E como podemos usá-lo para construir soluções web funcionais, escaláveis e seguras? Para falar disso, começaremos explorando o nosso projeto e procurando onde está o HTTP no Back-End e no Front-End do AluraBooks.

Abriremos o Terminal e abriremos a pasta do Back-End do projeto. Escreveremos o comando "npm run start-auth" e pressionaremos a tecla "Enter" para iniciar o projeto. O Terminal exibirá a seguinte mensagem:

json-server-api@1.0.0 start-auth
Node server.js
API disponível em http://localhost:8000
Perfeito! Isso significa que o comando funcionou. Em seguida, abriremos em outra aba a pasta do Front-End e vamos iniciá-lo usando o comando "npm start".

Pode ser que o projeto abra automaticamente no seu browser. Caso isso não aconteça, basta copiar o endereço em "Local" exibido no Terminal (http://localhost:3000) e colá-lo na barra de endereço do seu navegador.

Com o Front-End aberto, clicaremos com o botão direito em qualquer lugar da página e selecionaremos Inspecionar (ou "Inspect"). Isso abrirá um menu do lado direito da página. Na parte superior deste menu, procuraremos a aba "Rede" (ou "Network"). Se ela não estiver visível, clicaremos na seta para o lado direito, que exibirá as abas seguintes da lista.

Ao selecionar "Rede", encontraremos uma área em branco, onde serão exibidos diversos logs com informações e mensagens do HTTP. Para interagir com o Front-End, clicaremos no botão "Cadastrar-se" no topo da tela. Essa ação gerará um request HTTP.

Podemos preencher brevemente as informações de cadastro com informações fictícias, apenas para teste (nome, e-mail, endereço, CEP e senha). Ao clicarmos no botão "Cadastrar", obteremos uma mensagem indicando que o usuário foi cadastrado com sucesso e observaremos que o campo em branco na aba "Rede" será preenchido com algumas informações.

Clicaremos no segundo registro, de número 200, e perceberemos que surge uma série de informações do lado direito, na aba "Headers". Abordaremos essas informações em detalhe mais adiante, mas são elas:

Request URL;
Request Method;
Status Code.
Abriremos a aba "Payload", ao lado de "Headers" e observaremos que isso nos dá acesso a um JSON que corresponde exatamente às informações preenchidas pela pessoa usuária na tela de cadastro. Com isso, observamos o HTTP sendo utilizado no Front-End.

Para identificarmos o HTTP trabalhando no Back-End, voltaremos ao Terminal, na aba usada para rodar o Back-End. Perceba que surgiu uma nova linha de log:

POST /public/registrar 200 5.621 ms - 207
Note que o número 200 aparece aqui novamente, além de outras informações, como o tempo total da requisição. O importante é o começo ("POST /public/registrar"). Esta é uma informação que veio do Front-End. O número 200 foi gerado pelo Back-End. Isso evidencia que o HTTP é sempre uma interação entre duas entidades, o cliente e o servidor.

Conhecendo o HTTP
"HTTP" é uma sigla que corresponde a Hypertext Transfer Protocol, ou seja, Protocolo de Transferência de Hipertexto. Ele é um protocolo de comunicação usado para transferir dados na web.

Podemos transferir quaisquer tipos de dados com HTTP: páginas HTML, scripts como o JavaScript, imagens e assim por diante.

A arquitetura HTTP é composta sempre por duas entidades: um cliente e um servidor. Mas isso já é conteúdo para o nosso próximo vídeo. Falaremos mais disso na sequência!

@@04
O significado de HTTP

Neste curso, vamos falar sobre a sigla mais importante da Web: o HTTP. O objetivo é entender o protocolo HTTP detalhadamente. Quanto mais o desenvolvedor souber sobre este protocolo, melhor, pois ele é utilizado em todas aplicações web.
No entanto, não entraremos em detalhes sobre como essas aplicações são criadas e funcionam internamente. Para isso, existem várias plataformas, como NodeJS, PHP ou Java (entre muitas outras) que não abordaremos. Temos cursos dedicados para conhecer estas plataformas. Resumindo, nosso foco será o protocolo HTTP!

No mundo de TI, temos muitas siglas e abreviações. O que menos importa é decorar esses nomes, mas é preciso entender o que há por trás. Pensando nisso,você sabe qual é o significado do HTTP?

Hyper Text Transfer Protocol
 
Em tradução livre, o significado em português seria "Protocolo de Transferência de Hipertexto" (hipertexto é um texto que contém links para outros textos, como por exemplo o HTML que permite o uso de links para outras páginas).
Alternativa incorreta
Help Text Transfer Protocol
 
Alternativa incorreta
High Text Transmission Protocol
 
Parabéns, você acertou!

@@05
Conhecendo a arquitetura do HTTP

Transcrição

No vídeo anterior, entendemos onde encontramos o protocolo HTTP no Front-End e no Back-End do nosso projeto. Agora, vamos nos aprofundar em como essa comunicação entre as duas entidades funciona, a chamada Arquitetura HTTP.
O nosso projeto envolve três partes:

Cliente (navegador);
Servidor Front-End;
Servidor Back-End.
O cliente é exibido no navegador enquanto os nossos dois servidores estão inicializados no Terminal. Até aqui, observamos alguns parâmetros do HTTP no browser, mas como será que essa comunicação acontece?

As camadas da internet
Para responder a essa pergunta, começaremos entendendo melhor quais são as camadas da internet e onde o HTTP se encaixa.

As duas primeiras camadas da internet são a Física e a de Enlace. Nelas, estão as partes físicas que possibilitam a nossa navegação via internet. Podemos citar como exemplos a conexão com cabos de fio, o Wi-fi e até o 5G.

A próxima é a camada de Rede. Um exemplo dessa camada é a conexão IP. Você já deve ter ouvido falar dos endereços IP, certo? Eles se encontram na camada de Rede.

Em seguida, temos a camada de Transporte, que engloba os protocolos TCP e UDP. Essa camada garante que as informações cheguem de um ponto A até um ponto B.

Por fim, temos a camada de Aplicação, onde está o HTTP. Essa camada é composta pelo browser usado no computador e no smartphone e pelos aplicativos instalados no celular. Toda vez que usarmos o HTTP, estamos usando a camada de Aplicação.

Assim, o HTTP é um protocolo da camada de aplicação.
Mas o que seria um protocolo?
Para responder a essa pergunta, usaremos uma analogia: um protocolo é como se fosse uma conversa. Se o nosso navegador pudesse enviar mensagens de WhatsApp para o servidor, a conversa entre eles seria semelhante à imagem abaixo:

Interface similar à de aplicativos de troca de mensagens. No topo, lemos o nome do interlocutor da troca de mensagens "Servidor", com o status "Online". A primeira mensagem diz "Oi, pode mandar o HTML?". A resposta é uma imagem encaminhada, com o fundo preto e um corpo de código em letras brancas ("<body> … </body>"). A próxima mensagem, enviada pelo remetente, diz: "Agora o Javascript…". A resposta é outra imagem encaminhada com um trecho de código escrito em letras brancas ("render () {…}").

O detalhe é que essa interação segue determinadas regras: se o cliente mandar uma mensagem e o servidor não responder, a coisa não funciona. Assim, um protocolo é uma conversa com regras.

E quais seriam as regras do HTTP?

Regras do protocolo HTTP
A primeira regra é que sempre deve haver duas entidades dialogando, sempre um cliente e um servidor.

Essa conversa é sempre iniciada pelo cliente. É o cliente quem pedirá o HTML, por exemplo, e não o contrário. O servidor não decidirá enviar informações ao cliente por conta própria.

Após a requisição do cliente, o servidor envia uma resposta com o que foi solicitado. O protocolo HTTP é baseado em mensagens de texto que seguem uma estrutura específica. Esse texto pode ser lido tanto por pessoas quanto por máquinas.

Por fim, temos uma camada sobre a qual o HTTP roda, ou seja, o Transmission Control Protocol - TCP. Essa é a camada de transporte, relevante para garantirmos que as mensagens HTTP chegarão ao seu destino com sucesso. Com isso, nenhuma das duas entidades ficará sem resposta.

Quais dispositivos podem usar HTTP?
Alguns dispositivos que utilizam o HTTP são:

Servidores;
Notebooks;
Computadores desktop;
Smartphones;
Dispositivos inteligentes conectados à internet.
De modo geral, dispositivos que se conectam à internet possivelmente utilizarão o protocolo HTTP. Alguns dos exemplos menos comuns são geladeiras, lâmpadas conectadas, câmeras de segurança e assim por diante.

Voltando ao nosso projeto, estamos trabalhando com o navegador (cliente), um servidor Front-End e outro servidor Back-End. Como será que o HTTP se encaixa nessa conversa?

O navegador envia um request para o servidor;
O servidor responde conforme o que o navegador pediu;
O navegador envia uma mensagem para o Back-End;
O Back-End processa o requerimento;
Se o requerimento fizer sentido, o Back-End retornará uma resposta adequada.
Devemos nos lembrar que, embora o HTTP possa rodar em vários dispositivos diferentes, o projeto AluraBooks ainda está em um ambiente de desenvolvimento. Por isso, todas as entidades rodam diretamente em um único computador.

Neste vídeo, contextualizamos a Arquitetura do HTTP. Agora você já sabe o que é um cliente e um servidor. Ambos são entidades que se comunicam usando o HTTP e seguem determinadas regras para isso. No próximo vídeo, aprenderemos sobre endereços e URLs.

@@06
Modelo Client-Server

O protocolo HTTP segue o modelo Client-Server, ou seja, a comunicação acontece sempre entre duas entidades com papéis bem definidos: uma é o cliente, e a outra é o servidor. O cliente sempre realiza as requisições, e o servidor envia as respostas.
O que o navegador (como Chrome ou Firefox) representa nesse modelo?

Servidor
 
Alternativa incorreta
Requisição
 
Alternativa incorreta
Cliente
 
Exato, nós que estamos utilizando o navegador somos o cliente do AluraBooks. Já o backend e o frontend, são servidos por dois servidores HTTP distintos.

@@07
Papel do HTTP entre Cliente e Servidor

Aprendemos que o HTTP é baseado em um modelo cliente-servidor, e que ele permite:
ao cliente enviar requisições e receber respostas;
e ao servidor receber requisições e enviar respostas.
Nesse contexto, qual o papel do HTTP nessa interação entre o cliente e o servidor?

Definir uma estrutura de dados.
 
Alternativa incorreta
Definir o melhor algoritmo de pesquisa.
 
Alternativa incorreta
Estabelecer regras de comunicação.
 
O HTTP foi criado para estabelecer regras de comunicação entre o modelo Cliente-Servidor que funciona na Web.
Para ilustrar: se você compreende este texto, é porque sabe português! Para que alguém consiga se comunicar com você, essa pessoa deverá usar o português também (supondo que você desconheça outro idioma). Isso significa que sua regra (protocolo) de comunicação com o mundo é a língua portuguesa, que define a forma com que as informações devem chegar até você (através do vocabulário, da gramática etc.). Uma outra pessoa que conheça português vai usar o mesmo formato, já que vocês têm um idioma em comum.
Na internet, como já vimos, o "idioma" mais comum é o HTTP. Ele é responsável por definir a forma de como os dados são trafegados na rede através de várias regras. Portanto, todo mundo que conhece o idioma HTTP poderá receber, enviar dados e participar dessa conversa!

@@08
Comunicação em HTTP

O HTTP define as regras para comunicação entre o cliente e o servidor. Uma dessas regras diz que há uma parte que sempre inicia a conversa.
Que parte vai iniciar?

Servidor
 
Alternativa incorreta
Cliente
 
Exato, quem inicia a comunicação é sempre o Cliente.
Alternativa incorreta
Camada de transporte

@@09
Para saber mais: Peer-To-Peer

Você já usou torrent para baixar algum arquivo na internet? Caso sim, aproveitou um outro modelo de comunicação, o P2P ou Peer-To-Peer!
O modelo Cliente-Servidor não é o único modelo de comunicação na rede, nem sempre o mais adequado. Por exemplo, imagine que precisemos contar as letras de 20 palavras. No caso do modelo Cliente-Servidor, quem fará esse trabalho é o servidor, certo? E se precisar contar as letras de 1 milhão de palavras? Muito trabalhoso para o servidor, não?

O modelo Cliente-Servidor tenta centralizar o trabalho no servidor, mas isso também pode gerar gargalos. Se cada Cliente pudesse ajudar no trabalho, ou seja, assumir um pouco da responsabilidade do servidor, seria muito mais rápido. Essa é a ideia do P2P! Não há mais uma clara divisão entre Cliente-Servidor, cada cliente também é servidor e vice-versa!

Isto é útil quando você precisa distribuir um trabalho ou necessita baixar algo de vários lugares diferentes. Faz sentido?

Usando algum aplicativo de Torrent, o protocolo utilizado não é o HTTP, e sim o protocolo P2P, como BitTorrent ou Gnutella.

@@10
Comparando com outros protocolos

O HTTP não é o único protocolo de comunicação que existe. Aliás, existem milhares de protocolos no mundo de TI, no entanto o HTTP é de longe o mais popular.
Marque as alternativas que apresentam um protocolo para internet.

FTP
 
File Transport Protocol é um protocolo para transferência de arquivos na Internet.
Alternativa correta
SQL
 
Alternativa correta
BitTorrent
 
Além de ser um protocolo, também é um aplicativo para troca de arquivos na internet.
Alternativa correta
SMTP
 
Simple Mail Transfer Protocol (protocolo simples de transferência de e-mail), protocolo para enviar e-mails.

@@11
Para saber mais: arquitetura da Alura

Agora já sabemos que existe um cliente, o navegador, como Chrome e Firefox, e um (ou mais) servidor HTTP. Para definir as regras de comunicação entre cliente e servidor, existe o protocolo HTTP.
Também já sabemos que o servidor usa alguma plataforma, por exemplo, no AluraBooks temos NodeJS no backend e React no frontend. Mas e aqui no site da Alura, qual plataforma realmente é utilizada? Não é tão fácil de descobrir, pois o HTTP, de propósito, não está focado em alguma plataforma específica e esconde isso de nós. Bom, eu não vou esconder nada e vou contar para vocês que a Alura usa a plataforma Java e o servidor concreto se chama Tomcat.

Também já falamos que o SQL é uma linguagem para consultar o banco de dados. Alura usa SQL para acessar o banco de dados MySQL. Com essas informações já temos uma breve ideia da arquitetura da Alura!

Cliente  <--- HTTP ---> Servidor Java  <--- SQL ---> Banco de dadosCOPIAR CÓDIGO
Analise o seguinte diagrama:

alt: Diagrama vertical em 5 partes que representa a arquitetura do site da Alura, onde se lê, de cima para baixo: navegador Chrome (cliente), HTTP (internet), Tomcat (servidor Java), SQL e MySQL (banco de dados).

Há arquiteturas muito mais complexas, mas a grande maioria usa o protocolo HTTP no topo. O protocolo HTTP garante a conectividade. Isso quer dizer que o protocolo HTTP funciona em todos os lugares, sem ter problemas com firewalls e outras regras de segurança. Nós podemos nos conectar sem maiores problemas com qualquer servidor no mundo!

@@12
O que aprendemos?

Nessa aula, você aprendeu a:
Configurar o AluraBooks, o projeto que utilizaremos ao longo do curso;
Contextualizar o HTTP nas camadas da Internet;
Caracterizar o que é o HTTP, e quais os seus principais componentes;
Identificar a arquitetura das comunicações utilizando HTTP.

#08/11/2025

@02-Aprendendo sobre URLs

@@01
Entendendo URLs

Transcrição

Olá! Estamos mais familiarizados com o projeto e como ele se estrutura em termos de arquitetura, como clientes e servidor, trocando mensagens HTTP, e seguindo as regras dos protocolos.
Agora vamos analisar um pouco as diferentes páginas que podemos acessar usando HTTP e comos nos referimos a cada página específica.

Acessando o navegador no endereço localhost:3000, estamos na aplicação AluraBooks. Aproveitando que já realizamos um cadastro, clicamos em "Login" no canto superior direito. Será exibida uma janela com o título "Login" e os campos "E-mail" e "Senha", abaixo temos um botão "Fazer login".

Dados que o instrutor preencheu para realizar o login:
E-mail: geo@alura.com.br
Senha: 123
Após clicarmos no botão "Fazer login", somos redirecionados para a página inicial, mas perceba que agora no canto superior direito ao invés de "Login" agora está escrito "Minha conta".

E se desejamos compartilhar a página do AluraBooks para um amigo? Ou até mesmo compartilhar a nossa página de perfil, clicando em "Minha conta". Precisamos nomear essas páginas, com um nome que qualquer pessoa entenda e consiga colocar no navegador, e buscar por elas. Mas como nomeamos as páginas?

Dar nome às páginas
Em 1991, o Tim Berners-Lee estava descobrindo o que usamos atualmente como web. E ele estava com essa mesma dúvida: como nomear páginas específicas?

Por exemplo:

Página da maria
https://twitter.com/maria
Vamos supor que uma amiga nossa chamada de Maria decidiu montar uma página. Ela pode colocar apenas "página da maria" ou precisará de mecanismos mais estruturados para nomear essa página e posteriormente se referir a ela para localizá-la?

URL (Uniform Resource Locator)
A resposta obviamente é que precisamos de um mecanismo padronizado, chamamos esse mecanismo de URL (Uniform Resource Locator, em português "Localizador de Recursos Universal").

O localizador nos permite acessar os recursos, que podem ser arquivos HTML, imagens, scripts de JavaScript que carregamos nas páginas, etc. É universal porque, como aprendemos, essas páginas podem ser carregadas em aplicações web, dispositivos móveis, servidor e desktop.

É na URL que nomeamos as páginas.
Vamos analisar o seguinte exemplo do nosso projeto

https://localhost:3000/
Compreenderemos as divisões da URL: o http delimita qual o protocolo utilizado para acessar a página. Nesse caso é o http, mas há outros, como o FTP (File Transfer Protocol) ou SSH (Secure Shell).

O //localhost:3000 é a parte que determina o servidor e qual a porta que a página web está disponível. No nosso caso é o localhost (computador do instrutor) na porta 3000.

Por fim, temos a barra / que representa o caminho (raiz), ou seja, onde está o recurso dentro de determinado servidor. Ao colocarmos a barra, geralmente é o primeiro recurso, a página principal do web site.

Composição da URL:
http: Protocolo
//localhost:3000: sendo "localhost" o servidor e 3000 a porta que a página web está disponível
/: caminho (raiz)
Portanto, a partir da URL https://localhost:3000/ conseguimos carregar a página inicial que está no meu servidor localhost na porta 3000, usando o protocolo HTTP.

Vamos usar esse conhecimento sobre URLs para entender um pouco mais sobre como funciona os domínios, e como podemos estruturar e criar novas páginas no sistema web que estamos desenvolvendo.

@@02
Identificando o protocolo

Acabamos de aprender que URLs são utilizadas para definir, de forma padronizada, como localizar um recurso (como um website ou um arquivo) na Internet. Além disso, vimos que a URL tem um formato padronizado, onde uma parte determina o protocolo, a outra o servidor, e assim por diante. Nesse contexto, analise a URL abaixo:
smb://server/download/videos/http.mp4COPIAR CÓDIGO
Como se chama o protocolo usado nesta URL?

smb
 
O protocolo especificado na URL se chama smb (aquilo que vem antes do ://), é a abreviação de Server Message Block. Ele é utilizado para compartilhar arquivos dentro de uma rede local.
Nesse curso, não iremos necessariamente usar outros protocolos, tais como o smb. No entanto, é importante saber que URLs podem ser usadas por vários protocolos diferentes, o que as torna muito úteis na prática.
Alternativa incorreta
http
 
Nesse caso não usamos o protocolo http.
Alternativa incorreta
ftp
 
Alternativa incorreta, embora o protocolo ftp exista, nesse caso ele não é utilizado. Ele significa File Transfer Protocol e é utilizado para enviar arquivos entre computadores na Internet.

@@03
Recursos na URL

Continuando nosso aprofundamento sobre URLs, vamos relembrar: vimos que os caminhos de uma URL também podem ser chamados de "recursos". Com isso em mente, analise a URL a seguir:
https://cursos.alura.com.br/course/introducao-html-cssCOPIAR CÓDIGO
Qual é o nome do recurso usado nessa URL?

cursos.alura
 
Alternativa incorreta
/course/introducao-html-css
 
O recurso é aquilo que vem depois do nome do servidor.
Falando nisso, uma curiosidade: No início da web, os recursos, na grande maioria, eram arquivos com a extensão .html ou .htm. Até hoje existem vários recursos que são arquivos na web. Mas reparem que a Alura não funciona dessa maneira. Em nenhum momento você acessa um arquivo na Alura. Por exemplo, para ver um curso, você usa a URL (:
https://cursos.alura.com.br/course/introducao-html-cssCOPIAR CÓDIGO
Perceba que não tem a extensão .html. Isso é um pouco mais legível e possui a vantagem que a URL não diz nada a respeito do formato. A URL não fica amarrada ao formato HTML.
Alternativa incorreta
http

@@04
Para saber mais: URI ou URL?

Muitas vezes, desenvolvedores usam a sigla URI (Uniform Resource Identifier) quando falam de endereços na web. Alguns preferem URL (Uniform Resource Locator), e alguns misturam as duas siglas à vontade. Há uma certa confusão no mercado a respeito e mesmo desenvolvedores experientes não sabem explicar a diferença. Então, qual é a diferença?
Resposta 1 (fácil): Uma URL é uma URI. No contexto do desenvolvimento web, ambas as siglas são válidas para falar de endereços na web. As siglas são praticamente sinônimos e são utilizadas dessa forma.

Resposta 2 (mais elaborada): Uma URL é uma URI, mas nem todas as URI's são URL's! Existem URI's que identificam um recurso sem definir o endereço, nem o protocolo. Em outras palavras, uma URL representa uma identificação de um recurso (URI) através do endereço, mas nem todas as identificações são URL's.

Humm ... ficou claro? Não? Vamos dar um exemplo! Existe um outro padrão que se chama URN (Uniform Resource Name). Agora adivinha, os URN's também são URI's! Um URN segue também uma sintaxe bem definida, algo assim urn:cursos:alura:course:introducao-html-css. Repare que criamos uma outra identificação do curso Introdução ao HTML e CSS da Alura, mas essa identificação não é um endereço.

alt: Diagrama horizontal com duas partes que representa a estrutura de uma URI, da esquerda para a direita: um quadro vermelho indicado como URL com o conteúdo “https://www.alura.com.br/course/introducao-html-css”, e, ao lado, outro quadro em verde indicado como URN com “urn:alura:coure:introducao-html-css”.

Novamente, a resposta 2 vai muito além do que você realmente precisa no dia a dia. Normalmente URL e URI são usados como sinônimos.

@@05
Acessando diferentes portas

Transcrição

Aprendemos como são formados os endereços das URLs, que usamos para acessar os recursos na web através do protocolo HTTP. Agora vamos focar em uma parte das URLs: as portas.
Acessando o navegador no endereço localhost:3000, estamos no nosso projeto AluraBooks. Já aprendemos que o número 3000 é a porta onde a página web está disponível. Mas vamos abrir uma nova aba e acessar o site da Alura .

Endereço do site da Alura: https://www.alura.com.br/
Compare as duas URLs. Observe que não temos o número da porta no endereço de site da plataforma da Alura. Isso acontece porque a maioria dos sites já utilizam uma porta padronizada, que já está especificada no padrão do HTTP, sendo a porta de número 80. Se adicionarmos o número 80 no endereço da Alura, funciona da mesma forma.

https://www.alura.com.br:80COPIAR CÓDIGO
Mas observe que após teclarmos "Enter", mesmo funcionando o navegador removeu a porta 80 do endereço, estamos somente com alura.com.br. Isso ocorre por ser a porta padrão mesmo, e não precisamos ficar exibindo no endereço.

Mas não temos somente a porta 80 como padrão:

Portas padrão
Número da(s) porta(s)	Padrão
80	HTTP
443	HTTPS
de 1023 até 65535	Livres para uso
portas entre 0 e 1023 são reservadas para serviços padronizados.
Nas portas livres para uso, estamos usando a 3000 no nosso front-end, e no back-end usamos a porta de número 8000. Usamos essas portão, então, para não influenciar as portas padrão, e para permitir a execução de mais de um servidor no mesmo computador simultaneamente.

Por fim, essas portas com número maior nos fazem perceber mais facilmente que estamos trabalhando no** ambiente de desenvolvimento**. Ou seja: o nosso projeto AluraBooks ainda não está pronto, estamos desenvolvendo na nossa máquina local.

Neste vídeo, aprendemos sobre as portas padrão e sobre como podemos configurar as portas. Na sequência, vamos entender mais sobre os domínios.

Até mais!

https://www.alura.com.br/

https://www.alura.com.br/

@@06
Porta padrão HTTP

Aprendemos que os protocolos, como o HTTP, podem utilizar portas padronizadas, para simplificar a construção de URL. Sabendo disso, confira a URL abaixo:
http://www.alura.com.brCOPIAR CÓDIGO
Qual é a porta utilizada?

8080
 
Alternativa incorreta
3000
 
Alternativa incorreta
443
 
Alternativa incorreta
80
 
Ela pode ser omitida do endereço pois é a porta padrão do HTTP.

@@07
Entendendo domínios

Transcrição

Já aprendemos bastante sobre URLs, e entendemos detalhes sobre as portas. Agora vamos compreender melhor a parte do servidor.
localhost:3000
Acessando a nossa aplicação pelo navegador no endereço localhost:3000, temos o nosso servidor como sendo o localhost (nome de domínio de onde estamos acessando o servidor) e a porta 3000.

Se acessarmos, por exemplo, o site google.com é outro nome de domínio, que conseguimos acessar de forma direta sem a necessidade de informar a porta (por ser padrão). Mas, e se colocássemos um endereço IP?

Endereço IP usado pelo instrutor:
http://142.251.128.14
Colando o endereço IP acima na barra de endereço do navegador e teclando "Enter", somos redirecionados para a página google.com.

O que será que aconteceu para um endereço IP virar o nome do site?

Sistema de Nomes de Domínios (DNS)
Site	IP
google.com	142.251.128.14
Todo computador precisa de um endereço IP para se conectar à internet. Entretanto, imagine se tivéssemos que ficar decorando endereços IPs de cada servidor conectado para acessarmos um site. O do Google, por exemplo, é o IP 142.251.128.14. Portanto, o DNS associa esse IP a um nome mais fácil de lembrarmos.

Os servidores DNS transformam requisições de nomes em endereços IP, isso para que a pessoa usuária consiga acessar a página web esperada quando digitar o nome de domínio no navegador web.
Domínios
O que são esses domínios?

Fazendo uma analogia, por exemplo, o Brasil é um domínio territorial por ser uma região administrativa que possui suas regras. Cada país é um domínio separado.

Na web, cada site, ou sistema, ou empresa possui seu próprio domínio, sendo onde tudo é controlado. Por exemplo, todos os sistemas da Alura estão sobre o domínio de alura.com.br; já o Google, está no domínio google.com e o nosso servidor local está em localhost. Este significa que o domínio funciona somente dentro do nosso computador.

Há domínios globais e domínios locais. Um exemplo de domínio global é o da Alura e do Google, já o domínio local é o nosso localhost.

Como funciona o DNS
Temos um servidor DNS que possui uma tabela grande, onde há uma coluna com o nome dos sites (domínios) e outra com os IPs relacionados aos domínios.

Site	IP
google.com	142.251.128.14
alura.com.br	172.67.72.232
…	…
Assim, toda vez que a pessoa acessar um site usando o HTTP, ela precisa saber qual o IP do servidor para que esse acesso seja efetivo. Dessa forma, perguntamos ao servidor DNS qual o IP, por exemplo, do domínio google.com e temos como retorno o 142.251.128.14. Com o endereço IP, a pessoa estabelece uma comunicação HTTP da forma como já aprendemos anteriormente.

Podemos fazer alguns testes relacionados a como descobrir o endereço IP.

No terminal, rodamos um programa através do comando nslookup google.com.

nslookup google.com
Como retorno, obtemos:

Server: 8.8.8.8
Address: 8.8.8.8#53

Non-authoritative answer:

Name: google.com

Address: 142.251.128.14

Temos como retorno o nome do domínio e o endereço IP associado a ele. Podemos usar esse comando, portanto, para descobrir qual o endereço IP de determinado domínio.

Imagine o tamanho da tabela que esse servidor DNS precisa ter para saber todos os sites do mundo, e o tempo de busca e leitura do endereço IP que está associado ao domínio. Isso está relacionado à performance e também à administração.

DNS é hierárquico
Para simplificar, o DNS é feito de uma forma hierárquica em formato de árvore. Quando acessamos algo .com.br ou .org, significa que são o primeiro nível dos nomes dos sites. Inicia-se da raiz (nível mais abstrato) que é para ter um ponto de onde começar, e a partir disso vamos descendo os níveis. Chamamos esse nível de top-level domains (TLD) (em português, "domínios de nível superior").

Descendo para os sub-domínios, temos os domínios da alura, g1 e fiap, por exemplo, alura.com.br e do Google ficaria apenas google.com. Esse mecanismo hierárquico permite uma busca mais rápida por usarmos uma árvore.

Além disso, facilita na administração, por exemplo, por sabermos que tudo que contém br está relacionado ao Brasil. Assim, é possível alocar essa parte dos domínios para ser administrada por uma entidade brasileira. Isso seria para cada país, assim eles conseguem gerenciar os seus domínios específicos.

Organograma hierárquico de DNS. O organograma possui formato de árvore e possui dois níveis de domínios: top-level domains(TLD) posicionados no topo e sub-domínios posicionados logo abaixo. No topo de top-level domain temos "raíz" que se conecta a 4 outros domínios: "com", "br", "org", "net". O domínio "com" se conecta ao subdomínio "google", enquanto o domínio "br" se conecta aos subdomínios "com", "gov", "edu". Já o sub-domínio "com" se conecta a outros subdomínios, exemplificados como "alura", "g1" e "fiap"

Composição da URL:
http: Protocolo
//localhost: Endereço IP ou Nome de domínio.
:3000/: caminho (raiz)
Portanto, na parte do servidor podemos usar tanto o endereço IP quanto o nome de domínio para acessar as páginas HTTP.

@@08
O que é um domínio na Internet?

Falamos bastante sobre o domínio nessa aula, mas o que é um domínio (ou domain name) e qual a sua importância?

Domínio é permitir uma conexão segura com o site Web de forma que o servidor garante a integridade do serviço. Falamos que o serviço foi acessado de forma dominante.
 
Alternativa incorreta
O domínio é o nome do site na Web. Ele facilita a navegação do usuário, que não precisa lembrar o IP de cada site.
 
O domínio é o nome do site na web e serve para facilitar a navegação do usuário, que precisa lembrar apenas do nome do site, e não do seu endereço IP.
Alternativa incorreta
O domínio é o endereço que digitamos no navegador para acessar o site. Para isso, precisamos registrá-lo no servidor de domínios do Google.
 
Alternativa incorreta
Domínios eram uma forma primordial de acesso à Internet antes da popularização dos navegadores modernos. Atualmente não são mais usados e o comum é acessar pelo nome de acesso (Access Name).

@@09
Como funciona o DNS?

Qual é o objetivo ou a função do DNS (Domain Name System ou servidor de domínios)?

O DNS serve para transferir arquivos pela internet de forma rápida e versátil.
 
Alternativa incorreta
O DNS é um protocolo usado no acesso remoto a uma caixa de correio eletrônico.
 
Alternativa incorreta
O DNS tem como função realizar a tradução do nome de um domínio para o endereço de IP correspondente.
 
O DNS realiza a tradução do nome de um domínio para o endereço de IP. Existem vários servidores DNS no mundo e é fundamental para a nossa web o funcionamento deles.
Alternativa incorreta
O DNS é usado para permitir o acesso seguro em redes inseguras, sendo muito usado para realizar o acesso remoto em outros computadores.

@@10
O que aprendemos?

Nessa aula, você a aprendeu a:
Identificar uma URL e entender o seu papel no protocolo HTTP;
Configurar URLs para utilizar: protocolos, domínios, portas, e caminhos específicos;
Utilizar a porta padrão nas URLs com o protocolo HTTP;
Usar nomes de domínios (ao invés de endereços IP) para acessar diferentes sites na Web.

#09/10/2025

@03-Inspecionando o protocolo HTTP

@@01
Preparando o ambiente

Para os próximos vídeos, vamos usar o telnet, uma ferramenta poderosa e versátil que é usada há décadas por pessoas desenvolvedoras e administradoras de sistemas para se conectar a servidores remotos e executar comandos.
Habilitando o telnet no Windows 10 e 11

O Windows 10 e 11 já vêm com o telnet instalado, porém é preciso habilitá-lo. Para isso, siga os passos abaixo:

1- Pressione a tecla Windows do seu teclado e digite "Painel de Controle"

Insira aqui a descrição dessa imagem para ajudar na acessibilidade

2- Clique na opção "Programas" (caso esteja vendo por categorias)

Insira aqui a descrição dessa imagem para ajudar na acessibilidade

3- Clique na opção "Ativar ou Desativar recursos do Windows"

Insira aqui a descrição dessa imagem para ajudar na acessibilidade

4 - Depois marque o checkbox "Telnet Client"

Insira aqui a descrição dessa imagem para ajudar na acessibilidade

Para testar, abra o prompt de comandos do Windows e digite telnet. Se deu tudo certo, você vai ver a mensagem "bem-vindo ao cliente telnet". Pode fechar a janela de comandos.

Usando o telnet no Windows

O telnet no Windows não possui uma interface muito amigável, por exemplo, por padrão ele não mostra na tela o que a gente digita, e causa timeouts sem razão aparente.

Por esse motivo, nós preparamos as seguintes instruções, que permitem que os testes que serão demonstrados nos vídeos posteriores sejam executados no Windows também.

Preparar, em um arquivo de texto, a mensagem HTTP que você quer enviar;
Abrir o cmd do windows (note que é diferente do powershell, mingw ou cygwin);
Digitar telnet localhost 8000;
Copiar a mensagem HTTP inteira que está no arquivo de texto (não coloque mais de uma mensagem no mesmo arquivo);
Colar na janela do telnet;
Clicar “enter” duas vezes.
Com esse setup, você deverá conseguir realizar as requisições HTTP pelo telnet no Windows.

Instalando o telnet no Mac

O Mac e o Linux não vêm com o telnet instalado por padrão. Para instalar, siga as etapas abaixo:

Mac
1- Abra o Terminal.

2- Digite o seguinte comando:

brew install telnet
COPIAR CÓDIGO
Pressione Enter.
O telnet será instalado. Para testar, abra o Terminal e digite o seguinte comando:

telnet localhost 8000
COPIAR CÓDIGO
Se deu tudo certo, você vai ver a mensagem "Welcome to telnet". Pode fechar a janela do Terminal.

Instalando o telnet no Linux
1- Abra o Terminal.

2- Digite o seguinte comando:

sudo apt-get install telnet
COPIAR CÓDIGO
3- Pressione Enter.

O telnet será instalado. Para testar, abra o Terminal e digite o seguinte comando:

telnet localhost 8000
COPIAR CÓDIGO
Se deu tudo certo, você vai ver a mensagem "Welcome to telnet". Pode fechar a janela do Terminal.

A mensagem HTTP será enviada para o servidor. Você pode ver a resposta do servidor na janela do Terminal.

Espero que isso ajude!

@@02
Ativando o modo hacker

Transcrição

Nesta aula, vamos colocar alguns conceitos em prática! Primeiramente, relembraremos o que fizemos até agora.
Recapitulando
Nós usamos o Chrome junto do JavaScript como um cliente HTTP, acessando nosso servidor do back-end e do front-end. Na aba de inspeção do navegador, mais especificamente na aba "Network" (Rede), analisamos informações obtidas de requisições.

Ao longo das aulas, descobrimos que o HTTP é um protocolo de textos. No entanto, apenas consultado os logs obtidos da requisição nessa aba, não temos certeza se são textos ou se o Chrome que está os organizando dessa forma.

Então, vamos introduzir uma nova ferramenta, chamada telnet, responsável por criar conexão TCP com outros servidores.

Telnet
Criaremos uma conexão TCP com back-end e o TCP será usado pelo HTTP para transportar as mensagens. Abriremos o telnet no terminal e digitaremos as mensagens HTTP como um cliente, semelhante ao navegador. A diferença é que o navegador realiza esse processo automaticamente, mas nós escreveremos as mensagens manualmente com telnet.

Em uma aba do terminal, temos o back-end rodando. Em outra aba, vamos usar o comando do telnet, passando como parâmetro o domínio e a porta:

telnet localhost 8000COPIAR CÓDIGO
Connected to localhost.
Em seguida, vamos fazer uma request, escrevendo o conteúdo da requisição HTTP.

GET / HTTP/1.1COPIAR CÓDIGO
O "GET" indica a obtenção de um conteúdo, a barra define que o conteúdo é da página inicial e o "HTTP/1.1" é o nome do protocolo, seguido da versão.

Pressionado "Enter" duas vezes, a resposta do servidor começa com HTTP/1.1 200 OK e uma série de configurações, que não precisamos nos atentar, por enquanto. Depois, temos todo o código HTML usado para renderizar a página inicial do AluraBooks.

Ou seja, fizemos uma requisição HTTP manualmente, usando o telnet! Na sequência, vamos realizar uma requisição um pouco mais interessante.

Na página inicial do AluraBooks, na parte superior direita, podemos clicar no botão "Login" e inserir nossos dados cadastrados no sistema:

E-mail: geo@alura.com.br Senha: 123
Pressionando o botão "Fazer login", entraremos no sistema, usando o protocolo HTTP. A seguir, vamos explorar como realizar a mesma ação com o telnet.

No terminal, podemos executar o comando clear para limpar a tela. Em seguida, abriremos uma nova sessão de telnet novamente:

telnet localhost 8000COPIAR CÓDIGO
E enviaremos a seguinte requisição:

POST /public/login HTTP/1.1
Content-Type: application/json
Content-length: 45

{"email": "geo@alura.com.br", "senha": "123"}COPIAR CÓDIGO
Dessa vez, informamos que estamos enviando um JSON e que o tamanho da requisição é de 45 bytes. Além disso, mandamos um JSON com dados de login.

Analisando o retorno, reparamos que a requisição foi bem-sucedida. A resposta em texto do servidor começa novamente com HTTP/1.1 200 OK e várias configurações. Depois, temos um JSON com um access token, que é o elemento usado para provar que estamos logados. Aprendemos sobre esse assunto mais adiante; por ora, vamos focar em entender o formato das mensagens HTTP.

Formato das mensagens HTTP
Aprendemos que a requisição tem o seguinte formato:

POST /public/login HTTP/1.1
Host: localhost
Content-Type: application/json
Content-length: 45

{"email": "geo@alura.com.br", "senha": "123"}COPIAR CÓDIGO
A linha inicial contém as informações principais sobre a requisição. O "POST" indica que estamos enviando conteúdo. Nas três linhas seguintes, temos os cabeçalhos (headers) com metadados sobre a requisição. Na última linha, consta o corpo da requisição (body). No caso, mandamos um JSON.

De maneira similar, a resposta também tem uma linha inicial, seguida de cabeçalhos e o corpo com a resposta:

HTTP/1.1 200 OK
X-Powered-By: Express
Vary: Origin, Accept-Encoding
(...)
Content-Type: application/json
Content-Length: 364

{
    "access_token: "eyJhiJ...WCbZof2rf",
    (...)
}COPIAR CÓDIGO
O objetivo deste vídeo era aprender que as mensagens HTTP tem esse formato específico de cabeçalhos e corpo.

Usamos o telnet, mas não precisamos usá-lo para sempre, afinal, ele é muito baixo nível. Nos próximos vídeos, aprenderemos a utilizar uma nova ferramenta: o Postman. Assim como o telnet, ele é poderoso e permite controlar os parâmetros HTTP. Assim como o Chrome, ele é mais amigável para utilizar.

@@03
Desafio

No vídeo anterior utilizamos o telnet, uma ferramenta poderosa e versátil que é usada há décadas por pessoas desenvolvedoras e administradoras de sistemas para se conectar a servidores remotos e executar comandos.
O telnet é muito útil em situações específicas, como quando queremos criar um request "na mão" ou conectar em um socket diretamente. Ou seja, no nosso contexto ele é uma ótima ferramenta de aprendizagem.

Assim, o seu desafio será utilizar o telnet para criar os requests HTTP que fizemos no vídeo.

Para facilitar, deixamos abaixo um tutorial sobre a instalação do telnet, que pode variar dependendo do seu sistema operacional.

Boa prática!

Instalação do telnet
Habilitando o telnet no Windows 10 e 11

O Windows 10 e 11 já vêm com o telnet instalado, porém é preciso habilitá-lo. Para isso, siga os passos abaixo:

Pressione a tecla Windows do seu teclado e digite "Painel de Controle":
recorte de tela mostrando o campo de pesquisa do Windows, pesquisando pelo painel de controle".

Clique na opção "Programas" (caso esteja acessando por categorias):
recorte de rela mostrando as opções do painel de controle do Windows, na tela está selecionada a opção "Programa"

Clique na opção "Ativar ou Desativar recursos do Windows":
recorte de tela mostrando a opção "Ativar ou Desativar recursos do Windows".

Depois marque o checkbox "Telnet Client":
recorte de tela do Windows Features, nela é possível ativar ou desativar diversas opções.

Para testar, abra o prompt de comandos do Windows e digite telnet. Se deu tudo certo, você vai ver a mensagem "bem-vindo ao cliente telnet". Pode fechar a janela de comandos.

Usando o telnet no Windows

O telnet no Windows não possui uma interface muito amigável, por exemplo, por padrão ele não mostra na tela o que a gente digita, e causa timeouts sem razão aparente.

Por esse motivo, nós preparamos as seguintes instruções, que permitem que os testes do vídeo anterior sejam executados no Windows também.

Preparar, em um arquivo de texto, a mensagem HTTP que você quer enviar (por exemplo, a do vídeo anterior);
Abrir o cmd do windows (note que é diferente do powershell, mingw ou cygwin);
Digitar telnet localhost 8000;
Copiar a mensagem HTTP inteira que está no arquivo de texto (não coloque mais de uma mensagem no mesmo arquivo);
Colar na janela do telnet;
Clicar “enter” duas vezes.
Com esse setup, você deverá conseguir realizar as requisições HTTP pelo telnet no Windows.

Instalando o telnet no MacOS e no Linux

O MacOS e o Linux não vêm com o telnet instalado por padrão. Para instalar, siga as etapas abaixo:

Mac
Abra o Terminal.
Digite o seguinte comando:
brew install telnet
COPIAR CÓDIGO
Pressione Enter.
O telnet será instalado. Para testar, abra o Terminal e digite o seguinte comando:

telnet localhost 8000
COPIAR CÓDIGO
Se deu tudo certo, você vai ver a mensagem "Welcome to telnet". Pode fechar a janela do Terminal.

Linux
Abra o Terminal.
Digite o seguinte comando:
sudo apt-get install telnet
COPIAR CÓDIGO
Pressione Enter.
O telnet será instalado. Para testar, abra o Terminal e digite o seguinte comando:

telnet localhost 8000
COPIAR CÓDIGO
Se deu tudo certo, você vai ver a mensagem "Welcome to telnet". Pode fechar a janela do Terminal!

Opinião do instrutor

Usando o telnet no Windows
O telnet no Windows não possui uma interface muito amigável, por exemplo, por padrão ele não mostra na tela o que a gente digita, e causa timeouts sem razão aparente.

Por esse motivo, nós preparamos as seguintes instruções, que permitem que os testes do vídeo anterior sejam executados no Windows também.

Preparar, em um arquivo de texto, a mensagem HTTP que você quer enviar (por exemplo, a do vídeo anterior);
Abrir o cmd do windows (note que é diferente do powershell, mingw ou cygwin);
Digitar telnet localhost 8000;
Copiar a mensagem HTTP inteira que está no arquivo de texto (não coloque mais de uma mensagem no mesmo arquivo);
Colar na janela do telnet;
Clicar “enter” duas vezes.
Com esse setup, você deverá conseguir realizar as requisições HTTP pelo telnet no Windows.

Espero que isso ajude!

@@04
Preparando o ambiente

Para os próximos vídeos, vamos usar o Postman, uma ferramenta muito mais expressiva e intuitiva que o telnet. Para instalar o Postman, siga o passo a passo neste link: Postman: saiba como instalar e dar seus primeiros passos | Alura.

https://www.alura.com.br/artigos/postman-como-instalar-dar-seus-primeiros-passos

@@05
Depurando métodos HTTP

Transcrição

Anteriormente, usamos o telnet no terminal, escrevemos mensagens manualmente e aprendemos sobre o formato das mensagens HTTP. Tanto na requisição quanto na resposta, temos os cabeçalhos seguidos do corpo da mensagem.
Agora, vamos continuar nos aprofundando no formato dos cabeçalhos de requisições, mais especificamente na linha inicial, por exemplo:

POST /public/login HTTP/1.1COPIAR CÓDIGO
A primeira palavra da linha tem um nome técnico: o método do HTTP. Para continuar explorando esses conceitos, vamos aprender a usar o Postman, uma ferramenta mais intuitiva que o telnet e bastante poderosa para manipulação de parâmetros.

Postman
O Postman é uma ferramenta para testar servidores HTTPs, APIs e assim por diante. Ao abrir o Postman, há um menu lateral à esquerda e uma área de trabalho (chamada de workbench) à direita.

Na parte superior do workbench, clicaremos no ícone de mais (+) para criar uma aba com uma nova requisição. No topo dessa aba, temos três elementos:

À esquerda, há um menu dropdown em que é possível alternar entre diversos métodos do HTTP — por padrão, o método GET está selecionado.
No centro, há um campo para digitar a URL.
À direita, temos um botão azul escrito "Send" (enviar).
Começaremos enviando uma requisição para obter as informações da página inicial do AluraBooks. Logo, selecionaremos o método GET e digitaremos a seguinte URL:

http://localhost:3000/COPIAR CÓDIGO
A barra ao final da URL indica que se trata da página inicial (home). Ao pressionar o botão "Send", recebemos a resposta na parte inferior da interface. No caso, trata-se do código HTML contendo todas as informações necessárias para desenhar a nossa tela do front-end. Nossa requisição foi bem-sucedida!

A seguir, vamos usar um método diferente: o POST. Podemos simplesmente reproduzir a requisição que fizemos no vídeo anterior, em que realizamos o login.

Dessa vez, selecionaremos o método POST. A URL também será diferente, dado que o destino agora é o back-end:

http://localhost:8000/public/loginCOPIAR CÓDIGO
Não precisamos escrever manualmente as informações do cabeçalho (como HTTP/1.1), pois o Postman ficará responsável por essa parte. Porém, é necessário definir o conteúdo da mensagem — o corpo da requisição. No caso, trata-se de um JSON com o e-mail e a senha para login.

Abaixo do campo em que digitamos a URL, há um menu com várias abas. Acessaremos a aba "Body", depois selecionaremos as opções "raw" e "JSON". No campo de texto exibido abaixo, informaremos o corpo da mensagem:

{"email": "geo@alura.com.br", "senha": "123"}COPIAR CÓDIGO
Por fim, clicaremos no botão "Send" para enviar a requisição. Na parte inferior, recebemos a resposta com o token de acesso, que podemos usar para acessar páginas protegidas.

Métodos HTTP
Ao clicar na seta do menu dropdown, temos uma lista de métodos HTTP. Sabemos que o GET serve para obter informações. Já o POST tem o significado de criar elementos. No caso, estamos enviando nossas credenciais e criando um token de acesso que pode ser usado para login.

Há uma lista extensa de métodos, mas os usados com mais frequência são apenas quatro:

Método	Significado
POST	criar (create)
GET	ler (read)
PUT	atualizar (update)
DELETE	apagar (delete)
Como estudamos, o POST serve para criar elementos (create) e o GET é utilizado para ler ou obter informações (read). O PUT é o método HTTP usado para atualizações (update), por exemplo, atualizar o endereço ou a senha. Já o DELETE é responsável por apagar elementos (delete), por exemplo, uma conta ou fotos salvas.

Esses métodos HTTP são tão comuns que foi criado um acrônimo, conforme seus significados em inglês, o CRUD:

C: create
R: read
U: update
D: delete
Esses métodos permitem que façamos a maioria das operações necessárias para nossas aplicações, por exemplo, o AluraBooks. No próximo vídeo, continuaremos explorando o HTTP e entenderemos o que podemos fazer com o token que recebemos do login.

@@06
Analisando Request e Response

Abaixo há um exemplo de uma requisição e resposta, usando a ferramenta telnet. Através dele, acessamos o recurso raiz da nossa API na porta 8000.
alt: Exemplo de uma requisição e resposta, usando a ferramenta telnet. A mensagem está dividida em duas partes, request e response. 
No request temos as seguintes informações

GET/HTTP/1.1
Host: localhost
COPIAR CÓDIGO
Já no response temos as seguintes informações:

HTTP/1.1 200 OK
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Access-Control-Allow-Credentials: true
Accept-Ranges: bytes
Cache-Control: public, max-age=0
Last-Modified: Mon, 27 Feb 2023 11:49:47 GMT
ETag: W/’809-18692b5194b’
Content-Type: text/html; charset=UTF-8
Content-Length: 2057
Date: Thu, 06 Apr 2023 06:47:15 GMT
Host: localhost
COPIAR CÓDIGO
O telnet estabelece apenas uma conexão TCP (protocolo de rede que roda abaixo do HTTP) e permite que enviemos dados em cima dessa conexão, através do terminal. Uma vez a conexão estabelecida, basta escrever no terminal e os dados serão enviados automaticamente para o servidor. Para o servidor realmente entender os dados, devemos respeitar a sintaxe do protocolo HTTP!

Nesse exemplo digitamos no terminal:

GET / HTTP/1.1
Host: localhost
COPIAR CÓDIGO
E a resposta do servidor segue logo abaixo:

HTTP/1.1 200 OK
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Access-Control-Allow-Credentials: true
Accept-Ranges: bytes
Cache-Control: public, max-age=0
COPIAR CÓDIGO
Agora, baseado nesses dados, qual foi o método HTTP utilizado?

POST
 
O método POST não é utilizado nesse caso.
Alternativa incorreta
200 OK
 
Apesar deste item fazer parte da interação entre o cliente e o servidor, ele não representa um método HTTP.
Alternativa incorreta
1.1
 
Alternativa incorreta
GET
 
O método HTTP é GET e o código da resposta é 200.Lembrando que o método define a ação ou intenção da requisição HTTP (GET é igual a receber). O código da resposta dá uma dica ao cliente se a requisição foi um sucesso ou não, e qual foi o problema em caso de falha. O código 200 significa que tudo deu certo!

@@07
Configurando cabeçalhos para autenticar o usuário

Transcrição

Aprendemos a usar o Postman e entendemos os significados dos métodos HTTP. Além disso, fizemos o login por meio do Postman e obtivemos um código de acesso. Ele permitirá o acesso a informações restritas a um usuário específico.
Com o AluraBooks aberto no navegador, vamos clicar no botão "Login" na parte superior direita e entrar no sistema:

E-mail: geovane@alura.com.br
Senha: 123
Após entrar, acessaremos o link "Minha conta" na parte superior direita da tela, onde antes tínhamos o botão para login. Nessa página, temos nossa lista com detalhes de pedidos.

Essa página é protegida, apenas a minha conta tem acesso a essa lista. Não faria sentido se, ao entrar em minha própria conta, eu pudesse consultar os pedidos de outra pessoa (nem que outra pessoa pudesse conferir a minha lista).

Acessando uma página protegida
Nós já fizemos o login por meio do Postman e recebemos um token de acesso. A seguir, vamos explorar como entrar na página de pedidos, acessível apenas para usuários logados.

Como a meta é ler os pedidos, usaremos o método GET e nossa URL será a seguinte:

http://localhost:8000/pedidosCOPIAR CÓDIGO
Ao enviar a requisição, recebemos o seguinte retorno na parte inferior do Postman:

{
    "status": 401,
    "message":"Token inválido"
}COPIAR CÓDIGO
Recebemos um resultado inesperado! Em vez de ler os pedidos, obtemos uma mensagem de token inválido. Nós já tínhamos obtido o token, então por que não conseguimos acessar?

Os servidores HTTP são stateless. Em outras palavras, os servidores HTTP não guardam estados, portanto não se lembram do aconteceu em requisições anteriores. No caso, ele não lembra que já havia nos autenticado no sistema.

A implicação é que precisamos continuamente comprovar ao servidor quem somos e que já fomos autenticados. É como mostrar nossa identidade e dizer:

"Servidor, sou eu de novo, o Geovane. Eu que estou tentando te acessar. Lembra que você já me autenticou? Aqui está a minha prova"
Logo, precisamos encontrar um jeito de enviar nosso token para o servidor em todas as requisições!

De início, vamos criar outro token de acesso, realizando o login novamente. No Postman, basta enviar uma requisição GET para a página de login, lembrando de informar as credenciais no corpo da requisição:

http://localhost:8000/loginCOPIAR CÓDIGO
{"email": "geovane@alura.com.br", "senha": 123}COPIAR CÓDIGO
Após enviar, copiaremos o token de acesso obtido na resposta do servidor. A seguir, começaremos a configurar os cabeçalhos da requisição!

Configurando cabeçalhos
No Postman, no menu abaixo da URL, acessaremos a aba "Headers". Nessa aba, há uma tabela cujas primeiras colunas são "Key" (chave) e "Value" (valor). Os cabeçalhos sempre seguem essa estrutura de chave e valor, como o Content-length: 45, que verificamos em aulas passadas.

Na primeira linha da tabela, vamos inserir a chave "Authorization", pois queremos que o servidor entenda que estamos autorizados a acessá-lo.

No valor correspondente, não basta colar o token, é preciso adotar a convenção do uso da palavra "Bearer". Em inglês, bearer significa portador, é a pessoa que carrega algo. Ou seja, é como se estivéssemos carregando nosso documento de identidade.

Portanto, vamos escrever "Bearer", colocar um espaço e colar o token:

Key	Value
Authorization	Bearer eyJhbGci0iJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Imd1b0BhbHVyYS5jb20uYnIiLCJzZW5oYSI6IjEyMyIsIm1hdCI6MTY30DQ3MTU20Cwi ZXhwIjoxNjc4NTEONzY4fQ.ZV5Z97oY7H94_hRDCX66Yf03G-wAQ8jNN-ARvhqKP6E
Lembre-se de usar o seu próprio token!
Agora que configuramos nosso cabeçalho para lembrar o servidor quem somos, vamos tentar acessar a página protegida novamente. Faremos uma requisição GET para a página de pedidos:

http://localhost:8000/pedidosCOPIAR CÓDIGO
Ao enviar a requisição, a resposta do servidor serão os dados dos nossos pedidos! A estrutura é parecida com a seguinte:

[
    {
        "id": 89019041,
        "data": "2022-05-26",
        "entrega": "2022-05-26",
        "total": 29.9
    },
    {
        "id": 89019963,
        "data": "2022-07-26",
        "entrega": "2022-08-01",
        "total": 58.8
    }
]COPIAR CÓDIGO
Apesar de ser em formato JSON, trata-se das mesmas informações que conferimos no front-end.

Formas de "lembrar" o servidor
Aprendemos que, por padrão, o servidor é stateless, logo ele não se lembra do que aconteceu em requisições anteriores. No entanto, existem algumas formas de o lembrarmos.

Uma das formas é o uso da sessão, que foi a abordagem que empregamos. Por exemplo, gerar um token e mostrá-lo ao servidor continuamente para ele lembrar quem está o acessando. A sessão é o tempo que a pessoa usuária permanece logada no sistema.

Outra forma é o uso de cookies. É comum a exibição de um pop-up na tela para a pessoa usuária aceitar ou rejeitar o uso de cookies em sites. Eles são um mecanismo utilizado nos cabeçalhos do HTTP para que o servidor peça para a pessoa cliente salvar algumas informações, que serão usadas posteriormente para lembrar o servidor.

Neste curso, não entraremos em detalhes sobre os cookies, mas deixaremos um "Para saber mais" com uma explicação excelente sobre o funcionamento deles.

Na sequência, continuaremos aprendendo mais sobre as respostas HTTP.

@@08
Autorização e estado do servidor

Durante o desenvolvimento do AluraBooks, um dos desenvolvedores estava testando o mecanismo de autenticação de usuários do backend. Para isso, ele primeiro fez login na API, e em seguida enviou o seguinte request:
POST /pedidos HTTP/1.1
Authorization: Yes (login)
COPIAR CÓDIGO
No entanto, a resposta que ele recebeu indicou que esse request não foi autorizado pelo servidor:

HTTP/1.1 401 Unauthorized
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Access-Control-Allow-Credentials: true
Cache-Control: no-cache
Pragma: no-cache
Expires: -1
Content-Type: application/json; charset=utf-8
Content-Length: 51
ETag: W/"33-YImdAd48xqkdD0FiXysFO1TLONs"
Date: Thu, 30 Mar 2023 08:53:09 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{
  "status": 401,
  "message": "Token inválido"
}
COPIAR CÓDIGO
Por que o request não foi autorizado pelo servidor?

O valor do cabeçalho Authorization está incorreto, pois deveria usar o token de autorização.
 
Exato, como o HTTP é um protocolo em que o servidor não guarda estado, o cliente precisa sempre lembrar o servidor que ele possui a devida autorização. Por isso, ele deve re-enviar ao servidor o token que ele obteve quando fez o login.
Alternativa incorreta
O request deveria ter usado o método GET ao invés do POST.
 
Alternativa incorreta
O cabeçalho de autorização não deveria ser preenchido, pois o HTTP é um protocolo que guarda estado e portanto o servidor já sabe que ele está logado.
 
@@09
Sessão HTTP

Ao digitar o endereço do site no seu navegador, diversos processos entram em ação para garantir que o conteúdo seja carregado corretamente. Um desses processos envolve o protocolo HTTP.
Qual o papel desse protocolo na comunicação entre seu navegador e o servidor do site que você quer acessar?

O protocolo HTTP é responsável por criptografar todas as informações trocadas entre seu navegador e o servidor.
 
Alternativa incorreta
O protocolo HTTP é utilizado exclusivamente para transferir arquivos de vídeo e áudio entre servidores e navegadores.
 
Alternativa incorreta
O protocolo HTTP define como as mensagens são formatadas e transmitidas, e como os navegadores e servidores devem responder a vários comandos.
 
Muito bem. O HTTP define a estrutura das mensagens e a comunicação entre cliente e servidor.
Alternativa incorreta
O protocolo HTTP é utilizado para configurar o endereço IP do servidor que você está tentando acessar.

@@10
Para saber mais: o que é um cookie?

Vimos no vídeo o uso de um cookie para gravar um número, aquele Session ID. Mas o que é um cookie?
Quando falamos de Cookies, na verdade queremos dizer Cookies HTTP ou Cookie web. Um cookie é um pequeno arquivo de texto, normalmente criado pela aplicação web, para guardar algumas informações sobre o usuário no navegador. Quais são essas informações depende um pouco da aplicação. Pode ser que fique gravado alguma preferência do usuário. Ou algumas informações sobre as compras na loja virtual ou, como vimos no vídeo, a identificação do usuário. Isso depende da utilidade para a aplicação web.

Um cookie pode ser manipulado e até apagado pelo navegador e, quando for salvo no navegador, fica associado com um domínio. Ou seja, podemos ter um cookie para www.alura.com.br, e outro para www.caelum.com.br. Aliás, um site ou web app pode ter vários cookies! Podemos visualizar os cookies salvos utilizando o navegador. Como visualizar, depende um pouco do navegador em questão:

No Chrome: Configurações -> Privacidade -> Configurações de conteúdo... -> Todos os cookies e dados de site... -> Pesquisar alura

No Firefox: Preferências -> Privacidade -> remover cookies individualmente -> Pesquisar alura

Caso queira aprender mais sobre isso pode ler o artigo "O que são cookies e como eles funcionam?".

https://www.alura.com.br/artigos/o-que-sao-cookies-como-funcionam

@@11
Depurando os códigos resposta HTTP

Transcrição

Em aulas anteriores, analisamos algumas informações no painel de inspeção do Chrome. Na página inicial do AluraBooks, clicamos com o botão direito do mouse no centro da tela e selecionamos "Inspecionar".
No menu superior do painel de inspeção, acessamos a aba "Network" (rede), onde aparecem diversos logs referentes às requisições do HTTP. Na ocasião, conferimos os logs do acesso à página "Minha conta", que faz uma requisição para o caminho "pedidos". Verificamos a seguinte informação:

Status Code: 200 OK
Ao lado dessa informação, há um círculo verde e concluímos que parecia um bom sinal.

No Postman, há uma barra acima da área onde recebemos a resposta do servidor. Na parte direita, é possível verificar o status code.

Além do "200 OK", já encontramos outros códigos de status ao longo deste curso. Ao enviar uma requisição para /pedidos sem informar o token, por exemplo, obtivemos o status "401 Unauthorized", isto é, "Não autorizado".

A seguir, vamos aprender o que são esses códigos e sua importância.

Códigos de status
Por ser um protocolo, o HTTP segue algumas regras. Então, vamos consultar o documento RFC 7231, que define as regras do protocolo HTTP.

RFCs são documentos que definem as regras de um protocolo. Elas são gratuitas na internet e qualquer pessoa pode acessá-las.
Descendo a página, encontraremos o sumário com todas as definições do HTTP. Por exemplo, na seção 4.3, temos subseções para os métodos que estudamos anteriormente — GET, POST, PUT e DELETE. Você pode ler por conta própria, caso te interesse.

Na seção 6, temos os códigos de status das respostas. Nas subseções, podemos identificar alguns que já conhecemos, como o "200 OK". O status "401 Unauthorized" não consta no sumário, mas ele aparecerá ao longo do documento.

Portanto, nessa seção, temos uma lista dos principais códigos de respostas do HTTP. Perceba que eles estão organizados em classes, de modo que já temos noções do seu significado ao examinar o primeiro dígito.

Os códigos que começam com o número 1 são raramente usados. Mais adiante, estudaremos a troca de protocolos (de HTTP para HTTPS, por exemplo) e encontraremos o status "101 Switching Protocols".

Os códigos iniciados com o número 2 indicam operações bem-sucedidas, como quando conseguimos criar um token ou acessar o conteúdo de um recurso HTTP. É o caso do "200 OK", com o qual já estamos familiarizados.

Os códigos que começam com o número 3 indicam redirecionamentos. Por exemplo, caso uma empresa mude de nome e o domínio de seu site seja alterado, ela pode usar um redirecionamento. Assim, quando uma pessoa acessar o domínio antigo, o HTTP a enviará para o novo site.

Como comentamos anteriormente, o HTTP tem duas entidades conversando: o cliente e o servidor. Os códigos que começam com o número 4 indicam erros provindos do lado do cliente, como "400 Bad Request" e "401 Unauthorized".

Já os códigos iniciados com o número 5 indicam erros do lado do servidor. Você provavelmente já se deparou com o código "500 Internal Server Error" (erro interno do servidor), quando algum site estava com problemas. No caso de erros, os servidores são configurados para responder com códigos iniciados com 5.

Esses códigos já definidos nos ajudam a criar aplicações fáceis de integrar. Vamos supor que trabalhamos em time de tecnologia. Nós somos responsáveis pelo back-end e há outras pessoas encarregadas do front-end. Ao usar esses métodos conforme as definições da RFC, a comunicação torna-se mais simples entre todos, já que se trata de uma linguagem universal.

Sendo assim, aprendemos sobre o formato das mensagens HTTP, detalhes sobre requisições e respostas, e como realizar o login com o token.

Falando em login, será que ele está protegido? Será que o sistema AluraBooks está seguro? Vamos explorar esse assunto na próxima aula.

@@12
Código de sucesso

Durante o desenvolvimento do AluraBooks, aprendemos que cada resposta HTTP possui um código de status que informa sobre o resultado da requisição.
Qual código de status HTTP indica que uma requisição foi bem-sucedida?

404
 
Alternativa incorreta
300
 
O código 300 representa múltipla escolha para o recurso que o cliente requisitou, como vários formatos de um vídeo.
Alternativa incorreta
100
 
Alternativa incorreta
200
 
O código 200 significa OK, ou Sucesso, que não houve nenhum problema no processamento da requisição e ela foi bem sucedida. Existem mais códigos que começam com 2xx. No entanto, 200 é de longe o mais utilizado, principalmente no desenvolvimento de uma aplicação web.
Na documentação oficial, se diz a respeito da classe de códigos que começam com 2xx:
2xx - Resposta bem sucedida!
Essa classe de códigos de status indica que a ação solicitada pelo cliente foi recebida, compreendida, aceita e processada com êxito.
A tabela completa de mensagens HTTP pode acessadas nos seguintes links: de forma resumida ou forma detalhada.

https://www.w3schools.com/tags/ref_httpmessages.asp

https://www.rfc-editor.org/rfc/rfc2616#section-10

@@13
Problema no servidor

Vimos que há diversos códigos HTTP, cada um com a finalidade de representar o status de uma operação com dados.
Qual código HTTP representa algum problema gerado no servidor?

302
 
Alternativa incorreta
402
 
Esse código é reservado e significa que é necessário um pagamento para acessar algum recurso.
Alternativa incorreta
500
 
A descrição completa deste código na documentação oficial é 500 Internal Server Error, que significa que o servidor teve algum problema interno na hora de tratar a requisição.
O código 500 acontece com frequência quando estamos desenvolvendo uma aplicação web e, ao testar, percebemos que erramos algo na lógica que gerou um problema no servidor.
De forma geral, erros da classe 5xx significam que houve algum problema no servidor.
Alternativa incorreta
301

@@14
Recurso não encontrado

Abra uma nova aba no navegador e tente acessar a seguinte URL:
http://g1.globo.com/algo-que-nao-existe

Qual foi o código de resposta?

Obs: Você precisa depurar a requisição HTTP para descobrir o código da resposta (retorne aos vídeos anteriores caso precise relembrar).

http://g1.globo.com/algo-que-nao-existe

200
 
Alternativa incorreta
500
 
Alternativa incorreta
405
 
Alternativa incorreta
404
 
404 é o código clássico que indica que o recurso não foi encontrado. Em geral, a classe 4xx indica que o cliente errou algo na requisição.

@@15
O que aprendemos?

Nessa aula, você a aprendeu a:
Inspecionar mensagens HTTP no terminal usando o telnet, para verificar que as mensagens trafegadas são baseadas em texto;
Verificar que as mensagens HTTP são divididas em cabeçalho e corpo da mensagem;
Depurar os métodos HTTP usando o Postman, permitindo ler e criar recursos no backend do AluraBooks;
Configurar cabeçalhos em requisições para o backend, permitindo o acesso a conteúdos que exigem que o usuário esteja logado;
Depurar os códigos de resposta HTTP, os quais são divididos em classes, tais como como 2xx (sucesso) e 4xx (erro do cliente).