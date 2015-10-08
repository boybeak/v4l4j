This page presents the "Frame interval" feature of v4l4j, the hardware and associated
drivers used to test it and the results.

**This feature is only supported by a few V4L drivers (see table below)**.

## Definition ##
A frame interval defines the amount of time in seconds elapsed between the capture of two successive frames. It is a floating-point number, represented by two integer values: a numerator, and a denominator.

There is a relationship between the frame interval and the frame rate: one is the inverse of the other, ie if the frame interval is set to 1/10 (or 0.1 second), the corresponding frame rate is 10 frames per second.

Frame intervals are specific to an image format and a capture resolution. This means to list supported frame intervals, you must first decide which image format and capture resolution you need the frame interval information for. See [the `FrameInterval` class JavaDoc](http://v4l4j.googlecode.com/svn/www/v4l4j-api/index.html?au/edu/jcu/v4l4j/FrameInterval.html) for more information.

## Implementation ##
In v4l4j the frame interval feature is divided in two independent parts:
  * querying supported frame intervals
  * setting / getting frame intervals.

### Querying supported frame intervals ###
Supported frame intervals are encapsulated in a `FrameInterval` object. Each image format supported by a `VideoDevice` carries a `ResolutionInfo` object which contains information on supported capture resolutions. Each supported resolution carries a `FrameInterval` object which can be obtained by calling "getFrameInterval()".

The entire call chain to obtain a `FrameInterval` object is as follow:

  * Create a `VideoDevice`,
  * Get its associated `DeviceInfo`,
  * Get its supported `ImageFormat`s and pick a format
  * Get its `ResolutionInfo` object and pick a supported capture resolution,
  * Get the `FrameInterval` for that resolution.

### Setting/Getting the frame interval used for capture ###

Setting and getting the frame interval is done via a `FrameGrabber` object using "setFrameInterval()" and "getFrameInterval()". **These methods can NOT be called while capturing.**

## Tested hardware / drivers & Results ##

All the tests below were carried out with the latest versions (as of 09/08/09) of the specified drivers from the V4L mercurial repository. In the last column, the image format & resolutions shown are the one used during the tests and listed frame rates are the ones achieved.

| **Driver** | **Device** | **Results** | **Frame rates** |
|:-----------|:-----------|:------------|:----------------|
| pwc        | Logitech Quickcam Orbit (046d:08b5) | The pwc driver lacks the IOCTL to get/set the frame intervals. It will only report supported frame intervals. However, you can set the frame rate when you load the module, by specifying the parameter "fps=XX", where XX is a supported frame rate. **If you set the frame rate to an invalid value, you will not be able to obtain a frame grabber.** | **Image format:** YUV420<br><b>640x480:</b><br>5 - 10 - 15<br><b>Lower resolutions:</b><br>5 - 10 - 15 - 20 - 25 - 30 <br>
<tr><td> pwc        </td><td> Logitech Quickcam Pro 4000 (046d:08b2) </td><td> The pwc driver lacks the IOCTL to get/set the frame intervals. It will only report supported frame intervals. However, you can set the frame rate when you load the module, by specifying the parameter "fps=XX", where XX is a supported frame rate. <b>If you set the frame rate to an invalid value, you will not be able to obtain a frame grabber.</b> </td><td> <b>Image format:</b> YUV420<br><b>640x480:</b><br>5 - 10 - 15<br><b>Lower resolutions:</b><br>5 - 10 - 15 - 20 - 25 - 30 </td></tr>
<tr><td> UVC video  </td><td> Logitech Quickcam Orbit/Sphere AF (046d:0994) </td><td> To achieve higher frame rates, set the "Exposure, Auto" control to "Aperture priority" and disable the "Exposure, Auto Priority" control.</td><td> <b>Image format:</b> YUYV<br><b>1600x1200:</b><br>5<br><b>Image format:</b>MJPEG<br><b>960x720:</b><br>5 - 10 - 15 - 20 - 25 - 30<br><b>800x600:</b><br>5 - 10 - 15 - 20 - 25 - 30<br><b>640x480:</b><br>5 - 10 - 15 - 20 - 25 - 30</td></tr>
<tr><td> UVC video  </td><td>  CNF7129 - eeepc webcam (04f2:b071) </td><td> When tested, all but the highest frame rate reported were successful.</td><td> <b>Image format:</b> YUYV<br><b>640x480:</b><br>5 - 10 - 15 - 20 (30 is reported but setting it causes the frame rate to drop to 8fps)<br><b>1280x1024:</b><br>5 (7 is reported but setting it causes the frame rate to drop to 4 fps)</td></tr></tbody></table>

<b>Help me expand this table. If you have successfully tested the frame rate with a device or driver not listed in the table above, please take some time to report it on <a href='http://groups.google.com/group/v4l4j'>the v4l4j mailing list</a>.</b>

Other drivers supporting adjustable frame rate include:<br>
<ul><li>tvp514x (TI TVP5146/47)<br>
</li><li>cafe_ccic (Marvell M88ALP01)<br>
</li><li>gspca (some webcams only)<br>
</li><li>tcm825x (TCM825x camera)<br>
</li><li>ov7670