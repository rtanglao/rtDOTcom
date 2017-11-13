---
layout: post
title: Zazzle T-shirt from 40000 flickr 2004-2012 photos using square pie chart aka waffle chart
---

tl;dr [Click here to see the t-shirt i made on zazzle.com](http://www.zazzle.com/pd/spp/pt-zazzle_shirt?dz=0520de75-0e70-4233-96ea-7a9fff542a61&clone=true&pending=true&design.areas=%5Bzazzle_shirt_10x12_back%2Czazzle_shirt_10x12_front%5D&color=white&size=a_m&style=champion_mens_premium_mesh_tshirt_t205&CMPN=shareicon&lang=en&social=true&view=113300311085901507&rf=238204589039311962)



## Things to consider for the next graphic

* Double the size and use 250-300 rows and 80000 photos (or to be "lucky" 88888 :-)?
* Use instagram vancouver 2016 instead of Roland's flickr 2004-2012

## How To

* 1\. copy the average hex colour file from
  https://github.com/rtanglao/rt-animated-gifs/blob/master/2016-11-03/flickr-roland-2004-12-avgcolour.txt
  to here: ```cp ../rt-animated-gifs/2016-11-03/flickr-roland-2004-12-avgcolour.txt .```
* 2\. ```mv flickr-roland-2004-12-avgcolour.txt flickr-roland-2004-12-avgcolour.csv``` and add line 1 with "colour"
* 3\. ```Rscript zazzle-tshirt-flickr2004-12-square-pie-chart.R flickr-roland-2004-12-avgcolour.csv ```
* 4\. ```head -40000 flickr-roland-2004-12-avgcolour.csv >1st40000-flickr-roland-2004-12-avgcolour.csv```
* 5\. ```Rscript zazzle-tshirt-flickr2004-12-square-pie-chart.R 1st40000-flickr-roland-2004-12-avgcolour.csv```
* 6\. ```mv r-png-1st40000-flickr-roland-2004-12-avgcolour.png 200-rows-16800x14400-r-png-1st40000-flickr-roland-2004-12-avgcolour.png``` go to zazzle .com and make tshirts with this graphic, it seems to resize to 2100x1800 from 16800 x 14400 


### 04December2016 Output

(resized to 2100x1800 from 16800x14400 to fit in flickr )<br />
<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/30622308813/in/datetaken-ff/" title="200-rows-2100x1800-r-png-1st40000-flickr-roland-2004-12-avgcolour.md"><img src="https://c6.staticflickr.com/6/5746/30622308813_9581190d97_n.jpg" width="320" height="274" alt="200-rows-2100x1800-r-png-1st40000-flickr-roland-2004-12-avgcolour.md"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

### The Code

The code is copy and pasted below and it's called [zazzle-tshirt-flickr2004-12-square-pie-chart.R](https://github.com/rtanglao/rt-04dec2016-flickr-2004-12-zazzle-tshirt/blob/master/zazzle-tshirt-flickr2004-12-square-pie-chart.R)

```R
library(ggplot2)
library(plotrix)
library(plyr)
library(waffle)
library(grid)

tc <- function(x) {
  return (head(color.id(x), n = 1))
}

printf <- function(...) {
  invisible(print(sprintf(...)))
}
#use letters658 instead of LETTERS R constant
letters658 = make.unique(rep(letters, length.out = 658), sep='') 
# The above code makes up for the R constant ```LETTERS``` 
# only having 26 levels when R has 657 colours (add 1 since 
# waffle() starts at 'B' instead of 'A'). So having 657 letters 
# will allow all R colours to be plotted safely instead of any colour beyond the 
# first 26 being turned into 'not a number' i.e. ```NA```.
roland_waffle <-
  function (parts,
            rows = 10,
            xlab = NULL,
            title = NULL,
            colors = NA,
            size = 2,
            flip = FALSE,
            reverse = FALSE,
            equal = TRUE,
            pad = 0,
            use_glyph = FALSE,
            glyph_size = 12,
            legend_pos = "right")
  {
    part_names <- names(parts)
    print("part_names BEFORE adding LETTERS:")
    print(part_names)
    if (length(part_names) < length(parts)) {
      print("Adding LETTERS to part_names!!!")
      printf("length:parts:%d", length(parts))
      printf("length partname:%d", length(part_names))
      part_names <- c(part_names, letters658[1:length(parts) -
                                               length(part_names)])
    }
    print("part_names after adding LETTERS:")
    print(part_names)
    if (all(is.na(colors))) {
      colors <- brewer.pal(length(parts), "Set2")
    }
    print("parts after adding LETTERS:")
    print(parts)
    printf("BEFORE unlist() length:parts:%d", length(parts))
    parts_vec <- unlist(sapply(1:length(parts), function(i) {
      rep(letters658[i + 1], parts[i])
    }))
    if (reverse) {
      parts_vec <- rev(parts_vec)
    }
    print("parts_vec:")
    print(parts_vec)
    dat <-
      expand.grid(y = 1:rows, x = seq_len(pad + (ceiling(sum(
        parts
      ) / rows))))
    dat$value <- c(parts_vec, rep(NA, nrow(dat) - length(parts_vec)))
    print(dat)
    if (!inherits(use_glyph, "logical")) {
      fontlab <- rep(fa_unicode[use_glyph], length(unique(parts_vec)))
      dat$fontlab <- c(fontlab[as.numeric(factor(parts_vec))],
                       rep(NA, nrow(dat) - length(parts_vec)))
    }
    if (flip) {
      gg <- ggplot(dat, aes(x = y, y = x))
    }
    else {
      gg <- ggplot(dat, aes(x = x, y = y))
    }
    gg <- gg + theme_bw()
    if (inherits(use_glyph, "logical")) {
      gg <- gg + geom_tile(aes(fill = value), color = "white",
                           size = size)
      gg <- gg + scale_fill_manual(name = "",
                                   values = colors,
                                   labels = part_names)
      gg <-
        gg + guides(fill = guide_legend(override.aes = list(colour = NULL)))
    }
    else {
      if (choose_font("FontAwesome", quiet = TRUE) == "") {
        stop(
          "FontAwesome not found. Install via: https://github.com/FortAwesome/Font-Awesome/tree/master/fonts",
          call. = FALSE
        )
      }
      suppressWarnings(suppressMessages(font_import(
        system.file("fonts",
                    package = "waffle"),
        recursive = FALSE,
        prompt = FALSE
      )))
      if (!(!interactive() || stats::runif(1) > 0.1)) {
        message("Font Awesome by Dave Gandy - http://fontawesome.io")
      }
      gg <- gg + geom_tile(
        color = NA,
        fill = NA,
        size = size,
        alpha = 0,
        show_guide = FALSE
      )
      gg <- gg + geom_point(
        aes(color = value),
        fill = NA,
        size = 0,
        show_guide = TRUE
      )
      gg <- gg + geom_text(
        aes(color = value, label = fontlab),
        family = "FontAwesome",
        size = glyph_size,
        show_guide = FALSE
      )
      gg <- gg + scale_color_manual(name = "",
                                    values = colors,
                                    labels = part_names)
      gg <-
        gg + guides(color = guide_legend(override.aes = list(shape = 15,
             size = 7)))
      gg <- gg + theme(legend.background = element_rect(fill = NA, color = NA))
      gg <- gg + theme(legend.key = element_rect(color = NA))
    }
    gg <- gg + labs(x = xlab, y = NULL, title = title)
    gg <- gg + scale_x_continuous(expand = c(0, 0))
    gg <- gg + scale_y_continuous(expand = c(0, 0))
    if (equal) {
      gg <- gg + coord_equal()
    }
    gg <- gg + theme(panel.grid = element_blank())
    gg <- gg + theme(panel.border = element_blank())
    gg <- gg + theme(panel.background = element_blank())
    gg <- gg + theme(panel.margin = unit(0, "null"))
    gg <- gg + theme(axis.text = element_blank())
    gg <- gg + theme(axis.title.x = element_text(size = 10))
    gg <- gg + theme(axis.ticks = element_blank())
    gg <- gg + theme(axis.line = element_blank())
    gg <- gg + theme(axis.ticks.length = unit(0, "null"))
    gg <- gg + theme(plot.title = element_text(size = 18))
    gg <- gg + theme(plot.background = element_blank())
    gg <- gg + theme(plot.margin = unit(c(0, 0, 0, 0), "null"))
    gg <- gg + theme(plot.margin = rep(unit(0, "null"), 4))
    gg <- gg + theme(legend.position = legend_pos)
    gg
  }


args <- commandArgs(TRUE)

## Default setting when no arguments passed
if (length(args) < 1) {
  args <- c("--help")
}
if ("--help" %in% args) {
  cat(
    "
    Arguments:
    CSV file with a column with colour with hex values for colours
    --help              - print this text
    Example:
    Rscript twenty-four-square-piechart-from-csv.R 001_ThuJan1.csv\n\n"
  )
  q(save = "no")
}


main <- function() {
  data3 = read.csv(file = args[1], stringsAsFactors = F)
  
  data3$colourname <- sapply(data3$colour, tc)

  countcolourname = count(data3, "colourname")
  countcolourname <- countcolourname[order(-countcolourname$freq), ]

  colour_vector2 <- setNames(countcolourname$freq, countcolourname$colourname)
  print(colour_vector2)
  print(sum(colour_vector2))
  magic_row_size_number = 100

  numrows = 200
  print (numrows)
  print(countcolourname$colourname)
  p = roland_waffle(
    colour_vector2,
    rows = numrows,
    size = 1.0,
    colors = countcolourname$colourname) +
    theme(legend.position = "none") 

  filename = sprintf("r-png-%s", gsub("csv", "png", basename(args[1])))
  ggsave(filename,
         p,
         width = 233.33333333,
         height = 200,
         dpi = 72,
         limitsize = FALSE,
         bg = "transparent"
         ) #multiply height and width by dpi to get px of 16800*14400
}

sink("log.txt")

main()

sink()
```
