Self Driving Car using Neural Networks

Modules:
android/ - An android app which streams video frames to the Driver app running on a PC.

arduino/ - The arduino sketch allowing Driver to send commands to the car via Serial interface.

Driver/  - Java applet which acts as both a TCP server, receiving streamed image frames from a video streaming app on a phone and a user interface allowing a human driver to control the car with the cursor keys or mouse

train/   - Octave code to train the neural network.


For the Android App :

Method 1:

Download the code from my github and import it in android studio. Say yes to all the grades queries and when the download and sync of gradle is finished run the app to check if it works. This is what I find easy to do for those who work with android studio.

Method 2:

Download and install apache ANT as well as Android SDK in your system. Then go to the directory of the code using command prompt and type:

cd android/
ant install

This will build and install the android app.


For Arduino 

The simplest way to run the sketch is to open it using Arduino IDE and simply upload it on your Arduino from the menu. If you find any issues with the port of your Arduino just try to install the drivers or google them.

For Driver App

In order to run the driver app which is a java applet you require the RxTx Serial library and Apache Commons Math library. You can search for them online. Then keep those dependencies in the source folder and then build the Driver app using the commands
cd Driver/
ant

Run the Driver app using

ant Driver [serial port path]

[serial port path] is the path to the serial port connected to your Arduino board - it's the same as the one used by the Arduino IDE so the value noted earlier is what you need.

Run the Android app (with phone and computer on the same wifi network). You'll be prompted to enter the IP address of the computer running the Driver app, once connected, you should start to see incoming video frames from the phone. You will also be able to note the location of the training data being written in record mode on standard out e.g.:

     [java] Features writing to: /tmp/nnrccar4119787618703988036features
     [java] RxTxSerialWrapper init /dev/tty.usbmodemfa131
Driver starts in Manual mode - confirm that you can drive the car using the arrow keys or mouse (Note that 'F' toggles forward, up arrow produces a momentary forward pulse).

Once you've gotten used to driving the car, you're ready to record examples for the neural network to learn from. Press 'R' to enter record mode and drive the car in the same environment you'd like it to drive itself. You can return to manual mode by pressing 'M' and re-enter record at any time by pressing 'R' again. When done, press 'M' and wait for the queue of samples to be written to disk. You're now ready to train the network.

Training:

Pre-process the recorded data into octave matrices:

change into the train/ directory and copy the temporary features file above to nnrccar.features
run the parse.py script which reads the features and writes two files X.dat and y.dat. X.dat is an octave matrix containing the input frames and y.dat is a matrix containing the labels corresponding to how you drove the car.
Train:

Follow the instructions in train/README to get set up with a solution to Ex4, then Run octave and start the nnrccar script:

octave-3.4.0:4> cd train/
octave-3.4.0:5> nnrccar

Elapsed time is 233.526 seconds.
Training Neural Network... 
It will take ~4 mins for octave to load the training data, after which you'll see the status output from fmincfg showing the progress of training the network. By default, 100 iterations of training will occur.

Once trained, the script will write out the parameters for the two sets of connections in Theta1.dat and Theta2.dat.

Copy these files to the Driver/data directory - note that they need to be renamed theta1.dat and theta2.dat [different capitalization].
Run Driver again, and press 'A' to enter auto mode. Now the self driving car is ready.


Edit: 
All the links to necessary dependencies can be found in the Readme files inside each modules. Plus download the version of libraries depending on your OS.
