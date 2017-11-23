FROM phusion/baseimage:0.9.22

MAINTAINER David Robakowski <david.robakowski@synlay.com>

# Important!  Update this no-op ENV variable when this Dockerfile
# is updated with the current date. It will force refresh of all
# of the base images and things like `apt-get update` won't be using
# old cached versions when the Dockerfile is built.
ENV REFRESHED_AT 2017-11-23

ENV OTP_VERSION 20.1
ENV OTP_BUILD_CONFIGURE_OPTIONS --enable-hipe --enable-smp-support --enable-threads --enable-kernel-poll --enable-m64-build --with-ssl
ENV REBAR_VERSION 2.6.4
ENV REBAR3_VERSION 3.4.7

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
	&& apt-get --only-upgrade -qq install gnupg libgcrypt20 openssh-client \
	    openssh-server openssh-sftp-server \
	&& apt-get install -y \
			build-essential=12.1\* \
			git=1:2.7\* \
			libncurses5-dev=6.0+20160213\* \
			openssl=1.0.2g\* \
			libssl-dev=1.0.2g\* \
			fop=1:2.1\* \
			xsltproc=1.1.28\* \
			unixodbc-dev=2.3.1\* \
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

# Building rebar3
RUN cd /usr/src \
	&& curl -SL https://github.com/rebar/rebar3/archive/${REBAR3_VERSION}.tar.gz | tar zxf - \
	&& cd rebar3-${REBAR3_VERSION} \
	&& ./bootstrap \
	&& cp rebar3 /usr/bin/rebar3 \
	&& cd / && rm -rf /usr/src/rebar3-${REBAR3_VERSION}

# Building relx
RUN cd /usr/src \
    && mkdir relx \
    && cp /root/.cache/rebar3/hex/default/packages/relx-* relx \
    && cd relx \
    && tar -xf relx-* \
    && tar -zxf contents.tar.gz \
    && /usr/bin/rebar3 update \
    && /usr/bin/rebar3 as escript escriptize \
    && chmod a+x _build/escript/bin/relx \
    && mv _build/escript/bin/relx /usr/bin/relx \
    && cd / && rm -rf /usr/src/relx

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
