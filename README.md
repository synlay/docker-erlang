# Basic Docker Container Images for Erlang/OTP

[![](https://badge.imagelayers.io/synlay/erlang:latest.svg)](https://imagelayers.io/?images=synlay%2Ferlang:latest,synlay%2Ferlang:19.0,synlay%2Ferlang:18.3,synlay%2Ferlang:18.2.1,synlay%2Ferlang:18.2,synlay%2Ferlang:18.1,synlay%2Ferlang:18.0,synlay%2Ferlang:17.5 'Get your own badge on imagelayers.io')

This repository does provide some Docker container images that include [Erlang/OTP](http://www.erlang.org/), along with the [rebar](https://github.com/rebar/rebar) and [relx](https://github.com/erlware/relx) build and release tools.

The image file for the different Erlang/OTP versions can be found within the subdirectories and are available through tags on the Docker Hub.

Latest Tools | Version
------------ | -------------
Base image | [phusion/baseimage:0.9.18](https://github.com/phusion/baseimage-docker/tree/6052c7a3e76fcb2aa16c15e39e5057dd8e7c2efb)
Erlang/OTP | 19.0
rebar | [2.6.1](https://github.com/rebar/rebar/tree/365ac649dc818619757f96a699ddb174f004cff9)
rebar3 | [3.2.0](https://github.com/erlang/rebar3/tree/2ffbb80cea3baf6763069319f089c078764edb59)
relx | [v3.19.0](https://github.com/erlware/relx/tree/1e15397a4924804f248facc18ccd07076baef7a4)

# Usage

Start a throw-away instance

```bash
docker run -it --rm synlay/erlang /bin/bash
```

Run a container to use as a development environment

```bash
docker run -it --name erlang-app synlay/erlang /bin/bash
```
