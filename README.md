[![npm](https://img.shields.io/npm/v/whatsapp-web.js.svg)](https://www.npmjs.com/package/whatsapp-web.js) [![Depfu](https://badges.depfu.com/badges/4a65a0de96ece65fdf39e294e0c8dcba/overview.svg)](https://depfu.com/github/pedroslopez/whatsapp-web.js?project_id=9765) ![WhatsApp_Web 2.2210.9](https://img.shields.io/badge/WhatsApp_Web-2.2210.9-brightgreen.svg) [![Discord Chat](https://img.shields.io/discord/698610475432411196.svg?logo=discord)](https://discord.gg/H7DqQs4)  

# whatsapp-web.js
A WhatsApp API client that connects through the WhatsApp Web browser app

It uses Puppeteer to run a real instance of Whatsapp Web to avoid getting blocked.

**NOTE:** I can't guarantee you will not be blocked by using this method, although it has worked for me. WhatsApp does not allow bots or unofficial clients on their platform, so this shouldn't be considered totally safe.

## Quick Links

* [Guide / Getting Started](https://wwebjs.dev/guide) _(work in progress)_
* [Reference documentation](https://docs.wwebjs.dev/)
* [GitHub](https://github.com/pedroslopez/whatsapp-web.js)
* [npm](https://npmjs.org/package/whatsapp-web.js)

## Installation

The module is now available on npm! `npm i whatsapp-web.js`

### Environment
Please note that Node v12+ is required.

npm init -y
npm install --save whatsapp-web.js // cliente para Whatsapp
npm install --save qrcode-terminal // Gera um QR dentro do terminal
npm install -g nodemon

You can also install nodemon as a development dependency:

npm install --save-dev nodemon

## Example usage

```js
const qrcode = require('qrcode-terminal');

// local session
const { Client, LocalAuth } = require('whatsapp-web.js');
const client = new Client({
    authStrategy: new LocalAuth()
});

client.on('qr', qr => {
    qrcode.generate(qr, {small: true});
});

client.on('ready', () => {
    console.log('Client is ready!');
});

client.on('message', message => {
	if(message.body === '!ping') {
		message.reply('pong');
	}
});

client.initialize();
```

Take a look at [example.js](https://github.com/pedroslopez/whatsapp-web.js/blob/master/example.js) for another example with more use cases.

For more information on saving and restoring sessions, check out the available [Authentication Strategies](https://wwebjs.dev/guide/authentication.html).

### Nodemom

* [GitHub](https://github.com/remy/nodemon)

At file package.json, there is a key scripts which normally comes like this by default:

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
},
```

To create a new application start script, it is possible to create a start key, below the test key, and pass the initialization command to this key, which in this case will be with nodemon.

Update package.json to leave the scripts key like this:

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon server.js"
},
```

This way the script is already created and will be working, to test it, navigate to the project directory through the terminal, and execute the following command:

```
npm start
//ou
yarn start //if you are using yarn
```

## Supported features

| Feature  | Status |
| ------------- | ------------- |
| Multi Device  | ✅  |
| Send messages  | ✅  |
| Receive messages  | ✅  |
| Send media (images/audio/documents)  | ✅  |
| Send media (video)  | ✅ [(requires google chrome)](https://wwebjs.dev/guide/handling-attachments.html#caveat-for-sending-videos-and-gifs)  |
| Send stickers | ✅ |
| Receive media (images/audio/video/documents)  | ✅  |
| Send contact cards | ✅ |
| Send location | ✅ |
| Send buttons | ✅ |
| Send lists | ✅ (business accounts not supported) |
| Receive location | ✅ | 
| Message replies | ✅ |
| Join groups by invite  | ✅ |
| Get invite for group  | ✅ |
| Modify group info (subject, description)  | ✅  |
| Modify group settings (send messages, edit info)  | ✅  |
| Add group participants  | ✅  |
| Kick group participants  | ✅  |
| Promote/demote group participants | ✅ |
| Mention users | ✅ |
| Mute/unmute chats | ✅ |
| Block/unblock contacts | ✅ |
| Get contact info | ✅ |
| Get profile pictures | ✅ |
| Set user status message | ✅ |

Something missing? Make an issue and let us know!