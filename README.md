# Estudo-sobre-o-docker
Resumo criado a partir do conhecimento próprio referente ao docker e docker compose. 


## O que é o docker: 
O docker é uma plataforma de conteinerização, sendo um conjunto de ferramentas, padrões e serviços que permitem a implementação das práticas DevOps. O Docker permite que os desenvolvedores empacotem e separem suas aplicações da infraestrutura de negócios, mantendo a leveza, padronização e a entrega dos recursos necessários para executar a aplicação.
Dentro de um Container Docker, os desenvolvedores executam seu projeto sem a preocupação do que está sendo instalado no host, isso proporciona maior flexibilidade, aumenta a segurança e torna mais vantajoso ao comparar com a utilização de máquinas virtuais, devido seu menor consumo de recursos. Dentro desse ambiente “isolado”, a equipe pode utilizar o Docker para criar, monitorar e enviar seus aplicativos para um ambiente de testes manuais e automatizados, corrigindo erros e em seguida validando o código antes de realizar a implantação na produção.

## Imagens vs Container, qual a diferença:
As imagens são modelos criados somente para a leitura, incluindo instruções para realizar a criação dos contêineres, uma imagem é considerada como um modelo daquilo que estará dentro de um contêiner quando ele estiver disponível operacionalmente. A imagem é composta por diversas camadas, onde cada uma altera algo em seu ambiente, elas incluem códigos do aplicativo, os ambientes de execução, as bibliotecas e alguns outros itens presentes no sistema de arquivos, vale ressaltar que a imagem Docker depende do SO principal do host.
Já o Contêiner são ambientes isolados de execução virtualizados e compactados usados para executar as aplicações, cada Contêiner é um pacote do software que contém todos os arquivos de configurações, dependências, ferramentas do sistema, bibliotecas e código fonte necessários para executar determinado aplicativo. Os requisitos são distintos do host e de qualquer outra instância em execução. 




## Dockerfile - Para que serve:
O Dockerfile, resumidamente é um arquivo utilizado para armazenar as instruções necessárias para realizar a criação de uma Docker image, nele é possível especificar qual imagem irá ser utilizada, quais dependências deverão ser instaladas, quais arquivos serão copiados para o ambiente de trabalho e até mesmo qual comando será executado ao iniciar o container, com isso, podemos dizer que o dockerfile é um passo a passo de tudo que é necessário para preparar o ambiente da aplicação. O padrão mínimo esperado em um dockerfile é:
From - Define a imagem base.
Workdir - Define o ambiente de trabalho dentro do contêiner.
Copy - Copia os arquivos presentes no host para a imagem.
Run - Executa comandos durante o build da imagem.
Cmd - Define o processo principal do contêiner.   	






## Docker Compose - O que é, quando usar, e qual problema resolve:
O Docker Compose é uma ferramenta que permite definir e executar aplicações Docker com vários containers de forma muito simples, ele possui como objetivo centralizar e padronizar o gerenciamento dos serviços que fazem parte da mesma aplicação.Ele é utilizado quando uma aplicação utiliza vários serviços para poder funcionar, como por exemplo, a utilização de uma API, um banco de dados e um servidor para, nesses casos o Docker compose nos permite configurar todos os serviços em um único arquivo.
Docker compose soluciona a necessidade de criar e gerenciar cada contêiner de forma manual, ao utilizar o compose, basta que utilize apenas um único comando para todos os containers da aplicação serem criados, configurados e iniciados.



## Exemplo prático do que ocorre quando utilizamos docker compose UP:
Ao executar o comando docker compose up, o Docker Compose primeiramente lê o arquivo docker-compose.yml, responsável por definir os serviços da aplicação. Como exemplo, podemos considerar uma aplicação composta por uma API desenvolvida em Express, utilizando o Prisma ORM para acesso aos dados, e um banco de dados PostgreSQL, seguindo a seguinte estrutura como exemplo para arquivo .yml
version: '3.8'services:db:image: postgres:15 environment: POSTGRES_USER: usuario POSTGRES_PASSWORD: senha POSTGRES_DB: app ports: - "5432:5432" api: build: ./backend ports: - "8080:8080" depends_on: - db
Após a leitura do arquivo, o Docker Compose valida a estrutura e identifica quais serviços precisam ser criados. Em seguida, ele verifica se as imagens necessárias já existem localmente. Caso a imagem do PostgreSQL não esteja disponível, ela será baixada automaticamente do Docker Hub. Já a imagem da API será construída utilizando as instruções definidas no Dockerfile do projeto, depois disso, o Docker Compose cria uma rede interna para permitir a comunicação entre os containers. Dessa forma, a API consegue se conectar ao banco de dados PostgreSQL através do Prisma utilizando apenas o nome do serviço definido no arquivo de configuração.Respeitando as dependências configuradas, o Docker Compose inicia primeiro o container do banco de dados e, em seguida, o container da API. Por fim, os logs dos serviços passam a ser exibidos em tempo real no terminal, permitindo acompanhar o funcionamento da aplicação.Com apenas um único comando, todo o ambiente necessário para a execução da aplicação é criado, configurado e iniciado automaticamente.



## Referências bibliográficas: 

https://www.reddit.com/r/docker/comments/keq9el/please_someone_explain_docker_to_me_like_i_am_an/?tl=pt-br
https://www.redhat.com/pt-br/topics/containers/what-is-docker
https://www.docker.com/blog/docker-for-devops/
https://aws.amazon.com/pt/compare/the-difference-between-docker-images-and-containers/
https://hanwenzhang123.medium.com/what-are-containers-images-and-volumes-in-the-docker-engine-886c0b289c86
https://cto.ai/blog/docker-image-vs-container-vs-dockerfile/
https://www.theknowledgeacademy.com/blog/docker-image-vs-container/
https://serverspace.com.br/support/help/o-que-e-um-dockerfile-guia-passo-a-passo-para-escrever-um-dockerfile/
https://www.mundodocker.com.br/o-que-e-dockerfile/
https://btholt.github.io/complete-intro-to-containers/dockerfile
https://blog.4linux.com.br/docker-compose-explicado/
https://fullcycle.com.br/docker-vs-docker-compose/
https://raccoon.ninja/pt/post/dev/um-pouco-sobre-docker-compose/
https://www.hostinger.com/br/tutoriais/o-que-e-docker-compose

