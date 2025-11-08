#08/11/2025

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

