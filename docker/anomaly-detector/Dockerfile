FROM continuumio/miniconda3

# Download dockerize and cache that layer
ENV DOCKERIZE_VERSION=v0.6.1
RUN wget -O dockerize.tar.gz https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_VERSION}/dockerize-alpine-linux-amd64-${DOCKERIZE_VERSION}.tar.gz
RUN tar xzf dockerize.tar.gz
RUN chmod +x dockerize


SHELL ["/bin/bash", "-c"]
ADD . /
RUN chmod +x set_uid.sh

ADD environment.yml /tmp/environment.yml
RUN chmod g+w /etc/passwd
RUN conda env create -f /tmp/environment.yml

USER 1001

# Ensure that assigned uid has entry in /etc/passwd.
CMD ./set_uid.sh && /opt/conda/envs/prophet-env/bin/python ${APP_FILE}
