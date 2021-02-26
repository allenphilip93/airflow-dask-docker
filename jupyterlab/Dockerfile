FROM python:3.8

RUN groupadd --gid 1000 promo-jupyter
RUN useradd --create-home --shell /bin/bash  --uid 1000 --gid 1000 promo-jupyter

ENV PYTHONUNBUFFERED=1
ENV PYTHONDONTWRITEBYTECODE=1
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8
ENV PORT=8888

RUN python3.8 -m venv /venv
ENV PATH=/venv/bin:${PATH}

# Install Jupyter
RUN pip install jupyter
RUN pip install ipywidgets
RUN jupyter nbextension enable --py widgetsnbextension

# Install JupyterLab
RUN pip install jupyterlab && jupyter serverextension enable --py jupyterlab

ENV LANG=C.UTF-8

# Install Python Packages & Requirements (Done near end to avoid invalidating cache)
COPY requirements.txt /app/requirements.txt
RUN pip install -r /app/requirements.txt

WORKDIR /app
RUN chown -R promo-jupyter:promo-jupyter /app
RUN chmod -R 755 /app
ENV PYTHONPATH=/app

USER 1000
CMD ["sh", "-c", "exec jupyter lab --ip=* --port=${PORT} --no-browser --notebook-dir=/app/ --allow-root"]