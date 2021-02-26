FROM continuumio/miniconda3:4.8.2

RUN conda install --yes \
    -c conda-forge \
    python==3.8 \
    python-blosc \
    cytoolz \
    dask[complete]==2021.2.0 \
    lz4 \
    nomkl \
    numpy>=1.15.1 \
    pandas>=0.25.0 \
    scipy \
    pyarrow>=0.14.0 \
    matplotlib \
    cloudpickle>=0.2.2 \
    airflow==2.0.1 \
    psycopg2 \
    cython \
    tini \
    && conda clean -tipsy \
    && find /opt/conda/ -type f,l -name '*.a' -delete \
    && find /opt/conda/ -type f,l -name '*.pyc' -delete \
    && find /opt/conda/ -type f,l -name '*.js.map' -delete \
    && find /opt/conda/lib/python*/site-packages/bokeh/server/static -type f,l -name '*.js' -not -name '*.min.js' -delete \
    && rm -rf /opt/conda/pkgs

COPY prepare.sh /usr/bin/prepare.sh

WORKDIR /app

ENTRYPOINT ["tini", "-g", "--", "/usr/bin/prepare.sh"]
