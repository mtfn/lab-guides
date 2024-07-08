# SLAM Toolbox setup
This assumes that your local machine has all relevant Turtlebot packages installed. Unless otherwise specified, run all commands on your local machine (lab laptop, etc.)

1) Download [customslam.launch.py](./customslam.launch.py) and edit the first line of code to reflect your robot’s namespace. Here we use `cabrillo` as an example. Remember to include the /

       bot_namespace = '/cabrillo'


2) Navigate to where you downloaded the file and run it. It will produce a lot of error messages, but give a few minutes for it to “register the LIDAR device”, after which the errors should stop or slow down.

       ros2 launch customslam.launch.py


3) On local machine: in a new terminal, launch Turtlebot4 visualization, using your robot’s namespace as an argument. You should see a map start to show up.

       ros2 launch turtlebot4_viz view_robot.launch.py namespace:=/cabrillo

4) Drive your robot around using teleop twist keyboard! Here’s a driving strategy:
    - Drive the robot in a straight line to a place it hasn’t seen
    - Stop and give it a few seconds to scan the new location
    - Repeat

5) Save your map. Change `my_map` to your desired map name and also supply the correct namespace.

       ros2 run nav2_map_server map_saver_cli -f "my_map" --ros-args -p map_subscribe_transient_local:=true -r /map:=/cabrillo/map

6) Abort processes as needed in terminal using Ctrl+C.
