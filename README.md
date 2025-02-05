# Dockerized WordPress and MySQL project:

# WordPress and MySQL Docker Deployment
This project demonstrates a Docker-based deployment of WordPress (blogging platform) with MySQL database, using persistent storage for data preservation.

## Features
- WordPress container with external volume for content persistence
- MySQL container with external volume for database persistence
- Environment variables for secure database configuration
- Port mapping for external WordPress access
- Fault-tolerant storage solution

## Prerequisites
- Docker installed on host system
- Create required directories:
  
  ```bash
  mkdir /dbdata /wpdata


