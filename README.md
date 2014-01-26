# freeice

The `freeice` module is a simple way of getting random STUN or TURN server
for your WebRTC application.  The list of servers (just STUN at this stage)
were sourced from this [gist](https://gist.github.com/zziuni/3741933).


[![NPM](https://nodei.co/npm/freeice.png)](https://nodei.co/npm/freeice/)


## Example Use

The following demonstrates how you can use `freeice` with
[rtc-quickconnect](https://github.com/rtc-io/rtc-quickconnect):

```js
var freeice = require('freeice');
var quickconnect = require('rtc-quickconnect');

// initialise a configuration for one stun server
var qcOpts = {
  room: 'icetest',
  iceServers: freeice()
};

// go ahead and connect
quickconnect('http://rtc.io/switchboard', qcOpts)
  .createDataChannel('chat')
  .once('chat:open', function(dc, peerId) {
    console.log('data channel opened for peer id: ' + peerId);

    dc.onmessage = function(evt) {
      console.log('peer ' + peerId + ' says: ' + evt.data);
    };

    dc.send('hi');
  });

```

As the `freeice` module generates ice servers in a list compliant with the
WebRTC spec you will be able to use it with raw `RTCPeerConnection`
constructors and other WebRTC libraries. 

## Hey, don't use my STUN/TURN server!

If for some reason your free STUN or TURN server ends up in the
[list](servers.js) of servers that is used in this module, you can feel
free to open an issue on this repository and those servers will be removed
within 24 hours (or sooner).  This is the quickest and probably the most
polite way to have something removed (and provides us some visibility
if someone opens a pull request requesting that a server is added).

## Please add my server!

If you have a server that you wish to add to the list, that's awesome! I'm
sure I speak on behalf of a whole pile of WebRTC developers who say thanks.
To get it into the list, feel free to either open a pull request or if you
find that process a bit daunting then just create an issue requesting
the addition of the server (make sure you provide all the details, and if
you have a Terms of Service then including that in the PR/issue would be
awesome).

## I know of a free server, can I add it?

Sure, if you do your homework and make sure it is ok to use (I'm currently
in the process of reviewing the terms of those STUN servers included from
the original list).  If it's ok to go, then please see the previous entry
for how to add it.

## Current List of Servers (as at last README generation)

```js
// STUN servers
exports.stun = [
  'stun.l.google.com:19302',
  'stun1.l.google.com:19302',
  'stun2.l.google.com:19302',
  'stun3.l.google.com:19302',
  'stun4.l.google.com:19302',
  'stun01.sipphone.com',
  'stun.ekiga.net',
  'stun.fwdnet.net',
  'stun.ideasip.com',
  'stun.iptel.org',
  'stun.rixtelecom.se',
  'stun.schlund.de',
  'stunserver.org',
  'stun.softjoys.com',
  'stun.voiparound.com',
  'stun.voipbuster.com',
  'stun.voipstunt.com',
  'stun.voxgratia.org',
  'stun.xten.com'
];

// TURN servers
exports.turn = [
];
```

## License(s)

### MIT

Copyright (c) 2014 Damon Oehlman <damon.oehlman@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.