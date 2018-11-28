# Progressive Web App Tutorial
## Intro
https://pwa.rocks/

https://www.progressivewebflap.com/
https://qrcodescan.in/


## Setup Ionic 4 / Angular 7 project
1. `ionic start pwa-demo sidemenu --type=angular`
    
    _skip installing Ionic Pro SDK_

    Docs: https://beta.ionicframework.com/docs/installation/cli

2. Go to `pwa-demo` directory and install dependencies with `npm i`

3. Run `ionic serve`

4. Open Chrome Dev tools and run a (Lighthouse) `Audit` 


## Add service worker

1. `ng add @angular/pwa --project app`
    - Creates the configuration file for the service worker
    - Creates the various icons that are required for the home screen
    - Updates the angular.json file to enable service worker support
    - Updates the package.json file to include the @angular/pwa package
    - Imports the service worker functionality into the root module file
    - Adds the required meta tags to the index.html file

2. `ionic serve` and run Audit again.

3. Running production build:
    - Install http-server `npm install serve -g`
    - Build production version `ionic build --prod`
    - Start http-server with `serve www -l 8080 --single` (`--single` is required for angular routing)
    - Open `http://localhost:8080`. Chrome Dev Tools `Application` shows a running service worker

4. Testing on device:
 - `npm install -g localtunnel`
 - Open tunnel: `lt -p 8080` (custom domain with `-s`)
 - Add App to home screen
 - Test app from Airplane mode


## App Manifest
Update the app using a manifest generator:
https://app-manifest.firebaseapp.com/

=> Dispay Mode (standalone, fullscreen, ...)
=> Orientation
=> Start URL

## Push Notifications

Test web push notifications on your device:
https://gauntface.github.io/simple-push-demo/



