FROM ubuntu:noble

COPY . /opt/app
WORKDIR /opt/app

# Install Latest OpenVPN Version
RUN apt-get update -y && \
  apt-get upgrade -y && \
  apt-get install gnupg wget -y && \
  wget -qO - 'https://swupdate.openvpn.net/repos/repo-public.gpg' | apt-key add - && \
  echo 'deb http://build.openvpn.net/debian/openvpn/release/2.5 noble main' > /etc/apt/sources.list.d/openvpn-aptrepo.list && \
  apt-get install openvpn -y

# Download easy-rsa
RUN wget -q https://github.com/OpenVPN/easy-rsa/releases/download/v3.1.7/EasyRSA-3.1.7.tgz && \
  tar xf EasyRSA-3.1.7.tgz && \
  rm -f EasyRSA-3.1.7.tgz && \
  mv EasyRSA-3.1.7 easy-rsa

# Install iptables
RUN apt-get install iptables -y

EXPOSE 1194/udp

RUN chmod +x bin/*
RUN chmod +x docker-entrypoint.sh
ENTRYPOINT ./docker-entrypoint.sh \
  "$REQ_COUNTRY" \
  "$REQ_PROVINCE" \
  "$REQ_CITY" \
  "$REQ_ORG" \
  "$REQ_OU" \
  "$REQ_CN"
