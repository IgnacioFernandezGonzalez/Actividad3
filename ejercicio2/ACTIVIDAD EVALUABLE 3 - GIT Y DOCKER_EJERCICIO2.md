# ACTIVIDAD EVALUABLE 3 - GIT Y DOCKER

[TOC]



## INTRODUCCION

Para empezar a organizar la entrega de la tarea se va a crear un repositorio GitHub (

[https://github.com/IgnacioFernandezGonzalez/Actividad3]: 

) para alojar las distintas soluciones de los ejercicios que componen la tarea.



<img src="ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324194209941.png" alt="image-20220324194209941" style="zoom:80%;" />



A continuación he generado un directorio en mi disco local para alojar mis ficheros y poder trasladar los cambios a GitHub



## Ejercicio 2 - almacenamiento

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

Vemos que una vez accedimos al contenedor c1, podemos visualizar el contenido de `index.html`

![image-20220326121826152](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326121826152.png)

Una vez montado podemos acceder por el navegador a nuestro fichero .html en el puerto 8181

![image-20220326115104988](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326115104988.png)

Para continuar, arrancaremos otro contenedor de nombre "c2", haciendo un bind mount de la carpeta saludo en la carpeta `/var/html/www` de dicho contenedor, y haciendo que podamos acceder a el contenido por el puerto 8282

Lo haremos con el comando

```
docker container run --name c2 -v /ejercicio2/saludo:/var/www/html --publish 8282:80 --detach --restart=always php:7.4-apache
```

![image-20220326115644724](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326115644724.png)

Ahora con el contenedor "c2" arrancado modificaremos el contenido del fichero `index.html`, vemos que se puede seguir accediendo a `index.html` con el contenedor c2 arrancado.

![image-20220326115829601](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326115829601.png)

Vamos a comprobar que efectivamente tenemos acceso a este index.html por el puerto 8282

![image-20220326120006000](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326120006000.png)

A continuación vamos a comprobar que podemos seguir accediendo a lso dos contenedores, sin necesidad de reiniciarlos

Primero comprobamos que están creados y en funcionamiento, con el comando

```
docker ps
```

![image-20220326120437792](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326120437792.png)

Efectivamente están en funcionamiento, y ahora vamos a acceder a cada uno de ellos con el comando

```
docker exec -i -t c1 /bin/bash
```

![image-20220326120802387](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326120802387.png)

Vemos que efectivamente accedemos al shell del contenedor c1

Ahora haremos lo mismo con el contenedor c2

```
docker exec -i -t c2 /bin/bash
```

![image-20220326120954816](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326120954816.png)

Como paso final borraremos ambos contenedores, para lo que antes tendremos que pararlos con el comando

```
docker stop c1 c2
```

![image-20220326121155519](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326121155519.png)

Para a continuación eliminarlos con el comando

```
docker rm c1 c2
```

![image-20220326121254703](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326121254703.png)

Si hacemos 

```
docker ps -a
```

Vemos que ya no existen estos contenedores

![image-20220326121406181](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220326121406181.png)