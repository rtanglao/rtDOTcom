---
layout: post
title: "How To refresh an image in place on a web page using JavaScript"
---
*  The `script` tag has to be after the `img` tag or this won't work! Big thanks to [Yoric](https://yoric.github.io/) and [Brendan](https://brendan.abolivier.bzh/) for the code!

```html
<!doctype html>
<html>
<head>
<title>Worldwide Flickr Barcode</title>
<script>
async function loop() {
  // Our `<img>`.
  let img = document.getElementById("barcode");

  // The url of the data that we download. Initially, we haven't downloaded any data,
  // so `null`.
  let objectURL = null;

  while (true) {
    // Wait 5 seconds.
    await new Promise(resolve => setTimeout(resolve, 5000));

    // Get the data.
    let response = await fetch("https://rytbarcode.ngrok.io/barcode.png", { cache: 'no-cache' });

    // For images, we want the response as a blob (Binary Large Object)
    let blob = await response.blob();
    if (objectURL) {
      // If we already have data, clean up the memory.
      URL.revokeObjectURL(objectURL);
    }

    // Convert the blob into a URL.
    objectURL = URL.createObjectURL(blob);

    // ...and point the `<img>` to this image.
    img.setAttribute("src", objectURL); 
  }
}
</script>
</head>
<body>
<img id="barcode"/>
<script>loop();</script>
</body>
</html>
```

* See also:
   * SO: [Refresh image with a new one at the same url](https://stackoverflow.com/questions/1077041/refresh-image-with-a-new-one-at-the-same-url)
    * SO:[Where should I put &lt;script> tags in HTML markup?](https://stackoverflow.com/questions/436411/where-should-i-put-script-tags-in-html-markup) <-- if I understand the following quote: `Unlike async scripts, defer scripts are only executed after the entire document has been loaded`, it looks like `defer` might be a better solution?!?
### Previously
* April 2011: [penmachine dodging buses barcode video & HTML5 Web App](http://rolandtanglao.com/2011/04/25/penmachine-dodging-buses-barcode-video-and-html5-web-app/)