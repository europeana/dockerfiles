FROM vimagick/dante

ENV SOCKS_PASSWORD=

RUN useradd -M socks
RUN sed -ri 's/^socksmethod.*/socksmethod: username/' /etc/sockd.conf

CMD printf "$SOCKS_PASSWORD\n$SOCKS_PASSWORD\n" | passwd socks && \
  sockd -f $CFGFILE -p $PIDFILE -N $WORKERS
