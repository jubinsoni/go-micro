# go-micro
microservices in golang

go -micro udemy go courses

stop nginx
sudo systemctl  stop nginx
~/Downloads/project/go-micro/front-end$ sudo go run ./cmd/web

~/Downloads/project/go-micro/broker-service$ go mod init broker

~/Downloads/project/go-micro/broker-service$ mkdir -p cmd/api

~/Downloads/project/go-micro/broker-service$ touch cmd/api/main.go


jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/broker-service$ go get github.com/go-chi/chi/v5
go: downloading github.com/go-chi/chi/v5 v5.1.0
go: downloading github.com/go-chi/chi v1.5.5
go: added github.com/go-chi/chi/v5 v5.1.0
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/broker-service$ go get github.com/go-chi/chi/v5/middleware
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/broker-service$ go get github.com/go-chi/cors
go: downloading github.com/go-chi/cors v1.2.1
go: added github.com/go-chi/cors v1.2.1

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/broker-service$ go get github.com/go-chi/chi/middleware

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch broker-service/cmd/api/routes.go
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch broker-service/cmd/api/handlers.go

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/broker-service$ sudo go run ./cmd/api

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch broker-service/broker-service.dockerfile

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch project/docker-compose.yml

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ sudo systemctl start docker.service

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ sudo apt install docker-compose


Imp debugging docker containers

cd ~/Downloads/project/go-micro/project
sudo systemctl status docker.service # if stopped then strart it by running below command
sudo systemctl start docker.service
docker-compose build --no-cache  #this will echo build failure logs on shell
docker-compose up -d


jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ docker-compose build --no-cache
 => ERROR [builder 5/6] RUN CGO_ENABLED=0 go build -o brokerApp ./cmd/api                                                                                                                                                                                                  3.2s
------
 > [builder 5/6] RUN CGO_ENABLED=0 go build -o brokerApp ./cmd/api:
1.585 go: errors parsing go.mod:
1.585 /app/go.mod:3: invalid go version '1.22.6': must match format 1.23
------

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ vi ./../broker-service/broker-service.dockerfile

#FROM golang:1.18-alpine as builder
FROM golang:1.22.6-alpine3.20 as builder

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ docker-compose build --no-cache
# if no error then
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ docker-compose up -d

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ docker ps -a
CONTAINER ID   IMAGE                    COMMAND            CREATED          STATUS         PORTS                                     NAMES
15f403bb9028   project_broker-service   "/app/brokerApp"   12 seconds ago   Up 9 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   project_broker-service_1
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ docker image ls
REPOSITORY               TAG       IMAGE ID       CREATED         SIZE
project_broker-service   latest    a05bab560503   3 minutes ago   16.3MB

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/front-end$ sudo go run ./cmd/web/
go to localhost:80
then hit test broker button

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch project/Makefile
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ docker-compose down
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ make stop

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ make up_build
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ make down

=================================================
3rd section

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ mkdir authentication-service
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ cd authentication-service
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/authentication-service$ go mod init authentication
# go: creating new go.mod: module authentication

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/authentication-service$ mkdir -p cmd/api

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ mkdir authentication-service/data
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch authentication-service/data/models.go

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch authentication-service/cmd/api/routes.go


jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/authentication-service$ go get github.com/go-chi/chi/v5
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/authentication-service$ go get github.com/go-chi/chi/v5/middleware
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/authentication-service$ go get github.com/go-chi/cors


jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/authentication-service$ go get github.com/jackc/pgconn

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/authentication-service$ go get github.com/jackc/pgx/v4

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/authentication-service$ go get github.com/jackc/pgx/v4/stdlib


jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ mkdir -p project/db-data/postgres


cd ~/Downloads/project/go-micro/project
make up_build
make down
make up
sudo make start # to start FE

docker logs -f --since=1h <container_id>
docker logs  --since=1h 58fd0d798d82 # to see logs
docker logs -f --since=1h 58fd0d798d82 # to tail logs

go to container postgres

docker exec -it 011aae678dbf bash
root@011aae678dbf:/# psql -U postgres
postgres-# \l # list all databases
postgres-# CREATE DATABASE mytest;
postgres-# \q

from machine shell

docker ps -a
CONTAINER ID   IMAGE                            COMMAND                  CREATED          STATUS          PORTS                                       NAMES
011aae678dbf   postgres:14.0                    "docker-entrypoint.s…"   10 minutes ago   Up 10 minutes   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   project_postgres_1

psql -h 127.0.0.1 -p 5432 -U postgres # password can be seen from project/docker-compose.yml

------

copy helpers.go from broker-service to authentication-service

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch authentication-service/cmd/api/handlers.go
-------------------
4th section

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ mkdir logger-service
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ cd logger-service
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/logger-service$ go mod init log-service
# go: creating new go.mod: module log

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/logger-service$ mkdir -p cmd/api

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ mkdir logger-service/data

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/logger-service$ go get go.mongodb.org/mongo-driver/mongo

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/logger-service$ go get go.mongodb.org/mongo-driver/mongo/options

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/logger-service$ go get github.com/go-chi/chi/v5
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/logger-service$ go get github.com/go-chi/chi/v5/middleware
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/logger-service$ go get github.com/go-chi/cors

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch logger-service/cmd/api/routes.go
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch logger-service/cmd/api/handlers.go
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch logger-service/cmd/api/helpers.go

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ touch logger-service/logger-service.dockerfile

