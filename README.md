dokku-options
========================

Basic docker options for dokku (https://github.com/progrium/dokku).

Requirements
------------

Development version of dokku at or after https://github.com/progrium/dokku/commit/c77cbf1d3ae07f0eafb85082ed7edcae9e836147.

Installation
------------

```bash
$ cd /var/lib/dokku/plugins
$ sudo git clone https://github.com/pixeltrix/dokku-options.git options
````

Usage
-----

```bash
$ dokku help
...
    options <app>                            display docker options for an app
    options:add <app> OPTIONS_STRING         add an option string an app
    options:remove <app> OPTIONS_STRING      remove an option string from an app
...
````

Add some options

```bash
$ dokku options:add myapp "-v /host/path:/container/path"
$ dokku options:add myapp "-v /another/container/path"
$ dokku options:add myapp "-link container_name:alias"
```

Check what we added

```bash
$ dokku options myapp
-link container_name:alias
-v /host/path:/container/path
-v /another/container/path
```

Remove an option
```bash
$ dokku options:remove myapp "-link container_name:alias"
```

Manual Usage
------------

In your applications folder (/home/dokku/app_name) create a file called OPTIONS.

Inside this file list one docker option per line. For example:

```bash
-link container_name:alias
-v /host/path:/container/path
-v /another/container/path
```

The above example will result in the following options being passed to docker during deploy and docker run:

```bash
-link container_name:alias -v /host/path:/container/path -v /another/container/path
```

You may also include comments (lines beginning with a #) and blank lines in the OPTIONS file.

Move information on docker options can be found here: http://docs.docker.io/en/latest/reference/run/ .


License
-------

MIT.
