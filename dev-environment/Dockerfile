# syntax=docker/dockerfile:1.3.1

FROM ubuntu:latest

RUN apt-get update -y \
    && apt-get install -y software-properties-common \
    && apt-get update -y

RUN rm -f /etc/apt/apt.conf.d/docker-clean \
    && apt-get update \
    && apt-get install -y \
        bash-completion \
	curl \
	gcc \
	g++ \
	git \
	libssl-dev \
	make \
        pkg-config \
	sudo \
        tree \
        unzip \
        vim \
        wget

# non-root ubuntu user
ARG USER=ubuntu
ARG GROUP=ubuntu
ARG UID=1000
ARG GID=1000

ENV HOME="/home/$USER" \
    USER=$USER \
    GROUP=$GROUP \
    UID=$UID \
    GID=$GID

WORKDIR $HOME
USER $USER

RUN mkdir $HOME/repo \
    && mkdir $HOME/.config \
    && mkdir -p $HOME/.local/bin \
    && mkdir $HOME/bash_history

ENV HISTFILE=$HOME/bash_history/.bash_history \
    HISTTIMEFORMAT='%F %T - ' \
    TZ="Australia/Brisbane"

# Touch the ~/.bash_history file, otherwise docker will create it as a directory
#RUN touch $HOME/.bash_history \
#    && chmod 600 $HOME/.bash_history

# Install the latest stable noevim release
# Note that I don't really know if this is necessary anymore
ENV NVIM_VERSION="0.11.4"
RUN wget https://github.com/neovim/neovim/releases/download/v$NVIM_VERSION/nvim-linux-x86_64.tar.gz -O /tmp/nvim.tar.gz \
    && tar xzvf /tmp/nvim.tar.gz -C $HOME \
    && ln -s $HOME/nvim-linux-x86_64/bin/nvim $HOME/.local/bin/nvim \
    && rm /tmp/nvim.tar.gz

ENV PATH=$PATH:$HOME/.local/bin

CMD ["sleep", "infinity"]
