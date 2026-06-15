FROM rockylinux:8

RUN dnf -y update && \
    dnf install -y procps-ng && \
    dnf clean all

RUN dnf install -y 'dnf-command(config-manager)' https://repo.openflighthpc.org/openflight/centos/8/x86_64/openflighthpc-release-3-1.noarch.rpm && \
dnf config-manager --set-enabled powertools && \
dnf install -y epel-release && \
dnf makecache

RUN dnf install -y flight-user-suite flight-web-suite

RUN dnf install -y flight-gather flight-hunter flight-profile flight-pdsh

RUN /opt/flight/bin/flight env create -g modules

RUN /opt/flight/bin/flight set --global always on

RUN /opt/flight/bin/flight env set-default modules

CMD ["/bin/bash"]
