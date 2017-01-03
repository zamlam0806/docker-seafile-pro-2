# Docker Image for Seafile 5 & 6 Pro Edition

[![Docker Automated buil](https://img.shields.io/docker/automated/xama/docker-seafile-pro.svg)]()
[![Docker Stars](https://img.shields.io/docker/stars/xama/docker-seafile-pro.svg)]()
[![Docker Pulls](https://img.shields.io/docker/pulls/xama/docker-seafile-pro.svg)]()
[![Docker Layers](https://images.microbadger.com/badges/image/xama/docker-seafile-pro.svg)]()

## Introduction

This image will pull the latest pro edition of seafile and helps you set it up in a docker environment.

You'll be guided through the setup procedure. It's kept very basic.

Advanced configurations can be done directly via the configuration files generated during the setup.

## Setup

This will pull the latest image and start the setup process automatically. (interactive mode)
You'll be asked for some details (e.g. admin credentials).

```
docker run -it --rm \
	--name=seafile-setup \
	-v /var/seafile:/seafile \
	xama/docker-seafile-pro setup
```

PLEASE NOTE THE "setup" FOLLOWING THE IMAGE NAME!

## Run

```
docker run -d \
	--name=seafile \
	-p 8082:8082 \
	-p 8000:8000 \
	-v /var/seafile:/seafile \
	xama/docker-seafile-pro
```

## Upgrade (EXPERIMENTAL)

CAUTION: THIS FEATURE IS IN ITS CURRENT STATE EXPERIMENTAL. USE AT YOUR OWN RISK!

This image supports upgrading seafile too!

First, remove the seafile image. (You'LL have to stop your container first)

```
docker stop seafile
docker rm seafile
docker rmi xama/docker-seafile-pro
```

Proceed to run the container the same way you ran the setup. (except you'LL need to use "upgrade" instead of "setup")

In our example you'll have to run the container by:

```
docker run -it --rm \
	--name=seafile-upgrade \
	-v /var/seafile:/seafile \
	xama/docker-seafile-pro upgrade
```

This procedure requires a few minutes to complete. Please be patient and grab a coffee.

If for some reason seafile fails to start or you weren't patient, you can restore a backup of the state before seafile has been upgraded.
Backups are located at (in our example) `/var/seafile/backup` in .tar.gz format.
Start the container as usual after restoring the backup (see "Run").

## Use a custom version

You can set the SEAFILE_VERSION environment variable manually using one of these compatible/tested versions.
 
- 5.1.11
- 6.0.2
- 6.0.5

I didn't test any of the older versions. They MAY be compatible.

However, I recommend using rather the image tags provided by docker hub, since changes to the container environment may always occur, which could break previous versions. 
When using container tags you ensure the docker environment really works with your version of preference.
For instance you'll want to use xama/docker-seafile-pro:5.1.11 instead of xama/docker-seafile-pro:latest if you want to stay at 5.1.11


## Contribute

This solution is quick'n'dirty, but works.
If you have any suggestions in order to improve this image, create a pull request. Thank you!
