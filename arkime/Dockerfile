#
# NOTE:
#   as of Feb-2021, v2.7.1 is the latest tag.
#   So, here, do "git checkout refs/tags/v2.7.1"
#   you can do just "git checkout master" whenever you want.
#
FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
apt-get install -y lsb-release ruby-dev make python3-pip git libtest-differences-perl sudo wget apt-utils tzdata && \
(cd /tmp && wget https://packages.ntop.org/apt-stable/20.04/all/apt-ntop-stable.deb && dpkg -i apt-ntop-stable.deb) && \
apt-get update && \
apt-get install -y pfring && \
gem install --no-document fpm && \
pip3 install awscli && \
git clone https://github.com/arkime/arkime && \
(cd arkime; git checkout refs/tag/v2.7.1; ./easybutton-build.sh --daq --pfring --install) && \
rm -rf arkime && \
rm -rf /var/lib/apt/lists/*

#
# NOTE:
#   bin/Configure with no CLI doesn't work as it is.
#   Here fix this problem.
#
ENV ARKIME_INSTALL_DIR=/opt/arkime
ENV ARKIME_INTERFACE=eth0
ENV ARKIME_ELASTICSEARCH=http://eshost:9200
ENV ARKIME_PASSWORD=admin
ENV ARKIME_LOCALELASTICSEARCH=no
ENV ARKIME_INET=yes

RUN cat /opt/arkime/bin/Configure | \
sed -e '/ARKIME_LOCALELASTICSEARCH=not-set/d' \
    -e '/ARKIME_INET=not-set/d' > .tmp && chmod u+x .tmp && \
mv .tmp /opt/arkime/bin/Configure && \
rm -f /opt/arkime/etc/config.ini && \
/opt/arkime/bin/Configure

