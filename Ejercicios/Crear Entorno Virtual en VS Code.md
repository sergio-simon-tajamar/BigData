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
