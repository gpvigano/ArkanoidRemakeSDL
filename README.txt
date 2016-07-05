Arkanoid Remake SDL
version 1.0
by Giovanni Paolo Vigano'
gpv.code@gmail.com
June 2016
--------------------------

Christmas version of an old famous game, using the SDL2 library.

To start the game
---------------------
In the SDL\bin\x86\ sub-folder run ArkanoidRemakeSdl.exe, press ESC to close it, press A to switch audio on/off.
You can find the Visual Studio 2010 solution including all the projects in "ArkanoidRemakeSdl\projects\VS2010\ArkanoidRemakeSdl.sln", or the version for Visual Studio 2015 in "ArkanoidRemakeSdl\projects\VS2015\ArkanoidRemakeSdl.sln".

Introduction
-------------
This game was developed primarily with educational purposes, to teach object-oriented programming in C++.
A first prototype (incomplete but working) was presented at the end of a programming course organized by Institute of Industrial Technologies and Automation of the National Research Council of Italy (CNR-ITIA) as part of Design4All project, in order to illustrate with an example some advantages the object-oriented programming.
The author, a researcher at CNR-ITIA, developed this project in his spare time using his netbook (Windows XP, 1GB RAM, Intel Atom N450), although a preliminary search of ideas and resources (in preparation of that course) and the creation of Visual Studio 2015 projects was conducted at CNR-ITIA.
The development is still continued in the spare time with the idea of finishing the work and reorganizing it in order to share it.
The author's original idea was to create an application to show how the object-oriented programming allows to encode the logic once and reuse that code to create alternative solutions, implemented by relying on different frameworks. This first implementation uses the SDL2 library for graphics, sound and input handling. The next step, not yet realized, could be the implementation of the same game using another library (eg. OpenGL, OpenSceneGraph, Delta 3d, Ogre 3D, etc.).
This project is not for sure a perfect software design model, there is still much to do and improve, but it can be a good starting point to become familiar with the concepts of object-oriented programming in C++.

The game
---------
Having been presented on December 22 (at the course of Design4All) this game has Christmas theme: a small snowball is thrown against bricks that break, dropping snowflakes, Christmas decorations and gifts, which increase the score if hit with the ship. The gameplay is simple: the ball hits the blocks and must bounce on the ship controlled by the mouse, otherwise it is lost and the score is lowered (to launch the ball again press the left mouse button). The goal is to bounce the ball until all the blocks are destroyed.
The game for now has only a hard-coded level that is repeated indefinitely. More levels should be added, possibly loaded from a configuration file.
A simple game configuration is stored in the file config.txt in the same folder of the executable. In the first line there is a brief description of the settings, in the second text line are stored Some basic settings (fullscreen mode, width and height of the window when not in fullscreen, audio enabled, music and sound volume). This configuration file is loaded when the game starts and saved when you exit.

Architecture
-------------
The application has a modular structure, with a main module (ArkanoidRemakeSDL) which is supported by other modules independent of each other (ArkanoidRemake, SDLTK). These last modules themselves use libraries (the case of SDLTK) or more generic interfaces (the case of ArkanoidRemake). Follows a brief explanation of the various modules.
ArkanoidRemake: implements a generic "App" interface, basic functions and the logic of the game. In this module, in addition to the interface "App", a class ArkanoidRemake is defined. The ArkanoidRemakeSDL class, used by the SDL implementation module, directly derives from ArkanoidRemake.
ArkanoidRemakeSDL: leaning on SDLTK it implements graphics and sound for the game, this module manages the keyboard and mouse input. In this module are defined (or redefined) only the features that affect the choice of implementation (graphics, audio and interaction based on SDL), while leaving the basic functions, the algorithms and the operating logic to the base module ArkanoidRemake. This module is defined just an ArkanoidRemakeSDL class that inherits directly from ArkanoidRemake class.
SDLTK: (SDL toolkit) implements graphics and sound, manages the keyboard and mouse input. This library is definitely neither complete nor optimized, and anyone with a bit of programming experience with SDL could do better (for the author this was the first programming experience with SDL). This simple library was built with the intention of hiding all implementation details, including internal data structures of SDL, to allow focusing on the operating logic while exploring the code of this application, without having to learn SDL (or any other library that could take its place). This approach would allow to use the interface implemented here with SDL to create a new version based on a different library, ideally without changes to the code of the other modules.

