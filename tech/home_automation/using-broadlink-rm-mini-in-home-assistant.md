**Model:** Broadlink RM 4 mini IR

In order for home assistant to interact with broadlink connected devices, home assistant is required to learn the IR codes first. 

[Python Broadlink GitHub](https://github.com/mjg59/python-broadlink)

- Using python-broadlink allows the extraction of raw IR code which can then be used in home assistant. 

## Usage of Python Broadlink CLI
1. Create virtual environment first and pip install broadlink before using below commands
2. Obtain broadlink RM device details (make sure in cli folder first)
`python broadlink_discovery`
3. To make things easier for cli to reference to the device information, create a file in cli folder named BEDROOM.device with contents of RM device details from above command e.g 0x613a 192.168.1.xx a04bcde3351
4. To learn IR codes (learnt IR code will be stored in a file in cli folder of file name aircon.poweron)
`python broadlink_cli —device @BEDROOM.device —learnfile aircon.poweron`

In order for the learnt code to be usable in Home Assistant, convert the string to base64 using [Hex to Base 64 Converter](https://base64.guru/converter/encode/hex)

## Using IR codes in Home Assistant
- Make sure to add Broadlink integration in Home Assistant first.
- [Broadlink - Home Assistant](https://www.home-assistant.io/integrations/broadlink)

1. Open Configuration.yaml with in-built file editor
2. Look for section under switch and add the following:
```yaml
 ..- platform: broadlink
..host: 192.168.1.93
....mac: a0:43:b0:31:f5:81
....switches:
....- name: fan
......command_on: IR base64 code from above
......command_off: IR base64 code from above
....- name: aircon
# and repeat as neccessary
```
3. Save configuration,yaml, proceed to server control and check configuration before restarting home assistant. 

## Using Python Broadlink python library as Python script
```python
import broadlink
devices = broadlink.discover(timeout=5)
devices[0].auth()
devices[0].enter_learning
```