# MicroservicesPOC


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


    ls
    mongo
    show dbs
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