Implementation
----------------
The code is written entirely in C++, developed with Microsoft Visual Studio 2010 Express SP1, using the standard library of C++ and some of the features in the standard C++11 (supported by Visual Studio 2010 SP1 onwards and the latest versions of GCC). Projects can be imported from later versions of Visual Studio, DLL libraries and the SDL are available on the web (http://www.libsdl.org/), however the SDL version distributed here should support all versions of Visual Studio (a Visual Studio 2015 version is also available). The x64 platform configurations, available for for the Visual Studio 2015 version, are not present in the Visual Studio 2010 projects.
The SDLTK library is internally linked to SDL, thus linking SDLTK also SDL is automatically linked, although it still requires the SDL DLLs in the same folder of the executable or in a registered path.
Even if the source code has been compiled and tested only on Windows, the SDL library is available for different platforms and this project uses only SDL and the Standard C++ Library, thus it should be possible to make it work also on different platforms.
Even if it is possible to edit the Visual Studio project to run the game without the console, in this version the console is displayed to for debugging purpose, to show possible error messages.
In this implementation the X axis is assumed to be horizontal and the Y axis vertical.

Acknowledgments
----------------
Although this project has been developed in the author's free time, it should be noted that the author owes his programming experience primarily to applied research carried out at CNR-ITIA, and the idea for this project came from the preparation of lessons at a programming course organized by that institute.
The implementation of the SDLTK framework leans to SDL2 library, an open source project, usable and distributable with ZLIB license (https://www.libsdl.org/license.php).
The idea of using SDL2 as first implementation was inspired by a similar code developed by Valtteri Ahlström (https://code.google.com/archive/p/sdl-arkanoid/), from which the author started to implement a first version, then completely rewritten using an object-oriented approach, keeping several ideas obtained from the original code.
The material used for graphics and sound comes from royalty free sources available on the net. The music comes from a source declared royalty free (http://www.freexmasmp3.com/), the sounds are remixes of royalty free sound clips from various sources, while the images were obtained or created by the author or processing images found on Google with the filter activated for permission to reuse with modification.
The images were edited using GIMP2 (http://www.gimp.org) and the sounds with Audacity (http://audacity.sourceforge.net).
The source code documentation was created using Doxygen (http://www.doxygen.org/).

Problems and possible improvements
-----------------------------------
The source code is not error free, there are some warnings during linking still to be solved, the SDLTK library code definitely could be rewritten more efficiently, and there is much to improve.
Furthermore a number of simplifications have been introduced, the implementation could be improved, but the purpose of this project is not primarily creating a quality videogame, rather providing a practical example of the benefits of object-oriented programming. The object model could be improved, especially in view of further extensions, such as the use of different graphics libraries.
At run time occasionally (rarely on author's PC) the application could crash, probably the problem is the text rendering in SDLTK, but this issue has not be solved yet.

Licence
--------
The source code of this project is freely distributed (zlib license, www.zlib.org), the other resources (images, etc.) made by the author are of public domain (for the music and possible other files not made by the author their related licenses are valid).

Directory tree
---------------
The directory tree is structured to allow the extension of the projects to more platform and more compilers.

+---ArkanoidRemakeSdl   Implementation with SDL2
|   +---bin             binaries and configuration files for each platform
|   |   +---x64         (64 bit SDL2 DLLs)
|   |   \---x86         executable and DLLs
|   +---data            game data
|   |   +---font        fonts for text rendering
|   |   +---images      images
|   |   +---music       in game music
|   |   \---sound       sound effects
|   +---projects        ArkanoidRemakeSdl Visual Studio projects
|   |   \---VS2010      Visual Studio 2010 (Express) project and solution
|   |   \---VS2015      Visual Studio 2015 (Community) project and solution
|   +---src
|   |   +---include     ArkanoidRemakeSdl header files
|   |   \---source      ArkanoidRemakeSdl source files
|   \---TEMP            ArkanoidRemakeSdl build intermediate files
|
+---doc                 Complete ArkanoidRemakeSdl documentation
|   \---html            HTML documentation (open "index.html")
|
+---lib                 ArkanoidRemakeSdl library files
|   |---VC100-x86       library files for Visual Studio 2010, 32 bit platform
|   |---VC140-x86       library files for Visual Studio 2015, 32 bit platform
|   \---VC140-x64       library files for Visual Studio 2015, 64 bit platform
|
+---projects            Visual Studio projects
|   |---VS2010          Visual Studio 2010 (Express) project
|   \---VS2015          Visual Studio 2015 (Community) project
|
+---SDL                 SDL2 library
|   +---include         SDL2 header files
|   \---lib             SDL2 library files
|       +---x64         SDL2 library files for 64 bit platform
|       \---x86         SDL2 library files for 32 bit platform
|
+---sdltk               SDLTK library
|   +---bin             SDLTK test program executable
|   +---doc             SDLTK documentation
|   +---lib             SDLTK library files
|   |   \---VC100-x86   library files for Visual Studio 2010, 32 bit platform
|   +---projects        Visual Studio projects
|   |   |---VS2010      Visual Studio 2010 (Express) projects and solution
|   |   \---VS2015   Visual Studio 2015 (Community) projects and solution
|   +---src
|   |   +---include     SDLTK header files
|   |   \---source      SDLTK source files
|   |       \---test    source files for the SDLTK test program
|   \---TEMP            SDLTK build intermediate files
|
+---src
|   +---include         ArkanoidRemake header files
|   \---source          ArkanoidRemake source files
|
\---TEMP                ArkanoidRemake build intermediate files



