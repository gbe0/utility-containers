## Base on Ubuntu Jammy
FROM ubuntu:jammy

## Set maintainer label
LABEL maintainer="Chris <git@gbe0.com>"

## Configure the default apt mirror for package installations
ARG APT_MIRROR="http://archive.ubuntu.com/ubuntu/"

## Configure LANG, LC_ALL and LANGUAGE environment vars to prevent various errors
ENV LANG="C.UTF-8" LC_ALL="C.UTF-8" LANGUAGE="C.UTF-8"

## Set env variable to make git easier to work with when using SSH
ENV GIT_SSH_COMMAND="ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no"

## Update sources list and run system upgrade
RUN echo \
      ### Update current sources list and install lsb_release and gpg utility
      && apt-get update \
      && DEBIAN_FRONTEND="noninteractive" apt-get -q -y install \
        lsb-release gpgv \
      ### Configure package sources list
      && echo "deb ${APT_MIRROR} $(lsb_release -sc) main restricted" > /etc/apt/sources.list \
      && echo "deb ${APT_MIRROR} $(lsb_release -sc)-updates main restricted" >> /etc/apt/sources.list \
      && echo "deb ${APT_MIRROR} $(lsb_release -sc) universe" >> /etc/apt/sources.list \
      && echo "deb ${APT_MIRROR} $(lsb_release -sc)-updates universe" >> /etc/apt/sources.list \
      && echo "deb ${APT_MIRROR} $(lsb_release -sc) multiverse" >> /etc/apt/sources.list \
      && echo "deb ${APT_MIRROR} $(lsb_release -sc)-updates multiverse" >> /etc/apt/sources.list \
      && echo "deb ${APT_MIRROR} $(lsb_release -sc)-backports main restricted universe multiverse" >> /etc/apt/sources.list \
      && echo "deb ${APT_MIRROR} $(lsb_release -sc)-proposed main restricted universe multiverse" >> /etc/apt/sources.list \
      && echo "deb http://archive.canonical.com/ubuntu $(lsb_release -sc) partner" >> /etc/apt/sources.list \
      && echo "deb http://security.ubuntu.com/ubuntu/ $(lsb_release -sc)-security main restricted" >> /etc/apt/sources.list \
      && echo "deb http://security.ubuntu.com/ubuntu/ $(lsb_release -sc)-security universe" >> /etc/apt/sources.list \
      && echo "deb http://security.ubuntu.com/ubuntu/ $(lsb_release -sc)-security multiverse" >> /etc/apt/sources.list \
      ### To add source package lists, uncomment the below lines
      # && echo "deb-src ${APT_MIRROR} $(lsb_release -sc) main restricted" >> /etc/apt/sources.list \
      # && echo "deb-src ${APT_MIRROR} $(lsb_release -sc)-updates main restricted" >> /etc/apt/sources.list \
      # && echo "deb-src ${APT_MIRROR} $(lsb_release -sc) universe" >> /etc/apt/sources.list \
      # && echo "deb-src ${APT_MIRROR} $(lsb_release -sc)-updates universe" >> /etc/apt/sources.list \
      # && echo "deb-src ${APT_MIRROR} $(lsb_release -sc) multiverse" >> /etc/apt/sources.list \
      # && echo "deb-src ${APT_MIRROR} $(lsb_release -sc)-updates multiverse" >> /etc/apt/sources.list \
      # && echo "deb-src ${APT_MIRROR} $(lsb_release -sc)-backports main restricted universe multiverse" >> /etc/apt/sources.list \
      # && echo "deb-src ${APT_MIRROR} $(lsb_release -sc)-proposed main restricted universe multiverse" >> /etc/apt/sources.list \
      # && echo "deb-src http://archive.canonical.com/ubuntu $(lsb_release -sc) partner" >> /etc/apt/sources.list \
      # && echo "deb-src http://security.ubuntu.com/ubuntu/ $(lsb_release -sc)-security main restricted" >> /etc/apt/sources.list \
      # && echo "deb-src http://security.ubuntu.com/ubuntu/ $(lsb_release -sc)-security universe" >> /etc/apt/sources.list \
      # && echo "deb-src http://security.ubuntu.com/ubuntu/ $(lsb_release -sc)-security multiverse" >> /etc/apt/sources.list \
      ### Update package cache
      && apt-get update \
      ### Perform full system upgrade
      && DEBIAN_FRONTEND="noninteractive" apt-get -q -y dist-upgrade \
      ### Install useful command line utilities
      && DEBIAN_FRONTEND="noninteractive" apt-get -q -y install \
        vim neovim less strace curl wget screen telnet git tmux dnsutils jq net-tools \
        iputils-ping bash-completion sudo tcptraceroute \
      ### Install zsh
      && DEBIAN_FRONTEND="noninteractive" apt-get -q -y install \
        zsh zsh-syntax-highlighting \
      ### Create nvim and SSH config directories
      && mkdir -p /root/.config/nvim /root/.ssh

## Add editor configuration files
COPY .vimrc /root/.vimrc
COPY init.vim /root/.config/nvim/init.vim

## Add the zsh configuration file
COPY .zshrc /root/.zshrc

## Add the tmux configuration file
COPY .tmux.conf /root/.tmux.conf

## Add the SSH config
COPY ssh_config /root/.ssh/config

## Install oh-my-zsh
RUN echo \
      && bash -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

## Change default shell to zsh
SHELL ["/bin/zsh", "-c"]
ENTRYPOINT ["/bin/zsh"]