##Installation

InAir SDK comes with an emulator to make the development process easier. To download and install InAir Emulator, follow these steps:

1. Download InAir Emulator file: [`inair-image-x86.zip`](http://developer.inair.tv/upload_file/attachment/inair-image-x86.zip)
2. Extract `inair-image-x86.zip`
3. Open __terminal__ (Unix) or __cmd__ (Windows)
4. Change working directory to extracted directory
5. Run `install.sh` (Unix) or `install.bat`(Windows)
6. Optional. If you use an x86 intel computer, you should install "Intel® Hardware Accelerated Execution Manager" to improve emulator performance. The installation instructions can be found [`here`](https://software.intel.com/en-us/android/articles/intel-hardware-accelerated-execution-manager)
7. Start the emulator through **Android Studio**

If you encouter any problem, please report to [our forum](http://developer.inair.tv).

##Basic Controls

###Touch
We simulate input events sent to InAir by listening to Touch Events sent to the Emulator. Recognizable Events are:

- __Double Tap:__ By default, this event is used to Init/Dismiss InAir's launcher. Can be programatically handle inside an App to do other various things.
- __Pan up, Pan down:__ This event is used to move up/down on the Menu Views like our Launcher, or scroll inside a scrollable view.
- __Swipe Horizontally:__ This gesture is determined by the moving your finger accross the middle line of the screen. It's also used to start an App from the Launcher or quit an app, depends on which direction your finger moves. Normally, you don't handle this event inside your app, unless you know exactly what you are doing.
- __Swipe Vertically:__ Swiping vertically has two variations: swiping vertically on the left side on the screen and swiping vertically on the right side of the screen. An example of this gesture is best seen in a Layered Navigation View, where swiping on the left side would move the layers forward or backward, and swiping on the right side would actually send the events down to the other child View.

###Keyboard:
Keyboard are mainly used for debugging purpose, and only available to the Emulator. Here're some default keyboard actions:

- __Enter/Return Key:__ Go forward, start something
- __Backspace:__ Go backward, go to previous view, quit app
- __M Key:__ Move to Next Layer in a LayeredView
- __N Key:__ Move to Previous Layer in a LayeredView
- __W/S Key:__ Move Up/Down on the Menu