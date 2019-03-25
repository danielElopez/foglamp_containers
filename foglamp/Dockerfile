FROM arm32v7/debian

# Update package lists
RUN apt-get update
ENV DEBIAN_FRONTEND=noninteractive

# Install needed prerequisites
RUN apt-get install -y avahi-daemon curl git cmake g++ make build-essential autoconf automake
RUN apt-get install -y sqlite3 libsqlite3-dev
RUN apt-get install -y libtool libboost-dev libboost-system-dev libboost-thread-dev libssl-dev libpq-dev uuid-dev
RUN apt-get install -y python3-dev python3-pip python3-dbus python3-setuptools
RUN apt-get install -y postgresql

# Install helpful prerequisites for use on Debian
RUN apt-get install -y apt-utils libz-dev sudo

# Download the raw FogLAMP source files
RUN git clone https://github.com/foglamp/FogLAMP.git /foglamp

# Build and install FogLAMP
WORKDIR /foglamp
RUN make
RUN make install

# Install rsyslog for log processing
RUN apt-get install -y rsyslog

# Change directories to where the FogLAMP startup script will reside
WORKDIR /usr/local/foglamp

# Add a script that will start up FogLAMP (first starting rsyslog, which must be running first)
RUN echo "#!/bin/bash \nservice rsyslog start \nbin/foglamp start \ntail -f /var/log/syslog" > foglamp.sh 

# Apply permissions to the FogLAMP startup script
RUN chmod 777 /usr/local/foglamp/foglamp.sh

# Expose the FogLAMP management TCP port externally
EXPOSE 8081

# Set the container to run the startup script on boot
CMD ["./foglamp.sh"]