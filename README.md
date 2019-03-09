# minehut-file-watcher
[![David](https://img.shields.io/david/jellz/minehut-file-watcher.svg?style=flat-square)](https://david-dm.org/jellz/minehut-file-watcher)
[![GitHub followers](https://img.shields.io/github/followers/jellz.svg?style=flat-square)](https://github.com/jellz)
[![npm](https://img.shields.io/npm/v/minehut-file-watcher.svg?style=flat-square)](https://www.npmjs.com/package/minehut-file-watcher)
[![npm](https://img.shields.io/npm/dt/minehut-file-watcher.svg?style=flat-square&maxAge=3600)](https://www.npmjs.com/package/minehut-file-watcher)
[![GitHub](https://img.shields.io/github/license/jellz/minehut-file-watcher.svg?style=flat-square)](https://github.com/jellz/minehut-file-watcher)
[![Discord](https://img.shields.io/discord/395189137981964288.svg?style=flat-square)](https://discord.gg/CdaSWx6)


minehut-file-watcher is a simple package that will watch your files and automatically push them to your Minehut server when they are changed. This is great for people writing config files or scripts, as they don't have to copy-and-paste the content from their editor to Minehut's editor, then click Save, then reload in-game. Instead, they can just reload in-game. Nothing more.

## Getting Started

> To get started run **`yarn global add minehut-file-watcher`** (or `npm install -g minehut-file-watcher` if you use NPM).

```
$ mh-watch

--setserverid=<server id>
Set the server to push files to (persistent)

--setauthtoken=<auth token>
Set the auth token to use to authenticate with Minehut (persistent)

--minehutpath=<remote path>
Set the path of the file you want to update remotely

After setting the above config values, use mh-watch <file>.
```

### Getting your auth token

You need your Minehut auth token to authenticate with Minehut. When you type in your username and password on minehut.com the server returns an auth token for you to use for a certain period of time. The duration of the token before it expires is currently unknown to me.

To get your Minehut auth token, follow these steps:
1. Login to [minehut.com](https://minehut.com)
2. Press F12 on your keyboard to open DevTools (should be the same for Firefox, Chromium, Edge) - I'm not sure the OS X way to do it on each browser you'll have to look it up yourself
3. You should see a window similar to this: ![DevTools](https://i.imgur.com/W06hByW.png)
4. Click on the two right arrows at the top and click 'Application' if it is not in the top bar already
5. Click Storage -> Local Storage -> https://minehut.com on the left-hand panel. You should see something like this: ![Local storage](https://i.imgur.com/ugGp4NR.png)
6. Copy the value of the `auth_token` key and set it on your computer using the command `mh-watch --setauthtoken=YOUR_AUTH_TOKEN`.

### Getting your server ID

Each Minehut account can have more than one server, which means minehut-file-watcher needs to know which server you want to push files to. Getting your server ID is simple if you follow the steps below:

1. Go to [`https://api.minehut.com/server/YOUR_SERVER_NAME?byName=true`](https://api.minehut.com/server/YOUR_SERVER_NAME?byName=true). It should be a long string of characters, beginning with something like this (I'm using the server 'Sanction' as an example): ![Minehut API JSON response](https://i.imgur.com/5AI4mYZ.png)
2. Copy the value of the `_id` field in the `server` object. In my case, the ID is `5a44799e1780c236415fbafe`. You can set it on your computer using the command `mh-watch --setserverid=YOUR_SERVER_ID`

After setting the two config values, run the following command in a terminal: `mh-watch --minehutpath=path/to/file/on/minehut.yml path/to/my/file.yml`. If I was editing a (Skript) script, I would use the command `mh-watch --minehutpath=plugins/Skript/scripts/shop.sk shop.sk`. You need to pass the `--minehutpath` option every time you watch a file, while the other two config options are persistent.

> **Note:** If the value of `minehutpath` is a path to a nonexistent file, the file will automatically be created.
