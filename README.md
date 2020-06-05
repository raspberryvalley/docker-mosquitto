# Mosquitto docker image for Raspberry Pi

This is yet another [Mosquitto](https://mosquitto.org) image for Docker, for use in our makerspace.

This Mosquitto image provides an MQTT broker for the Raspberry PI, the default configuration includes a MQTT endpoint on port 1883 and a WebSocket endpoint on port 9001.

The purpose of this image is to unify our base with [Balena Raspberry Pi 3 Images](https://www.balena.io/docs/reference/base-images/base-images-ref/).

## Docker Image

Our Docker image is based on a [Balena base image](https://www.balena.io/docs/reference/base-images/base-images/). It is targeted at Raspberry Pi 3, you can check all available images [here](https://www.balena.io/docs/reference/base-images/base-images-ref/) (search for the 'Raspberry Pi 3' section). See [eclipse-mosquitto](https://hub.docker.com/_/eclipse-mosquitto) for more detail.

---

Please note that we provide only the Raspberry Pi image, tagged as **rpi**. We use the official, non-modified PC image for testing.

---

## Running the image

The latest image is available on [Docker Hub](https://cloud.docker.com/u/raspberryvalley/repository/docker/raspberryvalley/mosquitto).

You can pull the image from our Raspberry Valley Docker Hub. Simply type the following:

```bash
docker pull raspberryvalley/mosquitto:rpi
```

Note: This is an optional step which fits our workflow. If you don't pull the image, the run scripts below will do it for you.

And launch with something like this:

```bash
docker run -d -p 1883:1883 -p 9001:9001 --name mymosquitto raspberryvalley/mosquitto:rpi
```

This launches your broker in the background, exposing the direct and sockets ports. Note that after a restart you need to start the container which was just created above.

## Building your own image

If you don't want to use our pre-made image, simply build your own. This is a sign of sanity: be careful about using 3rd party images: a bit of paranoia helps.

To build your own image, follow the steps below:

* clone this repository
* Open up PowerShell (or the command prompt) and navigate to the 'build' repository folder (where the Dockerfile is located)
* Update/modify the Dockerfile to your liking, then invoke the build command:

```bash
docker build -t "mymosquittoimage" .
```

## Testing your own image

To test everything works as expected follow the simple steps below. We will be using MQTT clients, which need to be installed first:

```bash
sudo apt install mosquitto-clients
```

Once installed:

* launch a container from the image you created above, i.e. **mymosquittoimage** (we'll create a temporary container, and keep a terminal open)

```bash
docker run -it -p 1883:1883 --rm mymosquittoimage
```

* Now open a terminal and subscribe t a test topic:

```bash
mosquitto_sub -t "test"
```

* In a third terminal window, send yourself a message:

```bash
mosquitto_pub -m "test message" -t "test"
```

You should see, in the second terminal, that the message was received.

## About

Raspberry Valley is a maker community in Karlskrona, Sweden, sponsored by [Dynapac](https://dynapac.com/en). We run makerspaces every week, working with Raspberry Pis, Arduinos and other interesting hardware.

This repository is here to support our community of makers. A lot of our achievements are based and inspired by the community at large. We wish to pay back and share our experiences and lessons learned. Join us!

You can find our pages here: [Raspberry Valley](https://raspberry-valley.azurewebsites.net). You can also join us on [Twitter](https://twitter.com/RaspberryValley) or check [Docker Hub](https://hub.docker.com/r/raspberryvalley/) for images of interest.

## Links

* [Mosquitto](https://mosquitto.org) - Official Mosquitto site
* [Mosquitto on Docker](https://hub.docker.com/_/eclipse-mosquitto) - Official Docker image
* [docker-mosquitto on Docker Hub](https://cloud.docker.com/u/raspberryvalley/repository/docker/raspberryvalley/mosquitto)

Raspberry Valley makerspace links

* [Raspberry Valley](https://raspberry-valley.azurewebsites.net) - Other things we make and do
* [Raspberry Valley on Twitter](https://twitter.com/RaspberryValley)
* [Raspberry Valley on Github](https://github.com/raspberryvalley)
* [Raspberry Valley Docker Hub Images](hub.docker.com/r/raspberryvalley/)
