# crm-app
## Tech Stack
- Frontend: **NextJs/ViteJS**
- Backend: **Java-SpringBoot**
- DataBase: **MySQL**

# Manual Deployment Process
## Server setup:
    Server type: T2.medium server
    Database: mysql 
    Backend: java-17
    Frontend: node-20
    Ports: 22,80,8080,3306
## Database setup:
    Install mysql db: sudo apt install mysql-server -y
    Mysql secure installations: sudo mysql_secure_installation
        Choose option: y/n
<img width="515" alt="image" src="https://github.com/user-attachments/assets/1c9470b7-a100-4b89-9a71-ad92d440ddc3">

    Check status: sudo service mysql status
    Restart service: sudo service mysql restart
### MySQL Password setup:
    sudo mysql -u root -p
    Enter password: empty+enter
    Password setup query:
    ```
        ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Admin!23';
        FLUSH PRIVILEGES;
        EXIT;
    ```
<img width="609" alt="image" src="https://github.com/user-attachments/assets/9102d1c4-acdb-4dcf-bba1-9d74f5863775">

## Backend Setup
### backend folder: CRUD
- Update your database details in this file
  - crm-api/src/main/resources/**application.properties**
### Install java: 
- sudo apt install openjdk-21* -y
- Java --version
### build backend:
- Change to backend directory: cd ~/crm-app/crm-api
- chmod +x mvnw
- ./mvnw clean package -D skipTest
- you will get target folder
- For manually running the application:
  - java -jar target/CRUD-0.0.1-SNAPSHOT.jar
- Browser pub-ip:8080
  - you will get message: **Whitelabel Error Page**
### Backend service setup:
- backend service file to run the application in background
- sudo vi /etc/systemd/system/crm-api.service
```
[Unit]
Description=Your Spring Boot Application
[Service]
User=ubuntu
ExecStart=/usr/bin/java -jar /home/azureuser/crm-app/crm-api/target/CRM-0.0.1-SNAPSHOT.jar
SuccessExitStatus=143
[Install]
WantedBy=multi-user.target
```
- sudo systemctl daemon-reload
- sudo systemctl start crm-api
- sudo systemctl status crm-api
- sudo systemctl enable crm-api
##### Check backend in browser: http://pub-ip:8080
 
## Frontend Setup 
### frontend folder: crm-web
- **crm-web/.env**
  - In **Line-1**: insted of **localhost** give backend **pub-ip**
![image](https://github.com/user-attachments/assets/4a198445-3f59-4e2e-8d1b-f19b0ac76d8b)

### Install Node-20
```
curl -fsSL https://deb.nodesource.com/setup_20.x -o nodesource_setup.sh
sudo -E bash nodesource_setup.sh
sudo apt-get install -y nodejs
node -v
```
- cd crm-app/crm-web/
- build tool is **npm**:
  - npm install
  - npm run build
- Output folder **dist**
<img width="604" alt="image" src="https://github.com/user-attachments/assets/5affd2ff-4ef2-41c5-b20b-1458fa144c2e">

### install nginx
- sudo apt install nginx -y
- sudo rm -rf /var/www/html/*
- sudo cp -rf dist/* /var/www/html/
- sudo systemctl restart nginx
![image](https://github.com/user-attachments/assets/c9cc8a1e-ce49-4abd-a4d4-f1029641db7b)

## Default Logins
- username: admin
- password: admin@123

### Create Lead
- Just click on **Create Lead** and fill the details
<img width="484" alt="image" src="https://github.com/user-attachments/assets/985d35be-7e35-48f0-95cd-9396e6fcd03b">
- once lead create you can see the leads, if you can select and delete them

![image](https://github.com/user-attachments/assets/dcfca898-81f0-4ed3-bb87-fbef4c6484be)



