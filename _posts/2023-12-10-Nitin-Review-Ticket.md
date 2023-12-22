---
hide: False
toc: False
comments: True
layout: post
title: Nitin Balaji Review Ticket
description: Nitin Balaji Review Ticket
type: tangibles
courses: {'csp': {'week': 16}}
---

<video  height="500" controls>
    <source src="/student/videos/BinaryImageProcessing.mp4" type="video/mp4">
    Your browser does not support the video tag.
</video>

<a href="https://nitinsandiego.github.io/binarycptproject//2023/11/26/Binary-Image-Processing.html">Image Processing</a>

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Image Processing with JS</title>
</head>
<body>
  <label for="imageLink">Image Link:</label>
  <br>
  <input type="file" id="fileInput" accept="image/*">
  <br>
  <button id="loadButton" style="display: inline;">Load Image</button>
  <br>
  <canvas id="canvas" style="border: 1px solid #000;"></canvas>
  <br>
  <button id="processButton" style="display: none;">Process Image to Binary</button>
  <button id="reverseHexButton" style="display: none;">Reverse Hex Color</button>
  <button id="originalButton" style="display: none;">Show Original Image</button>

  <script>
  document.addEventListener('DOMContentLoaded', function() {
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    const loadButton = document.getElementById('loadButton');
    const processButton = document.getElementById('processButton');
    const originalButton = document.getElementById('originalButton');
    const reverseHexButton = document.getElementById('reverseHexButton');
    const fileInput = document.getElementById('fileInput');
    let img = new Image();

    function clearCanvas() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
    }

    function loadAndDisplayImage() {
      const file = fileInput.files[0];

      if (!file) {
        alert('Please select a file.');
        return;
      }

      clearCanvas();

      const reader = new FileReader();
      reader.onload = function(e) {
        img.onload = function() {
          const targetWidth = 1000;
          const scaleFactor = targetWidth / img.width;
          canvas.width = targetWidth;
          canvas.height = img.height * scaleFactor;
          ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
          processButton.style.display = 'inline';
          reverseHexButton.style.display = 'inline';
          originalButton.style.display = 'none';
        };
        img.src = e.target.result;
      };
      reader.readAsDataURL(file);
    }

    function convertToBinary() {
      const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
      const data = imageData.data;
      for (let i = 0; i < data.length; i += 4) {
        const brightness = 0.34 * data[i] + 0.5 * data[i + 1] + 0.16 * data[i + 2];
        const threshold = 128;
        const color = brightness > threshold ? 255 : 0;
        data[i] = data[i + 1] = data[i + 2] = color;
      }
      ctx.putImageData(imageData, 0, 0);
      toggleButtonsAfterProcessing();
    }

    function reverseHexColor() {
      const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
      const data = imageData.data;
      for (let i = 0; i < data.length; i += 4) {
        data[i] = 255 - data[i];       // Reverse Red
        data[i + 1] = 255 - data[i + 1]; // Reverse Green
        data[i + 2] = 255 - data[i + 2]; // Reverse Blue
      }
      ctx.putImageData(imageData, 0, 0);
      toggleButtonsAfterProcessing();
    }

    function toggleButtonsAfterProcessing() {
      processButton.style.display = 'none';
      reverseHexButton.style.display = 'none';
      originalButton.style.display = 'inline';
    }

    loadButton.addEventListener('click', loadAndDisplayImage);
    processButton.addEventListener('click', convertToBinary);
    reverseHexButton.addEventListener('click', reverseHexColor);
    originalButton.addEventListener('click', () => {
      if (img.complete && img.src) {
        ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
        processButton.style.display = 'inline';
        reverseHexButton.style.display = 'inline';
        originalButton.style.display = 'none';
      }
    });
  });
</script>
</body>
</html>
```

## Convert to Binary
The goal of this function is to convert the loaded image into a binary format. It achieves this by applying a threshold to the brightness of each pixel in the image. Here's the breakdown:<br>

**Get Image Data**
```javascript
   const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
```
**Decide Whether Pixel is White or Black**
```javascript
for (let i = 0; i < data.length; i += 4) {
  const brightness = 0.34 * data[i] + 0.5 * data[i + 1] + 0.16 * data[i + 2];
  const threshold = 128;
  const color = brightness > threshold ? 255 : 0;
  data[i] = data[i + 1] = data[i + 2] = color;
}
```
It calculates the brightness of each pixel using a weighted sum of its RGB values. If the brightness is greater than a threshold (128), it sets the pixel color to white (255); otherwise, it sets it to black (0).

## Reverse Hex Color
The purpose of this function is to reverse the hex color of each pixel in the loaded image. It achieves this by subtracting each color component from 255. Here's the breakdown:<br>

**Get Image Data**
```javascript
   const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
```
**Reverse Hex Color**
```javascript
for (let i = 0; i < data.length; i += 4) {
  data[i] = 255 - data[i];        // Reverse Red
  data[i + 1] = 255 - data[i + 1]; // Reverse Green
  data[i + 2] = 255 - data[i + 2]; // Reverse Blue
}
```
It subtracts each color component (Red, Green, Blue) from 255, effectively creating a color negative.

# If I had more time
If I had more time I would add...

    A more user-interactive interface

    Include some more features that display conversions of Binary Image Processing

    Talk more about how the conversions work and give more details about this topic

# Problems I cam across
    My conversions wouldn't work many, like converting to binary or reversing the hex. I had to debug the code and look at was wrong.

    Figuring the conversion between regular pixels and binary

    Figuring out how to reverse the pixels. 