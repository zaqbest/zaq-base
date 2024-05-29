FROM --platform=$TARGETPLATFORM alpine:3.18

ARG TARGETPLATFORM
ARG BUILDPLATFORM

WORKDIR /app

COPY ./entrypoint.sh /app/entrypoint.sh

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories && \
    apk update && \
    apk add curl wget tzdata mysql-client redis openssh bash  && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo Asia/Shanghai > /etc/timezone && \
    apk del tzdata && \
    rm -rf /tmp/* /var/cache/apk/* && \
    chmod 755 /app/entrypoint.sh

RUN ln -s /usr/bin/redis-cli /usr/local/bin/redis-cli

# 添加环境变量设置时区
ENV TZ=Asia/Shanghai

CMD ["/bin/bash"]

ENTRYPOINT ["./entrypoint.sh"]