# Usar la imagen base de Bitnami Spark 3.2.1
FROM bitnami/spark:3.2.1

# Establecer el usuario root para instalar las dependencias
USER root

# Instalar dependencias necesarias (sin Java ni libhadoop-dev)
RUN apt-get update && apt-get install -y \
    python3-pip \
    python3-dev \
    scala \
    curl \
    wget \
    git \
    python3-venv \
    software-properties-common \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Instalar Jupyter, PySpark, Findspark y Apache Toree (para el kernel de Scala)
RUN pip3 install --no-cache-dir jupyter pyspark findspark toree

# Establecer las variables de entorno para Spark y Scala
ENV SPARK_HOME=/opt/bitnami/spark
ENV PATH=$PATH:$SPARK_HOME/bin
ENV PYSPARK_DRIVER_PYTHON=jupyter
ENV PYSPARK_DRIVER_PYTHON_OPTS="notebook"
ENV PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
ENV PYTHONPATH=$SPARK_HOME/python/lib/py4j-*-src.zip:$PYTHONPATH

# Configurar el puerto que Jupyter va a usar
EXPOSE 8888 7077

# Instalar el kernel de Scala para Jupyter
RUN jupyter toree install --spark_home=$SPARK_HOME --kernel_name=scala

# Crear un directorio de trabajo para Jupyter
WORKDIR /home/jupyter

# Comando para iniciar Spark y Jupyter
CMD /opt/bitnami/scripts/spark/entrypoint.sh /opt/bitnami/spark/sbin/start-master.sh & \
    jupyter notebook --ip=0.0.0.0 --allow-root --no-browser --port=8888
