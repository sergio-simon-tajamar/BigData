# Databricks-cluster-and-notebook
Tutorial de Sergio Pulido Salvador , Javier Pérez Álvarez 

Configuración de la cuenta básica de DataBricks, creando poosteriormente un clúster, añadiendo varias tablas de datos y creando un notebook en el que ejecutar consultas.

![image](https://github.com/user-attachments/assets/41487d2e-e8a6-43ed-baf7-e2d84b4eff3a)


## Registrarse en www.databricks.com
### Registrar Cuenta como personal
![image](https://github.com/user-attachments/assets/c2e884f4-b4a4-41e5-97ab-ed7593006bc8)



### Validar el Correo electrónico
![image](https://github.com/user-attachments/assets/a49cc8fc-401c-4471-9973-ae40a840fa11)



### Crear el clúster

![image](https://github.com/user-attachments/assets/3887a375-be0a-49f5-8366-7d7405097416)


Seleccionar Create compute (Botón Azul).

![Screenshot_2](https://github.com/user-attachments/assets/810b33c2-e78b-4e5c-93a1-59edce75342d)


Dejar por defecto Spark, cambiar el nombre al deseado.

![Screenshot_3](https://github.com/user-attachments/assets/1b7b042a-18b7-4617-87e5-970ee3869ca7)

Esperar a que se cree, cuando esté el punto verde al lado del nombre estará listo.

![Screenshot_4](https://github.com/user-attachments/assets/b5d8c040-b9e0-4534-8063-7421b2dd1e3b)

### Importación de Datos

En el apartado de inicio, seleccionar 'Create Table'
![Screenshot_5](https://github.com/user-attachments/assets/df18f7a3-17dd-4cd5-9853-4917de1c0849)

Seleccionar donde se almacenaran los datos, y adjuntar los CSV ubicados en /sample_data . Una vez adjuntos, seleccionar 'Create Table in Notebook', que llevará a la pestaña de edición del Notebook

![Screenshot_6](https://github.com/user-attachments/assets/b0a4c3dc-921f-4ab6-a640-920dd8f4fbf2)

### Importar Notebook para procesamiento

Databricks generará un Notebook por defecto, pero se utilizará el notebook adjunto en github. 
Para ello se descarga y se selecciona el apartado 'File > Import > Import From File', se adjunta el notebook.
![](images_databricks/Screenshot_13.jpg)
![](images_databricks/Screenshot_14.jpg)

Una vez abierto, se selecciona el cluster creado al lado de 'Share' y 'Publish'
![Screenshot_8](https://github.com/user-attachments/assets/77938b41-ef26-4c76-ae3f-dee41980396d)

Ahora se selecciona 'Run All', esto ejecutará todo el notebook, que creará las vistas y tablas de la base de datos basandose en los ficheros.csv
![Screenshot_7](https://github.com/user-attachments/assets/2c8f38ba-af64-44f4-8406-aada3eb087b5)

Una vez terminada la ejecución, se puede ver que se han creado las tablas, y se muestran los resultados de las consultas elaboradas.

![Screenshot_9](https://github.com/user-attachments/assets/1eb7a110-5bd6-4c0a-ad50-6cc538282597)
![Screenshot_10](https://github.com/user-attachments/assets/2d6060c0-b27f-450a-a615-d9f5baf56296)
![Screenshot_11](https://github.com/user-attachments/assets/64b81274-69df-4ca4-b1ec-95796cf76b96)

Se pueden personalizar las consultas dentro del Notebook. Se proporciona una consulta básica que muestra las ardillas que han presentado observaciones.
![Screenshot_12](https://github.com/user-attachments/assets/4c9682b6-e16b-4622-8261-7371cac6fcaf)




