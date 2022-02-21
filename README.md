We have used  React client, Node.js backend, PostgreSQL and Nginx

this is just a basic application to input numbers from client and retrieve saved numbers from DB.


in this Demo we are using a existing container 

Server: boobalan/pro-server (https://hub.docker.com/repository/docker/boobalan/pro-server)
Client: boobalan/pro-client (https://hub.docker.com/repository/docker/boobalan/pro-client)
postgres : public postgres image

If you are willing to create your own image. we have the docker file provided to build it.

cd client
docker build -t <imagename:version> .
docker push <imagename:version> <repo/imagename:version>

Similar steps for Server.

all Kubernetes manifestare under kubernetes folder.

