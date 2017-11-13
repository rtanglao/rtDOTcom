---
layout: post
title: My version of the waffle() function can handle all 657 r colours
---
## Pontification :-)

TIL ([as alluded to previously](http://rolandtanglao.com/2016/09/05/p1-fixed-waffle-function-that-handles-more-than-25-levels/)):

* Again check the data, if the data isn't clean or has ```NA``` aka "not a number" you've got a problem.
* I need to figure out a way to write tests :-)
* I guess it's time to [file a github issue and/or submit a pull request with the waffle() folks](https://github.com/hrbrmstr/waffle) although I don't think most data scientists will agree with the use-case of having more than 26 elements in the vector passed to waffle() :-) Then again most data scientists aren't making art for tshirts LOL!
* Sometimes R Studio gets out of sync with R and you have to restart R.
* Sometimes R Studio's file browser aka the "Files sub-pane"gets out of sync and you have to force refresh it by clicking on the refresh arrow.
 
## roland_waffle()
[Herewith the code](https://github.com/rtanglao/2016-r-rtgram/blob/master/file-numphotos-square-piechart.R) (tl;dr change ```LETTERS``` (which fails after 25 colours) to ```levels658``` (which can handle 657 colours) where:

 ```letters658 = make.unique(rep(letters, length.out = 658), sep='')```

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
      gg <- gg + theme(legend.background = element_rect(fill = NA,
                                                        color = NA))
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
if (length(args) < 2) {
  args <- c("--help")
}
if ("--help" %in% args) {
  cat(
    "
    Arguments:
    CSV file with a column with colour with hex values for colours
    number_of_photos
    --help              - print this text
    Example:
    Rscript file-numphotos-square-piechart.R 001_ThuJan1.csv 25\n\n"
  )
  q(save = "no")
}

main <- function() {
  data3 = read.csv(file = args[1], stringsAsFactors = F)
  numphotos = as.integer(args[2])
  print(numphotos)
  data3 = head(data3, numphotos)
  
  data3$colourname <- sapply(data3$colour, tc)
  
  countcolourname = count(data3, "colourname")
  countcolourname <- countcolourname[order(-countcolourname$freq), ]
  
  colour_vector2 <- setNames(countcolourname$freq, countcolourname$colourname)
  print(colour_vector2)
  print(sum(colour_vector2))
  magic_row_size_number = 100
  
  numrows = numphotos %/% magic_row_size_number
  if (numrows == 0) {
    numrows = 1
  }
  else if ((numphotos %% magic_row_size_number) != 0) {
    numrows = numrows + 1
  }
  print (numrows)
  print(countcolourname$colourname)
  p = roland_waffle(
    colour_vector2,
    rows = numrows,
    size = 1.0,
    colors = countcolourname$colourname) +
    theme(legend.position = "none") 
  
  filename = sprintf("%4.4d-%s", numphotos, gsub("csv", "png", basename(args[1])))
  ggsave(filename,
         p,
         width = 14.222222222,
         height =10.666666667,
         dpi = 72,
         limitsize = FALSE) #multiply height and width by dpi to get px
}

sink("log.txt")

main()

sink()
```