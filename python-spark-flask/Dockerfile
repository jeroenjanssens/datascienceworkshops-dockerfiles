FROM jupyter/pyspark-notebook

LABEL maintainer="Jeroen Janssens <jeroen@datascienceworkshops.com>"

USER root

RUN pip install flask flask-restful flask-rest-jsonapi flask-themes flask-user flask-wtf flask-uploads

RUN conda install -y altair rpy2 r-tidyverse
RUN jupyter nbextension enable vega --py --sys-prefix

USER $NB_USER

