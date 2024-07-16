# SSH

## SSH tutorial
### Over WiFi (preferred)

1) Find a Turtlebot and check its little display. It should show an IP of the form `192.168.185.xxx`. If the IP starts with something else, you'll want to connect with an Ethernet cable instead.
2) Connect your device to the `dronenet` WiFi network if it is not already.
3) In a terminal window, type `ssh ubuntu@192.168.185.xxx` (whatever you saw on the display).
4) Type `yes` if it asks you to trust the connection.
5) The password is `turtlebot4`.

### Over Ethernet cable
1) Connect your device and the Turtlebot via an Ethernet cable (the port is on the rear, behind the camera).
2) `ssh ubuntu@192.168.185.3`. You won't need to connect to any WiFi network.
3) Same process as above from here.

## Convenient tricks
### Aliasing
Instead of memorizing IP addresses, a file containing robot names is provided.
1) Find your SSH config file. It's probably `%/.ssh/config` on Linux/Mac, `%USERPROFILE%\.ssh\config` on Windows. If it doesn't exist, create it. Keep in mind that it's a file with no extension.
2) Copy the contents of the [provided file](./config) and append it at the end of your SSH config file.
3) Now you can SSH into robots named in the file with a command like `ssh cabrillo`.

Note that this approach won't account for if robot IP's change. If it's failing, try SSHing the normal way as listed above.

### Passwordless login
Here's how you can setup an SSH key so you don't have to type in the password every time you SSH into a robot.
1) Inspect your `~/.ssh` folder. You'll find your config file, and hopefully some SSH keys (ex. `id_rsa.pub`).
2) If there aren't any keys, type `ssh-keygen` to create a new one.
3) Upload it to the Turtlebot using `ssh-copy-id ubuntu@192.168.185.xxx` or just something like `ssh-copy-id cabrillo` if you have aliasing set up. Do this for every robot you want to connect to.

Note: `ssh-copy-id` doesn't exist on Windows. You'll need to manually copy the contents of your `.pub` file and append them at the end of the `~/.ssh/authorized_keys` file on the robot.
