# Docker scripts

## amule

```sh
docker run -p 4712:4712 -p 4662:4662 -p 4672:4672/udp 
    -e GUI_PWD=password 
    -v amule/conf:/home/amule/.aMule -v amule/incoming:/incoming -v amule/tmp:/temp tchabaud/amule

docker run -p 4711:4711 -p 4662:4662 -p 4672:4672/udp
    -e WEBUI_PWD=password
    -v ./amule/conf:/home/amule/.aMule -v ./amule/incoming:/incoming -v ./amule/tmp:/temp tchabaud/amule
```

## mongo

```sh
# create volume
docker create -v /data/db --name MongoData alpine
# create container and use created volume
docker run -p 27017:27017 --name mongo -d --volumes-from MongoData mongo

# create container and mount volume from path
docker run -p 27017:27017 --name mongo -v ~/Docker/mongo:/data -d mongo

# mongo client
docker run -d -p 27018:3000  --name mongoclient -v ~/Docker/mongo:/data mongoclient/mongoclient
```

## mysql

```sh
 docker run -p 3306:3306 --name mysql 
    -e MYSQL_ROOT_HOST=% -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=myorg -e MYSQL_USER=me -e MYSQL_PASSWORD=password 
    -d mysql
```

## nodered

```sh
docker run -d  -p 1880:1880 -v ~/Docker/nodered:/data --name nodered nodered/node-red
```

## postgres

```sh
# postgres with volume
docker run -d --name postgres -p 5432:5432 
    -e POSTGRES_PASSWORD=password -e POSTGRES_USER=mario -e PGDATA=/var/lib/postgresql/data/pgdata 
    -v ~/Docker/postgres:/var/lib/postgresql/data postgres

# pgadmin
docker run --name pgadmin -e "PGADMIN_DEFAULT_EMAIL=mario.lazzari@gmail.com" -e "PGADMIN_DEFAULT_PASSWORD=password" -p 5050:80 --link postgres -d dpage/pgadmin4
```

## redis

```sh
docker run --name redis -v ~/Docker/redis:/data -p 6379:6379 redis
```

## SQL Server

[Article](https://blog.sqlauthority.com/2019/04/20/sql-server-docker-volume-and-persistent-storage/)

```sh
docker run --name mssql -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=P@ssword2023" -p 1433:1433 
    -v ~/Docker/mssql/data:/var/opt/mssql/data 
    -v ~/Docker/mssql/log:/var/opt/mssql/log 
    -v ~/Docker/mssql/secrets:/var/opt/mssql/secrets 
    -d mcr.microsoft.com/mssql/server:2019-latest

# copy backup file to container
docker cp backup.bak sql2019:/var/opt/mssql/data/backup.bak
```

## SuperMario

```sh
docker run -d -p 8600:8080 bharathshetty4/supermario
```