# **Instalación de Spark en una VM (Local)** 
Tutorial de Hugo, Pablo, Samu, Dani y Miguel

## Iso
Puedes descargar la ISO desde el archivo Iso Enlace accediendo al enlace y descargando el iso del onedrive
### Paso 1: Clonar repositorio
``` bash
git clone http://github.com/Mikemaranon/linux-cosas.git
```
### Paso 2: Dar permisos de ejecución
``` bash
sudo chmod +x installSpark.sh
sudo chmod +x sour.sh
```
### Paso 3: Ejecutar source en caso de no tener spark
``` bash
source ~/.bashrc
```
###  Paso 4: Iniciar spark
``` bash
# scala
spark-shell
# PySpark
pyspark
# SQL
spark-sql
```
---------------------------------------------

## Paso 1: Instalar Java en VM
``` bash
# Actualizamos la Vm a la última versión
sudo apt update
# Instalamos el java openjdk-8-jdk
sudo apt install openjdk-8-jdk
# Comprobamos la versión de Java para comprobar su correcta instalación
java -version
``` 
## Paso 2:Instalar Python3 en VM
``` bash
# Instalamos Python3 en la VM
sudo apt install python3
# Comprobamos la versión de python3
python3 -version
``` 
## Paso 3: Instalar Spark
``` bash
# Nos conectamos a internet para conseguir el .tar que contiene spark
wget https://downloads.apache.org/spark/spark-3.5.3/spark-3.5.3-bin-hadoop3.tgz
# Descomprimimos el tar 
tar -xvf spark-3.5.3-bin-hadoop3.tgz
# Movemos el contenido del tar a /opt/spark
sudo mv spark-3.5.3-bin-hadoop3 /opt/spark
``` 
## Paso 4: Añadir variables de entorno al archivo .bashrc
``` bash
# Abrimos el editor de texto para editar el archivo .bashrc (Recomendable hacerlo desde home)
sudo nano .bashrc 
```
Añadir variables de entorno al archivo:
``` bash
export SPARK_HOME=/opt/spark
export PATH=$SPARK_HOME/bin:$PATH
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
``` 
## Paso 5: Iniciar Spark
``` bash
source ~/.bashrc
spark-shell # Scala
pyspark # pyspark
spark-sql # SQL
```
------------------------------------------------------
## Jupyter Notebook

### Paso 1: Instalar Jupyter
``` bash
sudo apt install python3-pip
pip install notebook

sudo apt install jupyter-core
```
### Paso 2: Instalar pyspark
``` bash
pip install findspark
``` 
### Paso 3: Configurar Adaptador VM
Tener un solo adaptador de red en la VM y que sea adaptador puente

### Paso 4: Iniciar Jupyter
Reiniciar la VM antes de jupyter notebook
``` bash
jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser # Cambiar el puerto segun la disponibilidad
```
Tras iniciar Jupyter Notebook, acceder al enlace que te devuelve, sera algo asi:
``` bash
http://tuip:9999/tree?token=b915a2fa08ebb6578ecfc31420f8bc754325f08490173570
```

### Paso 5: Pagina Web
Iniciar sesión con el token, en mi ejemplo es: b915a2fa08ebb6578ecfc31420f8bc754325f08490173570
![image](https://github.com/user-attachments/assets/ad58c709-a7db-4a7d-8afa-bf0b767077a0)

### Paso 6: EJEMPLO
``` bash
!pip install pandas
```
``` bash
import pandas as pd
 
# Crear un diccionario con los datos
data = {
    'Nombre': ['Ana', 'Luis', 'Carlos', 'María', 'Elena'],
    'Edad': [23, 34, 45, 29, 35],
    'Ciudad': ['Madrid', 'Barcelona', 'Sevilla', 'Valencia', 'Bilbao'],
    'Puntuación': [85, 90, 78, 92, 88]
}
 
# Crear el DataFrame
df = pd.DataFrame(data)
 
# Mostrar el DataFrame
df
```
![image](https://github.com/user-attachments/assets/c3766876-732c-4c80-b9d1-f0c9edc2948e)

------------------------------------------------------

### OPCIONAL. Para trabajar con redes privadas

## Paso 1: Editar archivo 00-installer-config.yaml
``` bash
# Abrimos el editor de texto para editar el archivo 00-installer-config.yaml
sudo nano /etc/netplan/00-installer-config.yaml
```
## Paso 2: Escribrir dentro del 00-installer-config.yaml:
Configuramos el contenido de 00-installer-config.yaml
``` bash
network:
  ethernets:
     enp0s3:
         addresses:
             -192.168.56.18/24
     enp0s8:
        dhcp4: true
  version: 2
  ```
