---
layout: post
title: "How I designed my geeky Zazzle T-shirt from Kennedy Space Centre pics"
---
## Pontifications

* Following up on my [Mozlando 2018 Kennedy Space Center amazement](http://rolandtanglao.com/2018/12/09/p1-blown-away-again-by-kennedy-space-center/), here's how I designed my t-shirt:

### How To make a Dazzle Graphic out out of photos

* 1\. resize

```bash
cd /home/rtanglao/GIT/rt-mozlando2018-ksc/FIFTYPERCENT
convert '../ORIGINALS/*.jpg' -resize 50% -set filename:area '%wx%h' 'ksc-%03d-size-%[filename:area].png' #originals come from flickr set and i deleted the vertical ones !
```

* 2\. get 120 files

```bash
ls -d1 $PWD/* | head -120 >1st-120files.txt
```

* 3\. make montage in 2100x1800 approx 1.2 to 1
```bash
montage -verbose -adjoin -tile 12x10 +frame +shadow +label -adjoin -geometry '2304x1728+0+0<' @FIFTYPERCENT/1st-120files.txt mozlando-ksc-12x10.png
% ls -lh mozlando-ksc-12x10.png
-rw-rw-rw- 1 rtanglao rtanglao 578M Dec  9 22:54 mozlando-ksc-12x10.png
```

* 4\. the above makes a huge 578M image so try 25%

```bash
cd /home/rtanglao/GIT/rt-mozlando2018-ksc/TWENTYFIVEPERCENT
convert '../ORIGINALS/*.jpg' -resize 25% -set filename:area '%wx%h' 'ksc-%03d-size-%[filename:area].png'
ls -d1 $PWD/* | head -120 >1st-120files.txt
cd ..
montage -verbose -adjoin -tile 12x10 +frame +shadow +label -adjoin -geometry '1152x864+0+0<' @TWENTYFIVEPERCENT/1st-120files.txt 25percent-mozlando-ksc-12x10.png
```

* 5\. still over 100MB, let's try 19%

```bash
cd /home/rtanglao/GIT/rt-mozlando2018-ksc/TENPERCENT
convert '../ORIGINALS/*.jpg' -resize 10% -set filename:area '%wx%h' 'ksc-%03d-size-%[filename:area].png'
ls -d1 $PWD/* | head -120 >1st-120files.txt
cd ..
montage -verbose -adjoin -tile 12x10 +frame +shadow +label -adjoin -geometry '461x346+0+0<' @TENPERCENT/1st-120files.txt ten-percent-mozlando-ksc-12x10.png
```

* 6\. 12x10 seems to be wrong, let's try 10x12

```bash
montage -verbose -adjoin -tile 10x12 +frame +shadow +label -adjoin -geometry '461x346+0+0<' @TENPERCENT/1st-120files.txt ten-percent-mozlando-ksc-10x12.png
```

* 7\. resized graphic in preview.app on OS X to **1800x2100 300dpi**

* 8\. order your #Mozlando2018 Kennedy Space Center tshirt here :-) :

[www.zazzle.com/z/16oru?rf=238729664665771966](https://www.zazzle.com/z/16oru?rf=238729664665771966)</a>

### Output 

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/45537349384/in/datetaken-ff/" title="For Zazzle Tshirt - distorted :-) in previw to 1800x2100 300dpi 1800x2100-ten-percent-mozlando-ksc-10x12"><img src="https://farm5.staticflickr.com/4858/45537349384_ff274fb60d_z.jpg" width="549" height="640" alt="For Zazzle Tshirt - distorted :-) in previw to 1800x2100 300dpi 1800x2100-ten-percent-mozlando-ksc-10x12"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
