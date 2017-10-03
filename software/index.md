---
layout: page
title: Software,  Projects, and Manuals
excerpt: "software&projects"
modified: 2016-06-01T14:07:07-04:00
insert_logo: true
insert_title: true
#image:
#  feature: so-simple-sample-image-6.jpg
#  credit: WeGraphics
#  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
---

# ROBOT PERCEPTION, DECISION-MAKING, CONTROL

## Perception for pick and place

#### Tools: ROS, Gazebo, Rviz, Python

The objective of this project was to construct a perception pipeline to allow the PR2-robot to recognize specific objects in a cluttered environment for pick and place operations. The pipeline takes as input noisy data from the robot's RGB-D camera and outputs .yaml files containing objects labels, their pick and place positions, and the arm to be used during these operations.

<center>
<figure>
	<img src="../../images/Software/RoboND_Perception/image_cover1.png" alt="image">
	<figcaption> PR2 robot in an environment cluttered with different objects. </figcaption>
</figure>
</center>


The perception pipeline consisted of 3 mains parts:
* Part 1: Filtering and RANSAC plane fitting to clean the image and isolate the region of interest.
* Part 2: Clustering for segmenting the scene into individual objects.
* Part 3: Feature extraction, SVM training and object recognition

Given a list of objects to pick from the scene, the pipeline is used to recognize the desired objects and assign them labels. This information is later used to determine the object's pick and place position and the arm to be used in this operation.

Below is an example scene where this pipeline was used for object recognition. The robot was able to recognize 8/8 objects:

<center>
<figure>
	<img src="../../images/Software/RoboND_Perception/image11.png" alt="image">
	<figcaption> PR2 robot recognizing objects in a cluttered environment. </figcaption>
</figure>
</center>

