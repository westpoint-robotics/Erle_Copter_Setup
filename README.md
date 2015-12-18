### Connecting Erle Copter on Wifi Network.
 1. Power up the Erle copter and wait for erle brain to create a wifi hotspot.
 2. Connect to the erle wifi hotspot using the passwrod 'holaerle'
 3. Open a terminal and ssh into erle copter using following command.
   <br><code> ssh ubuntu@10.0.0.1 </code> and password is 'ubuntu'
 4. ROScommands are not permitted unless you are a root. Upgrate to root using following command
  <br> <code> su </code>
 5. You can check the running processes using <code> ps -e </code>
 6. check the published rostopics using <code>rostopic list</code>
 
### Connect to a wifi network
 1. Get to step 4 of the above setup.
 2. On the host laptop get the wifi network details using following command <code> wpa_passphrase <ssid> <pw></code>
 3. Paste this information into /etc/wpa_supplicant/wpa_supplicant.conf
 4. source wifi/wifi-setup.sh
 5. Erle brain will disconnect from the current setup and connects to the above mentioned network.
 6. Connect to Erle brain using <code> ssh ubuntu@10.0.0.1</code> PS: change IP to the assigned IP address of Erle brain
 
### connecting to Erle brain using USB.
 1. Connect Erle brain using usb
 2. check the port of the Erle brain( Either eth0 or usb0) 
 3. assign a IP address using <code> sudo ifconfig usb0 192.168.7.2 </code>
 4. and connect to Erle using ssh and the assigned IP address.
 
### Configuring roscore for host computer and Erle brain
 1. mavros node is already running on erle brain.
 2. To be able to access mavros topics on the host computer, set up two parameters on either side
  a.<br> On Erle brain: export these two environement parameters.</br>
      1. export ROS_MASTER_URI=http://10.0.0.1:11311  (Erle brain IP )
 <br> 2. export ROS_IP=10.0.0.1 (Erle brain IP)
  b.<br>on Host computer:</br>
      1. export ROS_MASTER_URI=http://10.0.0.1:11311  (Erle brain IP )
<br>  2. export ROS_IP=10.0.0.2 (Host computer IP)
 3. You should be able to check the erle brain mavros topics using <code> rostopic list </code> on the host computer.
      
### Takeoff and Land demo
 1. SSH into erle-copter(use PUTTY for Windows, username:ubuntu pw:ubuntu)
 2. Change directory to <code>:/# cd /home/ubuntu/trusty </code>
 3. Create a catking workspace using following commands.  
    <code>:/# mkdir catkin_ws </code>  
    <code>:/# cd catkin_ws </code>  
    <code>:/# mkdir src </code>  
    <code>:/# cd src </code>  
    <code>:/# catkin_init_workspace </code> and then build the package using <code>:/#catkin_make </code> (change directory to /catkin_ws)  
    <code>:/# source /home/ubuntu/opt/ros/indigo/setup.bash </code>
 4. Become the superuser using <code>:/# su </code> command.
 5. change the root directory using following command. <code>:/# chroot . </code>
 6. Copy the ros package using following command  
    <code>:/# cp -a /home/ubuntu/catkin_ws/src/ros_erle_takeoff /home/ubuntu/trusty/catkin_ws/src/ </code>
 7. Build the package using <code>:/# catkin_make </code>  in <code> catkin_ws </code>
 8. <code>:/# source catkin_ws/devel/setup.bash </code>
 9. <code>:/# export ROS_MASTER_URI=http://10.0.0.1:11311 </code>  
    <code>:/# export ROS_IP=10.0.0.1 </code>
 10. Run the demo using following command  
   <code>:/# rosrun ros_erle_takeoff_land ros_erle_takeoff_land </code>  
   ##Important : Make sure to check the Erle copter response using APM planner (Connect to UDP using following address 10.0.0.2:7000 )
   Assign channel 8 switch to emergency stop using 'extended tuning' tab in configuration tab in APMPlanner2  
   Run the script without props and check if the mode changes in APMplanner after the execution of the script.
   
   
### Connecting to APMplanner2
 1. Connect to UDP port using 10.0.0.2:7000 once wifi connection to erle brain is established.
 2. Calibrate the autopilot normally using mandatory calibration
 3. Assign E-stop to channel 8 using extended tuning tab under configuration.
 
