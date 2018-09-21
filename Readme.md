### Docker apps template

#### Folder 

 - app          --  application's folder
 - containers   --  configuration files for various docker services you running
 - data         --  database and logs files (NGINX + MYSQL by default)
 - docs         --  here you might save all project-related documents, components and so on
 
 
 #### Files
 
  - docker-compose.yml  -- main configuration file for Docker
  - vessel              -- simple CLI script to facilitate easy work with Docker. 
                           https://vessel.shippingdocker.com/docs/everyday-usage/
 
 
 #### Prerequisites       
 
 1. Install Docker 
    https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce  
    
 2. Install docker-compose
    https://docs.docker.com/compose/install/
                   
 
 #### Configure & run
 
 1. Install application in ```app``` folder.
 2. Make sure of 777 permissions for ```data\db``` and ```data\log``` folders
 3. Select appropriate ports in ```docker-compose.yml```
    As you can see there are several points on which docker containers touches with localhost. One of these are ports.
    Consider container ```web```. He has port mapping,for instance  ```- "8000:80"```. This means that nginx will be 
    listening on ```80``` inside containers and maps to port ```8000``` outside. 
    In other word, we MUST choose different outside ports if we're running another instance of web-server on localhost 
    but don't care about port inside container.     
 
 4. Configure database connection in your application. Defaults :
    ```DB_HOST = mysql```
    ```DB_PORT = 3306```
    ```ROOT_PASSWORD: eXam287#```          
    ```DATABASE: appdb``` 
    ```DB_USER: appuser```
    ```DB_USER_PASSWORD: apppwd``` 
    
    pay attention that     ```DB_HOST = mysql```  is the name of container which server MySQL , in our case it is ```mysql```
     
 5. Configure NGINX 
     Adjust nginx configuration in file ```conntainers\nginx\conf\site-enabled\default.conf```
     
     At least you should change two option:
     
     - server_name app.loc;    
     - root /app;
          
     After editing nginx configuration add to file ```/etc/hosts```  line like  ```127.0.0.1  app.loc```  
  
 6. Run environment with 
 
    ```./vessel start```    or    ```docker-compose up -d```
    
    On the first start Database will be automatically created. After DB will be accessible  at localhost:3306.
      
 7. Running composer and migrations.
   
    Very often is required to run ```composer install/update``` command when you work with fresh install of project.
    The best way is to run it inside docker container. You achieve this with aim of vessel
     
    ```./vessel composer install```
     
    or run migrations ( Laravel only)
     
    ```./vessel artisan migration```
  
  
  
    
  
 
  