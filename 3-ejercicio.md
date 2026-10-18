## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
# COMPLETAR CON EL COMANDO COMANDO
docker network create net-wp
### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es /var/lib/mysql.

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Inicialmente la carpeta db está vacía. 

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
# COMPLETAR CON EL COMANDO
docker run -d --name srv-mysql2 --network net-wp -v "C:\Users\leome\Downloads\ejercicio3\db:/var/lib/mysql" -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=admin -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin1 mysql:8
### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Se observa que la carpeta db ahora contiene archivos y subdirectorios creados por MySQL, como mysql, performance_schema, ibdata1 y archivos relacionados con InnoDB. 

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html.

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
# COMPLETAR CON EL COMANDO
docker run -d --name wordpress --network net-wp -p 9500:80 -v "C:\Users\leome\Downloads\ejercicio3\www:/var/www/html" -e WORDPRESS_DB_HOST=srv-mysql2:3306 -e WORDPRESS_DB_USER=admin -e WORDPRESS_DB_PASSWORD=admin1 -e WORDPRESS_DB_NAME=admin wordpress

### Personalizar la apariencia de wordpress y agregar una entrada
<img width="1892" height="897" alt="imagen" src="https://github.com/user-attachments/assets/e3fa1b16-6069-4385-8b41-6f9d71492c8d" />

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA 
Al eliminar el contenedor y crearlo nuevamente, se observa que la personalización de la apariencia y la entrada agregada se mantienen porque la información se almacena en la carpeta www del host, que está vinculada con la ruta /var/www/html del contenedor.