---------------
5th section 

we explore 3 ways of communicating between microservices
1) http POST request
2) rabbitmq producer-consumer via AMQP
3) RPC
4) gRPC

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ mkdir mail-service
cd mail-service
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/mail-service$ go mod init mailer
# go: creating new go.mod: module log
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/mail-service$ mkdir -p cmd/api
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/mail-service/cmd/api$ cp ../../../broker-service/cmd/api/main.go .
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/mail-service/cmd/api$ cp ../../../broker-service/cmd/api/helpers.go .
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/mail-service/cmd/api$ cp ../../../broker-service/cmd/api/routes.go .


jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/mail-service$ go get github.com/go-chi/chi/v5
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/mail-service$ go get github.com/go-chi/chi/v5/middleware
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/mail-service$ go get github.com/go-chi/cors

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/mail-service$ go get github.com/vanng822/go-premailer/premailer

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/mail-service$ go get github.com/xhit/go-simple-mail/v2
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ make up_build


jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ mkdir listner-service
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro$ cd listner-service/
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/listner-service$ go mod init listener
go: creating new go.mod: module listener
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/listner-service$ go get github.com/rabbitmq/amqp091-go
go: added github.com/rabbitmq/amqp091-go v1.10.0

# add rabbitmq in project/docker-compose.yml
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ docker-compose up -d

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/listner-service$ go run main.go

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/listner-service$ go run .

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/broker-service$ go get github.com/rabbitmq/amqp091-go

jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ make up_build
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ make stop
jubin@jubin-HP-Pavilion-Notebook:~/Downloads/project/go-micro/project$ sudo make start

check weather rabbitmq is up and running
docker ps -a | grep rabbit # copy container id from here and use below
docker logs -f --since=1h <container_id> # to tail logs
# should get below log
2024-11-03 17:49:34.089954+00:00 [info] <0.754.0> accepting AMQP connection <0.754.0> (172.18.0.6:45374 -> 172.18.0.8:5672)

check weather broker service is up and running
docker ps -a | grep broker # copy container id from here and use below
docker logs -f --since=1h <container_id> # to tail logs
# should get below log
2024/11/03 17:49:33 Starting broker service on port 80

---------------
8th section 

install grpc packages
cd ~/Downloads/project/go-micro/project
go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.27
# go: downloading google.golang.org/protobuf v1.27.1
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2
# go: downloading google.golang.org/grpc v1.2.1
# go: downloading google.golang.org/grpc/cmd/protoc-gen-go-grpc v1.2.0

mkdir logger-service/logs
touch logger-service/logs/logs.proto

grpc installation : https://grpc.io/docs/protoc-installation/

cd ~/Downloads
wget https://github.com/protocolbuffers/protobuf/releases/download/v29.0-rc2/protoc-29.0-rc-2-linux-x86_64.zip
unzip protoc-29.0-rc-2-linux-x86_64.zip
cp bin/protoc ~/go/bin/
which protoc
# /home/jubin/go/bin/protoc # this means it is correctly copied
protoc --version
# libprotoc 29.0-rc2 # this means protoc is correctly installed

cd ~/Downloads/project/go-micro/logger-service/logs
protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative logs.proto

cd ~/Downloads/project/go-micro/logger-service
touch cmd/api/grpc.go

go get google.golang.org/grpc
# go: downloading google.golang.org/grpc v1.67.1
# go: downloading golang.org/x/net v0.28.0
# go: downloading google.golang.org/protobuf v1.34.2
# go: downloading golang.org/x/sys v0.24.0
# go: downloading google.golang.org/genproto/googleapis/rpc v0.0.0-20240814211410-ddb44dafa142
# go: upgraded golang.org/x/net v0.21.0 => v0.28.0
# go: upgraded golang.org/x/sys v0.23.0 => v0.24.0
# go: added google.golang.org/genproto/googleapis/rpc v0.0.0-20240814211410-ddb44dafa142
# go: added google.golang.org/grpc v1.67.1
# go: added google.golang.org/protobuf v1.34.2

go get google.golang.org/protobuf
# go: downloading google.golang.org/protobuf v1.35.1
# go: upgraded google.golang.org/protobuf v1.34.2 => v1.35.1


cd ~/Downloads/project/go-micro
mkdir broker-service/logs
touch broker-service/logs/logs.proto

cd ~/Downloads/project/go-micro/broker-service/logs
protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative logs.proto

cd ~/Downloads/project/go-micro/broker-service
go get google.golang.org/grpc
# go: added golang.org/x/net v0.28.0
# go: added golang.org/x/sys v0.24.0
# go: added golang.org/x/text v0.17.0
# go: added google.golang.org/genproto/googleapis/rpc v0.0.0-20240814211410-ddb44dafa142
# go: added google.golang.org/grpc v1.67.1
# go: added google.golang.org/protobuf v1.34.2