You can find more details on this project in [this](https://github.com/Tonks89/RoboND-Perception-Project) repository.



## Pick and place 

#### Tools: ROS, Moveit!, Gazebo, Rviz, Python

The objective of this project was to write an Inverse Kinematics (IKM) solver for the KUKA KR210 robot. This solver is responsible for computing the joint angles corresponding to a desired end-effector or gripper trajectory. The algorithm was tested on pick and place operations, consisting of collecting objects from different locations on a shelf and depositing them on a bin.

<center>
<figure>
	<img src="../../images/Software/RoboND_Kinematics/kuka_pickplace.png" alt="image">
	<figcaption> Kuka KR210 in a pick and place operation. </figcaption>
</figure>
</center>


In order to create the IKM solver, first, a kinematic analysis was done consisting of the following steps:
* Mathematical description of the robot's geometry and determination of its DH parameters.
* Computation of its Forward Kinematic Model (FKM)
* Computation of its Inverse Kinematic Model (IKM): Since the robot has a spherical wrist, this problem was decoupled into an inverse position kinematic problem (to determine the first 3 joint variables), and an inverse orientation kinematic problem (to determine the last 3 joint variables).

After implementing this analysis as a python script, the robot was tested in 10 pick and place operations (with different spawn locations). The results show that the robot is able to successfully pick and place the objects 9/10 times while following the desired end-effector trajectories. 

The following video shows a pick and place operation in Rviz (2x actual simulation speed):

<iframe width="560" height="315" src="https://www.youtube.com/embed/OULJVEaE0yI" frameborder="0" allowfullscreen></iframe>


Here, is another example in in Gazebo (4x actual simulation speed):

<iframe width="560" height="315" src="https://www.youtube.com/embed/egHG-RJTBWs" frameborder="0" allowfullscreen></iframe>

You can find the code and a detailed writeup of this project in [this](https://github.com/Tonks89/RoboND-Kinematics-Project) repository.



## Search and sample

#### Tools: Python and Unity game engine 

This project was modeled after the "NASA sample return challenge", its objective was to enable a rover to navigate autonmously in an unknown environment by developing its ability perceive and decide. To achieve this, two modules were developed: a perception and ad decision-making module. The perception module was used to detect obstacles, rocks (sample of interest), and navigable terrain based on computer vision techniques such as perpective transform, color space transformation, thresholding and distortion reduction. The following video shows how the rover is able to perceive the navigable terrain (blue), rocks (yellow), and obstacles (red) to update its worldmap.

<iframe width="560" height="315" src="https://www.youtube.com/embed/QTcLjp4bDvg" frameborder="0"></iframe>

The decision-making module consisted of a decision tree which ensured obstacle avoidance and a wide exploration of the navigable terrain.
After implementing the previous perception and decision steps. The rover was launched in autonomous mode several times. A mean of its performance was made over 10 trials with respect to the base requirements for the project (40% mapping at 60% fidelity). The rover is able to map at least 40% of the terrain with an accuracy of approximately 81% while finding at least a rock. The rover is of course capable of mapping more terrain and finding more rocks, but the previous statistics were computed to compare its performance with the base requirements.

The following video shows the rover navigating autonomously while mapping 81% of its environment with 65% fidelity and several rock sample detections.

<iframe width="560" height="315" src="https://www.youtube.com/embed/t6gBQkwMJ14" frameborder="0"></iframe>

Currently, I am working on smoothing out the changes in steering direction by implementing a PD controller to minimize oscillations. This update will be posted shortly.
You can find the code and a detailed writeup in [this](https://github.com/Tonks89/RoboND-Rover-Project) repository.

 

## Toolbox for the simulation of the kinematics and sensors of mobile robots 

#### Tools: MATLAB and Simulink

Authors: Ana Lucia Cruz & Ekaterina Peshkova  
A toolbox in MATLAB/Simulink, containing:  
1) A library of kinematic models and sensors (exteroceptive and proprioceptive).    
2) A graphical user interface that allows users to build ready-to-use simulink models containing the different components in the library with personalized parameters.  
The toolbox has been tested on control and localization simulations (for example: odometry, sequential localization).

<figure>
	<a href="/images/GUI_mobilerobot.jpg"><img src="/images/GUI_mobilerobot.jpg" alt="image"></a>
</figure>

#### Download

Coming soon!


# ROBOT DESIGN

##  ARACHNIS: A GUI to design and analyze cable-driven robots 

#### Tools: MATLAB

ARACHNIS is a graphical user interface for the analysis and parametric design of Cable Driven Parallel Robots (CDPRs). This interface takes as inputs the design parameters of the robot, the task specifications, and returns a visualisation of a set of workspaces to assess the designs. These workspaces are the  Wrench Feasible Workspace (WFW) and the Interference-Free Constant Orientation Workspace (IFCOW). The WFW is traced from the capacity margin, a measure of the robustness of the equilibrium of the robot. On the other hand, the IFCOW is traced via an existing technique for determining the interferences between the moving parts of CDPRs.

<figure>
	<a href="/images/cable_robot_interface.jpg"><img src="/images/cable_robot_interface.jpg" alt="image"></a>
</figure>


#### Reference
* **Ana Lucia Cruz Ruiz**, Stéphane Caro, Philippe Cardou, François Guay.***"ARACHNIS: Analysis of Robots Actuated by Cables with Handy and Neat Interface Software"***, In Proceedings of the Second International Conference on Cable-Driven Parallel Robots. [Link](http://link.springer.com/chapter/10.1007/978-3-319-09489-2_21#page-1)


#### Download

Click [here](/share/Arachnis20.zip) to download the latest verion of the interface.


##  A 3 DOF PPR parallel robot

#### Tools: CATIA, MATLAB

This project consisted in designing a parallel robot for assembly operations. To perform this task, the desired mobility of the robot was two translations and one rotation. Such mechanisms are commonly known as cylindrical parallel mechanisms and they are usually employed in machining operations. To comply with the desired assembly task and motion pattern, the mechanism was designed according to the following priorities:

Priority 1: Be capable of moving throughout a circular regular positional workspace 
RPW of diameter 500 mm;  
Priority 2: The moving platform should have a rotation range equal to ±30 degrees for any 
position of its geometric center within the RPW;   
Priority 3: The mechanim should be light;  
Priority 4: The legs of the mechanism should be identical, namely, the mechanism 
should be symmetrical;  
Priority 5: The point-displacement of the geometric center of the moving-platform 
should be smaller than 1 mm for a payload equal to 500 N (the payload is supposed to 
be normal to the moving platform);  
Priority 6: The rotational error of the moving platform should be smaller than 1 degree for 
a moment equal to 100 N.m about the axis passing through the geometric center of the 
moving platform and normal to the latter.
<figure>
	<a href="/images/PPR_robot.jpg"><img src="/images/PPR_robot.jpg" alt="image"></a>
</figure>


#### Download
Coming soon!  
For a detailed report on how the mechanism was designed just drop me an email.

<hr>

# MACHINE LEARNING

## Low-dimensional control strategies for virtual characters

#### Tools: MATLAB, SimMechanics, Non-negative matrix factorization toolbox

This research work was done within the framework of the project [ENTRACTE](http://homepages.laas.fr/nmansard/entracte/index.php?n=Main.HomePage) (Anthropomorphic Action Planning and Understanding), winner of the Grand Prix de l'ANR and funded by the French National Research Agency.

The objective of this project was to design simple and compact motion controllers for virtual characters by analyzing how humans control motion. To do this, experiments were conducted in which humans were asked to perform different motor tasks while muscle activity and kinematics were recorded. From this data, an analysis was done to extract the underlying control strategies (or synergies) using machine learning techniques. Such controllers were then adapted to command virtual characters in physics-based environments.

<iframe width="560" height="315" src="https://www.youtube.com/embed/YHO3eeFI0NI" frameborder="0"></iframe>

#### Reference

* **Ana Lucia Cruz Ruiz**, Charles Pontonnier, and Georges Dumont. ***"A synergy-based control solution for overactuated
characters: application to throwing"***, Computer Animation and Virtual Worlds, 2016. [Link](http://onlinelibrary.wiley.com/doi/10.1002/cav.1743/abstract)