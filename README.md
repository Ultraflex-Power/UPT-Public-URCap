README

The purpose of this URCap is to provide an example of how you can set up Universal Robots to work with Ultraflex Power Robobraze.
https://ultraflexpower.com/induction-products/induction-heating-systems/solo-robobraze-series/

It shows a  way to set up the robot’s movements and brazing joint parameters for sequential brazing of an arbitrary number of joints. 

[The video tutorial](https://github.com/Ultraflex-Power/UPT-Public-URCap/blob/main/URCap%20Tutorial.mp4) shows the steps in adding the URCap to your program and customizing it for your application needs.

This URCap delivers 2 nodes to Polyscope: 

Brazing template node (“UF Brazing Template”) 

Brazing node (“UF Brazing Node”). 

## Brazing Template node 

The Brazing Template node generates user selected number of joints to braze. 

Each spawned joint is a folder node consisting of a moving node designated “Approach Nodes” and a moving node designated “Joint Nodes”.  

Approach nodes are meant to guide the robot from its current position to the position close to the target brazing joint. The approach Node Parameters section of the “UF Brazing” node allows the robot to set speed and acceleration while traversing approach nodes. Since this trajectory doesn’t require precise movements, “Approach Node Parameters” are meant to be faster than those for Joint Nodes. Additionally, to reduce robot lock-ups approach nodes use MoveJ type of movement, and both speed and acceleration is set in deg/sec of rotation of the robot’s joints. 

Joint nodes, namely “JoinX” node and “ExitX” (X – is the number of the joint) nodes, are used to get the coil around the target joint (“JointX” nodes) and to go back to the exit position (“ExitX” nodes). These robot movements between these joints are meant to be as precise as possible, so the robot will use MoveL movements with the speed and acceleration set in “Joint Node Parameters”. Note that joint node parameters are rated in mm/sec. In many practical cases, “ExitX” nodes can be linked to the last preceding “Approach Node” for the robot to return to the same position it departed from to get to the joint. 

The brazing template node can be run only when all the approach and joint nodes' waypoints are set up (no yellow nodes). 

## Brazing node 

The brazing node when run, sets the heating power (via a 4-20mA analog output) over the selected time delay to apply the heat. Its internal operation sets the analog output to the selected value, enables a digital output to start the heat, waits for the chosen time, and turns off the digital output to end the heat. 

The analog and digital outputs for the brazing node can be selected in the node itself (for the outside of the template, standalone operation) or in the “UF Brazing” template node. In the latter case, the selected ports will propagate to all spawned brazing nodes inside of the template.

Note: The user must make sure the RF_Enable and RF_Interlock (RF safety) are both on High (True) signal for the brazing node to function as expected

  
