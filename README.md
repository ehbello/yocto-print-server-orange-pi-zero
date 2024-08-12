# Yocto Print Server (Orange Pi Zero image)

## Build

```cnonsole
docker run --rm -it -v $(pwd):$(pwd) crops/poky --workdir=$(pwd)
source layers/poky/oe-init-build-env build/
bitbake core-image-full-cmdline
```

## Write the image to your SD

```
bzcat tmp/deploy/images/orange-pi-zero/core-image-full-cmdline-orange-pi-zero.wic.bz2 | sudo dd of=/dev/sda status=progress
```

## Deploy RAUC Bundle

```console
bitbake update-bundle
```

Locate the build/tmp/deploy/images/orange-pi-zero/update-bundle-orange-pi-zero.raucb

```console
scp build/tmp/deploy/images/orange-pi-zero/update-bundle-orange-pi-zero.raucb root@yocto-print-server:/tmp/
rauc install update-bundle-orange-pi-zero.raucb
ssh root@yocto-print-server rauc install update-bundle-orange-pi-zero.raucb
```

## Access CUPSd administration website

```
http://yocto-print-server:631/ (user: admin, passwd: admin)
```
