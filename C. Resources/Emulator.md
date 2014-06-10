InAir SDK comes with an emulator to make the development process easier. To download and install InAir Emulator, follow these steps:

If you already have the Android SDK and have your system PATH setup, please skip step 1 & 2;

1. Download & install latest android sdk from [http://developer.android.com/sdk/index.html](http://developer.android.com/sdk/index.html)
2. Add $SDK/tools and $SDK/platform-tools to PATH (platform-dependent)
3. Download InAir Emulator file: [`inair-avd.zip`](http://developer.inair.tv/upload_file/attachment/inair-image-arm.zip)
4. Extract `inair-avd.zip`
5. Open __terminal__ (Unix) or __cmd__ (Windows)
6. Change working directory to extracted directory
7. Run `install.sh` (Unix) or `install.bat`(Windows)
8. Use command-line `emulator -avd "InAir-0.2"` or start through **Android Studio**