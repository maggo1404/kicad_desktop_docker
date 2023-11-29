# kicad_desktop_docker
A package that builds docker image for KiCad using noVNC.

![image](https://user-images.githubusercontent.com/34224090/134472668-44e86380-3eb7-4ab2-8bb9-c19618cc00b0.png)  

## Overview
The software launches a noVNC-accessible GNOME desktop in a Docker container, providing a KiCad runtime environment.

### System Requirements
The environment required to run it is as follows

- Ubuntu 20.04
  - Operation has not been checked in other environments.
- Docker build & run Enabling environment.
  - amd64
  - An OpenGL-compatible PC is recommended.
  - 10 GB free space (required for image creation).
- (web) browser
  - Firefox,Chrome,Edge

### Software version
Version information of the software in use.

- Ubuntu
  - 20.04 (focal)
- [KiCad](https://www.kicad.org/)
  - 6.0 release ver
- [VirtualGL](https://www.virtualgl.org/)
  - 2.6.5
- [kicad-i18n](https://github.com/KiCad/kicad-i18n.git)
  - 5.1

## Build
Build a docker image as follows．

```
$ git clone https://github.com/nomumu/kicad_desktop_docker.git
$ cd kicad_desktop_docker
kicad_desktop_docker$ docker build . -t kicad_desktop_docker
```

## Run
Start the Docker environment with an executable script.

### Command
Run the executable script as follows.
```
kicad_desktop_docker$ ./run.sh
```

Mount `homedir` in the same hierarchy as `run.sh` as the desktop HOME directory.
Create a user in Docker that runs `run.sh` to do the work.

### VNC
You can connect to the desktop environment by accessing the 15900 port of the PC on which you have run `run.sh` from a browser.

```
http://192.168.x.xxx:15900/vnc.html
```

### Options
- Arguments can be specified as follows. Use this when you want to start multiple environments.
`./run.sh <CONTAINER_NAME> <PORT_NUMBER>`
  - CONTAINER_NAME: Specify the docker container name.
  - PORT_NUMBER: 

## KiCad
Specifies the port for the desktop connection

![image](https://user-images.githubusercontent.com/34224090/134477367-350aadbf-d0b5-4e3b-b63c-4f8aa37847ab.png)  

 If you want to check that it works, use the demo project installed in `/usr/shara/kicad/demos/`.

This Docker environment is configured to use VirtualGL to handle KiCad's 3D functionality. In the following dialog you can select `Enable Accelerator`.
![image](https://user-images.githubusercontent.com/34224090/134478189-dfd1be81-d03b-4c8b-866b-c3d9aac868e9.png)  

Libraries that need to be saved should be properly configured to be placed under `/home/<your kicad user>/`.

![image](https://user-images.githubusercontent.com/34224090/134479151-e37f9623-1c78-4384-b6e0-fa06edac6d5b.png)  

## Save
Data stored under `/home/<your kicad user>/` in the Docker environment will be maintained.
Substrate data can be retrieved by direct access to the mounted `homedir`.

## Download
Files stored in `/home/<your kicad user>/to_download/` can be downloaded from `http://192.168.x.xxx:15900/download/`. Use it to retrieve Gerber data, for example.
The contents of this directory are deleted when the Docker container is stopped, so treat it as a temporary area.

Übersetzt mit DeepL (https://www.deepl.com/app/?utm_source=ios&utm_medium=app&utm_campaign=share-translation)

## Tips
- Switching to full screen with F11 etc. will increase the number of shortcuts enabled, so please use them effectively.
- Japanese input is possible with the `Full/Halfwidth` key on the Japanese keyboard.
 - Please use it for file names and design memos.
- The system supports connections with multiple people, so please use it effectively for reviews, etc.
 - When screen resizing is enabled for multiple connections, the last resizing is reflected.
 - There may be processing problems with key codes in some environments and browser combinations.
 - Access from a browser on Windows is most stable.
 - If the desktop environment becomes sluggish, it may be possible to save the files that need saving and recreate homedir to resolve the problem.
 - The Docker container can be stopped with the following command
   docker stop kicad_desktop
