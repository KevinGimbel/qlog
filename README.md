# qlog
#### Quick Log Combiner
![Version - 0.0.1-alpha](https://img.shields.io/badge/version-0.0.1_alpha-red.svg)

`qlog` is a small utility for loosely combining log files inside a directory into one big log file inside `/tmp/`. It was build out of curiosity, mostly.
So far it only uses one level of depth which means it will not search for log files in sub directories. In general, as the badge says, this is a alpha release. It kinda works but it comes without any warenty!

#### Compatibility
The script was written on and tested on Ubuntu 15.10 using bash 4.3.42 - as far as I'm concerned the minimum required bash version is 4.2+. `qlog` should run on every unix like system that makes use of the `sudo` system (see below).

#### sudo

`qlog` uses `sudo` so it can read certain log files. This is - to be honest - an issue and I might find a way to work around this or optimize it. Feel free to open an issue or sent a pull request!

### Install

Install the script to a place where you keep your bash script source files, e.g. `~/bin` or `~/scripts`.
```sh
§ cd ~/scripts
$ git clone git@github.com/kevingimbel/qlog
```
Next, symlink the file somewhere inside your $PATH and make it executable.
```sh
$ ln -s ~/scripts/qlog/qlog /usr/local/bin/
$ chmod +x qlog
```

Verify that it is working by running `qlog -v` to print the version.

Then create the configuration file `.qlogcnf` inside the `$HOME` directory, usually this is `~` or `/home/$USER`. Create it with your favorite editor, e.g. `vim`
**Note the _dot_ in front of the filename!**
```sh
$ vim ~/.qlogcnf
```

The `.qlogcnf` file is used by `qlog` to map actions to log directories. Below is an example.

```yaml
apache: /var/log/apache2
magento: ./var/log
my_app: /var/www/html/my_app/debug
```
The schema is always `appname: path/to/log/dir`. The `appname` is important because this will be the only input that `qlog` becomes. With the above setup, `qlog my_app` will read all the files in `/var/www/html/my_app/debug` that end in `.log` and combine them into one big file inside `/tmp/my_app_qlog.log`.

### Usage

See `qlog -u` for examples and usage information.

The generic usage is running `qlog appname` where `appname` is one of the names defined inside the `.qlogcnf`.

### Update

To update the script simply pull from master.

```sh
$ cd ~/scripts/qlog
$ git pull origin master
```
