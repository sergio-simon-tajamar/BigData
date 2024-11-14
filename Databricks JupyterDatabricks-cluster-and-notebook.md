# Databricks-cluster-and-notebook
Configuración de la cuenta básica de DataBricks, creando poosteriormente un clúster, añadiendo varias tablas de datos y creando un notebook en el que ejecutar consultas.

Sergio Pulido Salvador , Javier Pérez Álvarez 

![](images_databricks/Scr1.jpeg)

## Registrarse en www.databricks.com
### Registrar Cuenta como personal
![](images_databricks/Scr2.jpeg)


### Validar el Correo electrónico
![](images_databricks/Scr3.jpeg)
![](images_databricks/Scr4.jpeg)


### Crear el clúster

![](images_databricks/Screenshot_1.jpg)

Seleccionar Create compute (Botón Azul).

!![](images_databricks/Screenshot_2.jpg)

Dejar por defecto Spark, cambiar el nombre al deseado.

![](images_databricks/Screenshot_3.jpg)

Esperar a que se cree, cuando esté el punto verde al lado del nombre estará listo.

![](images_databricks/Screenshot_4.jpg)

### Importación de Datos

En el apartado de inicio, seleccionar 'Create Table'
![](images_databricks/Screenshot_5.jpg)

Seleccionar donde se almacenaran los datos, y adjuntar los CSV ubicados en /sample_data . Una vez adjuntos, seleccionar 'Create Table in Notebook', que llevará a la pestaña de edición del Notebook

![](images_databricks/Screenshot_6.jpg)

### Importar Notebook para procesamiento

Databricks generará un Notebook por defecto, pero se utilizará el notebook adjunto en github. 
Para ello se descarga y se selecciona el apartado 'File > Import > Import From File', se adjunta el notebook.
![](images_databricks/Screenshot_13.jpg)
![](images_databricks/Screenshot_14.jpg)

Una vez abierto, se selecciona el cluster creado al lado de 'Share' y 'Publish'
![](images_databricks/Screenshot_8.jpg)
Ahora se selecciona 'Run All', esto ejecutará todo el notebook, que creará las vistas y tablas de la base de datos basandose en los ficheros.csv
![](images_databricks/Screenshot_7.jpg)

Una vez terminada la ejecución, se puede ver que se han creado las tablas, y se muestran los resultados de las consultas elaboradas.

![](images_databricks/Screenshot_9.jpg)
![](images_databricks/Screenshot_10.jpg)
![](images_databricks/Screenshot_11.jpg)

Se pueden personalizar las consultas dentro del Notebook. Se proporciona una consulta básica que muestra las ardillas que han presentado observaciones.
![](images_databricks/Screenshot_12.jpg)



