# INAV Configurator

INAV Configurator is a crossplatform configuration tool for the [INAV](https://github.com/iNavFlight/inav) flight control system.

It runs as an app within Google Chrome and allows you to configure the INAV software running on any supported INAV target.

Various types of aircraft are supported by the tool and by INAV, e.g. quadcopters, hexacopters, octocopters and fixed-wing aircraft.

# Support

INAV Configurator comes `as is`, without any warranty and support from authors. If you found a bug, please create an issue on [GitHub](https://github.com/iNavFlight/inav-configurator/issues).

GitHub issue tracker is reserved for bugs and other technical problems. If you do not know how to setup
everything, hardware is not working or have any other _support_ problem, please consult:

* [INAV Discord Server](https://discord.gg/peg2hhbYwN)
* [INAV Official on Facebook](https://www.facebook.com/groups/INAVOfficial)
* [RC Groups Support](https://www.rcgroups.com/forums/showthread.php?2495732-Cleanflight-iNav-(navigation-rewrite)-project)
* [INAV Official on Telegram](https://t.me/INAVFlight)

## INAV Configurator start minimized, what should I do?

You have to remove `C:\Users%Your_UserNname%\AppData\Local\inav-configurator` folder and all its content.

[https://www.youtube.com/watch?v=XMoULyiFDp4](https://www.youtube.com/watch?v=XMoULyiFDp4)

Alternatively, on Windows with PowerShell you can use `post_install_cleanup.ps1` script that will do the cleaning. (thank you James Cherrill)

## Installation

Depending on target operating system, _INAV Configurator_ is distributed as _standalone_ application or Chrome App.

### Windows

1. Visit [release page](https://github.com/iNavFlight/inav-configurator/releases)
1. Download Configurator for Windows platform (win32 or win64 is present)
1. Extract ZIP archive
1. Run INAV Configurator app from unpacked folder
1. Configurator is not signed, so you have to allow Windows to run untrusted application. There might be a monit for it during first run 

### Linux

1. Visit [release page](https://github.com/iNavFlight/inav-configurator/releases)
1. Download Configurator for Linux platform (linux32 and linux64 are present)
1. Extract tar.gz archive
1. Make the inav-configurator file executable (chmod +x inav-configurator)
1. Run INAV Configurator app from unpacked folder

### Mac

1. Visit [release page](https://github.com/iNavFlight/inav-configurator/releases)
1. Download Configurator for Mac platform
1. Extract ZIP archive
1. Run INAV Configurator
1. Configurator is not signed, so you have to allow Mac to run untrusted application. There might be a monit for it during first run 

## Building and running INAV Configurator locally (for development or Linux users)

For local development, **node.js** build system is used.

1. Install node.js
1. From project folder run `npm install`
1. To build the JS and CSS files and start the configurator:
    - With NW.js: Run `npm start`.
    - With Chrome: Run `npm run gulp`. Then open `chrome://extensions`, enable
    the `Developer mode`, click on the `Load unpacked extension...` button and select the `inav-configurator` directory.

Other tasks are also defined in `gulpfile.js`. To run a task, use `node ./node_modules/gulp/bin/gulp.js task-name`. Available ones are:

- **build**: Generate JS and CSS output files used by the configurator from their sources. It must be run whenever changes are made to any `.js` or `.css` files in order to have those changes appear
in the configurator. If new files are added, they must be included in `gulpfile.js`. See the comments at the top of `gulpfile.js` to learn how to do so. See also the `watch` task.
- **watch**: Watch JS and CSS sources for changes and run the `build` task whenever they're edited.
- **dist**: Create a distribution of the app (valid for packaging both as a Chrome app or a NW.js app)
in the `./dist/` directory.
- **release**: Create NW.js apps for each supported platform (win32, osx64 and linux64) in the `./apps`
directory. Running this task on macOS or Linux requires Wine, since it's needed to set the icon
for the Windows app. If you don't have Wine installed you can create a release by running the **release-only-linux** task.

To build a specific release, use the command `release --platform="win64"` for example.

### Running with debug | Inspector

To be able to open Inspector, you will need SDK flavours of NW.js

`npm install nw@0.61.0 --nwjs_build_type=sdk`

## Different map providers

INAV Configurator 2.1 allows to choose between OpenStreetMap, Bing Maps, and MapProxy map providers. 
INAV Configurator is shipped **WITHOUT** API key for Bing Maps. That means: every user who wants to use Bing Maps has to create own account, agree to all _Terms and Conditions_ required by Bing Maps and configure INAV Configuerator by himself. 

### How to choose Map provider

1. Click **Settings** icon in the top-right corner of INAV Configurator
1. Choose provider: OpenStreetMap, Bing, or MapProxy
1. In the case of Bing Maps, you have to provide your own, personal, generated by you, Bing Maps API key
1. For MapProxy, you need to provide a server URL and layer name to be used

### How to get Bing Maps API key

1. Go to the Bing Maps Dev Center at [https://www.bingmapsportal.com/](https://www.bingmapsportal.com/). 
    * If you have a Bing Maps account, sign in with the Microsoft account that you used to create the account or create a new one. For new accounts, follow the instructions in [Creating a Bing Maps Account](https://msdn.microsoft.com/library/gg650598.aspx).
1. Select **My keys** under **My Account**.
1. Select the option to create a new key.
1. Provide the following information to create a key:
    1. Application name: Required. The name of the application.
    1. Application URL: The URL of the application. This is an optional field which is useful in helping you remember the purpose of that key in the future.
    1. Key type: Required. Select the key type that you want to create. You can find descriptions of key and application types here. 
    1. Application type: Required. Select the application type that best represents the application that will use this key. You can find descriptions of key and application types [here](https://www.microsoft.com/maps/create-a-bing-maps-key.aspx). 
1. Click the **Create** button. The new key displays in the list of available keys. Use this key to authenticate your Bing Maps application as described in the documentation for the Bing Maps API you are using.

### How to setup a MapProxy server for offline caching and mission planning
1. Follow process described in [MAPPROXY.md](MAPPROXY.md)
1. Test your MapProxy server in web browser, eg: http://192.168.145.20/inavmapproxy/
1. Once you have a working MapProxy server choose MapProxy as your map provider
	1. Enter MapProxy service URL, eg: http://192.168.145.20/inavmapproxy/service?
	1. Enter MapProxy service layer (inav_layer if configured from MAPPROXY.md)
1. Once completed, you can zoom in on area you will be flying in while connected to the internet in either GPS or Mission Control tab to save the cache for offline use

## Notes

### WebGL

Make sure Settings -> System -> "User hardware acceleration when available" is checked to achieve the best performance

### Linux users

1. Dont forget to add your user into dialout group "sudo usermod -aG dialout YOUR_USERNAME" for serial access
2. If you have 3D model animation problems, enable "Override software rendering list" in Chrome flags chrome://flags/#ignore-gpu-blacklist

## Issue trackers

For INAV configurator issues raise them here

https://github.com/iNavFlight/inav-configurator/issues

For INAV firmware issues raise them here

https://github.com/iNavFlight/inav/issues

## Developers

We accept clean and reasonable patches, submit them!
