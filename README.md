# WordPress Local Development with Docker

This project provides a clean and developer-friendly setup for running WordPress locally using Docker. It includes MySQL, phpMyAdmin, MailHog, and custom PHP configuration — ideal for plugin/theme development, marketing tests, or client site prototypes.

---

## 🚀 Quick Start

1. **Clone this repository or copy it to a new folder**
2. Make sure you have [Docker Desktop](https://www.docker.com/products/docker-desktop) installed
3. Adjust the `.env` file if needed (see below)
4. Launch the project:

```bash
docker-compose up -d
```

5. Open in your browser:
   - WordPress: [http://localhost:8000](http://localhost:8000)
   - phpMyAdmin: [http://localhost:8080](http://localhost:8080)
   - MailHog: [http://localhost:8025](http://localhost:8025)

---

## ⚙️ Configuration (`.env`)

All key variables are stored in `.env`:

```env
COMPOSE_PROJECT_NAME=mywp           # Prefix for Docker containers and network

# WordPress Database
WORDPRESS_DB_NAME=wordpress
WORDPRESS_DB_USER=wordpress
WORDPRESS_DB_PASSWORD=wordpress
MYSQL_ROOT_PASSWORD=root

# Port mapping
PROJECT_PORT=8000          # WordPress
PMA_PORT=8080              # phpMyAdmin
MAILHOG_HTTP_PORT=8025     # MailHog UI
MAILHOG_SMTP_PORT=1025     # MailHog SMTP
```

Change these values if you're running multiple projects simultaneously.

---

## 🧠 Running Multiple Projects Without Conflict

To avoid issues when copying this project to a new folder or running several projects in parallel:

1. Use a **unique `COMPOSE_PROJECT_NAME`** in each `.env` file
2. Change the **host ports** (e.g. `8000`, `8080`) to avoid clashes
3. Alternatively, run with dynamic naming:
   ```bash
   COMPOSE_PROJECT_NAME=$(basename "$PWD") docker-compose up -d
   ```

This uses the folder name as the project name — handy when cloning or duplicating.

---

## ⚙️ Custom MySQL Configuration

You can fine-tune MySQL settings for WordPress performance and compatibility using `mysql-config/wp.cnf`. The container mounts this file into MySQL at runtime.

Here’s a sample config:

```ini
[mysqld]
max_allowed_packet = 64M
innodb_buffer_pool_size = 256M
innodb_log_file_size = 128M
default_authentication_plugin = mysql_native_password
sql_mode = ""
```

This helps with:
- Importing large databases
- Preventing SQL strict mode errors
- Ensuring stable plugin performance (e.g. WooCommerce, Elementor)

---

## 📦 File Structure

```
project-root/
│
├── docker-compose.yml        # Main Docker configuration
├── .env                      # Project-specific variables
├── wordpress/                # WordPress source files
├── php-config/php.ini        # Custom PHP settings
├── mysql-config/wp.cnf       # MySQL tuning for WordPress
└── mysql-data/               # Persisted DB data
```

---

## 🧪 Useful URLs

- WordPress: `http://localhost:8000`
- phpMyAdmin: `http://localhost:8080`
- MailHog (email testing): `http://localhost:8025`

---

## 🧼 Cleanup

To stop and remove all containers:

```bash
docker-compose down
```

To remove volumes and clean database data:

```bash
docker-compose down -v
```

---

## 📬 Tips

- Use MailHog to intercept emails locally instead of real SMTP
- You can inspect PHP settings by creating a file like `wordpress/phpinfo.php` with `<?php phpinfo(); ?>`

---

Happy coding! 🚀
