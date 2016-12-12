# chrony
Network Time Protocol Server Container


## How to build the container

```docker build --tag=chrony .```

## How to use the container

The chrony server uses a config file (/etc/chrony.conf:) on the host, this file needs to be created first.
Example contents of /etc/chrony.conf, see 'man chrony.conf' for more options:
```
server 127.127.8.0 mode 2 # local radio clock
server 127.127.1.0 # local clock
fudge 127.127.1.0 stratum 12 # local fallback clock
```



Command for running chrony docker container:
```
  # in privileged mode, try to avoid this:
  # docker run --privileged -v /etc/chrony.conf:/etc/ntp.conf:ro -d chrony
  # better solution with capabilities, needs docker-1.12:
  docker run --net=host --cap-add SYS_TIME -v /etc/chrony.conf:/etc/ntp.conf:ro -d $(IMAGE_NAME)

```

## How to test the chrony server


Commands for testing chrony docker container:

```ntpq -c "host localhost -pn```

replace localhost with container IP if required

