---
layout: post
title:  "Use fontawesome to display awesome characters for Firefox support tags (antivirus, operating system, certificates, addons, etc) but currently the R fontawesome package only supports fontawesome 4.7 even though the current version is version 5 and 6 is in beta"
---

* [Discovered](https://checkvist.com/p/RjpwQvvwnw89WecevQFXxe) Jan 16, 2022.23:04  [Pictogram waffle plot using emojifont](https://data-se.netlify.app/2019/11/25/pictogram-waffle-plot-using-emojifont/) <--links to the [fontawesome 4.7 cheatsheet](https://fontawesome.com/v4.7/cheatsheet/) which works unlike the v5 cheatsheet  which I linked to in the next bullet point!
* Jan 16, 2022.21:46  [Refer to the fontawesome V5 cheatsheet](https://fontawesome.com/v5/cheatsheet) to see all the possible nice font things.The following code using `library(ragg)` and `library(fontawesome)` works. I failed to get `Arial Unicode MS` to work

```r
agg_png("wineglass.png", width = 1000, height = 500, res = 144)
ggplot(mtcars, aes(wt, mpg)) +
  geom_text(
    label=fontawesome(c('fa-assistive-listening-systems')),
    family='fontawesome-webfont', aes(color = as.character(gear)),
            size=10) +
  scale_color_discrete(name = "gear") +
  theme(text = element_text(family = "fontawesome-webfont"))
invisible(dev.off())
```

* My guess is that I can load in the version 6 font of fontawesome using the R package [extrafonts](https://cran.r-project.org/web/packages/extrafont/README.html) but I haven't had time to try that yet.
* Previously:
  * From January 11, 2022 use `geom_image` instead of fontawesome: [Firefox  Support Question Art: Stack images for operating system, anti-virus,  sync,email, gmail, cookies, certificates. bookmarks, javascript, addons,  youtube, facebook, chrome, chromium, webrtc, zoom, duckduckgo,  microsoft, google](http://rolandtanglao.com/2022/01/11/p2-stack-logos-os-antivirus-sync-email-gmail-cookies-certificates-bookmarks-javascript-addons-youtube-facebook-chrome-chromium-webrtc-zoom-duckduckgo-tags/)        