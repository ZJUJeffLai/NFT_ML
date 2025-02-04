# FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04
FROM nvidia/cuda:11.5.1-cudnn8-devel-ubuntu20.04
ENV DEBIAN_FRONTEND noninteractive

RUN apt update && apt install -y tcl
#########################################
# SECTION 1: Essentials                 #
#########################################
RUN apt-get update && apt-get install -y --no-install-recommends \
    vim git curl wget yasm cmake unzip pkg-config \
    checkinstall build-essential ca-certificates \
    software-properties-common apt-utils bash-completion \
  && apt-get upgrade -y \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

#########################################
# SECTION 2: Setup Image Libraries      #
#########################################
RUN apt-get update && apt-get install -y --no-install-recommends \
    zlib1g-dev libjpeg-dev libpng-dev xvfb ffmpeg xorg-dev \
    xorg-dev libboost-all-dev libsdl2-dev swig \
    libblas-dev liblapack-dev \
    libopenblas-base libatlas-base-dev graphviz \
    libvips \
  && apt-get upgrade -y \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

#########################################
# SECTION 3: Install Python Libraries   #
#########################################
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip

# Upgrade pip
RUN python3 -m pip install --upgrade pip

# Install Python libraries
RUN apt-get update && apt-get install -y \
    --no-install-recommends libvips libvips-dev
RUN apt-get -y upgrade

RUN pip3 install pip --upgrade
RUN pip3 install -U numpy cython ipython \
    jupyter matplotlib pandas scikit-learn \
    scikit-image scipy tqdm pyvips 
    

RUN pip3 install torch==1.4.0 torchvision==0.5.0

RUN pip3 install -U opencv-python



# Install jupyter notebook extensions (code folding)
RUN pip3 install jupyter_contrib_nbextensions \
  && jupyter contrib nbextension install \
  && pip3 install jupyter_nbextensions_configurator \
  && jupyter nbextensions_configurator enable

# Install argcomplete for auto tab completing argparse in Python
RUN pip3 install argcomplete \
  && activate-global-python-argcomplete

######################################
# SECTION 4: Additional Utilities    #
######################################
RUN echo "export PATH=$PATH:~/.local/bin/" >> /root/.bashrc
RUN apt update && apt -y upgrade

WORKDIR /root/NFT_Project

######################################
# SECTION 5: Add running instruction #
######################################
RUN echo "echo -e \"\n\"" >> /root/.bashrc
RUN echo "echo -e \"################################################################################\n\"" >> /root/.bashrc
RUN echo "echo -e \"\tCommand to enter repository:\n\t\tcd /root/NFT_Project && jupyter notebook --no-browser --ip=0.0.0.0 --allow-root --port=9000 &\n\"" >> /root/.bashrc
RUN echo "echo -e \"################################################################################\n\"" >> /root/.bashrc
