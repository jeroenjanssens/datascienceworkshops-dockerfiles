# Data Science at the Command Line

FROM alpine:3.8
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
    boost-dev \
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
    m4 \
    man \
    man-pages \
    mdocml-apropos \
    ncurses \
    nodejs-lts \
    nodejs-npm \
    openjdk7 \
    openssl \
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
    xmlstarlet-doc \
    zlib-dev

RUN echo "install.packages(c('tidyverse','ggmap'),repos='https://cloud.r-project.org')" | R --slave --no-save --no-restore-history

RUN easy_install-3.6 pip && \
    pip3 install --upgrade pip && \
    pip3 install \
    awscli \
    bigmler \
    csvkit \
    numpy \
    scipy \
    nose

RUN pip3 install skll

RUN pip2 install --upgrade pip && \
    pip2 install cssselect

RUN npm install -g \
    cowsay \
    xml2json-command

# tapkee
RUN curl -sL http://bitbucket.org/eigen/eigen/get/3.2.9.tar.gz > /tmp/eigen.tar.gz && \
    cd \tmp && \
    mkdir eigen && tar -xzvf eigen.tar.gz -C eigen --strip-components=1 && \
    cd eigen && \
    mkdir build && cd build && cmake .. && make && make install

RUN cd /tmp && \
    git clone https://github.com/lisitsyn/tapkee.git && \
    cd tapkee && mkdir build && cd build && cmake .. && make && \
    cp -v /tmp/tapkee/bin/tapkee /usr/bin


# feedgnuplot
RUN yes | cpan List::MoreUtils && \
    git clone https://github.com/dkogan/feedgnuplot.git && \
    cd feedgnuplot && \
    perl Makefile.PL && \
    make && \
    make install && \
    cd .. && \
    rm -r feedgnuplot

# pup
RUN export GOPATH=/usr && \
    go get github.com/ericchiang/pup && \
    go get github.com/jehiah/json2csv


# csvfix
RUN curl https://bitbucket.org/neilb/csvfix/get/version-1.6.zip > /tmp/csvfix.zip && \
    cd /tmp && \
    unzip csvfix.zip && \
    mv neilb* csvfix && \
    cd csvfix && \
    make lin && \
    mv csvfix/bin/csvfix /bin


# weka
RUN cd /tmp && \
    curl -L https://sourceforge.net/projects/weka/files/weka-3-8/3.8.1/weka-3-8-1.zip > weka.zip && \
    unzip weka.zip && \
    mv weka-3-8-1/weka.jar /bin


# curlicue
RUN cd /tmp &&\
    curl -L https://github.com/decklin/curlicue/archive/master.zip > curlicue.zip && \
    unzip curlicue.zip && \
    mv curlicue-master/curl* /bin


# drake and drip
RUN curl -L https://raw.githubusercontent.com/Factual/drake/master/bin/drake > /usr/bin/drake && \
    chmod 755 /usr/bin/drake
RUN SHELL=/bin/bash drake; exit 0
ENV JAVA_HOME=/usr/lib/jvm/default-jvm
RUN ln -sf "${JAVA_HOME}/bin/"* "/usr/bin/"
RUN curl -L https://raw.githubusercontent.com/ninjudd/drip/master/bin/drip > /usr/bin/drip && \
    chmod 755 /usr/bin/drip && \
    drip; exit 0


# csvquote
RUN cd /tmp && \
    git clone https://github.com/dbro/csvquote.git && \
    cd csvquote && \
    make && make BINDIR=/usr/bin/ install


# vowpal wabbit
RUN cd /tmp && \
    git clone --depth 1 --branch master --single-branch git://github.com/JohnLangford/vowpal_wabbit.git && \
    cd vowpal_wabbit && \
    make && \
    make install


# crush tools
RUN cd /tmp && \
    curl -L https://github.com/google/crush-tools/releases/download/20150716/crush-tools-20150716.tar.gz > crush-tools.tar.gz && \
    tar -xzvf crush-tools.tar.gz && \
    cd crush-tools-20150716/ && \
    sed -i '12i#include <sys/types.h>' src/fieldsplit/fieldsplit.c && \
    ./configure --prefix=/usr && \
    make && \
    make install


# data science at the command line tools, book content, and example data
RUN cd /tmp && \
    git clone https://github.com/jeroenjanssens/data-science-at-the-command-line.git && \
    cp -v data-science-at-the-command-line/tools/* /usr/bin/ && \
    cp -rv data-science-at-the-command-line/data /home/ && \
    cp -rv data-science-at-the-command-line/book /home/


RUN rm -rf /tmp/* /var/cache/apk/*

RUN echo "export PAGER='less'" >>~/.bashrc && \
    echo "export SHELL='/bin/bash'" >>~/.bashrc && \
    echo "alias l='ls -lph --group-directories-first'" >>~/.bashrc && \
    echo "alias parallel='parallel --will-cite'" >>~/.bashrc && \
    echo 'export PS1="\[\033[38;5;6m\][\w]$\[$(tput sgr0)\] "' >>~/.bashrc

RUN cat $(which weka) | sed -ne '/WEKAPATH=/,/complete /p' | cut -c3- | sed -e 's|/home/joe||' >>~/.bashrc

RUN apk --no-cache add msttcorefonts-installer fontconfig && \
    update-ms-fonts && fc-cache -f
RUN rm -rf /tmp/* /var/cache/apk/*

WORKDIR /data
CMD bash
