# Tutorial Completo: Iniciar Apache Spark en Azure HDInsight

Azure HDInsight es un servicio gestionado que permite trabajar con herramientas del ecosistema Hadoop, como Apache Spark. Este tutorial te guiará paso a paso para configurar y usar Spark en HDInsight, desde la creación del clúster hasta la ejecución de trabajos Spark.

---

## 1 - Crear un clúster HDInsight con Spark

### 1.1 - Crear un recurso HDInsight en el portal de Azure

Acceder al portal de [Azure](https://portal.azure.com).

Hacer _click_ en **Crear un recurso**:

![image](https://github.com/user-attachments/assets/ccb1ae51-fd57-434a-b73a-7a59d89bd6fb)

Buscar **HDInsight** en la barra de búsqueda:

![image](https://github.com/user-attachments/assets/afdc8abf-6e62-46cf-9f85-e592b6994389)

Seleccionar **Azure HDInsight** y hacer _click_ en **Crear** >> **Azure HDInsight**:

![image](https://github.com/user-attachments/assets/31f1b753-31ba-4713-a738-965cb3b8d284)

### 1.2 - Configurar el clúster

**Datos básicos**:

- **Nombre del clúster**: Debe ser un nombre único para identificar el clúster.
- **Suscripción**: Seleccionar la suscripción de Azure.
- **Grupo de recursos**: Crear un grupo de recursos o seleccionar uno existente.
- **Región**: Seleccionar la región, en este caso, Italy North.

![image](https://github.com/user-attachments/assets/72738e01-687d-45b6-a2cc-b68b97ca2ea5)

![image](https://github.com/user-attachments/assets/3aa0fb33-4bcb-4771-9a60-9132d8030ce0)

- **Tipo de clúster**: Seleccionar **Spark**, y elegir la última versión disponible:

![image](https://github.com/user-attachments/assets/0ffd8c87-4540-47e2-a168-ec6feac77f7e)

![image](https://github.com/user-attachments/assets/f81088a7-d773-47bb-89dc-cd8c85dc9787)

![image](https://github.com/user-attachments/assets/fe6082a1-60e9-4948-a4a2-a01f1f3d06ca)

- **Credenciales del clúster**: Crear unas credenciales de acceso para el clúster. Después, hacer _click_ en **Siguiente: Almacenamiento>>**:

![image](https://github.com/user-attachments/assets/10a9b76a-5c3a-4da8-bf7b-e8e478e13b17)

**Almacenamiento**:

   - **Tipo de almacenamiento principal**: **Azure Storage**.
   - **Cuenta de almacenamiento principal**: _Crear nuevo_ >> Introducir un nombre válido para la nueva cuenta de almacenamiento, y hacer _click_ en **De acuerdo**.

   ![image](https://github.com/user-attachments/assets/683c468c-ae1a-4fe9-ba76-87981b6c40e1)

   ![image](https://github.com/user-attachments/assets/c0960219-3a3b-43bf-8db5-b1898f625c48)

**Configuración y precios**:

   - En **Nodo Trabajador**, cambiar el número de nodos de `4` a `1`, para evitar el siguiente error:

   ![image](https://github.com/user-attachments/assets/142556a7-6eb8-437e-940e-1a71b078cbef)
     
Dejar el resto de las configuraciones como están y hacer _click_ en **Revisar y crear**.

Esperar a que finalice la implementación (esto puede tardar entre 15 y 30 minutos).

![image](https://github.com/user-attachments/assets/cc9e36bf-f46a-4f51-9614-2fd6aab9712b)

---

## 2 - Conectar al clúster

Entrar al recurso del clúster, y buscar la sección de _Configuración_ >> _SSH e inicio de sesión del clúster_. Seleccionar el **nombre del host** en el desplegable, y copiar el comando que aparece debajo:

```bash
ssh <usuario>@<nombre_del_cluster>-ssh.azurehdinsight.net
```

![image](https://github.com/user-attachments/assets/8b642776-9421-4a93-970f-57fe716dc92d)

Conectarse a una Cloud Shell.

![image](https://github.com/user-attachments/assets/dc48336b-45c5-43d8-a21b-12325ecd18f0)

Introducir el comando que se copió en el paso anterior e indicar la contraseña cuando sea solicitada:

![image](https://github.com/user-attachments/assets/5e83c2a1-9208-4581-958e-db9ec88e18f9)

---

## 3 - Usar Spark en HDInsight

### 3.1 - Iniciar una sesión interactiva con Spark

Una vez conectado al clúster:

-	Ejecutar el siguiente comando para iniciar el Shell interactivo de Spark en **Scala**:

```bash
spark-shell
```

> Para salir de Spark (Scala):
> ```bash
> :quit
> ```

![image](https://github.com/user-attachments/assets/9ca5d279-3cd0-4b6b-b87a-51df12e46425)

- Para trabajar con Python (**PySpark**):

```scala
pyspark
```

> Para salir de PySpark, hay dos opciones, la combinación de teclas `CTRL` + `D`, o también:
> ```python
> exit()
> ```

![image](https://github.com/user-attachments/assets/438aea76-1652-442b-ac0f-aa688b843078)

### 3.2 - Ejecutar un ejemplo en Spark

**Ejemplo en Scala:**

Dentro del Shell de Spark, ejecutar este código para crear y mostrar un DataFrame:

```scala
val data = Seq(("Juan", 30), ("Josefa", 25), ("Chema", 35))
val df = data.toDF("Nombre", "Edad")

// Mostrar el contenido del DataFrame
df.show()
```

**Ejemplo en Python (PySpark):**

Si se está utilizando PySpark, el código sería el siguiente:

```python
data = [("Juan", 30), ("Josefa", 25), ("Chema", 35)]
columns = ["Nombre", "Edad"]

df = spark.createDataFrame(data, columns)

# Mostrar el contenido del DataFrame
df.show()
```

### 3.3 - Subir y ejecutar trabajos Spark

En la **máquina local**, crear un Script PySpark (`job.py`):

```python
from pyspark.sql import SparkSession

# Crear una sesión de Spark
spark = SparkSession.builder.appName("EjemploSimple").getOrCreate()

# Crear un DataFrame de ejemplo
data = [("Juan", 30), ("Josefa", 25), ("Chema", 35)]
columns = ["Nombre", "Edad"]

df = spark.createDataFrame(data, columns)

# Mostrar los datos
df.show()

# Finalizar la sesión
spark.stop()
```

En una **terminal local**, se puede usar el siguiente comando para copiar directamente el archivo al clúster usando scp:

```bash
scp </ruta/local/del/archivo> <usuario_de_azure>@<nombre_del_cluster>-ssh.azurehdinsight.net:/home/<usuario_de_azure>/
```

![image](https://github.com/user-attachments/assets/732c2e1d-f1be-4467-b90e-b9c222dd5fc6)

De nuevo en la **Cloud Shell** de Azure, se puede comprobar también que el archivo se ha subido correctamente:

```bash
ls -l
```

![image](https://github.com/user-attachments/assets/a0524a69-6849-4622-a1c5-229818c5f24c)

Para ejecutar el script y observar los resultados:

```bash
spark-submit job.py
```

Observar los resultados directamente en la terminal.

---

## 4 (Opcional) - Usar Jupyter Notebooks con HDInsight

### 4.1 - Ir al Dashboard del clúster

En el portal de Azure, acceder al recurso HDInsight. En la sección de _Información general_, hacer _click_ en _Cuaderno de Jupyter_.

![image](https://github.com/user-attachments/assets/645d8318-6a2e-474b-aee8-e62b097be88e)

### 4.2 - Iniciar sesión

Utilizar las credenciales que se configuraron al crear el clúster.

![image](https://github.com/user-attachments/assets/8ef382de-7395-4fae-8057-f37fdf724352)

### 4.3 - Crear un nuevo notebook

En la página principal de Jupyter, hacer _click_ en **New** y seleccionar el kernel deseado (PySpark para Python y Spark para Scala). En este ejemplo, se utilizará **PySpark**, para poder usar el mismo código que en el ejemplo del paso `3.3`:

![image](https://github.com/user-attachments/assets/b653f028-1bbb-4752-b9ef-1b237a6df9f9)

![image](https://github.com/user-attachments/assets/925d3ca4-f870-45ee-bf0e-bf0ddbba8567)

### 4.4 - Escribir el código

Copiar el ejemplo del paso `3.3`, y ejecutar la celda (haciendo click en **Run**) para ver los resultados:

```python
from pyspark.sql import SparkSession

# Crear una sesión de Spark
spark = SparkSession.builder.appName("EjemploSimple").getOrCreate()

# Crear un DataFrame de ejemplo
data = [("Juan", 30), ("Josefa", 25), ("Chema", 35)]
columns = ["Nombre", "Edad"]

df = spark.createDataFrame(data, columns)

# Mostrar los datos
df.show()

# Finalizar la sesión
spark.stop()
```

![image](https://github.com/user-attachments/assets/b653fd76-81d9-4157-af2e-0a8d9826b968)

Esperar a que termine el proceso:

![image](https://github.com/user-attachments/assets/1b35cb75-3e65-4fb5-a9e0-8aad1066acc3)

Comprobar los resultados en el propio cuaderno.

### 4.5 - Guardar el notebook

Se puede guardar el notebook, haciendo _click_ en _File_ >> _Save as_, para documentar procesos o reutilizar el código.

![image](https://github.com/user-attachments/assets/880db44e-4600-4118-9f5b-8c8a408fd7d9)

![image](https://github.com/user-attachments/assets/5c930722-256a-4669-8af3-4109299734b7)

---

## 5 - Detener el clúster

HDInsight cobra mientras el clúster está activo, incluso si no se está usando. La única forma de detenerlo es eliminarlo. En este caso, vamos a eliminar el grupo de recursos que se creó al principio, para evitar costes adicionales.

Para detener el clúster, desde el portal de Azure:

Acceder al grupo de recursos.

![image](https://github.com/user-attachments/assets/fa09ceb8-5e28-46d7-b2a1-cb4d33c86670)

![image](https://github.com/user-attachments/assets/0866369e-d119-4b08-8e71-5d36efaa117e)

En el menú superior, hacer _click_ en _Eliminar grupo de recursos_.

![image](https://github.com/user-attachments/assets/4a5c8049-7073-4738-a2ca-90427fd0485a)

![image](https://github.com/user-attachments/assets/1d91a46d-9082-46ae-b0a1-419ba263e9e5)

![image](https://github.com/user-attachments/assets/a1cbb30c-81f1-4639-b54a-28c65ac9641d)

Por último, esperar a que se elimine por completo el grupo de recursos que incluye el clúster.

![image](https://github.com/user-attachments/assets/dd457007-2e04-4978-80fc-95b6a9d4e977)
