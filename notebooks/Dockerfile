FROM continuumio/miniconda3:latest
LABEL maintainer="Eugene Morozov <emorozov@gmail.com>"

RUN conda update -n base -c defaults conda
RUN conda install anaconda-project

RUN mkdir /notebooks
RUN mkdir /models

WORKDIR /notebooks

COPY anaconda-project.yml /notebooks/anaconda-project.yml
COPY .projectignore /notebooks/.projectignore

RUN anaconda-project prepare --env-spec notebook
RUN anaconda-project run register-kernel
RUN anaconda-project run generate-config

COPY *.ipynb /notebooks/
COPY *.csv /notebooks/

ENTRYPOINT ["anaconda-project", "run", "models", "--anaconda-project-address", "0.0.0.0", "--no-browser", "--allow-root"]