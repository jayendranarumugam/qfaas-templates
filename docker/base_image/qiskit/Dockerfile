# FROM python:3.9.10-slim-buster
# RUN pip3 install qiskit pylatexenc
FROM python:3.10-slim-bookworm

RUN apt-get update \
&& apt-get --no-install-recommends -qy install gcc make python3-dev \
&& pip install --upgrade pip \
&& rm -rf /var/lib/apt/lists/*

# Add non root user with proper home directory
RUN addgroup --system app && \
    adduser app --system --ingroup app --home /home/app && \
    mkdir -p /home/app && \
    chown app:app /home/app
USER app

ENV PATH=$PATH:/home/app/.local/bin
RUN pip install --user "qiskit==2.2.0"