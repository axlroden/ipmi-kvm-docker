## ipmi-kvm-docker

![Docker Image Size (tag)](https://img.shields.io/docker/image-size/solarkennedy/ipmi-kvm-docker/latest)
![Docker Pulls](https://img.shields.io/docker/pulls/solarkennedy/ipmi-kvm-docker)

Ever wanted to access and IPMI KVM console, only to find that you don't
have network access or the right version of java or a compatible
browser or credentials?

This container runs:

* Xvfb - X11 in a virtual framebuffer
* x11vnc - A VNC server that scrapes the above X11 server
* [noNVC](https://kanaka.github.io/noVNC/) - A HTML5 canvas vnc viewer
* Fluxbox - a small window manager
* Firefox - For browsing IPMI consoles
* Java-plugin - Because... you need java to access most IPMI KVM Consoles.

This is a [trusted build](https://registry.hub.docker.com/u/solarkennedy/ipmi-kvm-docker/)
on the Docker Hub.

## Run It

    # on a remote host that can reach ipmi
    ssh admin
    $ docker run -p 8080:8080 axlroden/ipmi-kvm-docker

    # Now on your laptop
    xdg-open http://admin:8080
    # On a mac
    open http://admin:8080
    # Or just open in a browser

### Custom resolution

By default, the VNC session will run with a resolution of 1024x768 (with 24-bit color depth).
Custom resolutions can be specified with the docker environment variable RES, and must include color depth.

    $ docker run -p 8080:8080 -e RES=1600x900x24 axlroden/ipmi-kvm-docker

### Mount volume

In case you need to mount floppy/iso images to the machine you can mount a volume to the container.

    $ docker run -p 8080:8080 -v /your/local/folder:/root/images solarkennedy/ipmi-kvm-docker
