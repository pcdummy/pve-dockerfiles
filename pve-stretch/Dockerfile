FROM pcdummy/stretch-systemd

ENV DEBIAN_FRONTEND noninteractive
ENV container docker

LABEL maintainer="rene@jochums.at"

# Fixup LVM2
RUN apt-get install -y lvm2 && echo "lvm2 hold" | dpkg --set-selections

# Add the pvetest repository
RUN apt-get -qq update && apt-get install -y wget && \
        wget http://download.proxmox.com/debian/proxmox-ve-release-5.x.gpg -O /etc/apt/trusted.gpg.d/proxmox-ve-release-5.x.gpg && \
        echo "deb http://download.proxmox.com/debian/pve stretch pvetest" > /etc/apt/sources.list.d/pvetest.list && \
        echo -e "127.0.0.1\tpvelocalhost" >> /etc/hosts && \
        apt-get -qq update && apt-get -qq dist-upgrade -y

# Install some packages from stretch-backports else we get errors
RUN apt-get install -y -t stretch-backports iptables iptables-dev ipset

# # Install all dev packages needed to build pve packages
RUN apt-get install -y build-essential git-core git-email debhelper \
                        autotools-dev autogen dh-autoreconf dkms doxygen check pkg-config \
                        groff quilt dpatch automake autoconf libtool lintian libdevel-cycle-perl \
                        libjson-perl libcommon-sense-perl liblinux-inotify2-perl libio-stringy-perl \
                        libstring-shellquote-perl dh-systemd rpm2cpio libsqlite3-dev sqlite3 \
                        libglib2.0-dev librrd-dev librrds-perl rrdcached libdigest-hmac-perl \
                        libxml-parser-perl gdb libcrypt-openssl-random-perl \
                        libcrypt-openssl-rsa-perl libnet-ldap-perl libauthen-pam-perl \
                        libjson-xs-perl libterm-readline-gnu-perl oathtool libmime-base32-perl \
                        liboath0 libpci-dev texi2html libsdl1.2-dev libgnutls28-dev \
                        libspice-protocol-dev xfslibs-dev libnuma-dev libaio-dev \
                        pve-libspice-server-dev libusbredirparser-dev glusterfs-common \
                        libusb-1.0-0-dev librbd-dev libpopt-dev iproute bridge-utils numactl \
                        glusterfs-common ceph-common python-ceph libgoogle-perftools4 \
                        libfile-chdir-perl glusterfs-client liblockfile-simple-perl \
                        libsystemd-dev libreadline-gplv2-dev libio-multiplex-perl \
                        libnetfilter-log-dev libipset3 socat libsasl2-dev libogg-dev \
                        python-pyparsing libfilesys-df-perl libcrypt-ssleay-perl \
                        libfile-readbackwards-perl libanyevent-perl libanyevent-http-perl \
                        unzip liblocale-po-perl libfile-sync-perl cstream \
                        lzop dtach apt-transport-https hdparm gdisk parted ttf-dejavu-core \
                        liblzma-dev dosfstools mtools libxen-dev libfuse-dev corosync-dev \
                        libcpg-dev libquorum-dev libcmap-dev libuuid-perl \
                        libqb-dev libapparmor-dev docbook2x libcap-dev dh-apparmor \
                        graphviz libseccomp-dev libglib-perl libgtk3-perl libnss3-dev libdlm-dev \
                        libudev-dev asciidoc-dblatex source-highlight inkscape \
                        libiscsi-dev libiscsi7 libssl-dev flex bc libtest-mockmodule-perl \
                        libjpeg-dev libpixman-1-dev libjemalloc-dev acpica-tools nasm unifont \
                        help2man libpam0g-dev node-es6-module-transpiler librsvg2-bin \
                        asciidoc libnet1-dev libnl-3-dev libprotobuf-c-dev libprotobuf-dev \
                        protobuf-c-compiler protobuf-compiler \
                        cm-super-minimal libatm1-dev libdb-dev libmnl-dev linuxdoc-tools \
                        dh-exec libdbus-1-dev librdmacm-dev libsnmp-dev libstatgrab-dev libxml2-dev bison \
                        initramfs-tools python-all dctrl-tools bash-completion

# Install pve packages which are needed to build new pve packages
RUN apt-get install -y pve-manager pve-qemu-kvm qemu-server spiceterm vncterm && \
        rm -f /etc/apt/sources.list.d/pve-enterprise.list

CMD ["/lib/systemd/systemd"]