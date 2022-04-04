# ACTIVIDAD EVALUABLE 3 - GIT Y DOCKER

[TOC]



## INTRODUCCION

Para empezar a organizar la entrega de la tarea se va a crear un repositorio GitHub (

[https://github.com/IgnacioFernandezGonzalez/Actividad3]: 

) para alojar las distintas soluciones de los ejercicios que componen la tarea.



<img src="ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220324194209941.png" alt="image-20220324194209941" style="zoom:80%;" />



A continuación he generado un directorio en mi disco local para alojar mis ficheros y poder trasladar los cambios a GitHub



## Ejercicio 3 - redes

Lo primero que vamos a hacer va a ser crear la red bridge que se nos solicita, para ello ejecutaremos el siguiente comando

```
docker network create --driver bridge redbd
```

![image-20220328182154568](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220328182154568.png)

Como podemos observar se ha creado la red "redbd", con el comando

```
docker network ls
```

![image-20220328182325734](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220328182325734.png)

Lo siguiente será crear un contenedor con la imagen de mariaDB en esta red bridge "redbd", para ello ejecutaremos el siguiente comando, esta red será accesible a través del puerto 3306 y tendra root como contraseña del usuario root, además de un volumen de datos persistente.

```
docker run -d --network redbd --name bbdd --env MARIADB_ROOT_PASWORD=root -p 3306:3306 -v /ignaciofernandez/ejercicio3 mariadb:latest
```

![image-20220328184424294](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220328184424294.png)

El siguiente paso que se nos pide es crear un contenedor Adminer que se pueda conectar con el contendor mysql en el navegador

Con la consulta que he hecho a dockerHub.com, he encontrado el comando para usar la imagen Adminer, lo he hecho con el comando

```
docker run --link bbdd:db -p 8080:8080 adminer
```

 ![image-20220328190348282](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220328190348282.png)

Para después establecer un servidor de bases de datos externos, en este caso de mysql

```
docker run -p 8080:8080 -e ADMINER_DEFAULT_SERVER=mysql adminer
```

![image-20220328190530495](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220328190530495.png)

Una vez hecho esto comprobamos que nos podemos conectar con el contenedor mysql a traves del navegador y el puerto 3306

![image-20220328205343059](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220328205343059-16484936252701.png)

![image-20220328205449992](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220328205449992.png)

Como se observa en ambas capturas, hemos podido acceder a Adminer, ahora vamos a crear una base de datos directamente en Adminer

Creamos la base de datos ignaciofernandez

![image-20220328205623158](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220328205623158.png)

Ahora vamos a comprobar que desde la consola del servidor se ve esta nueva base de datos, en la siguiente captura se puede ver que antes no estaba creada y posteriormente si.

![image-20220328205753418](ACTIVIDAD%20EVALUABLE%203%20-%20GIT%20Y%20DOCKER.assets/image-20220328205753418.png)

Esto lo podemos comprobar con la consulta

```sql
show databases;
```







