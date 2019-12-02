FROM python:2.7.17-slim-buster@sha256:5e6fb7cec84571b570b9dc971fc501f38a2bd3d55c4a2451b644cbc2bebd250c

RUN groupadd -g 65532 nonroot && \
  useradd --create-home --home-dir /home/nonroot --uid 65532 --gid 65532 -c nonroot -s /usr/sbin/nologin nonroot
USER nonroot:nonroot
WORKDIR /home/nonroot

ARG pip_package=tmuxp
ENV PIP_PACKAGE ${pip_package}
RUN pip install --user ${PIP_PACKAGE} && \
  mv -v ~/.local ~/${PIP_PACKAGE} && \
  mv -v ~/${PIP_PACKAGE}/lib/python2.7/site-packages ~/${PIP_PACKAGE}/site-packages

RUN PYTHONPATH=~/${PIP_PACKAGE}/site-packages ${PIP_PACKAGE}/bin/${PIP_PACKAGE} --version
