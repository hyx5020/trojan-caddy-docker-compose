FROM gtary/trojan:latest

CMD ["/bin/sh"]

RUN apk add --no-cache --virtual .build-deps         \
  build-base         \
  cmake         \
  boost-dev         \
  openssl-dev         \
  mariadb-connector-c-dev         \
  tzdata     \
 && apk add --no-cache --virtual .trojan-rundeps      \   
  libstdc++         \
  boost-system         \
  boost-program_options         \
  boost-regex         \
  mariadb-connector-c         \
  curl     \
 && cp -r -f /usr/share/zoneinfo/Hongkong /etc/localtime     \
 && (cd trojan && cmake . && make -j $(nproc) && strip -s trojan     \
 && mv trojan /usr/local/bin)     \
 && rm -rf trojan     \
 && apk del .build-deps

WORKDIR /config

CMD ["trojan" "config.json","/wait_for_caddy.sh"]
