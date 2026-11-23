FROM jenkins/jenkins:lts-jdk21

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends python3 python3-venv python3-pip git openssh-client && \
    rm -rf /var/lib/apt/lists/*

RUN python3 -m venv /opt/ansible-venv && \
    /opt/ansible-venv/bin/pip install --no-cache-dir ansible && \
    ln -s /opt/ansible-venv/bin/ansible* /usr/local/bin/

USER jenkins