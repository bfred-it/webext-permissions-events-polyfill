# chrome-permissions-events-polyfill

> WebExtensions: Polyfill for [permissions.onAdded](https://developer.chrome.com/apps/permissions#event-onAdded) and [permissions.onRemoved](https://developer.chrome.com/apps/permissions#event-onRemoved) events for Firefox.

[![Travis build status](https://api.travis-ci.com/bfred-it/chrome-permissions-events-polyfill.svg?branch=master)](https://travis-ci.com/bfred-it/chrome-permissions-events-polyfill)
[![npm version](https://img.shields.io/npm/v/chrome-permissions-events-polyfill.svg)](https://www.npmjs.com/package/chrome-permissions-events-polyfill)

[Optional permissions](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/optional_permissions) can be added and removed by both Chrome and Firefox, but Firefox doesn't yet support Permission Events: https://bugzilla.mozilla.org/show_bug.cgi?id=1444294

This polyfill will add those two events to Firefox.

## Install

You can just download the [standalone bundle](https://packd.bfred-it.now.sh/chrome-permissions-events-polyfill) (it might take a minute to download) and include the file in your `manifest.json`, or:

```sh
npm install chrome-permissions-events-polyfill
```

```js
import 'chrome-permissions-events-polyfill';
```

```js
require('chrome-permissions-events-polyfill');
```

## Usage

Include the polyfill as a _background_ script and then refer to the original [Permissions Events](https://developer.chrome.com/apps/permissions#event-onAdded) documentation.

**This polyfill will exclusively work if permissions are requested/removed from the same page where the listener is.** That means, if you run `chrome.permissions.request` in the background page, only the same exact page will receive the event.

If you want to request from `options.html` or `popup.html`, [add your request here](https://github.com/bfred-it/chrome-permissions-events-polyfill/issues/1) or send a PR to add support via `runtime.sendMessage`

```js
chrome.permissions.onAdded.addListener(permissions => {
	console.log('New permissions');
	console.log(permissions.origins);
	console.log(permissions.permissions);
});

chrome.permissions.onRemoved.addListener(permissions => {
	console.log('Permissions that have been removed');
	console.log(permissions.origins);
	console.log(permissions.permissions);
});
```

## Related

* [webext-options-sync](https://github.com/bfred-it/webext-options-sync) - Helps you manage and autosave your extension's options.
* [webext-domain-permission-toggle](https://github.com/bfred-it/webext-domain-permission-toggle) - Browser-action context menu to request permission for the current tab.
* [webext-dynamic-content-scripts](https://github.com/bfred-it/webext-dynamic-content-scripts) - Automatically inject your `content_scripts` on custom domains.
* [webext-detect-page](https://github.com/bfred-it/webext-detect-page) - Detects where the current browser extension code is being run.
* [webext-content-script-ping](https://github.com/bfred-it/webext-content-script-ping) - One-file interface to detect whether your content script have loaded.
* [`Awesome WebExtensions`](https://github.com/bfred-it/Awesome-WebExtensions): A curated list of awesome resources for Web Extensions development.

## License

MIT © Federico Brigante — [Twitter](http://twitter.com/bfred_it)