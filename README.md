# docker-gr-satellites
gr-satellites in docker

## About

This is a GNU Radio installation with gr-satellites installed. Using Ubuntu 19.10 the GNU Radio version from repository should be > 3.7.13.4.

Gr-satellites should be the latest from https://github.com/daniestevez/gr-satellites.

It's huge and not set up well, I'll try and fix it up a bit.

## Building 

To build from github:
```
 git clone https://github.com/JayGe/docker-gr-satellites.git
 docker build . -t gi7ugv/gr-satellites
```
Or pulled from docker hub with:
```
 docker pull gi7ugv/gr-satellites
```
## Usage

You firstly will have to run something like the following to allow the X11 connection from the container to your local X server:
```
 xhost local:root
```
Start the container for telemetry only flows with the following: 
```
 docker run --rm -it -e DISPLAY --net=host gi7ugv/gr-satellites
```
It starts with the QO-100 flow open, the others are available to load from gnuradio-companion.

Input audio over the network as described in the gr-satellites documentation. By default the flows will listen on the local interface of the host so GQRX UDP audio to 127.0.0.1:7355 running on the host should be available to the flows. 

For flows with audio out if there are any either run the following or use pulse over a network connection, not confirmed this works yet:
```
docker run --rm -it -e DISPLAY --net=host --pid=host --ipc=host --privileged -e PULSE_SERVER=unix:${XDG_RUNTIME_DIR}/pulse/native -v ${XDG_RUNTIME_DIR}/pulse/native:${XDG_RUNTIME_DIR}/pulse/native -v ~/.config/pulse/cookie:/root/.config/pulse/cookie gi7ugv/gr-satellites
```
