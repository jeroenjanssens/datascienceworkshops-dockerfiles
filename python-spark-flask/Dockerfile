FROM jupyter/pyspark-notebook

LABEL maintainer="Jeroen Janssens <jeroen@datascienceworkshops.com>"

USER root

RUN pip install flask flask-restful flask-rest-jsonapi flask-themes flask-user flask-wtf flask-uploads

USER $NB_USER
