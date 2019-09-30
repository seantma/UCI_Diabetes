# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
# ARG BASE_CONTAINER=jupyter/scipy-notebook
# FROM $BASE_CONTAINER
FROM jupyter/scipy-notebook

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

# Set when building on Travis so that certain long-running build steps can
# be skipped to shorten build time.
ARG TEST_ONLY_BUILD

# `root` section
USER root

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    gfortran \
    gcc \
    # RODBC related
    unixodbc \
    unixodbc-dev \
    r-cran-rodbc \
    # MS ODBC related
    gnupg \
    curl && \
    rm -rf /var/lib/apt/lists/*

# Sean::Microsoft SQL server ODBC driver (Ubuntu)
# https://docs.microsoft.com/en-us/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=sql-server-2017
# https://github.com/microsoft/mssql-docker/blob/master/linux/mssql-tools/Dockerfile
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

RUN apt-get update && \
    ACCEPT_EULA=Y apt-get install msodbcsql17
    
# User `jovyan` section
USER $NB_UID

# R packages including IRKernel which gets installed globally.
RUN conda install --quiet --yes \
    'r-base=3.6.1' \
    'r-caret=6.0*' \
    'r-crayon=1.3*' \
    'r-devtools=2.1*' \
    'r-forecast=8.7*' \
    'r-hexbin=1.27*' \
    'r-htmltools=0.3*' \
    'r-htmlwidgets=1.3*' \
    'r-irkernel=1.0*' \
    'r-nycflights13=1.0*' \
    'r-plyr=1.8*' \
    'r-randomforest=4.6*' \
    'r-rcurl=1.95*' \
    'r-reshape2=1.4*' \
    'r-rmarkdown=1.14*' \
    'r-rsqlite=2.1*' \
    'r-shiny=1.3*' \
    'r-sparklyr=1.0*' \
    'r-tidyverse=1.2*' \
    # Sean:: R Feather
    'r-feather=0.3*' \
    # Sean:: ODBC related
    'r-rodbc=1.3*' \
    'unixodbc=2.3.*' \
    'pyodbc=4.0*' \
    && \
    conda install -c glaxosmithkline 'r-odbc=1.1*' && \
    # Sean:: Misc python packages
    pip install 'rpy2==3.1.0' && \
    pip install 'feather-format==0.4.0' && \
    pip install 'vtreat==0.2.9' && \
    pip install 'wvpy==0.1.2' && \
    pip install 'xgboost==0.9*' && \
    conda install -c conda-forge 'imbalanced-learn=0.4.3' && \
    conda install -c conda-forge 'pandas-profiling=2.3.0' && \
    conda install -c conda-forge vim && \
    # cleanup
    conda clean --all -f -y && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
