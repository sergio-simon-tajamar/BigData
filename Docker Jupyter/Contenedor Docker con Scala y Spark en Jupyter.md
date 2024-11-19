# Guía para Iniciar el Contenedor Docker con Scala y Spark en Jupyter

![imagen](https://github.com/user-attachments/assets/19f80df9-e7a1-4e84-80bb-35ce124d1f30)

## Requisitos previos
1. Tener Docker y Docker Compose instalados
Docker: Asegúrate de tener instalado Docker en tu máquina. Puedes verificarlo ejecutando:

    ```bash
    docker --version
    ```
    Si no está instalado, sigue las instrucciones de instalación en la  [documentación oficial de Docker](https://docs.docker.com/engine/install/).

    Docker Compose: Necesitas Docker Compose para orquestar los servicios. Verifica la instalación con:

    ```bash
    docker-compose --version
    ```
    Si no está instalado, consulta la [documentación de Docker Compose](https://docs.docker.com/compose/install/).

2. Repositorio Base
Debes contar con un proyecto Docker existente que ya tenga una configuración inicial de Spark o el repositorio base leo-narvaez/docker-spark.

    Clona el repositorio si aún no lo tienes:
    ```bash
    git clone https://github.com/leo-narvaez/docker-spark-jupyter.git
    ```
    ```bash
    cd docker-spark-jupyter
    ```

## Paso 1: Iniciar el contenedor y acceder a Jupyter
Tener docker instalado y en ejecución.

Inicia el contenedor utilizando **Docker Compose**:

```bash
docker-compose up --build
```

Una vez que el contenedor esté en funcionamiento, abre tu navegador y accede a Jupyter Notebook en http://localhost:8888.

El token de acceso o la password la podemos encontrar en los logs.

![docker_spark_logs](https://github.com/user-attachments/assets/c307bbe6-60d9-43dd-b32d-75424bbb3a94)

## Paso 2: Crear un notebook de Scala

Seleccionar el kernel de Scala:

Al abrir Jupyter, deberías poder ver un botón que dice `New` en la parte superior derecha. Al hacer clic allí, verás una opción llamada `Scala`, que corresponde al kernel de Scala instalado a través de Apache Toree.

![Scala_button](https://github.com/user-attachments/assets/eced4b8d-7830-4324-8463-32c1bf1f86d9)

Crear un nuevo notebook con el kernel de Scala:

Selecciona Scala como el kernel para el notebook y se abrirá una nueva pestaña donde podrás comenzar a escribir código en Scala.

# Ejemplo con Scala y Spark
Vamos a crear un DataFrame más complejo, simular algunas operaciones de transformación y luego ejecutar consultas SQL sobre este DataFrame.

Copiaremos y ejecutamos el siguien código:

Ejemplo en `Scala`:
```scala
import org.apache.spark.sql.SparkSession
import org.apache.spark.sql.functions._

// Crear una sesión de Spark
val spark = SparkSession.builder
  .appName("Ejemplo avanzado en Scala con Spark")
  .master("spark://spark-jupyter:7077") // Asegúrate de que el master es el correcto
  .getOrCreate()

// Datos más complejos
val data = Seq(
  ("John", "Doe", 30, "M", "New York"),
  ("Alice", "Smith", 25, "F", "Los Angeles"),
  ("Bob", "Brown", 28, "M", "Chicago"),
  ("Eve", "Davis", 22, "F", "Miami"),
  ("Charlie", "Wilson", 35, "M", "San Francisco")
)

// Crear un DataFrame con columnas más complejas
val df = spark.createDataFrame(data).toDF("first_name", "last_name", "age", "gender", "city")

// Mostrar el DataFrame original
df.show()

// Registrar el DataFrame como una vista temporal para SQL
df.createOrReplaceTempView("people")

// Realizar una consulta SQL avanzada para filtrar, agrupar y ordenar
val result = spark.sql("""
  SELECT city, gender, COUNT(*) as count, AVG(age) as avg_age
  FROM people
  WHERE age > 25
  GROUP BY city, gender
  ORDER BY avg_age DESC
""")

// Mostrar los resultados
result.show()
```

### Explicación:
**DataFrame:** Creamos un DataFrame con más columnas (nombre, apellido, edad, género, ciudad).

**Transformaciones y Consultas:** Usamos `spark.sql()` para realizar una consulta SQL que filtra personas mayores de 25 años, agrupa los resultados por ciudad y género, y luego ordena los resultados por la edad promedio en orden descendente.

**Salida:** El DataFrame resultante contiene las ciudades y géneros con el número de personas y la edad promedio, ordenado por la edad promedio.

![results](https://github.com/user-attachments/assets/ee3c4ae1-5fa3-4228-a2d9-2d8e0a1d6329)

# Ejemplo equivalente con PySpark:
El equivalente en PySpark sería muy similar, pero con la sintaxis de Python.
A continuación te muestro cómo hacer lo mismo.

Abrimos un nuevo notebook y seleccionamos el kernel de Python:

![kernel_python](https://github.com/user-attachments/assets/bdedd014-3aec-48cf-bdfe-7840ee1ae29a)

Copiaremos y ejecutamos el siguiente código:

Ejemplo en `PySpark`:
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col, avg, count

# Crear la sesión de Spark
spark = SparkSession.builder \
    .appName("Ejemplo avanzado en PySpark") \
    .master("spark://spark-jupyter:7077") \
    .getOrCreate()

# Datos más complejos
data = [
    ("John", "Doe", 30, "M", "New York"),
    ("Alice", "Smith", 25, "F", "Los Angeles"),
    ("Bob", "Brown", 28, "M", "Chicago"),
    ("Eve", "Davis", 22, "F", "Miami"),
    ("Charlie", "Wilson", 35, "M", "San Francisco")
]

# Crear un DataFrame con columnas más complejas
df = spark.createDataFrame(data, ["first_name", "last_name", "age", "gender", "city"])

# Mostrar el DataFrame original
df.show()

# Registrar el DataFrame como una vista temporal para SQL
df.createOrReplaceTempView("people")

# Realizar una consulta SQL avanzada para filtrar, agrupar y ordenar
result = spark.sql("""
  SELECT city, gender, COUNT(*) as count, AVG(age) as avg_age
  FROM people
  WHERE age > 25
  GROUP BY city, gender
  ORDER BY avg_age DESC
""")

# Mostrar los resultados
result.show()
```
### Explicación:
**Crear DataFrame en PySpark:** Usamos spark.createDataFrame() para crear el DataFrame a partir de una lista de tuplas.

**Registrar la vista temporal:** Al igual que en el ejemplo de Scala, registramos el DataFrame como una vista temporal llamada people.
Consulta SQL avanzada: Realizamos una consulta SQL usando `spark.sql()` para filtrar, agrupar y ordenar los resultados.
Mostrar los resultados: Mostramos el resultado con el método `show()`.

Este proceso tardará unos minutos, tras unos logs veremos el resultado.
