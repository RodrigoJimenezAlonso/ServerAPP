````markdown
# TutorFinder Database Server (MariaDB + Docker)

This repository provides the **database server** for the [TutorFinder App](https://github.com/RodrigoJimenezAlonso/TutoringApp).  
It contains a **Dockerized MariaDB instance** with initialization scripts to set up the schema and seed data automatically.

---

## 📂 Project Structure
```text
.
├─ docker-compose.yml      # Main Docker Compose config
├─ .env.example            # Example environment variables
├─ .gitignore              # Prevents secrets & data from being committed
├─ sql/
│  └─ init/
│     └─ 001-init.sql      # Initialization script (auto-imported on first run)
````

---

## 📊 Database Design

<img width="800" alt="UML Report" src="https://github.com/user-attachments/assets/e4baf406-24da-46f2-809f-e0368cc442d4" />

<img width="800" alt="ER Diagram" src="https://github.com/user-attachments/assets/69bfad9e-80a8-477a-9d54-6437d7f975ba" />

---

## ⚙️ Setup

### 1. Clone the repository

```bash
git clone https://github.com/your-username/tutorfinder-db.git
cd tutorfinder-db
```

### 2. Configure environment variables

Copy the example file and fill in your values:

```bash
cp .env.example .env
```

`.env.example`:

```env
DB_NAME=tutorfinder
DB_USER=tf_user
DB_PASSWORD=change_me
DB_ROOT_PASSWORD=change_me_root
```

### 3. Start the server

```bash
docker compose up -d --build
```

### 4. Verify the container is running

```bash
docker compose ps
docker logs tutorfinder-mariadb
```

---

## 🔑 Usage

### Connect from CLI

```bash
docker exec -it tutorfinder-mariadb mysql -u${DB_USER} -p${DB_PASSWORD} ${DB_NAME}
```

### Connect from TutorFinder App

Use the credentials defined in `.env` (the app connects via the backend services).

---

## 🔄 Resetting the Database

The SQL scripts in `sql/init/` are executed **only on first initialization**.
If you want to re-seed the DB after changes:

```bash
docker compose down -v
docker compose up -d --build
```

---

## 📌 Notes

* Default MariaDB port: **3306**
* Never commit your real `.env` file (it’s in `.gitignore`).
* Rotate credentials if they are ever exposed.

---

## 📈 Future Improvements

* Add migration scripts (Flyway or Liquibase).
* Support multiple environments (dev, staging, prod).
* Add test dataset for integration testing.

---

## 📝 License

MIT

```
