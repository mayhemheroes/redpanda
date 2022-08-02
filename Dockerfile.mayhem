FROM fedora:34 as builder

COPY --chown=0:0 install-dependencies.sh /

RUN /install-dependencies.sh
RUN dnf clean all
RUN rm install-dependencies.sh

RUN yum install wget -y
RUN wget https://go.dev/dl/go1.18.1.linux-amd64.tar.gz
RUN tar -C /usr/local -xvf go1.18.1.linux-amd64.tar.gz
ENV PATH=$PATH:/usr/local/go/bin

ADD . /redpanda
WORKDIR /redpanda

WORKDIR /redpanda/src/go/rpk
RUN ./build.sh

FROM fedora:34 

COPY --from=builder redpanda/src/go/rpk/linux-amd64/rpk /
