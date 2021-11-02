Bootstrap: docker
From: ubuntu:20.04
IncludeCmd: yes

%environment
export LC_ALL=C
export PATH=$PATH:/opt/software/miniconda3/bin:/opt/software/eggnog-mapper:/opt/software/eggnog-mapper/bin

%post
  apt-get update
  apt-get install -y apt-transport-https apt-utils software-properties-common
  apt-get install -y add-apt-key
  export DEBIAN_FRONTEND=noninteractive
  ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime
  apt-get install -y tzdata
  dpkg-reconfigure --frontend noninteractive tzdata

  apt-get install -y wget python3-pip git

  mkdir -p /opt/software

  wget -q https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh 
  bash Miniconda3-latest-Linux-x86_64.sh -b -p /opt/software/miniconda3
  rm -f Miniconda3-latest-Linux-x86_64.sh

  /opt/software/miniconda3/bin/conda install -y -c conda-forge -c bioconda diamond prodigal hmmer cd-hit 'pip<=20.2.1'

  # install eggnog-mapper
  cd /opt/software
  git clone https://github.com/eggnogdb/eggnog-mapper.git
  cd eggnog-mapper
  git log -1
  # /opt/software/miniconda3/bin/conda install --file requirements.txt
  pip install -r requirements.txt

  # install macsyfinder
  cd /opt/software
  git clone https://github.com/gem-pasteur/macsyfinder.git
  cd macsyfinder
  pip install .
  
  ## blargh
