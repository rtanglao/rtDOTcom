---

layout: post
title: "RStudio build script changes: changed from JDK7 to JDK 8, bionic from debian"
---

# Pontifications

* Regarding yesterday's [Successfully compiled ARM64 Windows 10 R Studio Server v1.2.5001 on Lenovo C630](http://rolandtanglao.com/2019/10/15/p1-compiled-rstudio-server-v1-2-5001-Lenovo-C630-ARM64-Windows-10/), here are the changes to the build script, [build_rstudio.sh](https://github.com/rtanglao/ARM-rstudio-server/blob/master/build_rstudio.sh):
* 1. [changed version number](https://github.com/rtanglao/ARM-rstudio-server/blob/master/build_rstudio.sh#L9) to  `1.2.4001` i.e. `VERS=v1.2.5001`. This will have to change when others build RStudio because new versions come out all the time
  2. [changed to jdk 8](https://github.com/rtanglao/ARM-rstudio-server/blob/master/build_rstudio.sh#L19): i.e. `sudo apt-get install -y openjdk-8-jdk`
     * because only java 8 is supported [https://github.com/rstudio/rstudio/issues/3157](https://github.com/rstudio/rstudio/issues/3157) ; see also: [https://github.com/rstudio/rstudio/wiki/Installing-RStudio-Dependencies](https://github.com/rstudio/rstudio/wiki/Installing-RStudio-Dependencies)
  3. [changed to use the ubuntu bionic install dependencies script](https://github.com/rtanglao/ARM-rstudio-server/blob/master/build_rstudio.sh#L21) i.e `./install-dependencies-bionic --exclude-qt-sdk`

## Code

Here's the full code in case github goes away :-)

```bash
#!/bin/bash
# This script installs R and builds RStudio Desktop for ARM Chromebooks running debian stretch

# Install R; Debian stretch has latest version
sudo apt-get update
sudo apt-get install -y r-base r-base-dev

# Set RStudio version
VERS=v1.2.5001

# Download RStudio source
cd ~/Downloads/
wget -O $VERS https://github.com/rstudio/rstudio/tarball/$VERS
mkdir ~/Downloads/rstudio-$VERS
tar xvf ~/Downloads/$VERS -C ~/Downloads/rstudio-$VERS --strip-components 1
rm ~/Downloads/$VERS

# Run environment preparation scripts
sudo apt-get install -y openjdk-8-jdk
cd ~/Downloads/rstudio-$VERS/dependencies/linux/
./install-dependencies-bionic --exclude-qt-sdk

# Run common environment preparation scripts
sudo apt-get install -y git
# No arm build for pandoc, so install outside of common script
sudo apt-get install -y pandoc
sudo apt-get install -y libcurl4-openssl-dev

cd ~/Downloads/rstudio-$VERS/dependencies/common/
#./install-common
./install-gwt
./install-dictionaries
./install-mathjax
./install-boost
#./install-pandoc
./install-libclang
./install-packages

# Add pandoc folder to override build check
mkdir ~/Downloads/rstudio-$VERS/dependencies/common/pandoc

# Get Closure Compiler and replace compiler.jar
cd ~/Downloads
wget http://dl.google.com/closure-compiler/compiler-latest.zip
unzip compiler-latest.zip
rm COPYING README.md compiler-latest.zip
sudo mv closure-compiler*.jar ~/Downloads/rstudio-$VERS/src/gwt/tools/compiler/compiler.jar

# Configure cmake and build RStudio
cd ~/Downloads/rstudio-$VERS/
mkdir build
sudo cmake -DRSTUDIO_TARGET=Server -DCMAKE_BUILD_TYPE=Release
sudo make install

# Additional install steps
sudo useradd -r rstudio-server
sudo cp /usr/local/lib/rstudio-server/extras/init.d/debian/rstudio-server /etc/init.d/rstudio-server
sudo chmod +x /etc/init.d/rstudio-server 
sudo ln -f -s /usr/local/lib/rstudio-server/bin/rstudio-server /usr/sbin/rstudio-server
sudo chmod 777 -R /usr/local/lib/R/site-library/

# Setup locale
sudo apt-get install -y locales
sudo DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8
#echo 'export LANG=en_US.UTF-8' >> ~/.bashrc
#echo 'export LANGUAGE=en_US.UTF-8' >> ~/.bashrc

# Clean the system of packages used for building
sudo apt-get autoremove -y cabal-install ghc openjdk-8-jdk pandoc libboost-all-dev
sudo rm -r -f ~/Downloads/rstudio-$VERS
sudo apt-get autoremove -y

# Start the server
sudo rstudio-server start

# Go to localhost:8787

```

