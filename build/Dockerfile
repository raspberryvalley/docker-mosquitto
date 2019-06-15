FROM balenalib/raspberrypi3:stretch-run
LABEL maintainer = Raspberry Valley <raspberryvalley@outlook.com>

RUN apt-get update \
 && apt-get full-upgrade \
 && apt-get install -y wget \
 && apt-get install -y apt-transport-https \
 && wget -q -O - http://repo.mosquitto.org/debian/mosquitto-repo.gpg.key | apt-key add - \
 && wget -q -O /etc/apt/sources.list.d/mosquitto-stretch.list http://repo.mosquitto.org/debian/mosquitto-stretch.list \
 && apt-get update \
 && apt-get install -y mosquitto \
 && apt-get purge -y --auto-remove \
 && rm -rf /var/lib/apt/lists/* \
 && apt-get clean

RUN mkdir -p /mqtt/config /mqtt/data /mqtt/log
COPY config /mqtt/config
RUN chown -R mosquitto:mosquitto /mqtt

VOLUME ["/mqtt/config", "/mqtt/data", "/mqtt/log"]

EXPOSE 1883 9001

CMD /usr/sbin/mosquitto -c /mqtt/config/mosquitto.conf
