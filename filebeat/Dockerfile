ARG BUILD_FROM
FROM $BUILD_FROM

RUN mkdir downloads

COPY rootfs /

ARG BUILD_ARCH

RUN \
    FB_VERSIONS="7.17.4 8.0.1 8.1.3 8.2.3 8.6.2 8.7.0" && \
    find /opt -iname *.yml | xargs chmod 644 && \
    for ver in $FB_VERSIONS; do echo "Copying filebeat file"; curl "https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${ver}-x86_64.tar.gz" --output downloads/filebeat-${ver}-x86_64.tar.gz; curl "https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${ver}-aarch64.tar.gz" --output downloads/filebeat-${ver}-aarch64.tar.gz; tar txvf downloads/filebeat-${ver}-x86_64.tar.gz -C downloads; mv downloads/filebeat-${ver}-x86_64 downloads/filebeat-${ver}-amd64; tar zxvf downloads/filebeat-${ver}-aarch64.tar.gz -C downloads; cp downloads/filebeat-${ver}-${BUILD_ARCH}/filebeat /bit/filebeat-${ver}; ln -s /bin/filebeat-${ver} /bin/filebeat; chmod +x /bin/filebeat-$ver; done && \
    rm -rf /env && rm -rf downloads

CMD [ "/run.sh" ]
