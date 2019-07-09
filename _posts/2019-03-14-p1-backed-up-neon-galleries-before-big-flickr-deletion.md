---
layout: post
title: "Downloaded Stephanie's neon and neon2 flickr galleries before the big flickr March 12, 2019 deletion"
---

# Pontifications

* Just in time for the [big March 12, 2019 deletion by flickr of non CC photos on free accounts and any non CC photos over 1000 on free accounts which I fully support :-) #ymmv](https://tidbits.com/2019/03/14/flickr-vows-to-not-delete-creative-commons-images-or-those-of-deceased-members/)
* See the original (or biggest available if the originals aren't available) photos here: [NEON 1](https://github.com/rtanglao/neon-for-stephanie/tree/master/NEON1_ORIGINALS), [NEON2](https://github.com/rtanglao/neon-for-stephanie/tree/master/NEON2_ORIGINALS)
* And the software:
    * [add-synthetic-galleryid-get-gallery-photo-metadata.rb](https://github.com/rtanglao/neon-for-stephanie/blob/master/add-synthetic-galleryid-get-gallery-photo-metadata.rb)
    * [backup-biggest-by-galleryid.rb](https://github.com/rtanglao/neon-for-stephanie/blob/master/backup-biggest-by-galleryid.rb)

## Colophon

```bash
./add-synthetic-galleryid-get-gallery-photo-metadata.rb 72157675774023387 2>neon2-add-galleryid-stderr.out &
./add-synthetic-galleryid-get-gallery-photo-metadata.rb 72157675752554377 2>neon1-add-galleryid-stderr.out &
cd /home/roland/GIT/neon-for-stephanie/NEON1_ORIGINALS
../backup-biggest-by-galleryid.rb  72157675752554377
cd /home/roland/GIT/neon-for-stephanie/NEON2_ORIGINALS
../backup-biggest-by-galleryid.rb  72157675774023387
```
