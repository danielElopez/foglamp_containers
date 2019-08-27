# foglamp_containers

This is a Docker image of FogLAMP based on Debian.  You can run the container for FogLAMP via

'''
$ docker run --name foglamp -p 8081:8081 danieleduardolopez/foglamp
'''

And you can run the container for the FogLAMP GUI via

'''
$ docker run --name foglamp-gui -p 8080:8080 danieleduardolopez/foglamp-gui
'''

To install a south plugin into FogLAMP (from GitHub; to see more plugins, see https://github.com/foglamp), enter a shell session on the FogLAMP container by running (from a new command prompt or from one of the prompts used earlier)

'''
docker exec -it foglamp bash
'''

And install the south plugin for generating simulated random data via these two commands (which you are now running from within the shell session that you opened to your FogLAMP container in your previous step) 

'''
PLUGIN_NAME="foglamp-south-randomwalk"

git clone https://github.com/foglamp/$PLUGIN_NAME.git /$PLUGIN_NAME && echo "Installing requirements (if needed)..." && (pip3 install -r /$PLUGIN_NAME/python/requirements* || true) && echo "Copying files to target directory..." && cp -R /$PLUGIN_NAME/python/foglamp/plugins/south/* /usr/local/foglamp/python/foglamp/plugins/south/ && echo "Plugin installed."
'''

You can also install the south plugin for generating a sine wave pattern via these two commands

'''	
PLUGIN_NAME="foglamp-south-sinusoid"

git clone https://github.com/foglamp/$PLUGIN_NAME.git /$PLUGIN_NAME && echo "Installing requirements (if needed)..." && (pip3 install -r /$PLUGIN_NAME/python/requirements* || true) && echo "Copying files to target directory..." && cp -R /$PLUGIN_NAME/python/foglamp/plugins/south/* /usr/local/foglamp/python/foglamp/plugins/south/ && echo "Plugin installed."
'''

Finally, you can install a plugin for reading live weather data using the below commands (which are identical to the ones above, save for the plugin name being different):

'''
PLUGIN_NAME="foglamp-south-openweathermap"

git clone https://github.com/foglamp/$PLUGIN_NAME.git /$PLUGIN_NAME && echo "Installing requirements (if needed)..." && (pip3 install -r /$PLUGIN_NAME/python/requirements* || true) && echo "Copying files to target directory..." && cp -R /$PLUGIN_NAME/python/foglamp/plugins/south/* /usr/local/foglamp/python/foglamp/plugins/south/ && echo "Plugin installed."
'''
	
Next configure the south plugin(s) that you just installed by opening a web browser to the following URL

http://localhost:8080/#/south 

Once there, click on the "Add +" button in the top-right corner to add a plugin (you can give it any name that you like); feel free to accept all of the defaults for these plugins.

Shortly, you should start seeing readings accumulate in your FogLAMP container!  To view that data, navigate your browser to

http://localhost:8080/#/asset 

And click the little blue trend icon next to each listed asset to start trending its data!
