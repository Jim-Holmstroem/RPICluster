FROM jimho/archlinux-armv7h:latest

RUN pacman -S --noconfirm \
    tar \
    erlang-nox \
    systemd

RUN useradd --create-home --home-dir /opt/rabbitmq --shell /bin/bash rabbitmq
ENV HOME /opt/rabbitmq
ENV USER rabbitmq
WORKDIR /opt/rabbitmq

ADD https://aur.archlinux.org/packages/ra/rabbitmq/rabbitmq.tar.gz rabbitmq.tar.gz
RUN chown -R rabbitmq:rabbitmq rabbitmq.tar.gz
USER rabbitmq
RUN tar -xvf rabbitmq.tar.gz && cd rabbitmq && makepkg
USER root
RUN cd rabbitmq && ls | grep tar.xz | xargs pacman -U --noconfirm

EXPOSE 5672
EXPOSE 15672

CMD ["rabbitmq-server"]
