# Scout

## Setup CAN

If no `can-utils` is installed, install it.

```
# install can utils
sudo apt install -y can-utils
```

If this is the first time to bring up CAN interface, enable the `gs_usb` kekrnel module.
```
# enable kernel module: gs_usb
sudo modprobe gs_usb
```

## Start CAN

```
# bring up can interface
sudo ip link set can0 up type can bitrate 500000
```
If your CAN port number is not `0`, use user CAN port number rather than `0` in `can0`.

# Oustere LIDAR

## Connecting the Sensor

If directly connecting to the host machine you may need to set your Ethernet interface to `Link-Local Only` mode. This can be done via the command line or GUI. 

### GUI

- Find `Wired` at Settings - Network. 
- Select the `IPv4` tab. 
- Under `IPv4 Method`, select `Link-Local Only`

## Launching Nodes

### Sensor Mode

The driver parameters are at `src/ouster-ros/ouster-ros/config/driver_params.yaml`

`sensor_hostname` must be set to connect. Use the IP address or hostname of the sensor.

```
ros2 launch ouster_ros driver.launch.py
```
