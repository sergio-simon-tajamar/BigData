# Usa una imagen base de Jupyter con Python 3.9
FROM jupyter/base-notebook:python-3.9

# Variables de entorno
ENV SPARK_VERSION=3.5.3
ENV HADOOP=3
ENV HADOOP_VERSION=3.4.1
ENV SPARK_HOME=/opt/spark
ENV HADOOP_HOME=/opt/hadoop  
ENV PATH="$SPARK_HOME/bin:$HADOOP_HOME/bin:$PATH"

# Instalar dependencias y Java
USER root
RUN apt-get update && \
    apt-get install -y openjdk-11-jdk wget curl gnupg && \
    apt-get clean

# Descargar e instalar Hadoop
RUN wget https://dlcdn.apache.org/hadoop/common/hadoop-$HADOOP/hadoop-$HADOOP_VERSION.tar.gz && \
    tar -xzf hadoop-$HADOOP_VERSION.tar.gz -C /opt/ && \
    mv /opt/hadoop-$HADOOP_VERSION $HADOOP_HOME && \
    rm hadoop-$HADOOP_VERSION.tar.gz

# Descargar e instalar Spark usando la URL correcta
RUN wget https://dlcdn.apache.org/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-hadoop$HADOOP.tgz && \
    tar -xzf spark-$SPARK_VERSION-bin-hadoop$HADOOP.tgz -C /opt/ && \
    mv /opt/spark-$SPARK_VERSION-bin-hadoop$HADOOP $SPARK_HOME && \
    rm spark-$SPARK_VERSION-bin-hadoop$HADOOP.tgz

# Instalar PySpark y dependencias de Python
RUN pip install pyspark

# Instalar JupyterLab, Apache Toree, findspark
RUN pip install jupyterlab findspark && \
    pip install toree && \
    jupyter toree install --spark_home=$SPARK_HOME --interpreters=Scala --user

# Crear un kernel de PySpark en Jupyter
RUN python -m ipykernel install --user --name=pyspark --display-name "PySpark"

# Crear directorios necesarios
RUN sudo mkdir -p /home/jovyan/.local/share/jupyter && \
    chown -R $NB_UID:$NB_GID /home/jovyan/.local

# Cambiar de nuevo al usuario original
USER $NB_UID

# Establecer el puerto para JupyterLab
EXPOSE 8888

# Iniciar JupyterLab
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''"]