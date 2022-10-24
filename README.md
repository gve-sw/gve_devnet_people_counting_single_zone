# GVE DevNet People Counting - Single Entrance/Exit
People counting and live occupancy solution for Meraki MV Sense cameras, displaying the number of people currently inside a certain space, as well as the total number of people that have entered. This solution is based on stateful processing of the MQTT stream coming from the Meraki MV cameras. 

![/IMAGES/overview.png](/IMAGES/overview.png)

## Contacts
* Stien Vanderhallen
* Roaa Alkhalaf

## Solution Components
* Meraki MV Camera
* Python 3.8
* MQTT Broker
* Docker

## Installation/Configuration

0. Clone this repository

1. Add Meraki API Key, Network ID and Camera Serial to the `env_var.py` file.

```python
MERAKI_API_KEY= "<your-meraki-api-key>"
NETWORK_ID = "<your-meraki-network-id>"
CAMERA_SERIAL = "<your-meraki-camera-serial-number>"
```

2. In the Meraki dashboard, go to the `Cameras` > `[Camera Name]` > `Settings` > `Sense` page.

- Click to `Add` or `Edit` `MQTT Brokers` > `New MQTT Broker` and add your MQTT broker information (one publicly available broker is `broker.emqx.io`, port 1883).

- Add the MQTT Server settings to the `env_var.py` file:

```python
MQTT_SERVER = "<your-mqtt-server>"
MQTT_PORT = <your-mqtt-port> #Please note: integer
```

3. In the Meraki dashboard, go to the `Cameras` > `[Camera Name]` > `Settings` > `Zones` page. 

- Click `New zone` to create a new zone

- Select your entrance/exit area for the zone, set the `Detection Overlap` to 75%, and name the zone `devnet_door` - then click `Add`.

4. In your terminal, build and run this Docker container

```
$ docker build . -t people-counting
$ docker run people-counting
```

5. OR In your terminal, run this prototype as a Python script

```
$ pip3 install -r requirements.txt # do this step only once
$ python3 main.py
```

## Usage

In your browser, navigate to `localhost:5001`.

# Screenshots
![/IMAGES/1.png](/IMAGES/1.png)

### LICENSE

Provided under Cisco Sample Code License, for details see [LICENSE](LICENSE.md)

### CODE_OF_CONDUCT

Our code of conduct is available [here](CODE_OF_CONDUCT.md)

### CONTRIBUTING

See our contributing guidelines [here](CONTRIBUTING.md)

#### DISCLAIMER:
<b>Please note:</b> This script is meant for demo purposes only. All tools/ scripts in this repo are released for use "AS IS" without any warranties of any kind, including, but not limited to their installation, use, or performance. Any use of these scripts and tools is at your own risk. There is no guarantee that they have been through thorough testing in a comparable environment and we are not responsible for any damage or data loss incurred with their use.
You are responsible for reviewing and testing any scripts you run thoroughly before use in any non-testing environment.
