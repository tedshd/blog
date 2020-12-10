---
title: "Canvas research log"
date: 2020-02-04T15:20:23+08:00
draft: false
---

## Online edit image

### Use canvas & how to do

Upload image -> trans to canvas -> download canvas to png

upload use files api

new canvas object

`toDataURL` download

## Some tips

- `toDataURL` default to `PNG` & resolution is 96 dpi

[Refer - HTMLCanvasElement.toDataURL() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toDataURL)

- Need notice device pixelRatio

Use `Window.devicePixelRatio` as base on canvas width & height

```javascript
var canvas = document.getElementById("canvas");
// Set display size (css pixels).
var size = 200;
canvas.style.width = size + "px";
canvas.style.height = size + "px";

// Set actual size in memory (scaled to account for extra pixel density).
var scale = window.devicePixelRatio; // Change to 1 on retina screens to see blurry canvas.
canvas.width = size * scale;
canvas.height = size * scale;
```

[Window.devicePixelRatio - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/devicePixelRatio)

- Maximum canvas size

| Browser | Maximum height | Maximum width | Maximum area                               |
| ------- | -------------- | ------------- | ------------------------------------------ |
| Chrome  | 32,767 pixels  | 32,767 pixels | 268,435,456 pixels (i.e., 16,384 x 16,384) |
| Firefox | 32,767 pixels  | 32,767 pixels | 472,907,776 pixels (i.e., 22,528 x 20,992) |
| Safari  | 32,767 pixels  | 32,767 pixels | 268,435,456 pixels (i.e., 16,384 x 16,384) |
| IE      | 8,192 pixels   | 8,192 pixels  | ?                                          |

## Upload use file API

```HTML
<input type="file" accept="image/*">
```

```javascript
document
  .querySelector("input[type=file]")
  .addEventListener("change", function () {
    handleFiles(this.files);
  });

function handleFiles(files) {
  if (!files.length) {
    // error haandle
  } else {
    return window.URL.createObjectURL(files[0]);
  }
}
```

## Download canvas to PNG

```html
<a id="download" href="#">Download Canvas</a>
```

```javascript
document.querySelector("#download").addEventListener("click", function () {
  downloadCanvas({
    link: this,
    canvasDom: document.querySelector("canvas"),
  });
});

function downloadCanvas(arg) {
  var link = arg.link,
    canvasDom = arg.canvasDom,
    filename = arg.filename || "canvas.png";

  if (!link || !canvasDom) {
    console.error("downloadCanvas: link or canvasDom not set");
    return;
  }

  var url = canvasDom.toDataURL("image/png");
  /* Change MIME type to trick the browser to downlaod the file instead of displaying it */
  url = url.replace(/^data:image\/[^;]*/, "data:application/octet-stream");
  /* In addition to <a>'s "download" attribute, you can define HTTP-style headers */
  url = url.replace(
    /^data:application\/octet-stream/,
    "data:application/octet-stream;headers=Content-Disposition%3A%20attachment%3B%20filename=" +
      filename
  );

  link.href = url;
}
```

[Refer - HTML5 Canvas to PNG File](https://stackoverflow.com/questions/12796513/html5-canvas-to-png-file)

## Edit canvas

Use [konvajs](https://konvajs.org/) edit canvass

### Init Canvass

```javascript
var stage = new Konva.Stage({
  container: "container",
  width: window.innerWidth,
  height: window.innerHeight,
});

var layer = new Konva.Layer();
stage.add(layer);

function initCanvas(arg) {
  var path = arg.path,
    x = arg.x,
    y = arg.y,
    width = arg.width,
    height = arg.heightq,
    shape = arg.shape;
  // main API:
  var imageObj = new Image();
  imageObj.onload = function () {
    var yoda = new Konva.Image({
      x: x,
      y: y,
      image: imageObj,
      width: width,
      height: height,
    });

    // add the shape to the layer
    layer.add(shape);
    layer.batchDraw();
  };
  imageObj.src = arg.path;
}
```

### Download use konvajs

```javascript
function downloadURI(uri, name) {
  var fileName = "grid_" + new Date() + ".png";
  var dataURL = stage.toDataURL({ pixelRatio: 1 });

  dataURL = dataURL.replace(
    /^data:image\/[^;]*/,
    "data:application/octet-stream"
  );
  dataURL = dataURL.replace(
    /^data:application\/octet-stream/,
    "data:application/octet-stream;headers=Content-Disposition%3A%20attachment%3B%20filename=" +
      fileName
  );

  var link = document.createElement("a");
  link.download = fileName;
  link.href = dataURL;
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
  delete link;
}

document.getElementById("save").addEventListener(
  "click",
  function () {
    downloadURI();
  },
  false
);
```

[Refer - HTML5 Canvas Export to Hight Quality Image Tutorial | Konva - JavaScript 2d canvas library](https://konvajs.org/docs/data_and_serialization/High-Quality-Export.html)
