# Connect your Bosch Indego with MQTT to Loxone

This is not a step-by-step howto. You should read some howtos to mosquitto and node-red to get it working and do understand it.

## USE AT YOUR OWN RISK

First of all, it is important to mention that I don't want to advertise any product, app or software. The components I use can be replaced by other, similar components if necessary. 

# Solution
Loxone -> Node-RED -> MQTT -> Bosch Indego MQTT Adapter

Node-RED is installed on a Raspberry Pi - of course :-)

# Installation
## Setup Node-Red
- Install Node-RED. See: https://nodered.org/docs/getting-started/installation
- Install node-red-contrib-httpauth

## Setup mosquitto
- Install the MQTT Broker mosquitto https://mosquitto.org
- Configure the connection (configure password, configure bind address, logging ...)

## Setup the Bosch Indego MQTT Controller
- Install the Bosch Indego Controller from https://github.com/zazaz-de/iot-device-bosch-indego-controller
- Place the files in /opt/indego/ so that there is /opt/indego/bin/IndegoMqttAdapter and /opt/indego/IndegoMqttAdapterConfig.properties
- Configure the IndegoMqttAdapterConfig.properties accordingly. See https://github.com/zazaz-de/iot-device-bosch-indego-controller for more information.
- Add the indego systemd service file (see this repo) to /lib/systemd/system and enable the service with systemctl enable indegomqtt.service.
- Afterward you should be able to start/stop the Indego MQTT service with systemctl start indegomqtt

## Setup Node-Red Flow
- Import the flow to Node-RED
- Setup the connection to your mosquitto MQTT Broker (in all MQTT nodes, like IndegoStateMessage or IndegoCommand)
- Change USERNAME/PASSWORD in all httpauth nodes
- Deploy the Node-RED flow
- Afterwards you should be able to get the Indego state by using http://node-red-ip-address:1880/indego/status

## Loxone Configuration
- Add a virtual input to receive the Indego mode_code, error and the completed state
- Add virtual output to send the commands to mow, pause and return

# Thanks
Thanks to all the great Open Source components - mosquitto, node-red-contrib-httpauth and Node-RED. 

- Thanks to zazaz-de for https://github.com/zazaz-de/iot-device-bosch-indego-controller
- Node-RED: https://nodered.org
- node-red-contrib-httpauth: https://www.npmjs.com/package/node-red-contrib-httpauth

## USE AT YOUR OWN RISK

# Copyright

Copyright(c) 2018 Bernhard Suttner / http://www.bernhard-suttner.de

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see http://www.gnu.org/licenses/.
