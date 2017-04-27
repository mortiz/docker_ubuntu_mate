# docker_ubuntu_mate

## What is docker_ubuntu_mate anyway?

It is a Ubuntu zesty  image with x11vnc, novnc and the Mate desktop environment installed. You can use it as a desktop or as the basis for a more customized

## Example Usage

### Basic

```
docker run -d -P rigormortiz/ubuntu_mate:zesty
```

### Persistent home directory

```
docker volume create ubuntu_desktop_home
docker run --rm -v ubuntu_desktop_home:/desktop_tmp rigormortiz/ubuntu_mate:latest cp -pr /home/ubuntu /desktop_tmp
docker run -d -P -v ubuntu_desktop_home:/home/ubuntu rigormortiz/ubuntu_mate:zesty
```
### Static port

```
docker run -d -p 5900:5900 -p 6080:6080 rigormortiz/ubuntu_mate:zesty
```

## Noteworthy

### Exposed ports

- x11vnc is exposed on port `5900`
- noVNC's http interface is exposed on port `6080`

### Misc.
- Default user is `ubuntu`
- Default VNC password is currently the same as `DESKTOP_USERNAME`. See TODO in next section. It can be easily changed at runtime with:

```
x11vnc -storepasswd somePassword /home/${DESKTOP_USERNAME}/.vnc/passwd
```

### NoVNC base image
This image is based on my ubuntu_novnc image. If you are using it to build your own image you may want to be familiar with it as some of the settings we use here are set in that image (like username) due to necessity/architecture.

### TODO

- support for ssl
- dynamically generated VNC password
