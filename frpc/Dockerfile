FROM alpine:3.15

LABEL maintainer="Mgrsc <migarishouchi@gmail.com>"

ARG FRP_VERSION=latest
ENV FRP_RELEASES_URL=https://github.com/fatedier/frp/releases/download

RUN apk add --no-cache curl \
    && if [ "${FRP_VERSION}" = "latest" ] ; then \
           FRP_VERSION=$(curl -s https://api.github.com/repos/fatedier/frp/releases/latest | grep tag_name | cut -d '"' -f 4 | sed 's/^v//') ; \
       fi \
    && cd /tmp \
    && curl -L "${FRP_RELEASES_URL}/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_amd64.tar.gz" -o frp.tar.gz  \
    && tar -xzf frp.tar.gz --strip-components=1 \
    && mv frps /usr/local/bin/ \
    && mkdir -p /etc/frp \
    && cp frps.ini /etc/frp/ \
    && chown -R nobody:nobody /etc/frp \
    && rm -rf frp.tar.gz \
    && apk del curl

WORKDIR /etc/frp
CMD ["sh", "-c", "exec /usr/local/bin/frps -c /etc/frp/frps.ini <&-"]

