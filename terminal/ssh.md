### Set Up and Create PostgreSQL Database into server

#### Connect to Server

To connect to the server, you need to know:
* The public/private IP of the server
* The username
* The user password
```bash
ssh [USER]@[SERVER_IP]
```

#### Check Active Ports

Install netstat and verify that the PostgreSQL port is available:
```bash
sudo apt update
sudo apt install net-tools
sudo netstat -tuln | grep [PORT]
```

#### Transfer Dump to Server
```bash
scp [DUMP_NAME].sql [USER]@[SERVER_IP]:[DESTINATION_DIRECTORY]
```

#### Create Database

 - **Option 1:** Create directly
```bash
docker exec -i [CONTAINER_NAME] psql -U [DB_USER] -d [DB_NAME] < [DUMP_PATH].sql
```

- **Option 2:** Recreate database from scratch
```bash
cd [PROJECT_DIRECTORY]
docker exec -i [CONTAINER_NAME] psql -U [DB_USER] -d postgres -c "DROP DATABASE [DB_NAME];"
docker exec -i [CONTAINER_NAME] psql -U [DB_USER] -d postgres -c "CREATE DATABASE [DB_NAME];"
docker exec -i [CONTAINER_NAME] psql -U [DB_USER] -d [DB_NAME] < [DUMP_PATH].sql
```

To verify if the database is configured correctly, we can run the following command:
```bash
docker exec -it [CONTAINER_NAME] psql -U [DB_USER] -d [DB_NAME]
```
