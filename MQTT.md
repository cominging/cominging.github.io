#### IBM IoTF

* [Reference Material](https://iotf.readthedocs.org/en/latest/) for IBM's IoT Foundation service 

#### Bridge a Mosquitto device to IBM IoTF

Required content of `mosquitto.conf`:
```bash
connection <connection-name>
address <address[:1883]>

#topic <topic> [[[out | in | both] qos-level] local-prefix remote-prefix]
topic iot-2/cmd/+/fmt/json in "" ""
topic iot-2/evt/+/fmt/json out "" ""

# A Device must authenticate using a client ID in the following format:
# d:org_id:device_type:device_id
remote_clientid <clientid>
remote_username use-token-auth
remote_password <token>

# Compatibility with IBM IoTF
notifications false
cleansession true
bridge_protocol_version mqttv311
# IoTF does not accept protocol version 132 (0x04 | 0x80)
# Turn try_private off; otherwise it refuse to authorize
try_private false
# IoTF does not accept unsubscribe for 'in'coming topics, turn this off
bridge_attempt_unsubscribe false
```
