# Introduction #
This page details some of the common issues you may come across when using v4l4j. You will find answers to the following questions:

**Compilation issues**<br>
<a href='#Missing_headers.md'>I get an error at compile time about `jni.h` or `jpeglib.h` not found. What do I do ?</a>

<b>JNI library issues</b><br>
<a href='#JNI_Library_issues.md'>I try to run my own Java program but the JVM complains that it cant load the JNI library `libv4l4j.so`.</a>

<b>Video streaming issues</b><br>
<a href='#lowFPS.md'>I have a `FrameGrabber` object using image format XX &amp; I get a very low frame rate. How can I improve it ?</a>

<b>JVM crash</b><br>
<a href='#SegFault.md'>When using v4l4j, the JVM crashes. What shall I do ?</a>

If you cannot find an answer to your question or if you need more help solving an issue, head to <a href='ContactMailingList.md'>this page</a> to contact the mailing list.<br>
<br>
<br>
<br>
<h1>Compilation issues</h1>

<h2>Missing headers</h2>
<b>Question:</b>
I get an error at compile time about <code>jni.h</code> or <code>jpeglib.h</code> not found. What do I do ?<br>
<br>
<b>Answer:</b>
v4l4j has a few dependencies that must be satisfied before you attempt compiling it. Make sure you have installed:<br>
<ul><li>the libjpeg package<br>
</li><li>libjpeg development package<br>
</li><li>a JDK 6, either from SUN or OpenJDK<br>
</li><li>the ant package<br>
</li><li>essential packages to build C programs (gcc, ld, make, C library header files...)</li></ul>

If you get this error:<br>
<pre><code>v4l4j_FrameGrabber.c: error: jni.h: No such file or directory<br>
</code></pre>
then set the <code>JDK_HOME</code> environment variable to point to the directory where you the JDK is installed. For instance<br>
<pre><code>set JDK_HOME="/usr/lib/jvm/java" ant clean all<br>
</code></pre>

If you get this error:<br>
<pre><code>v4l4j_FrameGrabber.c: error: jpeglib.h: No such file or directory<br>
</code></pre>
you have not installed the development files on libjpeg. It is usually a matter of installing the proper package. In Ubuntu / Debian, it is called <code>libjpeg-dev</code>, on OpenSuse / Fedora Core <code>libjpeg-devel</code>, on Mandriva <code>libjpeg62-dev</code>.<br>
<br>
<h1>Runtime issues</h1>

<h2>JNI Library issues</h2>
<b>Question:</b>
I try to run my own Java program but the JVM complains that it cant load the JNI library <code>libv4l4j.so</code>:<br>
<pre><code>Cant load v4l4j JNI library<br>
Exception in thread "main" java.lang.UnsatisfiedLinkError: no v4l4j in java.library.path<br>
	at java.lang.ClassLoader.loadLibrary(ClassLoader.java:1682)<br>
	at java.lang.Runtime.loadLibrary0(Runtime.java:823)<br>
	at java.lang.System.loadLibrary(System.java:1030)<br>
        ....<br>
</code></pre>

<b>Answers</b>:<br>
<ul><li>Have you compiled and installed the JNI library (<code>libv4l4j.so</code>) ?<br>
Run <code>ant clean all &amp;&amp; sudo ant install</code> in the v4l4j directory.</li></ul>

<ul><li>Is the JNI library in the JVM library path ?<br>
Make sure you tell the JVM where to find the v4l4j JNI library (<code>libv4l4j.so</code>) with  <code>-Djava.library.path=/path/to/JNI/lib/dir</code>. <b>Note the path is the directory where <code>libv4l4j.so</code> is located, not the actual path to <code>libv4l4j.so</code>.</b></li></ul>


<h2>Video streaming</h2>

<h2>Low FPS</h2>
<b>Question:</b>
I have a <code>FrameGrabber</code> object using image format XX & I get a very low frame rate. How can I improve it ?<br>
<br>
<b>Answer:</b>
First, make sure you disable auto-exposure. This is usually done through one of the controls. You may have to load extra controls for your device using <code>uvcdynctrl</code>.<br>
<br>
Some video devices can achieve higher frame rates if you select the right image format. For instance, on my test machine, the Hauppauge HVR 1300 card produces around 9 frames per second using YUYV, but achieves 29 frames per second if I use RGB32.<br>
First, find out the image formats supported by your video device by running the following command in the v4l4j directory (replace /dev/video0 with your device file):<br>
<pre><code>ant deviceInfo -Dtest.device=/dev/video0<br>
</code></pre>
Check the "Supported formats" section in the output. Each format has a name and an index.<br>
Second, for each supported format, run the test-fps command using (replace /dev/video0 with your device file, and replace XX with the index of the desired image format index, as per the output of the previous command):<br>
<pre><code>ant test-fps  -Dtest.device=/dev/video0 -Dtest.inFormat=XX -DoutFormat=0<br>
</code></pre>
This command will tell you the maximum frame rate you can achieve with the given image format.<br>
<br>
<h2>JVM crash</h2>
<h2>SegFault</h2>
<b>Question:</b>
When using v4l4j, the JVM crashes. What shall I do ?<br>
<br>
<b>Answser:</b>
Most of the time, this happens because of a bug in the JNI code. <a href='ContactMailingList.md'>Contact the mailing list</a> and<br>
submit a precise description of what you did to trigger the crash.