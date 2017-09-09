# Data Science at the Command Line

FROM alpine:3.5
LABEL maintainer "Jeroen Janssens <jeroen@datascienceworkshops.com>"

RUN apk update

RUN apk --no-cache add \
    R \
    R-dev \
    R-doc \
    arpack-dev \
    bash \
    bash-doc \
    bc \
    bc-doc \
    cmake \
    coreutils \
    coreutils-doc \
    curl \
    curl-doc \
    curl-dev \
    findutils \
    findutils-doc \
    font-adobe-100dpi \
    g++ \
    git \
    git-doc \
    gnuplot \
    go \
    grep \
    grep-doc \
    groff \
    jpeg-dev \
    jq \
    jq-doc \
    less \
    less-doc \
    libxml2-dev \
    man \
    man-pages \
    mdocml-apropos \
    nodejs-lts \
    p7zip \
    p7zip-doc \
    parallel \
    parallel-doc \
    perl-dev \
    py-lxml \
    py-pip \
    python3 \
    python3-dev \
    sed \
    sed-doc \
    sudo \
    sudo-doc \
    tar \
    tar-doc \
    tree \
    tree-doc \
    unrar \
    unrar-doc \
    unzip \
    unzip-doc \
    xmlstarlet \
    xmlstarlet-doc

RUN echo "install.packages(c('tidyverse','ggmap'),repos='https://cloud.r-project.org')" | R --slave --no-save --no-restore-history

RUN easy_install-3.5 pip && \
    pip install --upgrade pip && \
    pip install \
    awscli \
    csvkit \
    nose

RUN pip2 install --upgrade pip && \
    pip2 install cssselect

RUN npm install -g \
    cowsay \
    json2csv \
    xml2json-command

RUN cd /tmp && \
    git clone https://github.com/jeroenjanssens/data-science-at-the-command-line.git && \
    cp -v data-science-at-the-command-line/tools/* /usr/bin/

RUN curl -sL http://bitbucket.org/eigen/eigen/get/3.2.9.tar.gz > /tmp/eigen.tar.gz && \
    cd \tmp && \
    mkdir eigen && tar -xzvf eigen.tar.gz -C eigen --strip-components=1 && \
    cd eigen && \
    mkdir build && cd build && cmake .. && make && make install

RUN cd /tmp && \
    git clone https://github.com/lisitsyn/tapkee.git && \
    cd tapkee && mkdir build && cd build && cmake .. && make && \
    cp -v /tmp/tapkee/bin/tapkee /usr/bin

RUN yes | cpan List::MoreUtils && \
    git clone https://github.com/dkogan/feedgnuplot.git && \
    cd feedgnuplot && \
    perl Makefile.PL && \
    make && \
    make install && \
    cd .. && \
    rm -r feedgnuplot

RUN export GOPATH=/usr && \
    go get github.com/ericchiang/pup

RUN rm -rf /tmp/* /var/cache/apk/*

RUN echo "export PAGER='less'" >>~/.bashrc && \
    echo "alias l='ls -lph --group-directories-first'" >>~/.bashrc && \
    echo "export PS1='\[\033[38;5;6m\][\w]$\[\033[38;5;15m\] '" >>~/.bashrc

WORKDIR /data
CMD bash
