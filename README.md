# crm-app  - Docker Deployment Process
## Tech Stack
- Frontend: **NextJs/ViteJS - 20**
- Backend: **Java-SpringBoot - 21**
- DataBase: **MySQL - 8**
## Server setup:
    Server type: T2.medium server
    Ports: 22,80,8080,3306
    
## Setup Docker:
    sudo apt update
    curl -fsSL https://get.docker.com -o install-docker.sh
    sudo sh install-docker.sh
    sudo usermod -aG docker $USER
    newgrp docker
## Database setup:
- docker network create crmnetwork
- docker network ls
- docker container run -dt --name crmdb --network crmnetwork -p 3306:3306 -e MYSQL_ROOT_PASSWORD=admin123 mysql
- docker container ls

## Backend Setup
### Update Database Details: 
- Update your database details in this file
  - crm-api/src/main/resources/**application.properties**
      - update database container-pvt-ip
      - update database password
### Build Backend Image:
- docker build -t crm-api .
- docker image ls
### Run Backend Container:
- docker container run -dt --name crmapi --network crmnetwork -p 8080:8080 crm-api
- docker container ls
##### Check backend in browser: http://pub-ip:8080
 
## Frontend Setup 
### Update Backend Details: 
- **crm-web/.env**
  - In **Line-1**: insted of **localhost** give backend **pub-ip**

### Build Frontend Image: 
- docker build -t crm-web .
- docker image ls
   
### Run Frontend Container: 
- docker container run -dt --name crmweb --network crmnetwork -p 81:80 crm-web
- docker container ls
##### Check frontend in browser: http://pub-ip

## Default Logins
- username: **admin**
- password: **admin@123**

### Create Lead
- Just click on **Create Lead** and fill the details
<img width="484" alt="image" src="https://github.com/user-attachments/assets/985d35be-7e35-48f0-95cd-9396e6fcd03b">
- once lead create you can see the leads, if you can select and delete them

![image](https://github.com/user-attachments/assets/dcfca898-81f0-4ed3-bb87-fbef4c6484be)



