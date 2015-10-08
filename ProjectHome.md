Welcome to the v4l4j project site. Here, you will find information on the v4l4j software package, some documentation and various related links.

## What is v4l4j ? ##
Video4Linux4Java (v4l4j) is a GPL'd java package providing simple access to the capture interface of the Video4Linux (V4L) API from Java. Using v4l4j, an application can:
  * retrieve information about a video device, such as the number and type of video inputs, supported image formats, resolutions & video standards and available tuners,
  * capture frames from any V4L-supported devices, which includes USB/Firewire webcams, video capture cards and tuner cards.
  * access video controls, such as brightness, contrast, gain, Tilt, Focus, ...
  * access and control tuners (get / set frequency, access to received signal strength, ...)

## What can I do with v4l4j ? ##
v4l4j makes it easy to capture single frames or entire video streams from V4L devices (/dev/videoXX), including webcams and capture cards. After that, it is up to you :) . As a guide, v4l4j comes with several example applications:
  * a webcam server application, which encodes a video stream in MJPEG format and sends it to client applications over the network. The stream can be viewed by web browsers, VLC or ffplay. When viewed in web browsers, the list of available video controls is also presented so the user can adjust them.
  * a simple video viewer, which captures a video stream and displays it in a window (JFrame). See the [examples](Examples.md) page for more info.

## v4l4j features ##
The following features are implemented in v4l4j:
  * v4l4j hands out captured images encapsulated in byte`[``]`, DataBuffer, BufferedImage and Raster objects.
  * v4l4j can transparently convert raw image formats to either RGB24, BGR24, YUV420, YVU240 or JPEG.
  * v4l4j supports both V4L1 and V4L2 video devices under a single API. Differences between these two versions are managed by v4l4j and hidden to the user application.
  * All video controls are reported by v4l4j and made available. This includes [standard V4L controls](http://v4l2spec.bytesex.org/spec-single/v4l2.html#CONTROL), driver-private controls, [V4L2 extended controls](http://v4l2spec.bytesex.org/spec-single/v4l2.html#EXTENDED-CONTROLS) and private ioctls that may be implemented by some drivers. 
## Documentation ##
Download and installation instructions can be found on the GettingStarted page. The v4l4j API JavaDoc is available [here](http://v4l4j.googlecode.com/svn/www/v4l4j-api/index.html) and can be generated using `ant javadoc` in the source directory. Also, see the [example page](Examples.md) for a quick introduction to the API.
.



&lt;wiki:gadget url="http://www.ohloh.net/p/55413/widgets/project\_basic\_stats.xml" height="225" width="360" border="0"/&gt;