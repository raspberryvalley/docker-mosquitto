# Mosquitto docker image for Raspberry Pi

We are a maker community in Karlskrona, Sweden. See our site for other ideas and activities: [Raspberry Valley](https://raspberry-valley.azurewebsites.net).

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

## Links

* [Mosquitto](https://mosquitto.org) - Official Mosquitto site
* [Mosquitto on Docker](https://hub.docker.com/_/eclipse-mosquitto) - Official Docker image
* [docker-mosquitto on Docker Hub](https://cloud.docker.com/u/raspberryvalley/repository/docker/raspberryvalley/mosquitto)

Raspberry Valley makerspace links

* [Raspberry Valley](https://raspberry-valley.azurewebsites.net) - Other things we make and do
* [Raspberry Valley on Twitter](https://twitter.com/RaspberryValley)
* [Raspberry Valley on Github](https://github.com/raspberryvalley)
* [Raspberry Valley Docker Hub Images](hub.docker.com/r/raspberryvalley/)
