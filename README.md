# meteor-up [![Stories in Ready](https://badge.waffle.io/kadirahq/meteor-up.svg?label=ready&title=Ready)](http://waffle.io/kadirahq/meteor-up)

> This version of Meteor Up is still in development.
> Please check [arunoda/meteor-up](https://github.com/arunoda/meteor-up/tree/mupx) for the stable version.

Production Quality Meteor Deployment to Anywhere

First setup Meteor Up
```
git clone https://github.com/kadirahq/meteor-up
cd meteor-up
npm install
npm run prepublish
npm link
```

Then setup your project
```
mkdir .deploy
cd .deploy
mup init <your project>
```

make changes to `mup.js`. and add a `settings.json` file. Then,
```
mup setup
mup deploy
```

Your `settings.json` file should be in the same directory, and it will automatically be used.

## mup.js format
Note that we are using a `mup.js` file instead of the old `mup.json` file. You can write regular javascript code in this file to change things like reading the contents of an ssh key file. An example format for this file is as follows.

```js
module.exports = {
  servers: {
    one: {
      host: '1.2.3.4',
      username: 'root'
      // pem:
      // password:
      // or leave blank for authenticate from ssh-agent
    }
  },

  meteor: {
    name: 'app',
    path: '../app',
    servers: {
      one: {}, two: {}, three: {} //list of servers to deploy, from the 'servers' list
    },
    env: {
      ROOT_URL: 'app.com',
      MONGO_URL: 'mongodb://localhost/meteor'
    },
    logs: { //optional
      driver: 'syslog',
      opts: {
        url:'udp://syslogserverurl.com:1234'
      }
    }
    dockerImage: 'madushan1000/meteord-test', //optional
    deployCheckWaitTime: 60, //default 10

    dbname: dbname,         // this fork enables this
    graphicsMagick: true    // & this
  },

  mongo: { //optional
    oplog: true,
    port: 27017,
    servers: {
      one: {},
    },
  },
};
```
## FAQ
Q) I get an deploy verification error with logs like below (Similar to issue [88](https://github.com/kadirahq/meteor-up/issues/88))
```
Verifying Deployment: FAILED

Error:
-----------------------------------STDERR-----------------------------------
 run:
npm WARN deprecated
npm WARN deprecated   npm -g install npm@latest
npm WARN deprecated
```
A) Try increasing the value of `deployCheckWaitTime` field in `mup.js` file.
