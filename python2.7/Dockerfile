FROM lambci/lambda:build-python2.7

MAINTAINER "Max Ligus" <max.ligus@gmail.com>

RUN pip install -U pip && pip install -U zappa awscli 

WORKDIR /var/task

RUN virtualenv /var/venv && \
    source /var/venv/bin/activate && \
    pip install -U pip && \
    deactivate

COPY files/.bashrc /root/.bashrc

CMD ["zappa"]
