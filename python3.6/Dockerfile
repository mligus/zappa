FROM lambci/lambda:build-python3.6

MAINTAINER "Max Ligus" <max.ligus@gmail.com>

RUN pip3 install -U pip && pip3 install -U zappa

WORKDIR /var/task

RUN python -m venv /var/venv && \
    source /var/venv/bin/activate && \
    pip install -U pip && \
    deactivate

COPY files/.bashrc /root/.bashrc

CMD ["zappa"]
