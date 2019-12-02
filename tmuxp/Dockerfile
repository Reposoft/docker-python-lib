FROM python:2.7.17-slim-buster@sha256:5e6fb7cec84571b570b9dc971fc501f38a2bd3d55c4a2451b644cbc2bebd250c

RUN apt-get update && apt-get install -y tmux

RUN groupadd -g 65532 nonroot && \
  useradd --create-home --home-dir /home/nonroot --uid 65532 --gid 65532 -c nonroot -s /usr/sbin/nologin nonroot
USER nonroot:nonroot
WORKDIR /home/nonroot

RUN pip install --user tmuxp && \
  mv ~/.local ~/.python && \
  PYTHONPATH=~/.python/lib/python2.7/site-packages /home/nonroot/.python/bin/tmuxp --version
