# ExamenSistemas

Carlos Herrera Martín



## Introducción

A continuación describiré el proceso que he seguido al tratar de desplegar mi aplicación web en contenedores de docker, que consiste en generar contenedores que tienen imágenes servidores los cuales contendrán la aplicación.

## Requisitos previos:

Deberemos tener instalado docker engine para poderrealizar esta práctica así como una aplicación de java en formato .war y los documentos html necesarios.

## Docker compose

Debemos crear un documento docker-compose.yml que definirá las imágenes que queremos implementar, las variables de configuración de estas y los archivos que queremos desplegar en ellas desde nuestra máquina.

Este archivo deberá contener varias etiquetas como por ejemplo:
- version: aquí pondremos la versión de docker con que trabajamos.
- services: a continuación de esta etiqueta definiremos las imágenes a utilizar.
- db: hace referencia a la imágen que usaremos como base de datos.
- image: nombre de la imágen y versión de forma opcional, por defecto tomará el valor de :latest que se referirá a la última versión.
- volumes: Aquí definiremos los archivos a desplegar en el contenedor, en caso de una imágen de base de datos pondremos la ruta en que queremos que almacene los datos.
- environment: Dentro de esta etiqueta definiremos las variables del servidor y sus valor como pueden ser los usuarios y contraseñas.
- ports: A continuación de esto definiremos el puerto en que se desplegará en contenedor, si ponemos dos puntos seguidos de otro puerto este hará referencia al mismo puerto de nuestra  máquina lo que nos permitirá interactuar con el contenedor desde fuera de docker.

Para crear este archivo ya que se está realizando desde una máquina con ubuntu me he ubicado en la carpeta dónde se encuentran mis documentos para el frontend y mi archivo .war y desde allí mediante el comando ``nano docker-compose.yml`` creo y edito el archivo.

Una vez finalizado el documento debe quedar algo similar a esto:

![dockercompose](https://user-images.githubusercontent.com/91744455/172451262-4153ee1b-2f06-48d4-9a1c-637916d73a08.png)

En este caso hemos elegido como servidor de base de datos mysql, como servidor de aplicación apache tomcat y como servidor web nginx.

A continuación para poner en marcha nuestro contenedor debemos de utilizar el comando ``docker compose up -d ``  desde el terminal ubicados en la carpeta en que se encuentra el archivo docker-compose.yml.


Al ejecutar el comando me arroja el siguiente error que no se como solucionar:


![error1](https://user-images.githubusercontent.com/91744455/172452513-872eb24c-a932-47dd-93da-4ff391df6852.png)


Obviando el error los siguiente que deberiamos hacer es subir la imágen a docker hub que se trata de un repositorio en que e almacenan las imágenes que se pueden correr en docker.

Para ello debermos iniciar sesión desde el terminal usando el comando ``docker login`` y se nos pedirá nuestro usuario y contraseña de docker hub.

Ahora deberíamos crear una variante de nuestra imágen siguiendo la nomenclatura que requiere docker hub, por lo que deberiamos ejecutar el comando :
``docker tag ombre_de_usuario/nombre_del_repositorio:etiqueta``   y una vez creada la imágen con el nombre adecuado deberíamos utilizar el comando ``docker push nombre_del_repositorio:etiqueta``.

Así ya tendríamos la imágen en nuestro repositorio de docker hub.

## Conclusiones

Docker es una tecnología que puede resultar muy útil para poder utilizar ciertos programas sin tener que montar un sistema operativo completo, pero mi experiencia tras dedicar muchísimas hora ha sido muy frustrante al no poder hacer funcionar los contenedores que quería, aunque cabe decir que durante el proceso he apendido mucho acerca del funcionamiento de esta tecnolog
