## Use Ubuntu base image
FROM registry.gitlab.com/gbe0/utility-containers/ubuntu-python:latest

## Install Python
RUN echo \
      ### Install language servers and other utilities for vscode extensions to work
      && DEBIAN_FRONTEND="noninteractive" apt-get -q -y install \
        #### Python
        python3 python3-venv \
      ### Set default python version to 3
      && update-alternatives --install /usr/bin/python python /usr/bin/python3 1 \
      ### Run the Conda install script
      && wget -qO /tmp/miniconda-install.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
      && bash /tmp/miniconda-install.sh -b -p /root/conda \
      && rm -f /tmp/miniconda-install.sh \
      ### Upgrade conda
      && /root/conda/bin/conda update conda -q -y \
      ### Setup shell
      && /root/conda/bin/conda init bash \
      && /root/conda/bin/conda init zsh \
      ### Don't enable conda environment by default
      && /root/conda/bin/conda config --set auto_activate_base false

## Add zsh configuration file that includes conda plugin
COPY .zshrc /root/.zshrc

## Install Conda environments
RUN echo \
      ### Main python env
      && /root/conda/bin/conda create -q -y -n python3.10 python=3.10 \
      ### PyPy3
      && /root/conda/bin/conda config --add channels conda-forge \
      && /root/conda/bin/conda config --set channel_priority strict \
      && /root/conda/bin/conda create -q -y -n pypy3 pypy

## Install additional oh-my-zsh plugins
RUN echo \
      && git clone https://github.com/esc/conda-zsh-completion /root/.oh-my-zsh/custom/plugins/conda-zsh-completion