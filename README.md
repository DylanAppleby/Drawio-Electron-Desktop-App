About
----- 

**drawio-desktop** is a **diagrams.net** desktop app based on [Electron](https://electronjs.org/). draw.io is the old name for diagrams.net, we just don't want the hassle of changing all the binary's names.

Download built binaries from the [releases section](https://github.com/jgraph/drawio-desktop/releases).

Security
--------

draw.io Desktop is designed to be completely isolated from the Internet, apart from the update process. This checks github.com at startup for a newer version and downloads it from an AWS S3 bucket owned by Github. All JavaScript files are self-contained, the Content Security Policy forbids running remotely loaded JavaScript.

No diagram data is ever sent externally, nor do we send any analytics about app usage externally. This means certain functionality for which we do not have a JavaScript implementation do not work in the Desktop build, namely .vsd and Gliffy import.

Build Status
------------

[![Electron+Builder+CI+(WIN) Actions Status](https://github.com/jgraph/drawio-desktop/workflows/electron-builder-win/badge.svg)](https://github.com/jgraph/drawio-desktop/actions)

Developing
----------

**draw.io** is a git submodule of **drawio-desktop**. To get both you need to clone recursively:

`git clone --recursive https://github.com/jgraph/drawio-desktop.git`

To run this:
1. `npm install` (in the root directory of this repo)
2. `npm install` (in the drawio directory of this repo)
3. export DRAWIO_ENV=dev if you want to develop/debug in dev mode.
4. If you run in dev mode, clone https://github.com/jgraph/mxgraph as a sibling directory to this repo, rename the folder containing the repo "mxgraph2".
5. `npm start` runs the app.

To release:
1. Update the draw.io sub-module and push the change. Add version tag before pushing to origin.
2. Wait for the builds to complete (https://travis-ci.org/jgraph/drawio-desktop and https://ci.appveyor.com/project/davidjgraph/drawio-desktop)
3. Go to https://github.com/jgraph/drawio-desktop/releases, edit the preview release.
4. Download the windows exe and windows portable, sign them using `signtool sign /a /tr http://timestamp.globalsign.com/?signature=sha2 /td SHA256 c:/path/to/your/file.exe`
5. Re-upload signed file as `draw.io-windows-installer-x.y.z.exe` and `draw.io-windows-no-installer-x.y.z.exe`
6. Add release notes
7. Publish release
