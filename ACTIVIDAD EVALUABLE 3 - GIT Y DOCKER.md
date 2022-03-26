# ACTIVIDAD EVALUABLE 3 - GIT Y DOCKER

Para empezar a organizar la entrega de la tarea se va a crear un repositorio GitHub (

[https://github.com/IgnacioFernandezGonzalez/Actividad3]: 

) para alojar las distintas soluciones de los ejercicios que componen la tarea.



<img src="ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324194209941.png" alt="image-20220324194209941" style="zoom:80%;" />



A continuación he generado un directorio en mi disco local para alojar mis ficheros y poder trasladar los cambios a GitHub



## Ejercicio 1 - trabajo con imágenes

### Servidor WEB

Para empezar vamos a ejecutar un contenedor con la imagen de php:7.4-apache. Le vamos a dar de nombre web y vamos a hacer que sea accesible desde el navegador por el puerto 8080. 

Lo primero que podemos hacer es comprobar si tenemos algún contenedor con ese nombre "web" ya que de ser así,no se nos permitiría crear otro, para ello usamos el comando

```
docker ps -a
```

Que nos muestra el listado de contenedores que tenemos,como se puede observar no tenemos ninguno con el nombre "web"

<img src="ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324194947547.png" alt="image-20220324194947547" style="zoom:80%;" />

Ya podemos crear el contenedor con la imagen php:7.4-apache

Para ello ejecutamos el siguiente comando.

```
docker run -it -p 8000:80 --name web -v /ignaciofernandez/ejercicio1:/var/www/html/ -d php:7.4-apache
```

![image-20220324195939526](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324195939526.png)

Ahora que tenemos el contenedor corriendo, vamos a ponernos en su shell,para poder acceder a sus directorios y crear los siguientes ficheros.

Para ello ejecutamos el siguiente comando

```
docker exec -it web bash
```

Obteniendo el siguiente resultado

![image-20220324200228407](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324200228407.png)

Ahora podemos hacer el siguiente paso, que es crear el fichero `index.html`, para ello ayudándonos del editor nano (el cual hay que instalar en el contenedor), editaremos el fichero segun el enunciado del ejercicio.

Primero actualizamos la lista de paquetes con:

```
apt-get update
```

Para a continuación instalar el editor de textos nano, con el siguiente comando

```
apt-get install nano
```

Ya podemos crear el fichero index.html con el código que queramos.

<img src="ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324205200677.png" alt="image-20220324205200677" style="zoom:80%;" />

Ahora podemos visualizar este documento .html en el navegador y por el puerto 8000, como indicamos al correr el contenedor.

![image-20220324205329652](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324205329652.png)

En este punto, y haciendo uso de git, vamos a crear una rama en nuestro repositorio para alojar el documento .md que estamos creando con la solucion de este ejercicio.

Iniciamos un repositorio en la carpeta de local donde estamos guardando los documentos, con el comando.

```
git init
```

![image-20220324211208487](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324211208487.png)

Una vez iniciado el repositorio, añadimos los ficheros que tenemos actualmente a este repositorio con el comando

```
git add .
```

![image-20220324211341892](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324211341892.png)

Si ejecutamos el comado 

```
git status
```

observamos que tenemos cambios sin confirmar

![image-20220324211530767](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324211530767.png)

El siguiente paso es realizar un commit, para confirmar estos cambios que damos por buenos.

```
git commit -m "index.htm creado"
```

![image-20220324211705570](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324211705570.png)

Podemos subir estos ficheros a github, con el comando

```
git push origin master
```

Ahora estamos trabajando en la rama master, pero en el ejercicio se nos dice que trabjemos en ramas diferentes para cada apartado, por tanto vamos a crear una rama "ejercicio1" y ahí trabajaremos en este ejercicio.

```
git branch ejercicio1
```

Y nos situaremos en ella con el siguiente comando

```
git checkout ejercicio1
```

Como se observa ya estamos en la rama "ejercicio1"

![image-20220324212056453](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324212056453.png)

Ahora podemos subir estos ficheros de la rama a git hub, para ello, ejecutamos el comando

```
git push origin ejercicio1
```

Como vemos en github, tenemos las ramas subidas (main y ejercicio1)

![image-20220324212544869](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324212544869.png)

En este mismo apartado se nos manda incluir tambien en la misma ruta un fichero mes.php que muestre el mes actual. Para ello crearemos en el directorio /var/www/html de nuestro contenedor el fichero mes.php con el siguiente contenido.

```
<?php
setlocale(LC_TIME, 'esp');
echo date("F");
?>
```

Nos muestra lo siguiente (debería de mostrarlo en castellano, pero en mi navegador no es así, y el código es el correcto.)

![image-20220325184500294](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220325184500294.png)

En este punto vamos a comprobar el tamaño del contenedor web después de crear los ficheros index.html y mes.php, lo haremos con el comando

```
docker ps --size
```

Obteniendo como resultado 19.5MB

![image-20220325190934653](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220325190934653.png)

Por último borraremos el contenedor.

Primero tenemos que para el contenedor con el comando

```
docker stop web
```

Y ahora podremos eliminarlo con el comando

```
docker rm web
```

![image-20220325191437294](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220325191437294.png)

Como vemos ahora, el contenedor "web", no existe

![image-20220325191529855](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220325191529855.png)

### Servidor de base de datos

Ahora vamos a correr un contenedor que ejecute una onstancia de la imagen mariadb.

Como vemos esta imagen esta en GitHub, y es oficial

![image-20220325192124263](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220325192124263.png)

Lo primero que haremos, será dentro de nuestra rama para solucionar este ejercicio descargarnos la imagen de mariadb

```
docker pull mariadb
```

Una vez descargada podremos correr el contenedor y ponerle los datos de usuarios y contraseñas que se nos solicitan en el ejercicio, lo haremos con el comando

```
docker run --detach --name bbdd --env MARIADB_USER=invitado --env MARIADB_PASSWORD=invitado --env MARIADB_ROOT_PASSWORD=root --env MARIADB_DATABASE=prueba mariadb:latest
```

![image-20220325195010317](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220325195010317.png)

Vamos a conectarnos a la base de datos para comprobar que tenemos acceso con el usuario creado y donde se ve que esta creada la base de datos prueba

Para la conexion a la base da datos  primero nos pondremos en el shell del contenedor, con el comando

```
docker exex -it bbdd bash
```

Y a continuacion nos conectaremos a la base de datos con el usuario creado y su contraseña, a traves del siguiente comando

```
mysql --user=invitado --password=invitado
```

![image-20220325201610299](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220325201610299.png)

Una vez conectados podemos ver si se nos ha creado la base de datos "prueba", con el comando 

```sql
show databases;
```

Y como podemos comprobar, el resultado es satisfactorio

![image-20220325201726574](image-20220325201726574.png)

Para elimianr el contenedor usaremos el comando

```
docker rm bbdd
```

Al no haber parado el contenedor nos da un error y no nos deja borrarlo

![image-20220325201855647](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220325201855647.png)

Debemos de parar el contenedor con el siguiente comando, antes de eliminarlo

```
docker stop bbdd
```

Ahora ya podemos eliminar el contenedor. Cómo e ve en la imagen, ya esta eliminado

![image-20220325202040544](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220325202040544.png)



Ejercicio 2 - almacenamiento

Para la resolución de este segundo ejercicio lo primero que tenemos que crear es una carpeta "saludo", yo la haré en el directorio /ejercicio2/saludo

```
mkdir saludo
```

Una vez estemos en el directorio creado, crearemos un fichero `index.html`

con el siguiente contenido

![image-20220326114056666](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326114056666.png)

Como siempre usando el editor nano, con el comando 

```
sudo nano index.html
```

El siguiente paso será arrancar uno de los contenedores que se nos pide "c1", haciendo un bind mount de la carpeta saludo en la carpeta `/var/html/www` de dicho contenedor, y haciendo que podamos acceder a el contenido por el puerto 8181

Lo haremos con el comando

```
docker container run --name c1 -v /ejercicio2/saludo:/var/www/html --publish 8181:80 --detach --restart=always php:7.4-apache
```

![image-20220326114511884](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326114511884.png)

Una vez montado podemos acceder por el navegador a nuestro fichero .html en el puerto 8181

![image-20220326115104988](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326115104988.png)

