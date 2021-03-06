# Selendocker
Selenium Hub + Docker-compose [1366x768]

##Installation:
## Method 1

```shell
# install docker:
$ wget -qO- https://get.docker.com/ | sh

# install docker-compose:
$ curl -L https://github.com/docker/compose/releases/download/1.2.0/docker-compose-`uname -s`-`uname -m` > $ /usr/local/bin/docker-compose
$ chmod +x /usr/local/bin/docker-compose
```
## Method 2

```brew install docker-compose```

## Instantiation
```$ docker-compose up```

It will start two containers 1 with chrome and other with firefox. Check at http://172.17.0.2:4444/grid/console

## Scaling up containers
Open a new terminal tab and execute below

```$ docker-compose scale chrome=2 firefox=3```

It will add 1 more chrome container and 2 more firefox container.Total container count will be 5, Check at http://172.17.0.2:4444/grid/console

## Scaling down containers

```$ docker-compose scale chrome=1 firefox=1```

It will destroy 1 chrome container and 2 firefox container. Total container count will be 2, Check at http://172.17.0.2:4444/grid/console

# Note:
1. You may need to `sudo` if user permission are not optimal.
2. Point you Selenium remote at http://172.17.0.2:4444/wd/hub
3. It will start all the container you have previously created,so make sure you either control the container count by **scale** or remove the containers once you are done with them.
4. If you need a specifc node comment the other nodes. e.g. if you don't want firefox-
```Dockerfile
hub:
  image: selenium/hub
  ports:
    - "4444:4444"
#firefox:
#  image: selenium/node-firefox
#  links:
#    - hub
chrome:
  image: selenium/node-chrome
  links:
    - hub
```

# Extra config
1. If you need debug capabiliy such as vnc use debug node from https://github.com/SeleniumHQ/docker-selenium
