FROM phusion/baseimage:0.9.18

MAINTAINER David Robakowski <david.robakowski@synlay.com>

# Important!  Update this no-op ENV variable when this Dockerfile
# is updated with the current date. It will force refresh of all
# of the base images and things like `apt-get update` won't be using
# old cached versions when the Dockerfile is built.
ENV REFRESHED_AT 2015-07-21

ENV OTP_VERSION 17.5
ENV OTP_BUILD_CONFIGURE_OPTIONS --enable-hipe --enable-smp-support --enable-threads --enable-kernel-poll --enable-m64-build --with-ssl
ENV REBAR_VERSION 2.6.1
ENV RELX_VERSION v3.5.0

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

ENV DEBIAN_FRONTEND noninteractive
# Fix: erlexec: HOME must be set
ENV HOME /root

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# m4 = only needed for HiPE support
RUN DEBIAN_FRONTEND=noninteractive  \
	apt-get update -qq \
	&& apt-get install -y \
			build-essential=11.6\* \
			git=1:1.9.1\* \
			libncurses5-dev=5.9+20140118\* \
			openssl=1.0.1f\* \
			libssl-dev=1.0.1f\* \
			fop=1:1.1.dfsg\* \
			xsltproc=1.1.28\* \
			unixodbc-dev=2.2.14p2\* \
			m4=1.4.17\*

# Build OTP from source
RUN cd /usr/src \
	&& curl -SL http://erlang.org/download/otp_src_${OTP_VERSION}.tar.gz | tar zxf - \
	&& cd otp_src_${OTP_VERSION} \
	&& ./configure ${OTP_BUILD_CONFIGURE_OPTIONS} \
	&& make \
	&& make install \
	&& cd / && rm -rf /usr/src/otp_src_${OTP_VERSION}

# Building rebar
RUN cd /usr/src \
	&& curl -SL https://github.com/rebar/rebar/archive/${REBAR_VERSION}.tar.gz | tar zxf - \
	&& cd rebar-${REBAR_VERSION} \
	&& make \
	&& cp rebar /usr/bin/rebar \
	&& cd / && rm -rf /usr/src/rebar-${REBAR_VERSION}

# Building relx
RUN cd /usr/src \
	&& curl -SL https://github.com/erlware/relx/archive/${RELX_VERSION}.tar.gz | tar zxf - \
    && cd relx-* \
    && ./rebar3 update \
    && ./rebar3 escriptize \
    && cp _build/default/bin/relx /usr/bin/relx \
    && cd / && rm -rf /usr/src/relx-*

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
