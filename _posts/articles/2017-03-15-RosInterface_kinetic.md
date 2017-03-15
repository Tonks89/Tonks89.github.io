---
layout: post
title: Installing VREP-RosInterface on Kinetic
excerpt: "A guide for a manual installation."
modified: 2017-03-01T14:17:25-04:00
categories: articles
tags: [sample-post]
insert_logo: true
image:
  feature: so-simple-sample-image-1.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
comments: true
share: true
---

Here are a list of steps for manually installing the VREP-RosInterface using ROS kinetic. 

## 1. Install the required software
* ROS kinetic
* C++ compiler
* V-REP Stubs generator: v_repStubsGen
    * Python interpreter (2.7 or greater)
    * lxml package for Python
    * tempita package for Python  
(Note: This tutorial assumes you already have a C++ compiler)


### a) Install the required software for v_repStubsGen

```shell 
$ sudo apt-get install -y git cmake python-tempita python-catkin-tools python-lxml
```

or (if you dont’t have ROS kinetic)
    
```shell 
$ sudo apt-get install -y ros-kinetic-desktop-full git cmake python-tempita python-catkin-tools python-lxml
```


### b) Now, install v_repStubsGen in a directory that you want

```shell 
$ cd /home/user/Software/vrep_ros_interface 

$ git clone -q https://github.com/fferri/v_repStubsGen.git
```

(Check your installation: You should see v_repStubsGen listed)
```shell 
$ ls
```

### c) Add v_repStubsGen path to search path for importing python modules

```shell 
$ export PYTHONPATH=$PYTHONPATH:$PWD

$ echo $PYTHONPATH 
```

## 2. Create a temporary catkin workspace

```shell 
$ mkdir -p /tmp/quickstart_ws/src
```

## 3. Initialize this workspace

```shell
$ cd /tmp/quickstart_ws 

$ catkin init
```
You should see the following workspace configuration:

<figure>
	<img src="../../images/posts/vreprosint/Catkin_init.png" alt="image">
</figure>



## 4. Clone & build the vrep_ros_interface in this workspace

```shell
$ cd src/

$ git clone https://github.com/fferri/v_repExtRosInterface.git vrep_ros_interface
```
You should see the vrep_ros_interface listed.

```shell
$ ls
```


```shell
$ catkin build
```

Your workspace should now look like this:

<figure>
	<img src="../../images/posts/vreprosint/Catkin_build.png" alt="image">
</figure>




## 5. Check resulting vrep-ros library in devel folder

```shell
$ cd ../devel/lib/
$ ls
```
You should see a library called "libv_repExtRosInterface.so"

## 6. Source workspace

```shell
$ cd ..
$ cd ..
$ source devel/setup.bash
```

## 7. Copy library in Vrep installation folder

```shell
$ cp -iv devel/lib/libv_repExtRosInterface.so "$VREP_ROOT/"
```

Where  "VREP_ROOT" contains the path of your vrep installation folder. You can create this variable as follows:

* Add "VREP_ROOT" in bash:
    
    ```shell
    $ gedit ~/.bashrc &
    ```

* Add the following line at the end of the file:
    
    ```shell
    $ export VREP_ROOT="/home/user/Software/V-REP_PRO_EDU_V3_3_2_64_Linux/"
    ```

* Source bash in terminal:

    ```shell
    $  source ~/.bashrc 
    ```

* Check if the variable is working:
    
    ```shell
    $ echo $VREP_ROOT   
    ```


## 8. Run one of VREP’s simulation scenes/models

(Note: roscore should be running before vrep)

* rosInterfaceTopicPublisherAndSubscriber.ttt 
* controlTypeExamples.ttt (focus on the bright red robot) 
* Models/tools/rosInterface helper tool.ttm (model allowing to operate V-REP in Synchronous * mode, e.g. in order to manually step the simulation)

