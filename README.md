# docker-gr-satellites
gr-satellites in docker

## About

Docker with GNU Radion and gr-satellites from https://github.com/daniestevez/gr-satellites installed. 

It's huge and not set up well, I'll try and fix it up a bit.

## Building 

docker build . -t gi7ugv/docker-gr-satellites

## Usage

You firstly might have to run something like the following to allow the X11 connection:

xhost local:root

Start the container for telemetry only flows with the following: 

docker run --rm -it -e DISPLAY --net=host gi7ugv/docker-gr-satellites

For flows with audio out if there are any either run the following or use pulse over a network connection, not confirmed this works yet:

docker run --rm -it -e DISPLAY --net=host --pid=host --ipc=host --privileged -e PULSE_SERVER=unix:${XDG_RUNTIME_DIR}/pulse/native -v ${XDG_RUNTIME_DIR}/pulse/native:${XDG_RUNTIME_DIR}/pulse/native -v ~/.config/pulse/cookie:/root/.config/pulse/cookie gi7ugv/docker-gr-satellites

It starts with the QO-100 flow open, the others are available to load from gnuradio-companion.

