# hubot-mubot

Mubot, A Marking U Bot.

See [`src/mubot.coffee`](src/mubot.coffee) for full documentation.

## Quick Installation

In hubot project repo, (the directory where hubot resides) run:

`npm install hubot-mubot --save`

Then add **hubot-mubot** to your `external-scripts.json`:

```json
["hubot-mubot"]
```

## Full Instalation

Download setup and install nodejs. (For trouble shooting see: [Installing node.js](https://github.com/joyent/node/wiki/installing-node.js-via-package-manager))
```bash
sudo apt-get install curl
curl -sL https://deb.nodesource.com/setup | bash -
sudo apt-get install -y nodejs
```

Download, setup, and isntall hubot. (I entered 'irc' as my adapter NOT the default)
```bash
npm install -g hubot coffee-script yo generator-hubot
mkdir -p /path/to/mubot
cd /path/to/mubot
yo hubot
npm install hubot-mubot --save
```

Then add **hubot-mubot** to your `external-scripts.json: `

```json
  "hubot-mubot",
  "hubot-diagnostics",
  "hubot-help",
  "hubot-heroku-keepalive",
  "hubot-google-images",
  "hubot-google-translate",
  "hubot-pugme",
  "hubot-maps",
  "hubot-redis-brain",
  "hubot-rules",
  "hubot-shipit",
  "hubot-youtube"
]

```

To set your initial balance see Troubleshooting.

## Starting your mubot

If during setup of your hubot you selected the irc adapter as i did then this is how you would launch your mubot:
```
HUBOT_ADAPTER=irc HUBOT_IRC_SERVER=irc.swiftirc.net HUBOT_IRC_ROOMS="#AxE" HUBOT_IRC_NICK="Mubot" HUBOT_IRC_UNFLOOD="true" bin/hubot -a irc
```
Alternatively you can add `export` statements in your `/.bashrc` file.

## Sample Interaction

```
leathan>> mubot marks
Mubot>> You have <amount> marks!
```

## Troubleshooting

Q.) I get the following error `ERROR TypeError: Cannot read property '...' of undefined`

A.) You need to set your initial balance, open the file `src/marking.coffee` and find the line:

```
    robot.brain.resetSaveInterval(1) 
```

Then add this line after the above line:

```
    robot.brain.data.credits['...'] ?= <amount>
```

For example, for me that part of `src/marking.coffee` looks like:
```
module.exports = (robot) ->
  robot.brain.on 'loaded', ->
    robot.brain.data.credits ?= {}
    credits = robot.brain.data.credits or {}
    robot.brain.resetSaveInterval(1) 
    robot.brain.data.credits['irc://leathan@irc.swiftirc.net/'] ?= 12000
```

Q.) For further questions.

A.) Visit #AxE @ irc.swiftirc.net
