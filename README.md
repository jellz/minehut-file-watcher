# minehut-file-watcher
[![David](https://img.shields.io/david/jellz/minehut-file-watcher.svg?style=flat-square)](https://david-dm.org/jellz/minehut-file-watcher)
[![npm](https://img.shields.io/npm/v/minehut-file-watcher.svg?style=flat-square)](https://www.npmjs.com/package/minehut-file-watcher)
[![npm](https://img.shields.io/npm/dt/minehut-file-watcher.svg?style=flat-square&maxAge=3600)](https://www.npmjs.com/package/minehut-file-watcher)
[![GitHub](https://img.shields.io/github/license/jellz/minehut-file-watcher.svg?style=flat-square)](https://github.com/jellz/minehut-file-watcher)

minehut-file-watcher is a helpful command line tool that will watch your files and automatically push them to your Minehut server when they are changed. This is great for people writing config files or scripts, as they don't have to type in their editor, copy-and-paste the content from their editor to Minehut's editor, then click Save, wait for it to upload, then reload in-game. Instead, they can just type in their editor and reload in-game. Nothing more.

Like this project? [Star the repo](https://github.com/jellz/minehut-file-watcher/stargazers)  
Found a bug, have a suggestion? [Make an issue](https://github.com/jellz/minehut-file-watcher/issues)  

## Changes from v1
- You provide a server name instead of server ID
- You provide email and password instead of auth token
- Supports session IDs (which means it actually works, as opposed to v1 which wasn't compatible with certain API changes)  
You can view the v1 README [here](https://github.com/jellz/minehut-file-watcher/blob/master/README-v1.md)

## Getting Started

> To get started run **`yarn global add minehut-file-watcher`** (or `npm install -g minehut-file-watcher` if you use NPM).

```
$ mh-watch

minehut-file-watcher

--setserver=<server name>
Set the server to push files to (persistent)

--setemail=<email address>
Set the email to use to authenticate with Minehut (persistent)

--setpassword=<password>
Set the password to use to authenticate with Minehut (persistent)

--getconfig
Get your current config. Useful for debugging.

--minehutpath=<remote path>
Set the path of the file you want to update remotely

After setting the above persistent config values, use mh-watch <file> (--minehutpath=<remote path>).
```

To clarify the --minehutpath option: you must provide it when you run `mh-watch <file>`, not before as a standalone option. For example, `mh-watch --minehutpath=/plugins/Skript/scripts/myscript.sk` and then `mh-watch script.sk` will **not work**. You need to do `mh-watch script.sk --minehutpath=/plugins/Skript/scripts/myscript.sk`.

### Setup

In v1 of minehut-file-watcher, you needed to go through a convoluted process to get your auth token and server ID. v2 makes it really easy to get started because all you need to do is provide your email, password and server name, and minehut-file-watcher will handle the rest.

- Set your Minehut account email with `mh-watch --setemail=myemail@yahoo.com`
- Set your Minehut password with `mh-watch --setpassword=minehutisfree78`
- Choose your server with `mh-watch --setserver=MyServer` (the command should output the server ID if it was successful)

After setting the three config values, run the following command in a terminal: `mh-watch --minehutpath=path/to/file/on/minehut.yml path/to/my/file.yml`. If I was editing a script, I would use the command `mh-watch --minehutpath=plugins/Skript/scripts/shop.sk shop.sk`. You need to pass the `--minehutpath` option every time you watch a file, while the other three config options are persistent.

> **Note:** If the value of `minehutpath` is a path to a nonexistent file, the file will automatically be created on the server.
