FROM ubuntu:xenial

MAINTAINER Robert Dempsey <robertonrails@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# Update the base install
RUN apt-get update && apt-get -y upgrade && apt-get -y install wget bzip2 && apt-get autoremove

# Install Java 8
RUN apt-get -y install openjdk-8-jre
RUN apt-get -y install openjdk-8-jdk

# Install Scala 2.12.2
RUN wget --quiet www.scala-lang.org/files/archive/scala-2.12.2.deb
RUN dpkg -i scala-2.12.2.deb
RUN rm scala-2.12.2.deb


# Install Python 3.6
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh \
    && wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    && /bin/bash Miniconda3-latest-Linux-x86_64.sh -b -p /opt/conda \
    && rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH /opt/conda/bin:$PATH

# Install Apache Spark 2.1.0
RUN wget --quiet https://archive.apache.org/dist/spark/spark-2.1.0/spark-2.1.0-bin-hadoop2.7.tgz
RUN tar -xvzf spark-2.1.0-bin-hadoop2.7.tgz
RUN mv spark-2.1.0-bin-hadoop2.7 /opt/spark
RUN cd /opt/spark/python && python setup.py install
ENV SPARK_HOME /opt/spark
ENV PATH $SPARK_HOME/bin:$PATH

# Start PySpark
#CMD ["pyspark"]

CMD ["/bin/bash"]