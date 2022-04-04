# ACTIVIDAD EVALUABLE 3 - GIT Y DOCKER





## INTRODUCCION

Para empezar a organizar la entrega de la tarea se va a crear un repositorio GitHub (

[https://github.com/IgnacioFernandezGonzalez/Actividad3]: 

) para alojar las distintas soluciones de los ejercicios que componen la tarea.

![image-20220331185117830](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220331185117830.png)



A continuación he generado un directorio en mi disco local para alojar mis ficheros y poder trasladar los cambios a GitHub



## Ejercicio 4 - imagen con Dockerfile

En este ejercicio vamos a crear una imagen personalizada basada en nginx, para poder desplegar una pagina web en nuestro propio servidor.

Lo primero que tenemos que hacer es crear nos un directorio en local donde vamos a almacenar los ficheros necesarios para que nuestra pagina web funcione correctamente, además de un fichero Dockerfile, que será el que usemos para montar la imagen deseada.

![image-20220401195633409](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220401195633409.png)

Ahora tendremos que configurar el fichero Dockerfile, para que tenga las instrucciones necesarias para montar nuestra imagen, como nosotros queramos, el código de este fichero es el siguiente

![image-20220401195806522](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220401195806522.png)

Una vez que hemos guardado estas modificaciones en el fichero Dockerfile, abrimos una terminal en este mismo directorio y  creamos la nueva imagen, en mi caso le he puesto de nombre imagen_nginx_ignacio

Lo haremos con el comando

```
docker build -i imagen_nginx_ignacio .
```

![image-20220401195959296](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220401195959296.png)

Ya tenemos creada nuestra propia imagen, ahora nos quedará crear una contenedor con esta imagen, en mi caso lo he llamado mynginx.

Lo haremos con el comando

```
docker run --name mynginx -p 80:80 -d imagen_nginx_ignacio
```

![image-20220401200358789](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220401200358789.png)

Ahora ya podremos acceder a nuestra web desde nuestro navegador

![image-20220401200650139](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220401200650139.png)

Por último vamos a subir nuestra imagen de nginx modificada a nuestro repositorio de Docker Hub, para ello tendremos que como primer paso crear una espejo de nuestra imagen, lo haremos con el comando 

```
docker commit e52172f393c5 nginx_ignacio:1.0
```

![image-20220401203436183](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220401203436183.png)

A continuación, nos exportaremos a un fichero . jar este espejo. lo haremos con el comando

```
docker save -0 nginx_ignacio.jar nginx_ignacio:1.0
```

![image-20220401203604087](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220401203604087.png)

Con la imagen ya exportada a nuestro fichero `nginx_ignacio.jar`, lo que nos queda es subir nuestra imagen a nuestra cuenta de Docker Hub para que cualquier persona pueda usarla, incluso nosotros mismos tengamos acceso desde cualquier lado.

Para ello, lo primero que vamos a hacer es modificar el tag de la imagen en cuestión, acorde a nuestra cuenta de Docker Hub (ignaciofernandezgonzalez), lo haremos con el comando

```
docker tag nginx_ignacio:1.0 docker.io/ignaciofernandezgonzalez/nginx_ignacio
```

![image-20220404161847778](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220404161847778.png)

Una vez que lo hemos hecho sólo nos quedará subir nuestra imagen a nuestra cuenta de Docker Hub, para lo que nos tendremos que loguear con el comando

```
docker login -i "ignaciofernandezgonzalez" -p "contraseña" docker.io
```

![image-20220404162448876](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220404162448876.png)

Y a continuación, subir la imagen con el comando

```
docker push ignaciofernandezgonzalez/nginx_ignacio
```

![image-20220404162235787](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220404162235787.png)

Como se puede observar en la imagen siguiente, se ha subido nuestra imagen `"nginx_ignacio"` a nuestro repositorio en Docker Hub.

![image-20220401203315048](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220401203315048.png)

