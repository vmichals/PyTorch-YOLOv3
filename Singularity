BootStrap: docker
From: ubuntu:18.04

%post
    apt -y update
    apt -y upgrade

    DEBIAN_FRONTEND=noninteractive apt install -y keyboard-configuration \
    rsync build-essential libffi-dev libssl-dev libhdf5-dev \
    git vim sudo software-properties-common wget unzip

    apt clean
    rm -rf /var/lib/apt/lists/*

    # install miniconda
    if [ ! -d /opt/conda ]; then
        wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
        bash ~/miniconda.sh -b -p /opt/conda
        rm ~/miniconda.sh
    fi
    # set conda path
    export PATH="/opt/conda/bin:$PATH"

    conda install python==3.6.9
    conda install ipython matplotlib numpy tqdm pip pillow tensorboard
    conda install pytorch torchvision cudatoolkit=10.1 -c pytorch

    pip --no-cache-dir install terminaltables

    conda clean --all -y

# Export global environment variables
%environment
    export PATH=/opt/conda/bin:$PATH
    export LC_ALL=C.UTF-8
    export SHELL=/bin/sh

%runscript
    exec /bin/sh "$@"
