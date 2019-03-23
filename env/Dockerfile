## PyRosetta Jupyter Environment
#
# Installation and Usage:
#   - Go to http://www.pyrosetta.org/ and request a license
#   - Download the latest PyRosetta4.Release.python36.ubuntu release and put it in 
#     the same directory as this Dockerfile
#   - Build the container, using
#       docker build -t pyro .
#   - Run the container using 
#       docker run -v $PWD:/home -p 8888:8888 -it pyro
#   - Look at the output. It will show something like:
#       http://(11d8ad1130ba or 127.0.0.1):8888/?token=9b45383a1bac13dbc3be82dbba95430d4841f2e96d321b97
#   - In this case, you would open a notebook via:
#       http://localhost:8888/?token=9b45383a1bac13dbc3be82dbba95430d4841f2e96d321b97
#

FROM ubuntu:bionic

RUN apt-get update && \
    apt-get install -y python3 && \
    apt-get install -y python3-pip && \
    apt-get install -y git && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y pymol

WORKDIR /usr/src

COPY PyRosetta4.Release.python36.ubuntu.release-214.tar.bz2 .

# Extract
RUN tar -xvjf PyRosetta4.Release.python36.ubuntu.release-214.tar.bz2 && \
    rm PyRosetta4.Release.python36.ubuntu.release-214.tar.bz2 
  
# Install
RUN cd PyRosetta4.Release.python36.ubuntu.release-214/setup/ && \
    python3 setup.py install

RUN pip3 install jupyter
RUN pip3 install numpy
RUN pip3 install matplotlib    
RUN pip3 install git+https://github.com/ocramz/ipymol.git@python3

EXPOSE 8888

WORKDIR /home

CMD ["jupyter","notebook", "--ip=0.0.0.0", "--allow-root"]