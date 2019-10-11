FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
    && apt-get install -y \
        build-essential \
        openssl \
        libxml2-dev \
        libncurses5-dev \
        uuid-dev \
        sqlite3 \
        libsqlite3-dev \
        pkg-config \
        libjansson-dev \
        libssl-dev \
        curl \
        msmtp

# Asterisk expects /usr/sbin/sendmail
RUN ln -s /usr/bin/msmtp /usr/sbin/sendmail

RUN apt-get update \
    && apt-get install libsrtp0 -y

ENV ASTERISK_VERSION 14.5.0
RUN cd /tmp && curl -o asterisk.tar.gz http://downloads.asterisk.org/pub/telephony/asterisk/releases/asterisk-${ASTERISK_VERSION}.tar.gz \
    && tar xzf asterisk.tar.gz
RUN cd /tmp/asterisk* \
    && ./configure --with-pjproject-bundled --with-crypto --with-ssl \
    && make \
    && make install \
    && make samples \
    && make config

CMD asterisk -fvvv

