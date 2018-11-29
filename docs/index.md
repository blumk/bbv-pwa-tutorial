# Progressive Web App Tutorial
## Intro
Take a look at some existing PWAs and test out the following features:
- add to home screen (smartphone)
- offline support (-> airplane mode)
- hardware access (qr code scanner)
- performance (time to load/open app)
- install on desktop (chrome 70, windows)


Sample PWAs: 
- [Showcases](https://pwa.rocks/)
- [Timer](https://polytimer.rocks/)
- [QR-Code scanner](https://qrcodescan.in/)
- [bbv Planning Poker](https://bbv-poker.netlify.com/) vs App Store version

Did you notice any differences compared to native apps?

## Build your own PWA
Make sure you have the latest Ionic CLI installed (4.5.0). This tutorial will guide you through the setup of a PWA using Ionic 4 / Angular 7.
1. `ionic start pwa-demo sidemenu --type=angular`

    _(skip the Ionic Pro SDK installation)_

    Further information on the Ionic CLI, [see documentation](https://beta.ionicframework.com/docs/installation/cli)

2. Go to `pwa-demo` directory and install dependencies with `npm i`

3. Run `ionic serve`

4. Open Chrome Dev tools and run a Lighthouse audit by clicking on the `Audit` tab.


## Add a service worker

1. `ng add @angular/pwa --project app`
    - Creates the configuration file for the service worker
    - Creates the various icons that are required for the home screen
    - Updates the angular.json file to enable service worker support
    - Updates the package.json file to include the @angular/pwa package
    - Imports the service worker functionality into the root module file
    - Adds the required meta tags to the index.html file

2. `ionic serve` and run the Lighthouse audit again.

3. Running production build:
    - Install http-server `npm install serve -g`
    - Build production version `ionic build --prod`
    - Start http-server with `serve www -l 8080 --single` (`--single` is required for angular routing)
    - Open `http://localhost:8080`. Chrome Dev Tools `Application` shows a running service worker

4. Cache *.svg icons:
    - Icons are missing in offline mode - we need to cache them
    - Configure service worker by editing `ngsw-config.json`
    - `prefetch` or `lazy`? 
    - [see Angular docs](https://angular.io/guide/service-worker-intro)
    - Verify SW version: `http://localhost:8080/ngsw/state`

### Testing on device with localtunnel
- `npm install -g localtunnel`
- Open tunnel: `lt -p 8080` (custom domain with `-s`)
- Add App to home screen
- Test app from Airplane mode


## App Manifest
Improve the app user experience by modifing the `manifest.json` using a [manifest generator](
https://app-manifest.firebaseapp.com/).

Experiment with the following settings:
- Dispay Mode (standalone, fullscreen, ...)
- Orientation
- Start URL


## Push Notifications

Test web push notifications on your device by using this
[example PWA](https://gauntface.github.io/simple-push-demo/).


[Ionic PWA Toolkit](https://ionicframework.com/pwa/toolkit)

`npx create-stencil ionic-pwa`



