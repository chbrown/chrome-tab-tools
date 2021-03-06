# Tab Tools (Google Chrome extension)

Move current tab left (⌘⌃[), right (⌘⌃]), first (⌘⌃0), or last (⌘⌃9).

| Short  | Long                              | Result                   |
|:-------|:----------------------------------|:-------------------------|
| ⌘ ⌃ [ | Command + Control + Left Bracket  | Move tab left             |
| ⌘ ⌃ ] | Command + Control + Right Bracket | Move tab right            |
| ⌘ ⌃ 0 | Command + Control + Digit 0       | Move tab to the far left  |
| ⌘ ⌃ 9 | Command + Control + Digit 9       | Move tab to the far right |


## Overview

* `content.js` gets loaded on each web page; it listens for `keydown` events on the document with `useCapture=true`,
  but only intercepts and handles the combinations listed above.
  Content scripts don't have sufficient privileges to manipulate tabs,
  so `content.js` calls `chrome.extension.sendMessage(...)` so that `background.js` can handle it from here.
* `background.js` is an event page, since `"persistent": false` in the `manifest.json`, and listens for extension messages.
  The `chrome.extension.onMessage.addListener(...)` call sets up a listener for messages from `content.js`,
  maps the message value to a function, and calls it with the current tab.
  Unlike content scripts, background scripts have access to `chrome.tabs`, which is required for the tab manipulation.


### Reference

* https://developer.chrome.com/extensions/tabs
* https://developer.chrome.com/extensions/event_pages
* https://developer.chrome.com/extensions/content_scripts


## Credits

Roughly inspired by / loosed based on / vaguely forked from
[Keyboard Shortcuts to Reorder Tabs](https://chrome.google.com/webstore/detail/moigagbiaanpboaflikhdhgdfiifdodd).
Thanks, [Greg Bullock](http://bonstio.net/)!


## License

Copyright 2017-2018 Christopher Brown.
[MIT Licensed](https://chbrown.github.io/licenses/MIT/#2017-2018).
