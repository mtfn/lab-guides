# Driving
Teleop-twist-keyboard must be run on the Turtlebot itself via SSH. In the home directory, there might be a drive.bash file which can be run using `source drive.bash`.
If the file is not there, here are instructions on how to create it/set up driving:

## On local machine
1) Download teleop-twist-keyboard to your machine and setup a workspace for it (here we'll call our workspace `drive_ws`).

       git clone https://github.com/ros2/teleop_twist_keyboard drive_ws/src/teleop_twist_keyboard

2) Upload the new workspace to the Turtlebot, using similar syntax to SSH. You'll have to switch to dronenet WiFi beforehand.

       scp -r drive_ws ubuntu@192.168.185.robot_number:~

## On Turtlebot
After SSHing into the Turtlebot with `ssh ubuntu@192.168.185.robot_number`,

1) Compile teleop-twist-keyboard:
       
       cd drive_ws
       colcon build

2) To start driving, run these two commands. The first sources the workspace with teleop-twist-keyboard and the second autodetects the robot namespace to launch it. It might take a few seconds before the robot becomes responsive.

       source ~/drive_ws/install/setup.bash
       ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args --remap /cmd_vel:=$(echo $ROBOT_NAMESPACE)/cmd_vel

You can save these two commands to a file called `setup.bash` and run that whenever you want to drive.