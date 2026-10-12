Flask + MySQL using Docker Compose

A simple Flask application connected to a MySQL database, running with Docker Compose and persistent database storage.

Project Structure
flask-mysql-app/
├── app.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── .env
├── .gitignore
└── README.md

Prerequisites

Install the following software before running the project:

Docker Desktop (Windows/macOS) or Docker Engine (Linux)
Docker Compose
A terminal or command prompt
Verify Docker Installation

Run the following commands:

docker --version
docker compose version
docker run hello-world


Download Docker Desktop: https://www.docker.com/products/docker-desktop/

Configuration

Create a .env file in the project root directory:

MYSQL_ROOT_PASSWORD=change_this_root_password
DB_PASSWORD=change_this_app_password


Replace the example passwords with strong, unique passwords. Do not commit the .env file to version control.

Build and Run

Open a terminal in the project directory and run:

docker compose up -d --build


This command builds the Flask image and starts the Flask and MySQL containers in the background.

Access the Application

Open these URLs in your browser:

Flask Home: http://localhost:5000
MySQL Connection Test: http://localhost:5000/db

The home endpoint should display:

Flask and MySQL running with Docker Compose!


The database endpoint should return a JSON response similar to:

{
  "status": "connected",
  "mysql_version": "8.0.x"
}


The exact MySQL version may vary.

Useful Docker Commands
Check Running Containers
docker compose ps

View Application Logs
docker compose logs -f flask

View MySQL Logs
docker compose logs -f db

Stop the Containers
docker compose stop

Restart the Containers
docker compose start

Stop and Remove Containers
docker compose down

Database Persistence

MySQL data is stored in a named Docker volume called mysql_data, mounted at /var/lib/mysql.

The database files remain available when containers are stopped or removed and recreated.

To verify persistence:

docker compose down
docker compose up -d


Then test the database connection again:

http://localhost:5000/db

Important: Avoid docker compose down -v unless you intend to delete the Compose-managed database volume and its stored data.

Troubleshooting
Docker is not running

Open Docker Desktop and wait for it to finish starting. Then retry the commands.

Port 5000 is already in use

Change the port mapping in docker-compose.yml:

ports:
  - "5001:5000"


Access Flask at http://localhost:5001.

Flask cannot connect to MySQL

Check the container status and logs:

docker compose ps
docker compose logs flask
docker compose logs db


Ensure that the Flask service uses DB_HOST=db and that the environment variables in .env match the MySQL configuration.

Rebuild after changing application code
docker compose up -d --build

Technologies Used
Python
Flask
MySQL 8.0
Docker
Docker Compose
Security Notes
Use strong passwords in .env.
Do not commit .env to Git.
Do not expose the MySQL port publicly unless required.
Use a secrets-management solution for production deployments.
License

This project is intended for learning and development purposes.