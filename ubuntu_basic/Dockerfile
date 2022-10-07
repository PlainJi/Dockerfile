From ubuntu:20.04

LABEL org.opencontainers.image.description="Ubuntu 22.04 with basic environment & tools" \
      org.opencontainers.image.authors="Plain Ji" \
      org.opencontainers.image.documentation="https://hub.docker.com/r/plainji/ubuntu20.04" \
      org.opencontainers.image.source="https://github.com/plainji/Dockerfiles"

ENV DEBIAN_FRONTEND=noninteractive

ARG SOURCES_FILE=/etc/apt/sources.list

    # change host name
RUN apt update && \
    # install ca
    apt install -y ca-certificates && \
    # replace apt sources
    > $SOURCES_FILE && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse" >> $SOURCES_FILE && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse" >> $SOURCES_FILE && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse" >> $SOURCES_FILE && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse" >> $SOURCES_FILE && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse" >> $SOURCES_FILE && \
    # install some basic tools
    apt update && \
    # `add-apt-repository` add pgp key tool
    apt install -y apt-utils software-properties-common apt-transport-https gnupg \
        # system
        sudo vim bash-completion lsb-release \
        # network tools
        wget curl git \
        net-tools iputils-ping ethtool netcat tcpdump iperf3 lsof \
        # system monitor tools
        cpanminus dstat htop nmon \
        # security tools
        libssl-dev openssh-client openssh-server openssh-sftp-server nfs-common rsync \
        # compress/uncompress tools
        unzip unrar \
        # build tools
        build-essential && \
    # install zsh and oh my zsh
    echo "185.199.108.133	raw.githubusercontent.com" >> /etc/hosts && \
    apt install -y zsh && \
        sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" "" --skip-chsh && \
        echo "setopt no_nomatch" >> /root/.zshrc && \
    # install python3.9
    add-apt-repository ppa:deadsnakes/ppa && \
    apt install -y python3.9 python3-pip ipython3 && \
    pip3 install --upgrade pip && \
    # anto remove unused
    apt-get autoremove -y

WORKDIR /root

CMD ["/bin/bash"]
