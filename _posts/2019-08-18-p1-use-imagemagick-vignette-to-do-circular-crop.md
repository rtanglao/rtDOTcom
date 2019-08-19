---

layout: post
title: "How to: Use Imagemagick vignette to circular crop"
---

# Pontifications

* Here's how to use the  [Imagemagick V7 -vignette option](https://imagemagick.org/script/command-line-options.php#vignette) to make a circular crop of an image (via Stack Overflow::ImageMagick: [How can I cut out round from image?](https://stackoverflow.com/questions/41314498/imagemagick-how-can-i-cut-out-round-from-image)):

```bash
magick input.png -vignette 0x0+0+0 output.png
```

* This assumes a square input image, but if it isn't you use the ```-vignette``` geometry parameter.
* This is simpler than my previous post from [August 15, HowTo: Circular Crop with ImageMagick](http://rolandtanglao.com/2019/08/15/p1-how-to-use-imagemagick-circular-crop/)

## How To Install Imagemagick V7

* from [https://linuxconfig.org/how-to-install-imagemagick-7-on-ubuntu-18-04-linux]( https://linuxconfig.org/how-to-install-imagemagick-7-on-ubuntu-18-04-linux) ; installed on Lenovo ARM64 C630 

```bash
cd
wget https://www.imagemagick.org/download/ImageMagick.tar.gz
tar xf ImageMagick.tar.gz
cd ImageMagick-7.0.8-61/
./configure
make
sudo make install
sudo ldconfig /usr/local/lib
identify -version
magick -version
```