FROM progrium/busybox

RUN opkg-install socat
ADD start.sh start.sh

ENTRYPOINT ["/start.sh"]
