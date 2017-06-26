# Criaçao  de um imagem Docker

Criação de uma imagem  Docker

O Docker é uma aplicação que torna simples e fácil executar processos de aplicação em um contêiner, que é como uma máquina virtual, apenas mais portátil, mais amigável, e mais dependente do sistema operacional do host.Para uma introdução detalhada aos diferentes componentes do contêiner Docker, confira The Docker Ecosystem: An Introduction to Common Components.Existem dois métodos para a instalação do Docker no Ubuntu 16.04. Um dos métodos envolve instalá-lo em uma instalação existente do sistema operacional.A outra envolve lançar um servidor com uma ferramenta chamada Docker Machine que instala o Docker automaticamente nele.

Pré-requisitos

Para seguir esse tutorial, você vai precisar do seguinte: • Droplet do Ubuntu 16.04 64 bits• Usuário não-root com privilégios sudo (Initial Setup Guide for Ubuntu 16.04 explica como configurar isto). Observação: O Docker requer uma versão de 64 bits do Ubuntu Todos os comandos nesse tutorial devem ser executados como usuário não-root. Se o acesso de root for requerido para o comando, ele será precedido pelo sudo. Initial Setup Guide for Ubuntu 16.04 explica como adicionar usuários e dar a eles o acesso ao sudo.


Instalando o Docker

Executar um scritp de instalação, adicionar um repositório na máquina e já fazendo a instalação.

#curl -sSL https://get.docker.com | sh
Iniciar o docker

#/etc/init.d/docker start
Verificar se o docker está rodando

#ps -ef | grep docker

#docker os

Criação de uma imagem no Docker


Imagem docker criada para servir como base de estudos ao servidor web apache.

Utilizando o Docker

Utilize:

docker run -dit --name apache-app --publish=9081:80 chicocx/docker-apache
Para configurar externamente à imagem docker o local onde o apache salvará o site, utilize:

docker run -dit --name apache-app --publish=9081:80 -v "$PWD":/usr/local/apache2/htdocs/ chicocx/docker-apache
O parâmetro

-v "$PWD":/usr/local/apache2/htdocs/
configura o diretório de onde o comando docker é executado como sendo o ponto de montagem do diretório /usr/local/apache2/htdocs/ da imagem criada. No caso, "$PWD" retorna o diretório atual.
É possível modificar esse diretório da seguinte forma:

-v /diretorio/do/host:/usr/local/apache2/htdocs/
Dessa forma, /diretorio/do/host passa a ser o diretório do host que conterá os arquivos lidos pela imagem em /usr/local/apache2/htdocs/

Demais comandos

Entrar na máquina/imagem

docker exec -it redmine1 bash
Sair sem encerrar a máquina:

ctrl p q
Lista o status dos containers

docker ps -a
Exclui os containers que estão parados

docker rm $(docker ps -q -f status=exited)
Lista as imagens baixadas

docker images
Exclui alguma imagem

docker rmi f72216345d97



