![Pushover](https://raw.github.com/dvdln/node-pushover-client/master/site/logo.png)

# node-pushover-client
Send push notifications to iOS and Android using [Pushover][site].

[![npm](https://badge.fury.io/js/node-pushover-client.png)](http://badge.fury.io/js/node-pushover-client)
[![Build Status](https://travis-ci.org/dvdln/node-pushover-client.png)](https://travis-ci.org/dvdln/node-pushover-client)
[![Dependency Status](https://gemnasium.com/dvdln/node-pushover-client.png)](https://gemnasium.com/dvdln/node-pushover-client)
[![Built with Grunt](https://cdn.gruntjs.com/builtwith.png)](http://gruntjs.com/)

## Usage
[Register an application with Pushover.net][site-app] to get your application and user tokens. You may optionally set `PUSHOVER_TOKEN` and `PUSHOVER_USER` environment variables to use as default values.

```js
var Pushover = require('node-pushover-client');

var pushNotification = new Pushover({
  token: 'KzGDORePK8gMaC0QOYAMyEEuzJnyUi',
  user: 'uQiRzpo4DXghDmr9QzzfQu27cmVRsG'
});

var req = pushNotification.send({ message: 'OH HAI' });

req.then(function (res) {
  console.log(res);
});
```

You can also pass the application token and/or user token alongside `send()` data.
```js
var req = (new Pushover()).send({
  token: 'KzGDORePK8gMaC0QOYAMyEEuzJnyUi',
  user: 'uQiRzpo4DXghDmr9QzzfQu27cmVRsG',
  message: 'OH HAI'
});
```

### Command Line Usage
```sh
$ npm -g install node-pushover-client
$ pushover --help
```

### Options
#### token *(required)*
Type: `String` Default: `PUSHOVER_TOKEN` env variable

Application token you receive after [registering an application with Pushover.net][site-app].

#### user *(required)*
Type: `String` Default: `PUSHOVER_USER` env variable

User token. You can find this on your [Pushover.net dashboard][site-dashboard].

#### message *(required)*
Type: `String`

Message to push to your mobile device.

#### title
Type: `String`

Message title. If not specified then Pushover will use the application name as the message title.

#### priority
Type: `Number` Default: 0

Message priority may be `-1` (lowest) to `2` (highest). Refer to [Pushover API][api-priority] for more information.

#### expires *(required if priority is 2)*
Type: `Number`

Number of seconds to keep trying to send a priority-2 message.

#### retry *(required if priority is 2)*
Type: `Number`

Interval (in seconds) between priority-2 message retries.

#### timestamp
Type: `Number` Default: current time

A Unix timestamp. The client automatically sets this to avoid messages showing up out of order on the device.

#### device
Type: `String`

Name of device to send the notification.

#### url
Type `String`

Supplementary URL.

#### urlTitle
Type: `String` Default: URL

Title for supplementary URLs.

#### sound
Type: `String`

Name of a [supported sound][api-sounds] to play on the app.

## License
The MIT License (MIT)

Copyright (c) 2013 [David Lane](mailto:me@dvdln.com)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

  [site]:           https://pushover.net                "Pushover"
  [site-app]:       https://pushover.net/apps/build     "Pushover: Register Application"
  [site-dashboard]: https://pushover.net/dashboard      "Pushover: Dashboard"
  [api]:            https://pushover.net/api            "Pushover API"
  [api-priority]:   https://pushover.net/api#priority   "Pushover API: Priority"
  [api-sounds]:     https://pushover.net/api#sounds     "Pushover API: Sounds"
