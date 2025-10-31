
---

**MySQL** es un sistema de gestión de bases de datos relacional (RDBMS) que permite almacenar, organizar y acceder a grandes volúmenes de información de forma estructurada. Funciona mediante el lenguaje SQL (Structured Query Language) para realizar operaciones como crear, leer, actualizar y eliminar datos. Es ampliamente usado en aplicaciones web, sistemas empresariales y servidores, gracias a su velocidad, estabilidad y compatibilidad con múltiples plataformas. Además, es de código abierto y forma parte del popular conjunto de tecnologías **LAMP** (Linux, Apache, MySQL, PHP/Python/Perl).


- Entrar a una base de datos con usuario y contraseña

```bash
mysql -u <usuario> -p<contraseña> -h <IpVictima>  # La contraseña se pone junto a la "p" para evitar problemas
```

- Si no deja acceder de esta forma a la base de datos por la compatibilidad de kail o parrot, podemos acceder desde docker de la siguiente manera:

```bash
sudo docker run -it debian:latest
apt update 
apt install mariadb-client
mysql -u <usuario> -p<contraseña> -h <IpVictima> # Comando ejecutado dentro del contenedor 
```


- Usos generales dentro de la base de datos Maria-db
```sql
show databases;
use <NombreBaseDeDatos>;
show tables;
select * from <NombredelaTabla>;
```






---
# Comandos mas Usados

### ⚙️ **Conexión**

`# Entrar como root sudo mysql  # O con usuario/contraseña mysql -u usuario -p`

---

### 💾 **Bases de datos**

`SHOW DATABASES;                  -- Ver bases CREATE DATABASE midb;            -- Crear base USE midb;                        -- Usar base DROP DATABASE midb;              -- Eliminar base`

---

### 📋 **Tablas**

`SHOW TABLES;                     -- Ver tablas CREATE TABLE usuarios (   id INT AUTO_INCREMENT PRIMARY KEY,   nombre VARCHAR(50),   email VARCHAR(100) ); DESCRIBE usuarios;               -- Ver estructura`

---

### ✏️ **CRUD básico**

`INSERT INTO usuarios (nombre, email) VALUES ('Ana', 'ana@mail.com'); SELECT * FROM usuarios; UPDATE usuarios SET nombre='Ana Pérez' WHERE id=1; DELETE FROM usuarios WHERE id=1;`

---

### 👤 **Usuarios y permisos**

`CREATE USER 'app'@'localhost' IDENTIFIED BY 'clave'; GRANT ALL PRIVILEGES ON midb.* TO 'app'@'localhost'; FLUSH PRIVILEGES;`

---

### 📤 **Importar / Exportar**

`mysqldump -u usuario -p midb > midb.sql      # Exportar mysql -u usuario -p midb < midb.sql          # Importar`

---

### 🔍 **Información útil**

`SELECT VERSION();               -- Ver versión SHOW PROCESSLIST;               -- Ver conexiones`