# Electron
Quick demo using [Nativefier](https://github.com/jiahaog/nativefier):

`npm install nativefier -g`

`nativefier --name "bbv.ch" "https://bbv.ch"`

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


# Ionic Capacitor
## Intro
>Invoke Native SDKs on iOS, Android, Electron, and the Web with one code base. Optimized for Ionic Framework apps, or use with any web app framework.
[Capacitor Website](https://capacitor.ionicframework.com/)

## Getting started
- Install [dependencies](https://capacitor.ionicframework.com/docs/getting-started/dependencies)
- Add [capacitor](https://capacitor.ionicframework.com/docs/getting-started/with-ionic) to your project:

    `npm install --save @capacitor/core @capacitor/cli`

    `npx cap init`

- Run it as a PWA: 

    `ionic build --prod`

    `npx cap serve`


- Add native support

    `npx cap add ios` or
    `npx cap add android`

    `npx cap open ios` or
    `npx cap open android`

### GeoLocation Example
- Add a button to `home.page.html`
```
<ion-button (click)="showAlert()" [disabled]="isLoading">Show Position</ion-button>
````

- Load the Postion and show a modal dialog

    _use firefox/safari, chrome will throw an error message_
```
import { Component } from '@angular/core';

import { Plugins } from '@capacitor/core';

const { Geolocation, Modals } = Plugins;

@Component({
  selector: 'app-home',
  templateUrl: 'home.page.html',
  styleUrls: ['home.page.scss'],
})
export class HomePage {
  isLoading = false;

  showAlert() {
    this.isLoading = true;

    Geolocation.getCurrentPosition()
    .then(result => {
      console.log(result);
      if (!result || !result.coords) { return; }

      const lat = result.coords.latitude;
      const long = result.coords.longitude;

      Modals.alert({
        title: 'Your position:',
        message: `Lat: ${lat} Long: ${long}`
      });

    }).catch(err => console.error(err))
    .finally(() => {
      this.isLoading = false;
    });
  }
}

```


## Publish as an Electron app
- Add electron

    `npx cap add electron` 

    `npm i -g electron-packager`


- cd into `electron` directory

    MacOS `electron-packager . --platform=darwin`

    Windows: `electron-packager . --platform=win32`
