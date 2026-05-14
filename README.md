# ABO YUMA WordPress Docker Nginx

![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![WordPress](https://img.shields.io/badge/WordPress-21759B?logo=wordpress&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?logo=nginx&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?logo=mariadb&logoColor=white)
![phpMyAdmin](https://img.shields.io/badge/phpMyAdmin-6C78AF?logo=phpmyadmin&logoColor=white)

**🐳 Lightweight WordPress sandbox using Docker, Nginx, PHP-FPM, and MariaDB.**

This project is designed for local WordPress plugin and theme development with a setup that behaves more like a modern production stack.  

This project also includes migration support for those transitioning from XAMPP-based environments.

## 🧩 Project Structure

```text
aboyuma/                              # Project workspace
├── aboyuma-wordpress-docker-nginx/   # Infrastructure ← This project
├── wordpress/                        # Bind-mounted WordPress development workspace
│   ├── wp-content/
│   │   ├── plugins/
│   │   ├── themes/
│   │   └── uploads/
└── migration/                        # Migration assets
````

## 🧑‍💻 Plugin & Theme Development

The WordPress core is stored inside a Docker volume.  

```yaml
volumes:
  - wordpress:/var/www/html
```

Only selected `wp-content` directories are bind-mounted to the host machine:

```yaml
# Bind-mounted wp-content directories
- ../wordpress/wp-content/plugins:/var/www/html/wp-content/plugins
- ../wordpress/wp-content/themes:/var/www/html/wp-content/themes
- ../wordpress/wp-content/uploads:/var/www/html/wp-content/uploads
```

Develop plugins and themes inside:

```text
wordpress/wp-content/plugins
wordpress/wp-content/themes
```
Changes are instantly reflected inside the container and persist even after stopping Docker containers.

## 🚀 Run Containers

Start containers:

```bash
docker compose up
```

Run in detached mode:

```bash
docker compose up -d
```

Stop containers:

```bash
docker compose down
```

Remove containers and database volume:

```bash
docker compose down -v
```

## 🌐 Access

### WordPress Site

[http://localhost](http://localhost)

### WordPress Admin Dashboard

[http://localhost/wp-admin](http://localhost/wp-admin)

### phpMyAdmin

[http://localhost:8081](http://localhost:8081)


## 🔐 Default Credentials

### Database User

* Username: `db_user`
* Password: `db_pass`

### Database Root User

* Username: `root`
* Password: `root123`

## 🗄️ Database Storage

MariaDB data is stored inside a Docker volume:

```yaml
volumes:
  - mariadb_data:/var/lib/mysql
```

This allows database data to persist across container restarts.

To completely reset the database:

```bash
docker compose down -v
docker compose up
```
