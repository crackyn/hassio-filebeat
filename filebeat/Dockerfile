ARG BUILD_FROM
FROM $BUILD_FROM

RUN mkdir /downloads

COPY rootfs /

ARG BUILD_ARCH

RUN \
    FB_VERSIONS="7.17.4 8.0.1 8.1.3 8.2.3 8.6.2 8.7.0" && \
    find /opt -iname *.yml | xargs chmod 644 && \
    for ver in $FB_VERSIONS; do echo "Downloading from https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${ver}-linux-x86_64.tar.gz"; curl "https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${ver}-linux-x86_64.tar.gz" --output /downloads/filebeat-${ver}-linux-x86_64.tar.gz; echo "Downloading from https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${ver}-linux-arm64.tar.gz"; curl "https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${ver}-linux-arm64.tar.gz" --output /downloads/filebeat-${ver}-linux-arm64.tar.gz; echo "extract amd64"; tar zxf /downloads/filebeat-${ver}-linux-x86_64.tar.gz -C /downloads; mv /downloads/filebeat-${ver}-linux-x86_64 /downloads/filebeat-${ver}-linux-amd64;echo "extract aarch64"; tar zxf /downloads/filebeat-${ver}-linux-arm64.tar.gz -C /downloads;  mv /downloads/filebeat-${ver}-linux-arm64 /downloads/filebeat-${ver}-linux-aarch64; cp /downloads/filebeat-${ver}-linux-${BUILD_ARCH}/filebeat /bin/filebeat-${ver}; chmod +x /bin/filebeat-$ver; done && \
    rm -rf /env && rm -rf downloads

CMD [ "/run.sh" ]
