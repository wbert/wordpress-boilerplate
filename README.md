# wbert-wordpress-boilerplate

A lightweight, Dockerized WordPress boilerplate configuration designed for quick local development or deployment. This setup includes pre-configured PHP settings for increased upload limits and memory, running on the latest WordPress image and MySQL 8.0.

## 🚀 Features

- **WordPress:** Latest stable version.
- **Database:** MySQL 8.0.
- **Custom PHP Config:** Pre-mapped `.ini` files to handle larger file uploads (256MB) and higher memory limits.
- **Data Persistence:** Docker volumes for both the database and WordPress core files.

## 📋 Prerequisites

Ensure you have the following installed on your machine:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## 🛠️ Quick Start

1.  **Clone or download** this repository.
2.  **Navigate** to the project directory:
    ```bash
    cd wbert-wordpress-boilerplate
    ```
3.  **Start the containers** in detached mode:
    ```bash
    docker-compose up -d
    ```
4.  **Access WordPress:**
    Open your browser and visit: `http://localhost`

## ⚙️ Configuration

### Environment Variables

The `docker-compose.yml` comes with default credentials. **For production use, please change these values.**

| Service | Variable                | Default Value        | Description                 |
| :------ | :---------------------- | :------------------- | :-------------------------- |
| **DB**  | `MYSQL_ROOT_PASSWORD`   | `your_root_password` | Root password for MySQL     |
| **DB**  | `MYSQL_USER`            | `wordpressuser`      | Database username for WP    |
| **DB**  | `MYSQL_PASSWORD`        | `your_db_password`   | Password for WP user        |
| **WP**  | `WORDPRESS_DB_PASSWORD` | `your_db_password`   | Must match `MYSQL_PASSWORD` |

### PHP Customization (`.ini` files)

This boilerplate mounts two configuration files into the PHP configuration directory (`/usr/local/etc/php/conf.d/`). You can modify these files locally to change PHP settings without rebuilding the image.

- **`uploads.ini`** & **`wordpress.ini`**:
  - `upload_max_filesize`: **256M**
  - `post_max_size`: **256M**
  - `memory_limit`: **512M**
  - `max_execution_time`: **300** (set in uploads.ini)

_To apply changes made to these files, simply restart the container:_

```bash
docker-compose restart wordpress
```

## Volume Management

Data is persisted using named Docker volumes. This ensures your database and uploaded files survive container restarts.

- `db_data`: Persists MySQL data (`/var/lib/mysql`).
- `wordpress_data`: Presist Wordpress core files, themes, and plugins (`/var/lib/mysql`).

To completely reset the project (delete all data including the DB and uploaded images):

```bash
docker-compose down -v
```

## 📝 Common Commands

### Start Docker Compose

```bash
docker-compose up
```

### Start Detach Docker Compose

```bash
docker-compose up -d
```

### Stop and remove containers/networks

```bash
docker-compose down
```

### Stop Containers

```bash
docker-compose down
```

### View logs (follow mode)

```bash
docker-compose logs -f
```
