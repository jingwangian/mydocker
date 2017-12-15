FROM jupyter/pyspark-notebook

MAINTAINER jing wang <jingwangian@gmail.com>

ENV MASTER "local[*]"

USER root

# Install all OS dependencies for openai gym
RUN apt-get update && apt-get install -yq --no-install-recommends unzip

RUN echo "spark.executor.memory   50g" >>$SPARK_HOME/conf/spark-defaults.conf

RUN echo $NB_USER:nopassword | chpasswd

# switch user
USER $NB_USER

RUN pip install --upgrade pip
pip install awscli

WORKDIR /home/$NB_USER/work

EXPOSE 22

#ENV PYSPARK_DRIVER_PYTHON="ipython"
#ENV PYSPARK_DRIVER_PYTHON_OPTS="notebook"

#CMD ["/bin/bash", "bin/pysparkling"]
