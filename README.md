
# Setup
## 1) Install repo
On Debian/Ubuntu:
    
    $ sudo apt-get install repo
    
Or, install manually:
    
    $ mkdir -p ~/.bin
    $ PATH="${HOME}/.bin:${PATH}"
    $ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo
    $ chmod a+rx ~/.bin/repo


## 2) Install git lfs (if using lfs for hosted binaries)

    $ curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
    $ sudo apt-get install git-lfs
    $ git lfs install
    
## 3) Initialize and Sync (Use NVIDIA Jetpack to download binaries)

    $ mkdir sol
    $ cd sol
    $ repo init -u https://github.com/SOL-Space-Operating-Linux/repo-manifest.git
    $ repo sync

This will require to make an NVIDIA developer account. Once created download the NVIDIA SDK Manager program and download the required sdk's for your device with version 4.3 of the Jetpack. When downloaded, there should be 40+ .deb packages generally dealing with nvidia, cuda, lib*, OpenCV, etc.

Download the correct packages next to poky-tx2i
    $ mkdir nvidia-sdk-binaries
    $ <Manually download packages to> ./nvidia-sdk-binaries/*

## 3 alternative) Initialize and Sync (UGA hosted binaries path)

    $ mkdir sol
    $ cd sol
    $ repo init -u https://github.com/SOL-Space-Operating-Linux/repo-manifest.git -i uga_hosted_nvidia_binaries_manifest.xml
    $ repo sync
    $ repo forall -c git lfs pull

## Setup OE Environment

    $ sudo apt install gawk wget git-core diffstat unzip texinfo gcc-multilib \
        build-essential chrpath socat libsdl1.2-dev xterm
    $ cd poky-tx2i
    $ . ./oe-init-build-env
    $ cd conf
    $ cp ../../../.repo/manifests/bblayers.conf.template bblayers.conf
    $ cp ../../../.repo/manifests/local.conf.template local.conf

## Build SOL image

    $ bitbake core-image-sol



