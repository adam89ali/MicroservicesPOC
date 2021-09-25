# MicroservicesPOC

this is the reference repo from where I have learned [link](https://github.com/aspnetrun/run-aspnetcore-microservices)  
![Architecture](https://github.com/adam89ali/MicroservicesPOC/blob/main/ArchitectureDiagram.png?raw=true)
![Architecture](https://github.com/adam89ali/MicroservicesPOC/blob/main/ArchitectureDiagram_BigPicture.png?raw=true)


## Docker Commands
```

Docker Commands

https://documentation.portainer.io/ -- container management tool
-- username password => admin, admin1234


Example docker hub pull :
	docker run -d --hostname swn-rabbit --name swn-rabbit -p 5672:5672 -p 15672:15672 rabbitmq:3-management

Single Container
For aspnetcore app after adding docker file -- for single container add docker file build and run = create new container
	$ docker build -t aspnetapp .
	$ docker run -d -p 8080:80 --name myapp aspnetapp

docker compose up
	This command run multiple container

Multi Container - docker-compose.yml
	docker-compose up
	docker-compose -f docker-compose.yaml -f docker-compose-infrastructure.yaml up --build

docker-compose -f docker-compose.yml -f docker-compose.override.yml up --build

2

DOCKER REMOVE ALL CONTAINER IMAGES PS -A

POWERSHELL commands

https://blog.baudson.de/blog/stop-and-remove-all-docker-containers-and-images

List all containers (only IDs)
docker ps -aq
Stop all running containers
docker stop $(docker ps -aq)
Remove all containers
docker rm $(docker ps -aq)
Remove all images
docker rmi $(docker images -q)
Remove all none images
docker system prune

-- You can also run all with copy paste

docker ps -aq
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
docker rmi $(docker images -q) -f
docker system prune


Close all dockers and run with below command on that location;

	docker-compose -f docker-compose.yml -f docker-compose.override.yml up --build   // used when we made changes in existing image and want to rebuild
	or
	docker-compose -f docker-compose.yml -f docker-compose.override.yml up -d
	docker-compose -f docker-compose.yml -f docker-compose.override.yml down
```

## Catalog API
This service is simple crud implementation and it has been designed with clean layered architecture.

### Catalog service set up

1. Download docker container
2. Download MongoDb image from Docker Hub by following command:
   ```
   Docker pull mongo
   ```
3. Start mongoDb instance on Docker by following command:
   ```
   Docker run -d -p 27017:27017 --name shopping-mongo mongo
   ```
   

  #### MongoDb Commands
  ```
  1
  -- Now we can open interactive terminal for mongo

  docker exec -it shopping-mongo /bin/bash

  2
  -- After that, we are able to run mongo commands. 
  Let me try with 

   - create database
   - create collection
   - add items into collection
   - list collection


    ls --> to see the directory
    mongo --> to run mongo command
    show dbs --> show databases
    use CatalogDb  --> for create db on mongo
    db.createCollection('Products')  --> for create people collection

    db.Products.insertMany([{ 'Name':'Asus Laptop','Category':'Computers', 'Summary':'Summary', 'Description':'Description', 'ImageFile':'ImageFile', 'Price':54.93 }, { 'Name':'HP Laptop','Category':'Computers', 'Summary':'Summary', 'Description':'Description', 'ImageFile':'ImageFile', 'Price':88.93 } ])

    db.Products.insertMany(
          [
              {
                  "Name": "Asus Laptop",
                  "Category": "Computers",
                  "Summary": "Summary",
                  "Description": "Description",
                  "ImageFile": "ImageFile",
                  "Price": 54.93
              },
              {
                  "Name": "HP Laptop",
                  "Category": "Computers",
                  "Summary": "Summary",
                  "Description": "Description",
                  "ImageFile": "ImageFile",
                  "Price": 88.93d
              }
          ])

    db.Products.find({}).pretty()
    db.Products.remove({})

    show databases
    show collections
    db.Products.find({}).pretty()
  ```

## Basket.API

This service is simple crud implementation and it has been designed with clean layered architecture.

### Basket service set up
1. Download docker container
2. Download redis image from Docker Hub by following command:
   ```
   Docker pull redis
   ```
3. Start redis instance on Docker by following command:
   ```
   Docker run -d -p 6379:6379 --name basket-redis redis
   ```
   
  #### redis Commands
 ```
docker exec -it basket-redis /bin/bash

redis-cli -- coonect to redis cli to run the command
ping -- check status it will return pong

set key value
get key
set name mehmet
get name

 ```

## Discount.API

This service is simple crud implementation and it has been designed with clean layered architecture.

### Discount service set up
1. Download docker container
2. Download postgres image from Docker Hub by following command:
   ```
   Docker pull postgres
   ```
3. Start postgres instance on Docker by following command:
   ```
  
   ```
   
  #### Postgres Commands
  ```
  -- Create Table with below script
  
  Tools - Query Tool

	CREATE TABLE Coupon(
		ID SERIAL PRIMARY KEY         NOT NULL,
		ProductName     VARCHAR(24) NOT NULL,
		Description     TEXT,
		Amount          INT
	);

  -- I would like to use ProductName in this table, we can also call it ProductCode, you can use ProductId or something else. 
  -- I am going to search with ProductName in this table, because our Basket microservices has ProductName.
  -- we will retrieve coupons by productName.

  -- After running query,
  
  See Tables - Refresh

  Right click View/Edit Table with All Rows

         SELECT * FROM public.coupon ORDER BY id ASC 

  See empty

	
  -- let's adding some data for seeding table;

	Insert Discount Data

	INSERT INTO Coupon (ProductName, Description, Amount) VALUES ('IPhone X', 'IPhone Discount', 150);

	INSERT INTO Coupon (ProductName, Description, Amount) VALUES ('Samsung 10', 'Samsung Discount', 100);


   Run - F5

   See Data

   Right click View/Edit Table with All Rows

	SELECT * FROM public.coupon ORDER BY id ASC 

  ```

## Discount.Grpc (server)

This Grpc service is simple crud implementation and it has been designed with clean layered architecture.

### Discount Grpc service set up

1. Create Grpc project on visual studio (grpc application provided by .NET)
2. same configuration as discount.API
  

## Ordering API
This service is simple crud implementation and it has been designed with clean layered architecture with CQRS and DDD.  
[Domain Driven Design](https://medium.com/aspnetrun/cqrs-and-event-sourcing-in-event-driven-architecture-of-ordering-microservices-fb67dc44da7a)  
[Clean Architecture](https://medium.com/software-alchemy/a-brief-intro-to-clean-architecture-clean-ddd-and-cqrs-23243c3f31b3)  
[JasonTaylorImplementations](https://github.com/jasontaylordev/CleanArchitecture)


## API Gateway (Ocelot)
This service has implemented gateway routing pattern and the entry point for the client to communicate with internal microservices. In addition, it will have several features like rate limiting, caching so on.

## Shopping Aggregator 
This service has implemented gateway aggregation pattern which takes single request and dispatches multiple calls to various backend systems and returns single aggregated result. The reason to umplement aggregatation pattern is to avoid latency and chaining calls between services problem.

## Identity Microservices
This service is not implemented yet in this solution but it will provide cross cutting concern related authentication & authorization service using OpenID connect & OAuth2 for other microservices.

[Solution 1](https://github.com/aspnetrun/run-aspnet-identityserver4)  
[Blog](https://medium.com/aspnetrun/securing-microservices-with-identityserver4-with-oauth2-and-openid-connect-fronted-by-ocelot-api-49ea44a0cf9e)  
[Solution 2](https://github.com/Shop-Microservices/AspnetMicroservices)  
[Solution 3](https://github.com/mansoorafzal/SecureMicroservices)  

## Shopping Web Application (client)
A ASP.NET Razor based client application which communicates with the API Gateway.

