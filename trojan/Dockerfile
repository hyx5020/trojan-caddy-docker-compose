FROM gtary/trojan:latest

ADD file:0c4555f363c2672e350001f1293e689875a3760afe7b3f9146886afe67121cba in / 

CMD ["/bin/sh"]
 
COPY dir:4b9a648a91edf54c636e578d98848c08cd4f4592fe6198b816cf1dae22b4c41d in trojan 

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
