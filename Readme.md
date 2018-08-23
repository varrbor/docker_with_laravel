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
 3. Configure database connection in your application. Defaults :
    ```DB_HOST = db```
    ```DB_PORT = 3306```
    ```ROOT_PASSWORD: eXam287#```          
    ```DATABASE: appdb``` 
    ```DB_USER: appuser```
    ```DB_USER_PASSWORD: apppwd``` 
 4. Run environment with 
 
    ```./vessel start```
    or 
    
    ```docker-compose up -d```
    
    
  On the first start Database will be automatically created. After DB will be accessible  at localhost:3306  
 
  