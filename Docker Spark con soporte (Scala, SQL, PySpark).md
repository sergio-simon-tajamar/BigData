## Docker Spark con soporte (Scala, SQL, PySpark)

![docker-spark](https://github.com/user-attachments/assets/2666f302-7f84-496b-9331-e13fa8233955)
Este repositorio proporciona un contenedor Docker preconfigurado para ejecutar **Apache Spark** con soporte para múltiples lenguajes de programación: **Scala**, **PySpark** y **SQL**. Este entorno es ideal para ejecutar tareas de procesamiento de datos a gran escala, permitiendo a los usuarios aprovechar las potentes capacidades de Spark en un entorno aislado y reproducible.

- **Apache Spark**: Framework de procesamiento de datos distribuido y de código abierto.
- **Scala**: Lenguaje funcional y orientado a objetos compatible con Spark.
- **PySpark**: Interfaz de Python para Spark, permitiendo escribir código en Python para el procesamiento distribuido.
- **SQL**: Soporte completo para ejecutar consultas SQL sobre grandes volúmenes de datos.
---
### Requisitos previos

1. **Docker**: Debes tener Docker instalado en tu máquina. Si no lo tienes, puedes seguir la [guía de instalación oficial de Docker](https://docs.docker.com/get-docker/).
   
2. **Red interna de Docker**: Asegúrate de poder crear redes internas en Docker, ya que es necesario para configurar la red entre contenedores (en este caso, para el contenedor `spark-master`).

3. **Conexión a Internet**: Asegúrate de tener acceso a Internet para descargar las imágenes de Docker necesarias.

4. **Espacio en disco**: Ten suficiente espacio en disco para ejecutar contenedores, ya que los contenedores de Spark pueden consumir varios gigabytes dependiendo de la carga de trabajo.


### ⚠️ Sugerencia
> Es recomendable apagar y eliminar contenedores o imágenes que ya no necesites para evitar conflictos o el uso innecesario de recursos del sistema. Aquí tienes algunos comandos útiles para gestionarlos:
> 
> - **Ver contenedores en ejecución:**
>   ```bash
>   docker ps
>   ```
> 
> - **Detener un contenedor:**
>   Si necesitas detener un contenedor en ejecución, puedes hacerlo con:
>   ```bash
>   docker stop <nombre_contenedor>
>   ```
> 
> - **Eliminar un contenedor detenido:**
>   Después de detener un contenedor, puedes eliminarlo para liberar recursos:
>   ```bash
>   docker rm <nombre_contenedor>
>   ```
> 
> - **Ver imágenes descargadas:**
>   Para ver las imágenes descargadas en tu sistema:
>   ```bash
>   docker images
>   ```
> 
> - **Eliminar una imagen no utilizada:**
>   Si ya no necesitas una imagen, puedes eliminarla para liberar espacio en disco:
>   ```bash
>   docker rmi <nombre_imagen>
>   ```
> 
> - **Eliminar contenedores e imágenes no utilizados de forma automática:**
>   Para eliminar todos los contenedores detenidos y las imágenes no utilizadas, puedes usar:
>   ```bash
>   docker system prune
>   ```
>   **Nota**: Este comando eliminará todo lo que no esté en uso, incluidos los contenedores detenidos, las redes no utilizadas y las imágenes no etiquetadas.
> 
> Realizar estas tareas de mantenimiento regularmente puede ayudarte a evitar conflictos o problemas de rendimiento en tu sistema.

## Instalación de Apache Spark

1. **Crear una red de Docker**
- Crearemos una red para que los contenedores se comuniquen.
   ```bash
   docker network create spark-network
   ```
- Confirma que la red se ha creado correctamente.
   ```bash
   docker network ls
   ```
  Esto mostrará una lista de todas las redes disponibles en Docker. Deberías ver `spark-network` en la lista.
2. **Ejecutar el contenedor `spark-master:`**
   ```bash
   docker run -d --name spark-master --network spark-network -p 8080:8080 -p 7077:7077 -e SPARK_MODE=master -e SPARK_MASTER_HOST=spark-master bitnami/spark:3.2.1
   ```
   Si entreamos al navegador con la ruta: `http://localhost:8080`, veremos spark desplegado:
  ![image](https://github.com/user-attachments/assets/1c5463ba-e3d9-4c02-8868-aa48e1761150)
>**Nota:** Si te da error en el puerto `8080`, asegurate de que se encuentre disponible, puede probar a modificarlo por `8081` o similares, si después de intentar modificar el puerto y no funciona, borra el puerto `8080:8080` en el comando anterior.

   Ahora que tenemos instalado correctamente ya podemos usar `pyspark`, `scala` y `sql`, para ello:
1. **Acceder al contenedor con una terminal interactiva:**
   ```bash
   docker exec -it spark-master /bin/bash
   ```
2. **Iniciar PySpark:**
   ```bash
   pyspark
   ```
   Ahora tienes acceso a `pyspark`. Si quieres salir de la terminal pulsa: ctrl + d.
3. **Iniciar Spark con Scala:**
   ```bash
   spark-shell
   ```
   Ahora tienes acceso a `scala`. Si quieres salir de la terminal pulsa: ctrl + d.
4. **Ejecutar SQL en Spark:**
   ```bash
   /opt/bitnami/spark/bin/spark-sql --master spark://spark-master:7077
   ```
   Ahora tienes acceso a `spark-sql`. Si quieres salir de la terminal pulsa: ctrl + d.
5. **Ejecutar JAVA:**
   - Verificamos la versión de java.
   ```bash
   java -version
   ```
   - Ahora vamos a probar java con un `HelloWord`
   ```bash
   echo 'public class HelloWorld { public static void main(String[] args) { System.out.println("Hello, Spark and Java!"); } }' > HelloWorld.java 
   ```
   - Compilamos el archivo `HelloWorld`:
   ```bash
   javac HelloWorld.java
   ```
   - Ejecutamos el programa:
   ```bash
   java HelloWorld
   ```
   Ahora ya tendremos disponible java para la ejecución de nuestros programas, para salir de la terminal pulsa: ctrl + d.
## Finalizar
7. **Detener el contenedor cuando hayas terminado:**
- Detener el contenedor:
   ```bash
   docker stop spark-master
   ```
- Eliminar el contenedor:
   ```bash
   docker rm spark-master
   ```
---
## Conclusión

Este repositorio proporciona una configuración fácil y rápida para ejecutar **Apache Spark** en un contenedor Docker, soportando lenguajes como **Scala**, **PySpark** y **SQL**. Con la configuración adecuada, puedes aprovechar el poder del procesamiento distribuido de Spark en un entorno aislado. Recuerda gestionar los contenedores y las imágenes para mantener tu sistema limpio y eficiente.
