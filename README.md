Docker: Arkime Viewer
======================

just run docker-compose up

```
git clone https://github.com/tanupoo/arkime-viewer
cd arkime-viewer
docker-compose up
```

you may see many messages like below:

```
arkime-docker_arkime_1 exited with code 1
```

because arkime needs to wait for starting elasticsearch up.

if you see the following message, arkime has started successfully.

```
arkime_1         | Express server listening on port 8005 in development mode
```
