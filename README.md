# comandos_docker


## comandos docker

https://github.com/badtuxx/DescomplicandoDocker

Comandos Utilizados:

curl -fsSL https://get.docker.com/ | bash

docker version

docker container ls
 

docker container run hello-world

docker image ls

docker ps

docker container ls

docker container ls -a

docker container run -ti centos:7

docker container run -ti ubuntu

docker container -d nginx

docker container attach [CONTAINER ID]

docker container exec -ti [CONTAINER ID] [COMANDO]

docker container start [CONTAINER ID]

docker container stop [CONTAINER ID]

docker container restart [CONTAINER ID]

docker container pause [CONTAINER ID]

docker container unpause [CONTAINER ID]

 

docker container start [CONTAINER ID]

docker container stop [CONTAINER ID]

docker container restart [CONTAINER ID]

docker container pause [CONTAINER ID]

docker container unpause [CONTAINER ID]

docker container inspect [CONTAINER ID]

docker container logs -f [CONTAINER ID]

docker container rm [CONTAINER ID]

docker container attach [CONTAINER ID]

docker container rm -f [CONTAINER ID]

docker container exec -ti [CONTAINER ID] [COMANDO]

docker container run -d nginx
 

docker container stats [CONTAINER ID]

docker container top [CONTAINER ID]

docker container run -d -m 128M --cpus 0.5 nginx

docker container update --memory 64M --cpus 0.4 nginx

docker container inspect [CONTAINER ID]

docker container stats [CONTAINER ID]

docker container top [CONTAINER ID]

Comando executados dentro do container:

apt-get update

apt-get install stress

stress --cpu 1 --vm-bytes 128M --vm1

 

docker image build -t toskeira:1.0
docker image ls
docker container run -d toskeira:1.0
docker container logs -f [CONTAINER ID]

No Dockerfile:

FROM debian 

LABEL app="Giropops" 

ENV JEFERSON="LINDO" 

RUN apt-get update && apt-get install -y stress && apt-get clean 

CMD stress --cpu 1 --vm-bytes 64M --vm1

## comandos docker

docker container run -ti --mount type=bind,src=/volume,dst=/volume ubuntu

docker container run -ti --mount type=bind,src=/root/primeiro_container,dst=/volume ubuntu

docker container run -ti --mount type=bind,src=/root/primeiro_container,dst=/volume,ro ubuntu

docker volume create giropops

docker volume rm giropops

docker volume inspect giropops

docker volume prune

docker container run -d --mount type=volume,source=giropops,destination=/var/opa  nginx

docker container create -v /data --name dbdados centos

docker run -d -p 5432:5432 --name pgsql1 --volumes-from dbdados -e POSTGRESQL_USER=docker -e POSTGRESQL_PASS=docker -e POSTGRESQL_DB=docker kamui/postgresql

docker run -d -p 5433:5432 --name pgsql2 --volumes-from dbdados -e  POSTGRESQL_USER=docker -e POSTGRESQL_PASS=docker -e POSTGRESQL_DB=docker kamui/postgresql

docker run -ti --volumes-from dbdados -v $(pwd):/backup debian tar -cvf /backup/backup.tar /data

## lcomandos docker

FROM debian

RUN apt-get update && apt-get install -y apache2 && apt-get clean

ENV APACHE_LOCK_DIR="/var/lock"

ENV APACHE_PID_FILE="/var/run/apache2.pid"

ENV APACHE_RUN_USER="www-data"

ENV APACHE_RUN_GROUP="www-data"

ENV APACHE_LOG_DIR="/var/log/apache2"

LABEL description="Webserver"

VOLUME /var/www/html/

EXPOSE 80
 

FROM debian

RUN apt-get update && apt-get install -y apache2 && apt-get clean

ENV APACHE_LOCK_DIR="/var/lock"

ENV APACHE_PID_FILE="/var/run/apache2/apache2.pid"

ENV APACHE_RUN_USER="www-data"

ENV APACHE_RUN_DIR="/var/run/apache2"

