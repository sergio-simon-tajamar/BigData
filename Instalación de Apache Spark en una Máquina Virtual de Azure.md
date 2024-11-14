# Ejercicio de Instalación de Apache Spark en una Máquina Virtual de Azure
Tutorial de Sergio

Este ejercicio tiene como objetivo crear e instalar **Apache Spark** en una **máquina virtual (VM) independiente** en **Azure**, utilizando un sistema operativo **Linux (Ubuntu)**. A lo largo del ejercicio, se aprenderán los pasos necesarios para configurar la máquina virtual, instalar Apache Spark y ejecutarlo en un entorno local.

#### Antes de crear la MV creamos un grupo de recursos:
Inicio >> Grupo de recursos >> Crear
![image](https://github.com/user-attachments/assets/486c9953-80eb-4a88-be36-cc0cd2018a06)

Las etiquetas las dejamos vacías. Pasamos a Revisar y crear y clickamos ``crear``:
![image](https://github.com/user-attachments/assets/92222ad2-c248-4e03-b8b9-0524cb25a959)

#### Una vez tengamos nuestro grupo de recursos creado, configuramos la MV en Azure:
 ![image](https://github.com/user-attachments/assets/cea3e020-03d4-415a-ab56-334372fd0cc2)
 ![image](https://github.com/user-attachments/assets/213e940a-7275-409b-83c1-6b3da3429a8b)
 ![image](https://github.com/user-attachments/assets/16d808bb-f605-4d67-b3ad-05d8d1dc9087)
 ![image](https://github.com/user-attachments/assets/22c0960c-2e84-4da0-9861-977d9cb6b9bb)
 
El resto de configuraciones las dejamos por defecto.

### Implementación de Spark en la MV

#### 1.Conexión mediante SSH a la MV
Para ello, usamos el siguiente comando en la ``Shell`` de Windows, donde utilizaremos las claves SSH previamente descargadas.
```bash
ssh -i "<ruta_a_clavepublica>" <usuario_MV>@<ip_pública>
```
#### 2. Instalación de Java y Python
Una vez dentro de la MV instalamos ``Java``:
```bash
sudo apt update
sudo apt install openjdk-8-jdk
```
Comprobamos que se haya instalado bien:
```bash
java -version 
```
Si queremos usar ``PySpark``, debemos tener instalado ``Python``:

Primero comprobamos si está instalado
```bash
python3 --version
```
Si no sale nada, no está instalado, entonces ejecutamos el siguiente comando:
```bash
sudo apt install python3
```
#### 3. Descarga del comprimido de ``Spark``
Para descargar spark, navegamos a la [página de Spark](https://spark.apache.org/downloads.html) para obtener el enlace de la descarga .tgz 

Una vez encontrado el enlace, ejecutamos este comando:
```bash
wget <enlace>
```
Nosotros en este caso hemos usado el siguiente:
```bash
wget https://downloads.apache.org/spark/spark-3.5.3/spark-3.5.3-bin-hadoop3.tgz
```
#### 4. Descomprimir archivo ``.tgz`` y reubicación.
Una vez descargado, descomprimimos el archivo y comprobamos que se haya ejecutado correctamente:
```bash
tar -xvf spark-3.5.3-bin-hadoop3.tgz
ls
```
Ahora, movemos los archivos a la carpeta /opt/spark y lo comprobamos:
```bash
 sudo mv spark-3.5.3-bin-hadoop3 /opt/spark
 ls /opt/spark
```
#### 5. Configuración de las variables de entorno.
Después, editamos el archivo ~/.bashrc para añadir variables de entorno:
```bash
nano ~/.bashrc
```
Escribimos el siguiente contenido:
```bash
export SPARK_HOME=/opt/spark

export PATH=$SPARK_HOME/bin:$PATH

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

export PATH=$JAVA_HOME/bin:$PATH
 
```
Guardamos y salimos del editor nano.
Para hacer efectivos estos cambios, ejecutamos el siguiente comando:
```bash
source ~/.bashrc
```
#### 6. Comprobación de la instalación.
Podemos comprobar que ``PySpark`` está siendo ejecutado de la forma esperada con el comando:
```bash
pyspark
```
A su vez, podemos comprobar que Scala se está ejecutando el siguiente comando: 
```bash
spark-shell
```

#### 7. Limpieza de recursos.
Para finalizar, paramos y eliminamos la MV:
![image](https://github.com/user-attachments/assets/9998f7f9-8e3d-4423-a45a-5494032c7816)
![image](https://github.com/user-attachments/assets/c67edb8d-e06b-4fa9-8d75-ceb0ad3ff8e5)


