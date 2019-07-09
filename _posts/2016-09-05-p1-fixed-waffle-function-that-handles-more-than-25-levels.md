---
layout: post
title: Fixed waffle function that handles more than 25 levels
---
## Untested solution which I believe should work!

```R
letters658 = make.unique(rep(letters, length.out = 658), sep='') #use letters658 instead of LETTERS R constant
```

The above code makes up for the R constant ```LETTERS``` only having 26 levels when R has 657 colours (add 1 since
waffle() starts at 'B' instead of 'A'). So having 657 letters will allow all R colours to be plotted safely instead of any colour beyond the 
first 26 being turned into 'not a number' i.e. ```NA```.

## Tested Solution
waffle(), the R function to compute square bar charts, fails when there are more than 25 levels. Herewith my fixed version!

```R
printf <- function(...) {
  invisible(print(sprintf(...)))
}
myletters <- function(n)
  unlist(Reduce(
    paste0,
    replicate(n %/% length(letters), letters, simplify = FALSE),
    init = letters,
    accumulate = TRUE
  ))[1:n]

letters1000 = myletters(657)

waffle2 <-
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
      part_names <- c(part_names, letters1000[1:length(parts) -
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
      rep(letters1000[i + 1], parts[i])
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
```
