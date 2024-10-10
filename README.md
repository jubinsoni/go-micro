# go-micro
microservices in golang




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

