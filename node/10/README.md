# Node

A Windows Server Core Docker container image with Node.js 10.19.0 installed.

## Images

- stefanscherer/node-windows:10.19.0 -> Nano Server + Node + NPM + Yarn + Git
- stefanscherer/node-windows:10.19.0-pure -> Nano Server + Node
- stefanscherer/node-windows:10.19.0-windowsservercore -> Windows Server Core + Node + NPM + Yarn + Git
- stefanscherer/node-windows:10.19.0-build-tools -> + Python + C++ build tools

## Building

To build the images yourself use the following commands:

```
docker build -t node:10.19.0-windowsservercore .
docker build -t node:10.19.0-nanoserver nano
docker build -t node:10.19.0-pure pure
```

### Build with 1803 or newer base images

On Windows Server 1803 or any current Windows 10 machine you might want to use the smaller base images.

The `Dockerfile` is prepared to run on any Windows platform, but you have to specify some build arguments to make it work with newer base images.

```
docker build -t node:10.19.0-windowsservercore `
  --build-arg core=mcr.microsoft.com/windows/servercore:1803 `
  --build-arg target=mcr.microsoft.com/windows/nanoserver:1803 .
docker build -t node:10.19.0-nanoserver `
  --build-arg core=mcr.microsoft.com/windows/servercore:1803 `
  --build-arg target=mcr.microsoft.com/windows/nanoserver:1803 `
  --build-arg "SETX= " nano
docker build -t node:10.19.0-pure `
  --build-arg core=mcr.microsoft.com/windows/servercore:1803 `
  --build-arg target=mcr.microsoft.com/windows/nanoserver:1803 pure
```

Watch out for the SETX parameter to have a blank value to overwrite the `/M` default needed for 2016.

