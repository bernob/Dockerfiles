##########################################

# Dockerfile to build Ubuntu:14.04 + LaTeX

# full distribution + GUI tools image

##########################################

# From inside this folder
# docker build -t jorgeluisrmx/latexide
# From DockerHub
# docker pull jorgeluisrmx/latexide
# Basic run
# docker run -it -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY -v /dev/snd:/dev/snd -v /home/phantom/Documents:/home/latexide --privileged jorgeluisrmx/latexide

FROM jorgeluisrmx/ubuntu-dev-base
MAINTAINER jorgeluisrmx "jorgeluisrmx@gmail.com"

# Installing TeXLive full and aspell

RUN apt-get update
RUN apt-get install -y texlive-full
RUN apt-get install -y \
    texlive-latex-extra \
    aspell \
    aspell-es \
    spellutils \
    ispell

# Installing GUI utilities

RUN apt-get install -y \
    kile \
    lyx \
    qtikz \
    xfig

# Creating the home directory

RUN mkdir ~/latexide
ENV HOME ~/latexide
WORKDIR $HOME


