# WordPress Docker Setup

This project provides a Docker-based environment to deploy and manage a WordPress website with Nginx, PHP-FPM, and MySQL. It allows easy local development and deployment to cloud services like AWS LightSail and Xserver.

## Features

- WordPress with Nginx and PHP-FPM
- MySQL database for storing WordPress content
- Docker Compose for easy setup and management
- SSL configuration using Nginx Proxy Manager
- Automatic deployment via GitHub Actions

## Requirements

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)
- Git

## Installation

1. Clone the repository:

   ```sh
   git clone https://github.com/hanhnq/wordpress_project.git
   cd wordpress_project
   ```

2. Copy the environment example file and configure it:

   ```sh
   cp .env.example .env
   ```

   Update the `.env` file with your database credentials and other necessary configurations.

3. Start the Docker containers:

   ```sh
   docker-compose up -d
   ```

4. Access your WordPress site at:

   ```
   http://localhost:8080
   ```

## Database Setup

If the database is not initialized, run the WordPress installation script manually inside the container:

```sh
docker exec -it wordpress_local_wordpress bash
wp core install --url="http://localhost:8080" --title="Local WordPress" --admin_user="admin" --admin_password="admin" --admin_email="admin@example.com"
```

## Deployment

This project is set up to use GitHub Actions for automatic deployment when changes are pushed to the `main` branch. Ensure your cloud server is properly configured with Docker and SSH keys.

## Troubleshooting

### Error: "This page isn’t working (500)"

- Check the logs for Nginx:
  ```sh
  docker logs wordpress_local_nginx
  ```
- Check PHP-FPM logs:
  ```sh
  docker logs wordpress_local_php
  ```
- Check if MySQL is running:
  ```sh
  docker logs wordpress_local_db
  ```

### Error: `the input device is not a TTY`

If using Windows (Git Bash or MinTTY), use:

```sh
winpty docker exec -it wordpress_local_wordpress bash
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

