FROM ubuntu:20.04

ARG ARCH=amd64
RUN echo ${ARCH}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -y update && \
    apt-get -y install git sed curl wget jq dnsutils libcap2-bin iputils-ping traceroute rsync stress tcpdump iproute2 procps diffutils nmap python3-pip gnupg vim software-properties-common telnet openssh-client && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip3 install yq

RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
    && chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
    && apt update \
    && apt install gh -y

RUN curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

ENV TINI_VERSION v0.18.0
RUN curl -sL https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini-${ARCH} -o /tini
RUN chmod +x /tini

ENTRYPOINT ["/tini", "--"]
CMD ["/bin/sleep", "infinity"]
