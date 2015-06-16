#############################################

# Dockerfile to build Ubuntu:14.04 + openFOAM

# + C/C++, Python dev libs image

#############################################

# From inside this folder
# docker build -t jorgeluisrmx/openfoam
# From DockerHub
# docker pull jorgeluisrmx/openfoam
# Basic run
# docker run -it jorgeluisrmx/openfoam /bin/bash

FROM jorgeluisrmx/ubuntu-dev-base
MAINTAINER jorgeluisrmx "jorgeluisrmx@gmail.com"

# Downloading source code
RUN mkdir ~/OpenFOAM
WORKDIR ~/OpenFOAM/

# OpenFOAM
RUN wget http://downloads.sourceforge.net/foam/OpenFOAM-2.3.1.tgz?use_mirror=mesh
RUN mv OpenFOAM-2.3.1.tgz?use_mirror=mesh OpenFOAM-2.3.1.tgz
RUN tar xzf OpenFOAM-2.3.1.tgz
RUN rm OpenFOAM-2.3.1.tgz

# Third-Party
RUN wget http://downloads.sourceforge.net/foam/ThirdParty-2.3.1.tgz?use_mirror=mesh
RUN mv ThirdParty-2.3.1.tgz?use_mirror=mesh ThirdParty-2.3.1.tgz
RUN tar xzf ThirdParty-2.3.1.tgz
RUN rm ThirdParty-2.3.1.tgz 

# Dependencies

RUN apt-get install -y flex
RUN apt-get install -y bison
RUN apt-get install -y zlib1g-dev
RUN apt-get install -y libopenmpi-dev
RUN apt-get install -y openmpi-bin
RUN apt-get install -y qt4-dev-tools
RUN apt-get install -y libqt4-dev
RUN apt-get install -y libqt4-opengl-dev
RUN apt-get install -y freeglut3-dev
RUN apt-get install -y libqtwebkit-dev
RUN apt-get install -y gnuplot
RUN apt-get install -y libreadline-dev
RUN apt-get install -y libncurses-dev
RUN apt-get install -y libxt-dev
RUN apt-get install -y libscotch-dev
RUN apt-get install -y libcgal-dev  

# Setting environment variables
RUN echo 'source $HOME/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc' >> $HOME/.bashrc
RUN source $HOME/.bashrc 

# Building the Sources
WORKDIR $WM_PROJECT_DIR
RUN ./Allwmake

# Compiling Paraview and the Paraview Reader Module
WORKDIR $WM_THIRD_PARTY_DIR

# replacing time make for make in $WM_THIRD_PARTY_DIR/makeCmake to avoid compilation error
# the command is
# 
#   sed -i 's/original/new/g' file.txt
# Explanation:
# sed = Stream EDitor
# -i = in-place (i.e. save back to the original file)
# The command string:
# s = the substitute command
# original = a regular expression describing the word to replace (or just the word itself)
# new = the text to replace it with
# g = global (i.e. replace all and not just the first occurrence)
# file.txt = the file name
RUN sed -i 's/time make/make/g' makeCmake

RUN ./makeCmake
RUN wmSET

WORKDIR $WM_THIRD_PARTY_DIR 
RUN ./makeParaView4

WORKDIR $FOAM_UTILITIES/postProcessing/graphics/PV4Readers 
RUN wmSET
RUN ./Allwclean
RUN ./Allwmake

# gmsh installation

RUN mkdir ~/gMsh
WORKDIR ~/gMsh
RUN wget http://geuz.org/gmsh/bin/Linux/gmsh-2.9.2-Linux64.tgz
RUN tar -xzvf gmsh-2.9.2-Linux64.tgz
RUN rm gmsh-2.9.2-Linux64.tgz
RUN ln -s ~/gMsh/gmsh-2.9.2-Linux/bin/gmsh /usr/bin/gmsh

