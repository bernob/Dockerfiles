Dockerfiles
===========

Collection of various Dockerfiles for different images

* `ubuntu-dev-base`: ubuntu14.04 + C/C++, Python dev libs. Aditionaly includes some CLI and GUI tools
* `ros-indigo`: Ubuntu_14.04 + ROS-Indigo-desktop-full + C/C++, Python dev libs

## Running GUI

1. Guarantee access to the x server

    	xhost +

2. Make the call to docker image

    	$ docker run -it \
            -v /tmp/.X11-unix:/tmp/.X11-unix \ # mount the X11 socket
            -e DISPLAY=unix$DISPLAY \ # pass the display
            -v /dev/snd:/dev/snd --privileged \ # sound
            --name name_for_container \ # assign any name
            jorgeluisrmx/imagename



## References

* sameersbn and his work with [docker-browser-box](https://github.com/sameersbn/docker-browser-box), from which provided an example of GUI and Audio support for apps within Docker
* The Fábio Rehm mini-tutorial [Running GUI apps with Docker](http://fabiorehm.com/blog/2014/09/11/running-gui-apps-with-docker/)
* A relevant [stackoverflow question](http://stackoverflow.com/questions/25281992/alternatives-to-ssh-x11-forwarding-for-docker-containers) about using docker with x-server.
* Jessie Frazelle's Blog about [Docker Containers on the Desktop](https://blog.jessfraz.com/posts/docker-containers-on-the-desktop.html)
* [Guidance for Docker Image Authors](http://www.projectatomic.io/docs/docker-image-author-guidance/)
* Stack overflow question about [running Gtk based GUI inside Docker](http://stackoverflow.com/questions/28392949/running-chromium-inside-docker-gtk-cannot-open-display-0)
