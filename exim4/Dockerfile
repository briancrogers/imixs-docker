FROM debian:buster

MAINTAINER Ralph Soika <ralph.soika@imixs.com>
# This dockerfile was inpired by greinacker/exim4

# install packages: exim4, mailutils
RUN apt-get update \
 && apt-get install --no-install-recommends -y \
  exim4-daemon-light mailutils xtail vim openssl \
 # Slim down image
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/man/?? /usr/share/man/??_*

# add the exim4 start script
ADD start.sh /exim_start
RUN chmod +x /exim_start

ENV EXIM_LOCALINTERFACE=0.0.0.0
ENV EXIM_ALLOWED_SENDERS=10.0.0.0/8:172.16.0.0/12:127.0.0.1:192.168.0.0/16

# keep mail queue in a volume
VOLUME /var/spool/exim4

ENTRYPOINT ["/exim_start"]
