- Build the application
- Build a Docker image for the application
- Create a Docker image from an artifact
- Upload Docker image to Docker Hub
- Remove unused Docker image
- Perform code analysis using SonarQube
- Deploy the application to Kubernetes using Helm

## Prerequisites
- JDK 1.8 or later
- Maven 3 or later
- MySQL 5.6 or later

## Technologies 
- Spring MVC
- Spring Security
- Spring Data JPA
- Maven
- JSP
- MySQL
- 
## Database
Here, I used Mysql DB 
MSQL DB Installation Steps for Linux ubuntu 14.04:
- $ sudo apt-get update
- $ sudo apt-get install mysql-server

Then look for the file :
- /src/main/resources/accountsdb
- accountsdb.sql file is a mysql dump file. We have to import this dump to the mysql db server
- > MySQL -u <user_name> -p accounts < accountsdb.sql


