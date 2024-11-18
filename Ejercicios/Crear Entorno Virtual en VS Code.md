# Configuración de un Entorno Virtual en VS Code para Trabajar con Python y Jupyter Notebooks

Este documento te guiará paso a paso para configurar un entorno virtual en **Visual Studio Code** (VS Code) y trabajar con **Python** y **Jupyter Notebooks**.

## Requisitos Previos

1. **Instalar Python**: Asegúrate de tener Python 3.x instalado en tu sistema. Puedes verificar si ya lo tienes con el siguiente comando:

    ```bash
    python --version
    ```

    Si no lo tienes instalado, descarga e instala Python desde [python.org](https://www.python.org/).

2. **Instalar Visual Studio Code (VS Code)**: Si aún no tienes VS Code, descárgalo e instálalo desde [Visual Studio Code](https://code.visualstudio.com/).

3. **Extensión de Python en VS Code**: Asegúrate de instalar la extensión de Python en VS Code. Esta extensión se puede encontrar y activar desde la barra lateral de Extensiones (`Ctrl+Shift+X`) en VS Code.

4. **Instalar Jupyter**: También necesitas instalar la extensión de Jupyter en VS Code. Esto te permitirá trabajar con Jupyter Notebooks directamente desde el editor. 

   La extensión de Jupyter también se puede encontrar desde la barra de Extensiones de VS Code.

---

## Pasos para Configurar el Entorno Virtual

### 1. **Abrir VS Code**

Abre **Visual Studio Code** en la carpeta de tu proyecto o crea una nueva carpeta para tu proyecto Python.

### 2. **Crear un Entorno Virtual**

En la terminal integrada de VS Code, crea un entorno virtual con el siguiente comando:

#### Windows:

```bash
python -m venv venv

macOS/Linux:
bash
Copiar código
python3 -m venv venv
Este comando creará una carpeta llamada venv en tu proyecto, que contendrá todos los paquetes y dependencias aisladas.

3. Activar el Entorno Virtual
Windows:
bash
Copiar código
.\venv\Scripts\Activate
macOS/Linux:
bash
Copiar código
source venv/bin/activate
Cuando el entorno virtual esté activado, deberías ver el prefijo (venv) en tu terminal, indicando que el entorno virtual está activo.

4. Instalar Dependencias Necesarias
Dentro del entorno virtual, instala los paquetes necesarios para trabajar con Jupyter Notebooks.

Primero, asegúrate de tener Jupyter y ipykernel instalados:

bash
Copiar código
pip install jupyter ipykernel
Este comando instalará Jupyter y ipykernel, lo cual es necesario para ejecutar notebooks de Jupyter.

Si también necesitas otros paquetes para tu proyecto, puedes instalarlos en este momento (por ejemplo, numpy, pandas, matplotlib, etc.):

bash
Copiar código
pip install numpy pandas matplotlib
5. Configurar el Entorno Virtual en VS Code
Abre el Command Palette en VS Code con Ctrl+Shift+P.
Escribe Python: Select Interpreter y selecciona la opción correspondiente.
Aparecerá una lista de intérpretes. Elige el que apunta a tu entorno virtual recién creado. Este debería estar en la ruta ./venv/Scripts/python en Windows o ./venv/bin/python en macOS/Linux.
VS Code ahora usará este entorno virtual como el intérprete de Python para el proyecto.

6. Abrir o Crear un Jupyter Notebook
Crea un nuevo archivo con la extensión .ipynb (por ejemplo, notebook.ipynb) o abre uno ya existente.

Si aún no tienes instalado el Jupyter Notebook en tu entorno, puedes iniciar Jupyter con el siguiente comando en la terminal:

bash
Copiar código
jupyter notebook
Abre el navegador web que se abre y carga el archivo .ipynb desde tu proyecto.

7. Configurar el Kernel de Jupyter
Asegúrate de que Jupyter use el entorno virtual como kernel para ejecutar el notebook. En el archivo .ipynb, haz clic en la esquina superior derecha donde dice "Select Kernel" o "Seleccionar kernel" y elige el entorno virtual que acabas de configurar.
