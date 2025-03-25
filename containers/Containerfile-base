# hardened_malloc
ARG BASE_IMAGE="fedora"
ARG BASE_VERSION="41"

FROM ${BASE_IMAGE}:${BASE_VERSION} AS hardened_malloc

RUN dnf install -y git gcc gcc-c++ make
RUN git clone --depth=1 --single-branch --branch=main \
        https://github.com/GrapheneOS/hardened_malloc.git /tmp/hardened_malloc \
    && cd /tmp/hardened_malloc \
    && make


FROM ${BASE_IMAGE}:${BASE_VERSION}

COPY --from=hardened_malloc /tmp/hardened_malloc/out/libhardened_malloc.so /usr/lib64/libhardened_malloc.so

RUN echo /usr/lib64/libhardened_malloc.so >> /etc/ld.so.preload
