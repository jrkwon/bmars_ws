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

# SLAM

`https://roboticsbackend.com/ros2-nav2-generate-a-map-with-slam_toolbox/`

## DDS Configuration
There might be some issues with a default DDS. Consider using `Cyclone DDS`.

## Install Nav2 and SLAM Toolbox 

```
sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup
```

```
sudo apt install ros-humble-slam-toolbox
```

## Start Nav2 and SLAM Toolbox

1. Start your robot.
2. Start Nav2
   ```
   ros2 launch nav2_bringup navigation_launch.py
   ```
3. Start SLAM Toolbox
   ```
   ros2 launch slam_toolbox online_async_launch.py
   ```
4. Start RViz2
   ```
   ros2 run rviz2 rviz2 -d /opt/ros/humble/share/nav2_bringup/rviz/nav2_default_view.rviz
   ```

## Build a map
1. Make the robot move
   ```
   ros2 run teleop_twist_joy teleop_node 
   ```
2. Save the map
   ```
   ros2 run nav2_map_server map_saver_cli -f my_map
   ```

# Navigation 
`https://husarion.com/tutorials/ros2-tutorials/8-slam/`
## Load a saved map
1. Load a map
   ```
   ros2 run nav2_map_server map_server --ros-args -p yaml_filename:=map.yaml
   ```
2. Start `map_server`
   ```
   ros2 run nav2_util lifecycle_bringup map_server
   ```

## AMCL
