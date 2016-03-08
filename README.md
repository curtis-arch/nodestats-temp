
# httpstats
---
Record and report on HTTP stats via an HTTP API.

Read API docs [./doc/http-api.md](./doc/api.md)

## Development setup
It works best when running rethinkdb locally. Otherwise you can figure out how to make
connect remotely.

You'll need some environment variables for `APP_CONFIG` and `NODE_ENV`

See the configuration here [./config/development.json](./config/development.json)

Install the packages
```sh
npm install
```

Install gulp globally if you don't have it
```sh
npm install gulp -g
```

Run development tasks
```sh
# run all tasks and watch for changes
gulp
# ...or run individual tasks
gulp jshint
gulp test
```
It will run jshint and mocha.

Test the HTTP API
```sh
./watch
./test-http
```

## Production setup
Install the packages
```sh
npm install --production
```

Install forever globally
```sh
npm install forever -g
```

Create the SSH tunnel to compose.io
```sh
autossh -N -L 127.0.0.1:28015:10.12.32.2:28015 -p 10478 \
    compose@aws-us-east-1-portal.0.dblayer.com \
    -i ~/.ssh/id_rsa &
```

Start the server
```sh
export NODE_ENV=production
export APP_CONFIG=/home/rethinkdbstats/rethinkdbstats/config/production.json

forever stop "rethinkdbstats-node"

forever start --uid "rethinkdbstats-node" \
    -p /home/rethinkdbstats/.forever \
    --sourceDir=/home/rethinkdbstats/rethinkdbstats \
    --workingDir=/home/rethinkdbstats/rethinkdbstats \
    --append \
    -o /home/rethinkdbstats/logs/rethinkdbstats-node-out.log \
    -l /home/rethinkdbstats/logs/rethinkdbstats-node-log.log \
    -e /home/rethinkdbstats/logs/rethinkdbstats-node-err.log \
    app.js
```

## Plugins
+ [flatiron](http://flatironjs.org) express-compatible framework
+ [rethinkdb](http://www.rethinkdb.com/api/javascript/) node driver
+ [moment](http://momentjs.com)
