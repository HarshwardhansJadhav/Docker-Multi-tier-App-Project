# Dockerized WordPress and MySQL project:
This project demonstrates a Docker-based deployment of WordPress (blogging platform) with MySQL database, using persistent storage for data preservation.
![Image](https://github.com/user-attachments/assets/d43ad96e-9666-4e23-8650-fca51a4fcecf)

## Features
- WordPress container with external volume for content persistence
- MySQL container with external volume for database persistence
- Environment variables for secure database configuration
- Port mapping for external WordPress access
- Fault-tolerant storage solution

## 📋 Project Overview
- **WordPress Container**: Hosts the blog application (port `8080` mapped to `80`).
- **MySQL Container**: Acts as the database server with persistent storage.
- **Data Persistence**: Volumes (`/wpdata` and `/dbdata`) ensure data remains intact even if containers are terminated.
 
## Prerequisites
- Docker installed on host system
- Create required directories.
- Terminal access to run docker commands.
___________________________________________________________________________________________________________________________________________________________________________________________________________

### 1. Download docker pre-cooked images from hub.docker.
 ```bash
 docker pull mysql
 docker pull wordpress
```
![Image](https://github.com/user-attachments/assets/dba5d80e-b6bd-4a7d-aeda-9ff2e48cd32a)
![Image](https://github.com/user-attachments/assets/3ea5bb02-0aa3-4ae1-bc61-9533a3d40afe)

___________________________________________________________________________________________________________________________________________________________________________________________________________


### 2. Create Directories for Persistent Storage.
  ```bash
  mkdir /dbdata /wpdata
```
![Image](https://github.com/user-attachments/assets/6ec03c00-0d01-4d0c-9a54-33ca3696f5a6)
___________________________________________________________________________________________________________________________________________________________________________________________________________

### 3. Deploy the MySQL Container.
```bash
MySql = docker run -dit --name db
-e MYSQL_ROOT_PASSWORD=redhat
-e MYSQL_DATABASE=myblog
-e MYSQL_USER=harsh
-e MYSQK_PASSWORD=redhat
-v /dbdata:/var/lib/mysql mysql
```
![Image](https://github.com/user-attachments/assets/9f022c82-946e-4764-ac9f-04285292bfe0)

- **Environment Variables:** Configure the root user, database, and application user.

- **Volume:** Data is stored in /dbdata on the host.
___________________________________________________________________________________________________________________________________________________________________________________________________________

### 4. Deploy the WordPress Container.
```bash
WordPress = docker run  -dit --name wp -p 8080:80 -v /wpdata:/var/www/html wordpress
```
- **Port Mapping:** Access WordPress at http://localhost:8080.

- **Volume:** WordPress files are stored in /wpdata on the host.

![Image](https://github.com/user-attachments/assets/e2a516a7-163d-4427-a05d-cb2cca455934)
___________________________________________________________________________________________________________________________________________________________________________________________________________

### 5. 🔄 Data Persistence Explained
- **Volumes:**

  - **WordPress:** Host directory /wpdata maps to container's /var/www/html.

  - **MySQL:** Host directory /dbdata maps to container's /var/lib/mysql.

- **Fault Tolerance:**

  - Data survives container termination/restarts.

  - To reset data, delete the host directories (/dbdata, /wpdata).
___________________________________________________________________________________________________________________________________________________________________________________________________________

### 6. Accessing/Installing/Logging in WordPress.

![Image](https://github.com/user-attachments/assets/711efcbe-a008-4eb2-b2c6-808226879a5e)

- Successfully accessed WordPress site.
___________________________________________________________________________________________________________________________________________________________________________________________________________

![Image](https://github.com/user-attachments/assets/a7455d4c-cb95-4643-a9c9-609e58c9ea73)
- Filling the below details to Login with WordPress
  - **Database Name** - myblog
  - **Username** -
  - **Password** - 
  - **Database Host** - mysql container ip
___________________________________________________________________________________________________________________________________________________________________________________________________________

![Image](https://github.com/user-attachments/assets/e8971f6a-2cc9-4c15-81db-be0329d5379c)
- Successfully submitted details.
- Run the installation.
___________________________________________________________________________________________________________________________________________________________________________________________________________

![Image](https://github.com/user-attachments/assets/13f50432-79b6-43eb-94ca-570f60451056)
- Adding more information for Wordpress
 - Site Title - myblog
 - Username - harsh
 - Password -
 - Your email -
Install WordPress.
___________________________________________________________________________________________________________________________________________________________________________________________________________

![Image](https://github.com/user-attachments/assets/8b8f935b-876c-44c9-8e88-15cf2778a2bc)

- Successfully installed WordPress
- Login with WordPress
___________________________________________________________________________________________________________________________________________________________________________________________________________
### 7. Creating Blogs on WordPress 

- WordPress Dashboard
  ![Image](https://github.com/user-attachments/assets/2c6886b6-c945-45bf-8153-4641baa175f3)
  ___________________________________________________________________________________________________________________________________________________________________________________________________________
- Creating Blogs
![Image](https://github.com/user-attachments/assets/7ea3edd3-7d07-4cde-b1ce-a229410a3d2f)
___________________________________________________________________________________________________________________________________________________________________________________________________________
- Blog published
![Image](https://github.com/user-attachments/assets/3d628861-236c-45f3-a7f3-1fa0c79f3c97)
___________________________________________________________________________________________________________________________________________________________________________________________________________
### 8. Test Data Persistence
- MySql data stored persistantly in external storage.
- Stopping & Removing mysql container.
  ```bash
  storage = ls /dbdata
  removed = docker rm -f db
  ```
![Image](https://github.com/user-attachments/assets/9e227c1a-a919-4909-a541-0f936be3ec38)

Re-run the docker run commands from Steps 3 and 4, and MySql data recovered.

___________________________________________________________________________________________________________________________________________________________________________________________________________
- WordPress data stored persistanly in external storage.
- Stopping & Restoring wordpress container.
```bash
storage = ls /wpdata
removed = docker rm -f wp
```
![Image](https://github.com/user-attachments/assets/2a0fdbbe-2a72-4151-9f42-9e6ac7f61002)

Re-run the docker run commands from Steps 3 and 4, and WordPress blogs data recovered. 
__________________________________________________________________________________________________________________________________________________________________________________________________________


### Troubleshooting

**WordPress Cannot Connect to MySQL**
- Ensure both containers are running:
 ```bash
  docker ps -a
```
- Permission issues:
```bash
  sudo chmod -R 755 /wpdata /dbdata
```
- User permissions to use MySql databash:
  ```bash
  check = mysql -u root -p
          - SHOW DATABASES;
          - SELECT user, host FROM mysql.user;
          - SHOW GRANTS FOR 'username'@'host';
          - SHOW GRANTS FOR 'myuser'@'%';
      - EXIT;
  ```
  

**If WordPress giving error 'can't asses database' while Installation**
  - stop & start Mysql container.
    ```bash
    docker stop db
    docker start db
    ```
___________________________________________________________________________________________________________________________________________________________________________________________________________

## ❓ FAQ

### **Q:** Will my data persist if I delete the containers?
Yes! Data is stored in /wpdata and /dbdata on the host, not inside the containers.

### **Q:** How do I change the WordPress port?
Modify the -p flag in the WordPress docker run command (e.g., -p 8081:80).

### **Q:** Can I use a different MySQL password?
Yes! Update the MYSQL_ROOT_PASSWORD and MYSQL_PASSWORD environment variables in the MySQL docker run command.

### **Q:** Where is the WordPress site accessible?
Visit http://localhost:8080 (or your server's IP if deployed remotely).

___________________________________________________________________________________________________________________________________________________________________________________________________________

# Thank you. 
