## Esquema para el ejercicio
![Imagen](imagenes/esquema-ejercicio5.PNG)

### Crear la red

```
docker network create net-wp
```

### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias

```
docker pull mysql:8
```

```
docker run -d --name mi_mysql --network net-wp -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=mi_base_de_datos -e MYSQL_USER=usuario -e MYSQL_PASSWORD=contraseña mysql:8
```

### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias

```
docker pull wordpress
```

```
docker run -d --name wordpress --network net-wp -e WORDPRESS_DB_HOST=mi_mysql:3306 -e WORDPRESS_DB_NAME=mi_base_de_datos -e WORDPRESS_DB_USER=usuario -e WORDPRESS_DB_PASSWORD=contraseña -p 8080:80 wordpress
```

De acuerdo con el trabajo realizado, en la el esquema de ejercicio el puerto a es **8080**

Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.

![Imagen](imagenes/wordpressConf1.png)

![Imagen](imagenes/wordpressConf2.png)

![Imagen](imagenes/wordpressConf3.png)

Desde el panel de admin: cambiar el tema y crear una nueva publicación.

Cambio del tema

![Imagen](imagenes/temaBefore.png)

![Imagen](imagenes/temaAfter.png)

Creacion de la publicacion

![Imagen](imagenes/publicacion.png)

Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

![Imagen](imagenes/publicacionvisual.png)

### Eliminar el contenedor wordpress

```
docker rm -f wordpress
```

### Crear nuevamente el contenedor wordpress

```
docker run -d --name mi_mysql --network net-wp -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=mi_base_de_datos -e MYSQL_USER=usuario -e MYSQL_PASSWORD=contraseña mysql:8
```

Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

![Imagen](imagenes/wordpressRenovada.png)

### ¿Qué ha sucedido, qué puede observar?

Podemos observar que la pagina web a mantenido la configuracion que hemos creado, el estilo y la publicacion nueva, esto puede ser debido a que esta informacion se guardo en el servidor mi_mysql y el contenedor de wordpress solamente seria la interfaz en la que se muestra lo del otro servidor
