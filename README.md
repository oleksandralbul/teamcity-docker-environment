# TeamCity Environment
This project provides a Docker Compose file to set up a ready-to-use TeamCity environment.

## Prerequisites

Before you begin, ensure you have the following installed on your local machine:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started
Follow these steps to set up the TeamCity environment on your local machine.

### 1. Clone the Repository
First, clone this repository to your local machine:

```bash
git clone https://github.com/oleksandralbul/teamcity-docker-environment.git 
cd teamcity-docker-environment
```

### 2. Start the TeamCity Environment
Use Docker Compose to build and start the TeamCity environment:

```bash
docker-compose up -d
```
This command will pull the necessary Docker images, build the containers, and start them in the background.

### 3. Set Up the Database
After starting the TeamCity environment, you need to set up the MySQL database that TeamCity will use.

#### 3.1 Open the Database Container via Docker
First, access the MySQL container running in Docker:

```bash
docker exec -it database mysql -uroot -p<root-password>
```

#### 3.2 Run the Following SQL Commands
Once you're in the MySQL console, execute the following SQL commands to create the database and user:

```sql
create database <database-name> collate utf8mb4_bin;
create user <user-name> identified by '<password>';
grant all privileges on <database-name>.* to <user-name>;
grant process on *.* to <user-name>;
```

- Replace `<database-name>` with the name of the database you want to create.
- Replace `<user-name>` with the username you want to create.
- Replace `<password>` with a secure password for the new user.
#### 3.3 Complete the TeamCity Database Setup
Access the TeamCity Web UI:

Open your web browser and navigate to http://localhost:8111.
Configure Database Connection:

During the TeamCity setup process, select MySQL as the database type.
Enter the database name, username, and password you just created.
#### Finish Setup:

Follow the on-screen instructions to complete the database setup and finalize your TeamCity configuration.
This step ensures that TeamCity is properly connected to a MySQL database with the necessary permissions.

### 4. Environment Variables
You can use a .env file to manage environment variables that are used in the Docker Compose setup. Below are the two variables currently included in the .env file:

`TEAMCITY_FOLDER`: Specifies the directory on your local machine where the TeamCity environment volumes will be stored.

`MYSQL_ROOT_PASSWORD`: Sets the root password for the MySQL database.

## Troubleshooting
If the containers fail to start, ensure that the required ports are not being used by other services on your machine.
Check the Docker logs for more detailed error messages:
```bash
docker-compose logs
```
## Contributing
Contributions are welcome! Please feel free to submit a Pull Request or open an issue.

## License
This project is licensed under the MIT License.