ENV APACHE_RUN_GROUP="www-data"

ENV APACHE_LOG_DIR="/var/log/apache2"

LABEL description="Webserver"

VOLUME /var/www/html/

EXPOSE 80

ENTRYPOINT ["/usr/sbin/apachectl"]

CMD ["-D", "FOREGROUND"]
 

package main

import "fmt"

func main() {
	fmt.Println("GIROPOPS STRIGUS GIRUS - LINUXTIPS")
}
 

FROM golang

WORKDIR /app

ADD . /app

RUN go build -o goapp

ENTRYPOINT ./goapp
 

FROM golang AS buildando

ADD . /src

WORKDIR /src

RUN go build -o goapp


FROM alpine:3.1

WORKDIR /app

COPY --from=buildando /src/goapp /app

ENTRYPOINT ./goapp
 

ADD => Copia novos arquivos, diretórios, arquivos TAR ou arquivos remotos e os adicionam ao filesystem do container;

CMD => Executa um comando, diferente do RUN que executa o comando no momento em que está "buildando" a imagem, o CMD executa no início da execução do container;

LABEL => Adiciona metadados a imagem como versão, descrição e fabricante;

COPY => Copia novos arquivos e diretórios e os adicionam ao filesystem do container;

ENTRYPOINT => Permite você configurar um container para rodar um executável, e quando esse executável for finalizado, o container também será;

ENV => Informa variáveis de ambiente ao container;

EXPOSE => Informa qual porta o container estará ouvindo;

FROM => Indica qual imagem será utilizada como base, ela precisa ser a primeira linha do Dockerfile;

MAINTAINER => Autor da imagem; 

RUN => Executa qualquer comando em uma nova camada no topo da imagem e "commita" as alterações. Essas alterações você poderá utilizar nas próximas instruções de seu Dockerfile;

USER => Determina qual o usuário será utilizado na imagem. Por default é o root;

VOLUME => Permite a criação de um ponto de montagem no container;

WORKDIR => Responsável por mudar do diretório / (raiz) para o especificado nele;

## comandos docker

docker image inspect debian

docker history linuxtips/apache:1.0

docker login

docker login registry.suaempresa.com

docker push linuxtips/apache:1.0

docker pull linuxtips/apache:1.0

docker image ls

docker container run -d -p 5000:5000 --restart=always --name registry registry:2

docker tag IMAGEMID localhost:5000/apache

## comandos docker

docker swarm init

docker swarm join --token \ SWMTKN-1-100_SEU_TOKEN SEU_IP_MASTER:2377

docker node ls

docker swarm join-token manager

docker swarm join-token worker

docker node inspect LINUXtips-02

docker node promote LINUXtips-03

docker node ls

docker node demote LINUXtips-03

docker swarm leave

docker swarm leave --force

docker node rm LINUXtips-03

docker service create --name webserver --replicas 5 -p 8080:80  nginx

curl QUALQUER_IP_NODES_CLUSTER:8080

docker service ls

docker service ps webserver

docker service inspect webserver

docker service logs -f webserver

docker service rm webserver

docker service create --name webserver --replicas 5 -p 8080:80 --mount type=volume,src=teste,dst=/app  nginx

docker network create -d overlay giropops

docker network ls

docker network inspect giropops

docker service scale giropops=5

docker network rm giropops

docker service create --name webserver --network giropops --replicas 5 -p 8080:80 --mount type=volume,src=teste,dst=/app  nginx

docker service update <OPCOES> <Nome_Service> 

## comandos docker

echo 'minha secret' | docker secret create 

docker secret create minha_secret minha_secret.txt

docker secret inspect minha_secret

docker secret ls

docker secret rm minha_secret

docker service create --name app --detach=false --secret db_pass  minha_app:1.0

docker service create --detach=false --name app --secret source=db_pass,target=password,uid=2000,gid=3000,mode=0400 minha_app:1.0

ls -lhart /run/secrets/

docker service update --secret-rm db_pass --detach=false --secret-add source=db_pass_1,target=password app
