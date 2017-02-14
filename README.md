# GreenBox
Very simple test of writing a native iOS plugin for unity

Loosely following the instructions [here](http://stackoverflow.com/a/14885024/575530).

1. Make a simple Unity project (this one's called "IOSPluginTestUnity") and add a cube to the main scene.  
2. Build a Cocoa Touch Static Library in Xcode (this one's called "IOSPluginTest").  
3. Place the .a file that results from building the Xcode project into an Assets/Plugins/iOS directory in the Unity project.  
4. Write a script and attach it to the cude in the main scene. Use it to call the native iOS and set the colour of the cube depending on the result of the call.
5. Build & run the Unity project for iOS. This generates another Xcode project (this one's called "IOSPluginTestUnityXcode").  
6. Build, deploy, and run the project on the iPhone. I needed to fix the signing team first. And later I needed to change the build target to > 8 (I went for 10.2).

The commit [afdf67](https://github.com/dumbledad/GreenBox/tree/afdf67c5f2af84e2d9e51a637641dd1f600a8cb7) contains just one simple call from the Unity C# script 
into the iOS native C++ code. 

Commit [c99815](https://github.com/dumbledad/GreenBox/tree/c998156626f1e0fe23ca80a4c0855ddd7f15dfbf) incudes a callback from the iOS native C++ code into the 
Unity C# script.

Then commit [32cea6](https://github.com/dumbledad/GreenBox/tree/32cea6e91f705d866d9ee9407029f2a1eaa28e8c) goes back to the simple call (without a callback). But 
the call from the Unity C# script into the iOS native C++ then calls further into an instance method on an Objective-C object.

The code in [05f4e4](https://github.com/dumbledad/GreenBox/tree/05f4e47892a628401cbd8ccf308346d1bde9a7d4) adds a callback from the Objective-C back into the 
Unity C# script.

For commit [b4f22f](https://github.com/dumbledad/GreenBox/tree/b4f22f2323036d5a8bc185999b6224d04ca519e8) I am back to a very simple call from a Unity C# script 
but this time it is into a Mono C# DLL.

And the latest code follows this approach with a Unity C# script calling into a Mono C# DLL which in turn calls into the native iOS static library, including 
a callback from the native iOS static library to the Mono C# DLL.