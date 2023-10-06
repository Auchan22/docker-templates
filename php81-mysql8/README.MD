# Template Base *PHP* y *MySQL*
---
Template creado para base de las siguientes tecnologías:
* 🐘 **PHP 8.1**
* ⚙️ **MySQL 8.0**
* 🖥️ **Nginx**
---
### Pasos a seguir para obtener el template
1) Realizar un `git clone <url_proyecto>` para obtener la base del proyecto
2) Crear y configurar un archivo *.env* con las propiedades:
```env
DATABASE_ROOT_PASS=<Contraseña del user root de la DB>
DATABASE_PASS=<Contraseña del user de la DB>
DATABASE_USER=<Usuario de la DB>
DATABASE_NAME=<Nombre de la DB>
```
3) Ejecutar el comando `docker compose up`