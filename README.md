# canvas-from-illustrator
Reads an Illustrator file and echoes Javascript canvas drawing code to draw the shape(s) in the file.

## Summary
This library reads an Adobe Illustrator file (Illustrator 7 format) and produces HTML5 canvas drawing function calls that will draw the vector shape(s) contained in the file.  This includes matching the stroke and fill colors as well as the line thickness.  It does not include raster image data.

**NOTE** - The postive y-axes of Illustrator and HTML5 canvas point in opposite directions, which means your shapes will be upside down when you use this function.  You can perform a quick negative scale on the y-axis to fix that.  I didn't want to introduce that scaling in the code in case you have other transformations you want to do and need to preserve the order of your transformations.

## How would one use this?
You include the php file in your web page, which must have a canvas element on it.  Get the context for that canvas element and pass it, along with the path to your Illustrator file, to the php function:
```
  function drawMyIllustratorShapes()  //this is a Javascript function you write
  {
	  var myCanvas = document.getElementById("idOfMyCanvasElement");
	  var myContext = myCanvas.getContext("2d");
	  <?php
	    //this is the function that is in this php library
	    canvasDrawCommandsFromIllustratorFile("my_illustrator_shapes.ai", "myContext");
	  ?>
  }
```
and the browser gets this:
```
function drawMyIllustratorShapes()  //this is a Javascript function you write
{
	var myCanvas = document.getElementById("idOfMyCanvasElement");
	var	myContext = myCanvas.getContext("2d");
	
	myContext.lineWidth = 5;
	myContext.strokeStyle = "#ff0000";
	myContext.fillStyle = "#ffff33";
	myContext.beginPath();
	myContext.moveTo(47.52, 40.80);
	myContext.lineTo(28.32, 40.08);
	myContext.bezierCurveTo(28.32, 40.08, 31.20, 46.32, 29.28, 49.92);
	...
	[other draw functions for the rest of the points in your shapes]
	...
	myContext.bezierCurveTo(49.44, 45.60, 47.52, 40.80, 47.52, 40.80);
	myContext.stroke();
	myContext.fill();
	myContext.closePath();
}
```
## Illustrator 7?  My god, man.  How old are you?
I wrote this because I was doing vector work in an old version of Fireworks (that old) and I wanted to be able to easily get the vectors onto a web page.  Fireworks will save as an Illustrator 7 file, and that was the only text-based file format that looked reasonably parseable.

I suspect the Illustrator file format, at least for things like lines, curves, and color values, hasn't changed all that much over the years, so I hope that this is useful for users with newer versions of Illustrator.  I don't have Illustrator so I can't test this, but do let me know if it works for you on other versions and I'll update this readme file.
