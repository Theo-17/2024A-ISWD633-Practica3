## Esquema para el ejercicio
![Imagen](imagenes/esquema-ejercicio3.PNG)

### Crear red net-wp
```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/)
En el esquema del ejercicio la carpeta contenedor (a) es /var/lib/mysql
Ruta carpeta host: C:\Users\sebas\Documents\GitHub\2024A-ISWD633-Practica3\ejercicio3\db

### ¿Qué contiene la carpeta db del host?
No contiene nada todavía, pero después de crear el volumen va a contenerla informacion que esta en /var/lib/mysql

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
```
docker run -d --name mysql-container --env-file "C:\Users\sebas\Documents\GitHub\2024A-ISWD633-Practica3\ejercicio3\pass.env" -v "C:\Users\sebas\Documents\GitHub\2024A-ISWD633-Practica3\ejercicio3\db:/var/lib/mysql" --network net-wp mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
La carpeta db que estaba inicialmente vacía ahora contiene los archivos y directorios creados por MySQL para almacenar la base de datos, como archivos de configuración y datos de las tablas.


### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta contenedor (b) es /var/www/html
Ruta carpeta host: C:\Users\sebas\Documents\GitHub\2024A-ISWD633-Practica3\ejercicio3\www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
```
docker run -d --name wordpress-container --env-file "C:\Users\sebas\Documents\GitHub\2024A-ISWD633-Practica3\ejercicio3\wordpress.env" -v "C:\Users\sebas\Documents\GitHub\2024A-ISWD633-Practica3\ejercicio3\www:/var/www/html" -p 1200:80 --network net-wp wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
```
docker rm -f wordpress-container
```

Las configuraciones personalizadas y las entradas que agregaste anteriormente se conservan debido a que los datos están almacenados en un volumen que está montado desde el host. Esta configuración garantiza que cualquier modificación realizada en WordPress se mantenga intacta, incluso si el contenedor se borra y se vuelve a crear.



