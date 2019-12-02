# Distribute a Python pip lib

... to hosts with only the Python that comes with the OS (Mac => 2.7.x)

Why? Because thanks to Docker and Golang our development team got used to standalone fixed-version utils
and not having to deal with the issues of everyone depending on a package manager like `brew`, `pip`, `gem`
that come with all the pre-microservices issues of transitive dependencies and local runtime requirements.

For example to run [tmuxp](https://github.com/tmux-python/tmuxp):

```bash
MYBIN=./bin
libbuild=solsson/python-lib-tmuxp:latest
docker run --rm --entrypoint sleep -d --name python-lib-tmuxp-for-copy $libbuild 3600
docker cp python-lib-tmuxp-for-copy:/home/nonroot/.python $MYBIN/tmuxp/.python
docker kill python-lib-tmuxp-for-copy

sed -i '' 's|#!/usr/local/bin/python|#!/usr/bin/env python|' $MYBIN/tmuxp/.python/bin/tmuxp

PYTHONPATH=$MYBIN/tmuxp/.python/lib/python2.7/site-packages $MYBIN/tmuxp/.python/bin/tmuxp
```
