# Photo Studio — Progressive Web App

Photo Studio is a browser-based batch photo tool. It can be installed as an app, follows your device’s light or dark appearance automatically, and keeps its application files available offline after the first online visit.

## Publish on GitHub Pages

1. Create a GitHub repository for the app.
2. Upload **the contents of this folder** to the repository root. `index.html`, `manifest.webmanifest`, `sw.js` and the `icons` folder must sit at the top level as shown below.
3. In the repository, open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**, select your main branch and the `/(root)` folder, then save.
5. Open the GitHub Pages HTTPS URL once the deployment is ready.

```text
index.html
manifest.webmanifest
sw.js
icons/
  icon-192.png
  icon-512.png
```

The manifest and service worker use relative paths, so both a user/organization site and a project site (for example, `https://username.github.io/photo-studio/`) are supported.

## Enable offline use

- The app shell (HTML, manifest and icons) is cached automatically on the first online visit.
- For offline use of **HEIC, CR2 and DNG**, open Photo Studio while online and click **Prepare offline support** once. This caches the HEIC converter, RAW decoder module and its WebAssembly binaries on that device.
- Once the cache preparation has completed, disconnect from the internet and reload the page to test offline mode.

The HEIC/RAW decoder libraries are downloaded from jsDelivr the first time offline support is prepared. The service worker caches them locally; the photo files themselves are never sent to a server. If you skip decoder preparation, standard browser-readable formats (JPG, PNG and WebP) still work offline, but HEIC/RAW decoding may require an internet connection until its decoder assets have been cached.

## Appearance

The interface automatically follows the device or browser setting for light and dark appearance. Change your system appearance setting and Photo Studio switches with it; there is no separate theme setting to manage.

## Install

On supported browsers, use the **Install app** button when it appears. On iPhone/iPad, open the site in Safari, use **Share → Add to Home Screen**. The browser only offers installation after the site has been served from HTTPS and its PWA requirements are met.

## Updating the app

When you publish a new version, change `CACHE_VERSION` in `sw.js` whenever you publish another update (for example, from `photo-studio-v2` to `photo-studio-v3`). The new service worker will install a fresh app-shell cache and remove the previous Photo Studio cache after activation.

## Privacy

All image processing runs locally in the browser. The service worker only caches the app files and the HEIC/RAW decoder libraries; it does not upload selected photos.
