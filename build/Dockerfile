# Mosquitto image for Raspberry Pi in the Raspberry Valley makerspace.

# Raspberry Valley is a makerspace in Sweden, Karlskrona. You can visit our sites and check what's developing: 
# * Knowledge base: https://raspberry-valley.azurewebsites.net
# * Github pages: https://github.com/raspberryvalley
# * Docker hub: hub.docker.com/r/raspberryvalley/
# * Follow on Twitter: https://twitter.com/RaspberryValley

FROM balenalib/raspberrypi3:stretch-run
LABEL maintainer = Raspberry Valley <raspberryvalley@outlook.com>

RUN apt-get update \
 && apt-get install -y --no-install-recommends wget \
 && apt-get install -y --no-install-recommends apt-transport-https \
 && wget -q -O - http://repo.mosquitto.org/debian/mosquitto-repo.gpg.key | apt-key add - \
 && wget -q -O /etc/apt/sources.list.d/mosquitto-stretch.list http://repo.mosquitto.org/debian/mosquitto-stretch.list \
 && apt-get update \
 && apt-get install -y --no-install-recommends mosquitto \
 && apt-get purge -y --auto-remove \
 && rm -rf /var/lib/apt/lists/* \
 && apt-get clean

RUN mkdir -p /mqtt/config /mqtt/data /mqtt/log
COPY config /mqtt/config
RUN chown -R mosquitto:mosquitto /mqtt

VOLUME ["/mqtt/config", "/mqtt/data", "/mqtt/log"]

EXPOSE 1883 9001

CMD /usr/sbin/mosquitto -c /mqtt/config/mosquitto.conf
