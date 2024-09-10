# netfoundry-router-container
The NetFoundry Router Container will download the ziti binary during startup and it will not autonomously update the ziti binary during run.

If "OVERRIDE_DOWNLOAD_URL" is specified, the binary will be downloaded from the specified link during the container restart.  Otherwise, the ziti binary will be downloaded from github to match the controller version.

### Start the docker ###
* docker run -v /home/ziggy/router2/:/etc/netfoundry/ --env REG_KEY=<Registration Key> <image_name>

If you want to run router in verbose mode:
* docker run -v /home/ziggy/router2/:/etc/netfoundry/ --env REG_KEY=<Registration Key> --env VERBOSE=1 <image_name>

If you want to run ziti with proxy server:
* docker run -v /home/ziggy/router2/:/etc/netfoundry/ --env REG_KEY=<Registration Key> --env HTTPS_PROXY=<proxy_address> <image_name>

**proxy_address** should be in this format: `http://<address>:<port>`
for example: http://10.20.30.40:3120

If you want to download ziti binary from a specific url:
* docker run -v /home/ziggy/router2/:/etc/netfoundry/ --env REG_KEY=<Registration Key> --env OVERRIDE_DOWNLOAD_URL=<url_link>

**WARNING when using OVERRIDE_DOWNLOAD_URL**: 
* This option turns off the automatic update of the binary.
* To update the binary, restart the container with a new `<url_link>`.
* The `<url_link>` will be used to download binary every time the container is restarted, so it is important to keep the url up.
* If the container is restarted without "OVERRIDE_DOWNLOAD_URL" option, it will try to pull binary from github matching controller version.
