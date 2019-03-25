# foglamp_containers

This is a Docker image of FogLAMP based on Debian.  You can run the container for FogLAMP via

$ docker run --name foglamp -p 8081:8081 danieleduardolopez/foglamp

And you can run the container for the FogLAMP GUI via

$ docker run --name foglamp-gui -p 8080:8080 danieleduardolopez/foglamp-gui
