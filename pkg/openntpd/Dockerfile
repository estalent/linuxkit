FROM linuxkit/alpine:f3cd219615428b2bd943411723eb28875275fae7 AS mirror

RUN mkdir -p /out/etc/apk && cp -r /etc/apk/* /out/etc/apk/
RUN apk add --no-cache --initdb -p /out \
    alpine-baselayout \
    busybox \
    musl \
    openntpd \
    && true
RUN rm -rf /out/etc/apk /out/lib/apk /out/var/cache

FROM scratch
ENTRYPOINT []
CMD []
WORKDIR /
COPY --from=mirror /out/ /
COPY etc/ /etc/
CMD ["/usr/sbin/ntpd", "-d", "-s"]
LABEL org.mobyproject.config='{"binds": ["/etc/resolv.conf:/etc/resolv.conf"], "capabilities": ["CAP_SYS_TIME", "CAP_SYS_NICE", "CAP_SYS_CHROOT", "CAP_SETUID", "CAP_SETGID"]}'
