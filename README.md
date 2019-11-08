<p align="center"><img src="https://cldup.com/1ATDf2JMtv.png"></p>

<p align="center"><a href="https://travis-ci.org/octalmage/robotjs"><img src="https://api.travis-ci.org/octalmage/robotjs.svg?branch=master"></a> <a href="https://ci.appveyor.com/project/octalmage/robotjs"><img src="https://ci.appveyor.com/api/projects/status/qh2eqb37j7ap6x36?svg=true"></a> <a href="https://www.npmjs.com/package/robotjs"><img src="https://img.shields.io/npm/v/robotjs.svg"></a> <a href="https://gitter.im/octalmage/robotjs?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge"><img src="https://img.shields.io/badge/gitter-join%20chat-blue.svg"></a> <a href="http://waffle.io/octalmage/robotjs"><img src="https://img.shields.io/waffle/label/octalmage/robotjs/ready.svg?maxAge=3600"></a></p>

> Node.js Desktop Automation. Control the mouse, keyboard, and read the screen.

RobotJS supports Mac, [Windows](https://github.com/octalmage/robotjs/issues/2), and [Linux](https://github.com/octalmage/robotjs/issues/17).

This is a work in progress so the exported functions could change at any time before the first stable release (1.0.0). [Ideas?](https://github.com/octalmage/robotjs/issues/4)

[Check out some of the cool things people are making with  RobotJS](https://github.com/octalmage/robotjs/wiki/Projects-using-RobotJS)! Have your own rad RobotJS project? Feel free to add it!

<p align="center"><a href="https://twitter.com/robotjavascript"><img width="300" src="https://cldup.com/Et-C6_ue45.png"></a><a href="http://blog.robotjs.io"><img width="300" src="https://cldup.com/3apDirNmSB.png"></a></p>

## Contents

- [Installation](#installation)
- [Examples](#examples)
- [API](https://robotjs.io/docs/syntax)
- [Building](#building)
- [Plans](#plans)
- [Progress](#progress)
- [FAQ](#faq)
- [License](#license)

## Build error with Node v13
```
$ if not defined npm_config_node_gyp (node ".\AppData\Roaming\nvm\v13.0.1\node_modules\npm\node_modules\npm-lifecycle\node-gyp-bin\\..\..\node_modules\node-gyp\bin\node-gyp.js" rebuild )  else (node "C:\Users\Wister\AppData\Roaming\nvm\v13.0.1\node_modules\npm\node_modules\node-gyp\bin\node-gyp.js" rebuild )
Building the projects in this solution one at a time. To enable parallel build, please add the "/m" switch.
  robotjs.cc
  win_delay_load_hook.cc
.\node_modules\robotjs\src\os.h(26): warning C4005: 'STRICT': macro redefinition (compiling source file ..\src\robotjs.cc) [.\node_modules\robotjs\build\robotjs .vcxproj]
  c:\program files (x86)\windows kits\10\include\10.0.17763.0\shared\minwindef.h(23): note: see previous definition of 'STRICT' (compiling source file ..\src\robotjs.cc)
.\node_modules\robotjs\src\robotjs.cc(159): error C2664: 'bool v8::Value::BooleanValue(v8::Isolate *) const': cannot convert argument 1 from 'v8::Local<v8::Context>' to 'v8::Isolate *' [C:\Users\Wist er\Documents\github\tracker\node_modules\robotjs\build\robotjs.vcxproj]
  .\node_modules\robotjs\src\robotjs.cc(159): note: No user-defined-conversion operator available that can perform this conversion, or the operator cannot be called
.\node_modules\robotjs\src\robotjs.cc(434): error C2661: 'v8::Object::Get': no overloaded function takes 1 arguments [.\node_modules\robotjs\build\robotjs.vcxpr oj]
.\node_modules\robotjs\src\robotjs.cc(768): error C2661: 'v8::Object::Get': no overloaded function takes 1 arguments [.\node_modules\robotjs\build\robotjs.vcxpr oj]
.\node_modules\robotjs\src\robotjs.cc(769): error C2661: 'v8::Object::Get': no overloaded function takes 1 arguments [.\node_modules\robotjs\build\robotjs.vcxpr oj]
.\node_modules\robotjs\src\robotjs.cc(770): error C2661: 'v8::Object::Get': no overloaded function takes 1 arguments [.\node_modules\robotjs\build\robotjs.vcxpr oj]
.\node_modules\robotjs\src\robotjs.cc(771): error C2661: 'v8::Object::Get': no overloaded function takes 1 arguments [.\node_modules\robotjs\build\robotjs.vcxpr oj]
.\node_modules\robotjs\src\robotjs.cc(772): error C2661: 'v8::Object::Get': no overloaded function takes 1 arguments [.\node_modules\robotjs\build\robotjs.vcxpr oj]
.\node_modules\robotjs\src\robotjs.cc(774): error C2661: 'v8::Object::Get': no overloaded function takes 1 arguments [.\node_modules\robotjs\build\robotjs.vcxpr oj]
gyp ERR! build error
```

## Installation

Install RobotJS using npm:

```
npm install robotjs
```
It's that easy! npm will download one of the prebuilt [binaries](https://github.com/octalmage/robotjs/releases/latest) for your OS.

You can get npm [here](https://nodejs.org/en/download/) if you don't have it installed.

If you need to build RobotJS, see the [building](#building) section. Instructions for [Electron](https://github.com/octalmage/robotjs/wiki/Electron).

## Examples

##### [Mouse](https://github.com/octalmage/robotjs/wiki/Syntax#mouse)

<p align="center"><img src="https://cldup.com/lugVjjAkEi.gif"></p>

```JavaScript
// Move the mouse across the screen as a sine wave.
var robot = require("robotjs");

// Speed up the mouse.
robot.setMouseDelay(2);

var twoPI = Math.PI * 2.0;
var screenSize = robot.getScreenSize();
var height = (screenSize.height / 2) - 10;
var width = screenSize.width;

for (var x = 0; x < width; x++)
{
	y = height * Math.sin((twoPI * x) / width) + height;
	robot.moveMouse(x, y);
}
```

##### [Keyboard](https://github.com/octalmage/robotjs/wiki/Syntax#keyboard)

```JavaScript
// Type "Hello World" then press enter.
var robot = require("robotjs");

// Type "Hello World".
robot.typeString("Hello World");

// Press enter.
robot.keyTap("enter");
```

##### [Screen](https://github.com/octalmage/robotjs/wiki/Syntax#screen)

```JavaScript
// Get pixel color under the mouse.
var robot = require("robotjs");

// Get mouse position.
var mouse = robot.getMousePos();

// Get pixel color in hex format.
var hex = robot.getPixelColor(mouse.x, mouse.y);
console.log("#" + hex + " at x:" + mouse.x + " y:" + mouse.y);
```
Read the [Wiki](https://github.com/octalmage/robotjs/wiki) for more information!

## [API](http://robotjs.io/docs/syntax)

The RobotJS API is hosted at <https://robotjs.io/docs/syntax>.

## Building

Please ensure you have the required dependencies before installing:

* Windows
  * windows-build-tools npm package (`npm install --global --production windows-build-tools` from an elevated PowerShell or CMD.exe)
* Mac
  * Xcode Command Line Tools.
* Linux
  * Python (v2.7 recommended, v3.x.x is not supported).
  * make.
  * A C/C++ compiler like GCC.
  * libxtst-dev and libpng++-dev (`sudo apt-get install libxtst-dev libpng++-dev`).

Install node-gyp using npm:

```
npm install -g node-gyp
```

Then build:

```
node-gyp rebuild
```

See the [node-gyp readme](https://github.com/nodejs/node-gyp#installation) for more details.

## Plans

* √ Control the mouse by changing the mouse position, left/right clicking, and dragging.
* √ Control the keyboard by pressing keys, holding keys down, and typing words.
* √ Read pixel color from the screen and capture the screen.
* Find an image on screen, read pixels from an image.
* Possibly include window management?

## Progress

| Module        | Status        | Notes   |
| ------------- |-------------: | ------- |
| Mouse         | 100%           | All planned features implemented.       |
| Keyboard      | 100%           | All planned features implemented.       |
| Screen        | 85%            | Image search, pixel search. |
| Bitmap        | 0%             |  Saving/opening, png support.  |

## FAQ

#### Does RobotJS support global hotkeys? 

Not currently, and I don't know if it ever will. I personally use [Electron](http://electron.atom.io/)/[NW.js](http://nwjs.io/) for global hotkeys, and this works well. Later on I might add hotkey support or create a separate module. See [#55](https://github.com/octalmage/robotjs/issues/55) for details. 

#### Can I take a screenshot with RobotJS? 

Soon! This is a bit more complicated than the rest of the features, so I saved it for last. Luckily the code is already there, I just need to write the bindings, and I've already started. Subscribe to [#13](https://github.com/octalmage/robotjs/issues/13) for updates. 

#### Why is &#60;insert key&#62; missing from the keyboard functions? 

We've been implementing keys as we need them. Feel free to create an issue or submit a pull request!

#### How about multi-monitor support?

The library doesn't have explicit multi-monitor support, so anything that works is kind of on accident. Subscribe to [#88](https://github.com/octalmage/robotjs/issues/88) for updates.

For any other questions please [submit an issue](https://github.com/octalmage/robotjs/issues/new).

## Story

I'm a huge fan of [AutoHotkey](https://www.autohotkey.com/), and I've used it for a very long time. AutoHotkey is great for automation and it can do a bunch of things that are very difficult in other languages. For example, it's [imagesearch](https://www.autohotkey.com/docs/commands/ImageSearch.htm) and [pixel](https://www.autohotkey.com/docs/commands/PixelGetColor.htm) related functions are hard to reproduce on Mac, especially in scripting languages. These functions are great for automating apps that can't be automated like [Netflix](http://blueshirtdesign.com/apps/autoflix/). This has never been a big deal since I've always used Windows at work, but for the past few years I've been using Mac exclusively. 

I like AutoHotkey, but I like Node.js more. By developing RobotJS I get an AutoHotkey replacement on Mac (finally!), and I get to use my favorite language. 

**TLDR:** There's nothing like AutoHotkey on Mac, so I'm making it. 

## License

MIT

Based on [autopy](https://github.com/msanders/autopy). 
Maintained by [Jason Stallings](http://jason.stallin.gs).
