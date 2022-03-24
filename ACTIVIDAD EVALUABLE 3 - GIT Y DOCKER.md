# ACTIVIDAD EVALUABLE 3 - GIT Y DOCKER

Para empezar a organizar la entrega de la tarea se va a crear un repositorio GitHub (

[https://github.com/IgnacioFernandezGonzalez/Actividad3]: 

) para alojar las distintas soluciones de los ejercicios que componen la tarea.



<img src="ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324194209941.png" alt="image-20220324194209941" style="zoom:80%;" />



A continuación he generado un directorio en mi disco local para alojar mis ficheros y poder trasladar los cambios a GitHub



## Ejercicio 1 - trabajo con imágenes

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

Ahora podemos hacer el siguiente paso, que es crear el fichero `index.html`, para ello ayudandonos del editor nano (el cual hay que instalar en el contenedor), editaremos el fichero segun el enunciado del ejercicio.

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

Ahora podemos visualizar este documento html en el navegados y por el puerto 8000, como indicamos al correr el contenedor.

![image-20220324205329652](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324205329652.png)

En este punto vamos a confirmar nuestros cambios en git y vamos a pasar los ficheros a nuestro repositorio de github

