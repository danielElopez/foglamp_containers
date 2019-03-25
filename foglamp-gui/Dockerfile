FROM ubuntu

# Update package lists
RUN apt-get update

# Install needed prerequisites
RUN apt-get install -y nginx-light git npm
RUN npm install -g yarn

# Download the raw FogLAMP GUI source files
RUN git clone https://github.com/foglamp/FogLAMP-gui.git /foglamp-gui

# Build and install FogLAMP GUI
WORKDIR /foglamp-gui
RUN ./build --clean-start

# Expose the FogLAMP GUI TCP port externally
EXPOSE 8080

# Set the container to run the GUI on boot
CMD ["nginx", "-c", "nginx.conf", "-p", "/foglamp-gui", "-g", "daemon off;"]