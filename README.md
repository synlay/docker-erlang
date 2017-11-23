# Basic Docker Container Images for Erlang/OTP

[![](https://badge.imagelayers.io/synlay/erlang:latest.svg)](https://imagelayers.io/?images=synlay%2Ferlang:latest,synlay%2Ferlang:20.1,synlay%2Ferlang:19.3,synlay%2Ferlang:19.1,synlay%2Ferlang:19.0,synlay%2Ferlang:18.3_xenial_xerus,synlay%2Ferlang:18.3,synlay%2Ferlang:18.2.1,synlay%2Ferlang:18.2,synlay%2Ferlang:18.1,synlay%2Ferlang:18.0,synlay%2Ferlang:17.5 'Get your own badge on imagelayers.io') [![Docker Repository on Quay](https://quay.io/repository/synlay/docker-erlang/status "Docker Repository on Quay")](https://quay.io/repository/synlay/docker-erlang) [![Docker Repository on Docker Hub](https://img.shields.io/docker/automated/synlay/erlang.svg?maxAge=2592000)](https://hub.docker.com/r/synlay/erlang/)

This repository does provide some Docker container images that include [Erlang/OTP](http://www.erlang.org/), along with the [rebar](https://github.com/rebar/rebar) and [relx](https://github.com/erlware/relx) build and release tools.

The image file for the different Erlang/OTP versions can be found within the subdirectories and are available through tags on the Docker Hub.

Latest Tools | Version
------------ | -------------
Base image | [phusion/baseimage:0.9.22](https://github.com/phusion/baseimage-docker/tree/cd23614b2741c5839e08585d9de778928c2b2146)
Erlang/OTP | 20.1
rebar | [2.6.4](https://github.com/rebar/rebar/tree/2429ddf7b46597222b0eaf6b79a438baafaaa96f)
rebar3 | [3.4.7](https://github.com/erlang/rebar3/tree/81a5711b6db4dedb1d151d39464f326be80e2285)
relx | [v3.24.3](https://github.com/erlware/relx/tree/63847133b4e171888f46e11b34dd00d2aa4ed081)

# Usage

Start a throw-away instance

```bash
docker run -it --rm synlay/erlang /bin/bash
```

Run a container to use as a development environment

```bash
docker run -it --name erlang-app synlay/erlang /bin/bash
```
