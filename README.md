# Hookserver

## Usage

```sh

# install Hookserver as a cli tool
npm install -g hookserver

# start Hookserver daemonized
hookserver start -d

# switch to the examples folder shipped with Hookserver
cd /usr/local/lib/node_modules/hookserver/examples  

# register a webhook with the name 'hello' that triggers the bash script found at './hello.sh' to executed
hookserver add hook hello ./hello.sh
# register a new security key 'my-test-key' to allow access to the registered webhooks via http requests
hookserver add key my-test-key

# test it out: send a get request to 'http://localhost:6086/hello?my-test-key'
# 6086 is the default port, you can use -p or --port flag to override it
curl http://localhost:6086/hello?my-test-key

# the output:
# {"status":"success","result":"Hello Webhooks!\n"}

```

For more information, see `hookserver help`.

**Note on permissions:** 
Hookserver uses `/var/lib/hookserver` to store hook scripts and security keys.
Usually only the root user is allowed to make changes in that directory, so probably you'll have to use `sudo`.
If `npm` was invoked with root privileges, then it will change the uid to the user account or uid specified by the user config, which defaults to `nobody`. 
Set the `--unsafe-perm` flag to run scripts with root privileges and let Hookserver register its working folders.

```sh
# so instead of...
 
npm install -g hookserver

# ...you should use

sudo npm i -g hookserver --unsafe-perm

```

## License

[MIT license](https://github.com/schwarzkopfb/hookserver/blob/master/LICENSE).