Driver README
-------------

Introduction
------------

Part of NNRCCar - a project to create a self driving radio controlled car.

Driver is an example AWT application which acts as both a TCP server,
receiving streamed image frames from a video streaming app on a phone and
a user interface allowing a human driver to control the car with the cursor
keys or mouse, sent to an RC unit over the serial interface.

MANUAL Mode (default, Press 'M' to enter manual mode)

The car can be driven manually with the cursor keys or mouse.

RECORD MODE (Press 'R' to enter record mode)

In record mode, the video frames are saved to disk, labelled with the current control
input coming from the human driver. The neural network is trained using these
labelled frames in a separate environment on the computer. Trained parameters
are saved out to files which are in turn read by the Driver app...

AUTO MODE (Press 'A' to enter auto mode)

Auto mode can feed incoming video frames directly to the neural network and
steer according to its predictions, by sending instructions over a serial
interface.


Dependencies
------------

Driver depends on:

The RxTx Serial library  http://rxtx.qbang.org/wiki/index.php/Main_Page
Apache Commons Math library  http://commons.apache.org/math/
  docs: http://commons.apache.org/math/userguide/linear.html


Build and Run
-------------

Using the build.xml file in the root of the Driver source:

ant
ant Driver [serial port path]

