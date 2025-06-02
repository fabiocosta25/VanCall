FROM debian:bullseye

# Instala dependências básicas e NDI SDK (você precisa baixar manualmente o SDK da NewTek)
RUN apt-get update && \
    apt-get install -y build-essential cmake git libmicrohttpd-dev libjansson-dev \
    libssl-dev libsrtp2-dev libsofia-sip-ua-dev libglib2.0-dev \
    libopus-dev libogg-dev libcurl4-openssl-dev liblua5.3-dev \
    libconfig-dev pkg-config gengetopt libtool automake \
    libwebsockets-dev doxygen graphviz wget unzip

# Copie o NDI SDK manualmente para a raiz do projeto antes de buildar
COPY Install_NDI_SDK_v5_Linux.tar.gz /tmp/
RUN cd /tmp && tar -xzf Install_NDI_SDK_v5_Linux.tar.gz && \
    cp -r NDI\ SDK\ for\ Linux/include/* /usr/local/include/ && \
    cp -r NDI\ SDK\ for\ Linux/lib/x86_64-linux-gnu/* /usr/local/lib/ && \
    ldconfig

# Clona e compila o Janus + plugin NDI
RUN git clone https://github.com/meetecho/janus-gateway.git /opt/janus-gateway
WORKDIR /opt/janus-gateway
RUN git clone https://github.com/meetecho/janus-gateway-ndi.git plugins/janus-ndi
RUN sh autogen.sh \
 && ./configure --prefix=/opt/janus --enable-ndi \
 && make -j4 && make install && make configs

# Copia configs customizados
COPY janus.jcfg /opt/janus/etc/janus/
COPY janus.plugin.ndi.jcfg /opt/janus/etc/janus/

EXPOSE 8088 8188 8000/udp 10000/udp

ENTRYPOINT ["/opt/janus/bin/janus"]
