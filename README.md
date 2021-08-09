# ROS_Basics
## Creating simple python publish and subscribe nodes 

## **A. Install ROS**



## **B. Creating Workspace and Package**

### **1. Create a workspace**

**1.1. Workspace**

* Create a directory named *‘FAIlearning_ws’* and then create a source folder. All our ROS packages will be in this source folder. Running *'catkin_make'* command will make this current directory a catkin workspace and also compile it. The workspace now is *‘FAIlearning_ws’*

```shell
$ mkdir -p ~/FAIlearning_ws/src
$ cd ~/FAIlearning_ws/
$ catkin_make
```

Output:

```shell
Base path: /home/hoangtu/FAIlearning_ws
Source space: /home/hoangtu/FAIlearning_ws/src
Build space: /home/hoangtu/FAIlearning_ws/build
Devel space: /home/hoangtu/FAIlearning_ws/devel
Install space: /home/hoangtu/FAIlearning_ws/install
Creating symlink "/home/hoangtu/FAIlearning_ws/src/CMakeLists.txt" pointing to "/opt/ros/noetic/share/catkin/cmake/toplevel.cmake"
####
#### Running command: "cmake /home/hoangtu/FAIlearning_ws/src -DCATKIN_DEVEL_PREFIX=/home/hoangtu/FAIlearning_ws/devel -DCMAKE_INSTALL_PREFIX=/home/hoangtu/FAIlearning_ws/install -G Unix Makefiles" in "/home/hoangtu/FAIlearning_ws/build"
####
-- The C compiler identification is GNU 9.3.0
-- The CXX compiler identification is GNU 9.3.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Using CATKIN_DEVEL_PREFIX: /home/hoangtu/FAIlearning_ws/devel
-- Using CMAKE_PREFIX_PATH: /home/hoangtu/catkin_ws/devel;/opt/ros/noetic
-- This workspace overlays: /home/hoangtu/catkin_ws/devel;/opt/ros/noetic
-- Found PythonInterp: /usr/bin/python3 (found suitable version "3.8.10", minimum required is "3") 
-- Using PYTHON_EXECUTABLE: /usr/bin/python3
-- Using Debian Python package layout
-- Found PY_em: /usr/lib/python3/dist-packages/em.py  
-- Using empy: /usr/lib/python3/dist-packages/em.py
-- Using CATKIN_ENABLE_TESTING: ON
-- Call enable_testing()
-- Using CATKIN_TEST_RESULTS_DIR: /home/hoangtu/FAIlearning_ws/build/test_results
-- Forcing gtest/gmock from source, though one was otherwise available.
-- Found gtest sources under '/usr/src/googletest': gtests will be built
-- Found gmock sources under '/usr/src/googletest': gmock will be built
-- Found PythonInterp: /usr/bin/python3 (found version "3.8.10") 
-- Found Threads: TRUE  
-- Using Python nosetests: /usr/bin/nosetests3
-- catkin 0.8.10
-- BUILD_SHARED_LIBS is on
-- BUILD_SHARED_LIBS is on
-- Configuring done
-- Generating done
-- Build files have been written to: /home/hoangtu/FAIlearning_ws/build
####
#### Running command: "make -j2 -l2" in "/home/hoangtu/FAIlearning_ws/build"
####
```

```shell
$ ls
build  devel  src
```

```shell
$ source ~/FAIlearning_ws/devel/setup.bash
```

**1.2. Environment Setup**

```shell
$ source /opt/ros/noetic/setup.bash
$ source ~/FAIlearning_ws/devel/setup.bash
```

```shell
$ gedit ~/.bashrc
```

```
# ROS environment setup
source /opt/ros/noetic/setup.bash
source ~/FAIlearning_ws/devel/setup.bash
```

### **2. Create a package**

```
catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
```

```shell
$ cd ~/FAIlearning_ws/src
$ catkin_create_pkg ros_basic_pkg std_msgs rospy roscpp
```

Output:

```shell
Created file ros_basic_pkg/package.xml
Created file ros_basic_pkg/CMakeLists.txt
Created folder ros_basic_pkg/include/ros_basic_pkg
Created folder ros_basic_pkg/src
Successfully created files in /home/hoangtu/FAIlearning_ws/src/ros_basic_pkg. Please adjust the values in package.xml.
```

```sh
$ cd ~/FAIlearning_ws/
$ catkin_make
```

Output:

```sh
Base path: /home/hoangtu/FAIlearning_ws
Source space: /home/hoangtu/FAIlearning_ws/src
Build space: /home/hoangtu/FAIlearning_ws/build
Devel space: /home/hoangtu/FAIlearning_ws/devel
Install space: /home/hoangtu/FAIlearning_ws/install
####
#### Running command: "cmake /home/hoangtu/FAIlearning_ws/src -DCATKIN_DEVEL_PREFIX=/home/hoangtu/FAIlearning_ws/devel -DCMAKE_INSTALL_PREFIX=/home/hoangtu/FAIlearning_ws/install -G Unix Makefiles" in "/home/hoangtu/FAIlearning_ws/build"
####
-- Using CATKIN_DEVEL_PREFIX: /home/hoangtu/FAIlearning_ws/devel
-- Using CMAKE_PREFIX_PATH: /home/hoangtu/FAIlearning_ws/devel;/home/hoangtu/catkin_ws/devel;/opt/ros/noetic
-- This workspace overlays: /home/hoangtu/FAIlearning_ws/devel;/home/hoangtu/catkin_ws/devel;/opt/ros/noetic
-- Found PythonInterp: /usr/bin/python3 (found suitable version "3.8.10", minimum required is "3") 
-- Using PYTHON_EXECUTABLE: /usr/bin/python3
-- Using Debian Python package layout
-- Using empy: /usr/lib/python3/dist-packages/em.py
-- Using CATKIN_ENABLE_TESTING: ON
-- Call enable_testing()
-- Using CATKIN_TEST_RESULTS_DIR: /home/hoangtu/FAIlearning_ws/build/test_results
-- Forcing gtest/gmock from source, though one was otherwise available.
-- Found gtest sources under '/usr/src/googletest': gtests will be built
-- Found gmock sources under '/usr/src/googletest': gmock will be built
-- Found PythonInterp: /usr/bin/python3 (found version "3.8.10") 
-- Using Python nosetests: /usr/bin/nosetests3
-- catkin 0.8.10
-- BUILD_SHARED_LIBS is on
-- BUILD_SHARED_LIBS is on
-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-- ~~  traversing 1 packages in topological order:
-- ~~  - ros_basic_pkg
-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-- +++ processing catkin package: 'ros_basic_pkg'
-- ==> add_subdirectory(ros_basic_pkg)
-- Configuring done
-- Generating done
-- Build files have been written to: /home/hoangtu/FAIlearning_ws/build
####
#### Running command: "make -j2 -l2" in "/home/hoangtu/FAIlearning_ws/build"
####
```

```sh
$ source ~/FAIlearning_ws/devel/setup.bash
```

## **C. Creating simple Publish and Subscribe nodes**

```sh
$ cd ~/FAIlearning_ws/
$ roscd ros_basic_pkg/
```

```sh
$ mkdir scripts
$ cd scripts/
```

**Node 1**: publisher.py

```python
#!/usr/bin/env python

import rospy
from std_msgs.msg import String

def publisher():
    pub = rospy.Publisher('test_topic', String, queue_size=10)
    rospy.init_node('publisher', anonymous=True)
    rate = rospy.Rate(2) # 2hz
    while not rospy.is_shutdown():
        hello_str = "Chao moi nguoi"
        rospy.loginfo(hello_str)
        pub.publish(hello_str)
        rate.sleep()

if __name__ == '__main__':
    try:
        publisher()
    except rospy.ROSInterruptException:
        pass
```

**Node 2**: subscriber.py

```python
#!/usr/bin/env python

import rospy
from std_msgs.msg import String

def callback(data):
    rospy.loginfo(rospy.get_caller_id() + "Receive: %s", data.data)
    
def subscriber():

    rospy.init_node('subsriber', anonymous=True)

    rospy.Subscriber("test_topic", String, callback)

    # spin() simply keeps python from exiting until this node is stopped
    rospy.spin()

if __name__ == '__main__':
    subscriber()
```

```shell 
$ chmod +x publisher.py
$ chmod +x subscriber.py 
```

```sh
$ cd ~/FAIlearning_ws/
$ catkin_make
```

Output:

```sh
Base path: /home/hoangtu/FAIlearning_ws
Source space: /home/hoangtu/FAIlearning_ws/src
Build space: /home/hoangtu/FAIlearning_ws/build
Devel space: /home/hoangtu/FAIlearning_ws/devel
Install space: /home/hoangtu/FAIlearning_ws/install
####
#### Running command: "make cmake_check_build_system" in "/home/hoangtu/FAIlearning_ws/build"
####
####
#### Running command: "make -j2 -l2" in "/home/hoangtu/FAIlearning_ws/build"
####

```

## **D. Running ROS and testing nodes**
Open a new Terminal and start ROS:
```sh
$ roscore
```

Output:

```sh
... logging to /home/hoangtu/.ros/log/51d6bb36-f8ff-11eb-9fb2-033d1f05d7d8/roslaunch-hoangtuVM-7886.log
Checking log directory for disk usage. This may take a while.
Press Ctrl-C to interrupt
Done checking log file disk usage. Usage is <1GB.

started roslaunch server http://hoangtuVM:34105/
ros_comm version 1.15.11


SUMMARY
========

PARAMETERS
 * /rosdistro: noetic
 * /rosversion: 1.15.11

NODES

auto-starting new master
process[master]: started with pid [7894]
ROS_MASTER_URI=http://hoangtuVM:11311/

setting /run_id to 51d6bb36-f8ff-11eb-9fb2-033d1f05d7d8
process[rosout-1]: started with pid [7904]
started core service [/rosout]

```

Run Nodes

```sh
$ rosrun [package_name] [node_name]
```

Open a new Terminal and run the following command to run the publisher node
```sh
$ rosrun ros_basic_pkg publisher.py
```

Output:

```
[INFO] [1628502901.677986]: Chao moi nguoi
[INFO] [1628502902.179363]: Chao moi nguoi
[INFO] [1628502902.678957]: Chao moi nguoi
[INFO] [1628502903.178396]: Chao moi nguoi
[INFO] [1628502903.678914]: Chao moi nguoi
[INFO] [1628502904.179213]: Chao moi nguoi
[INFO] [1628502904.679328]: Chao moi nguoi
[INFO] [1628502905.178520]: Chao moi nguoi
[INFO] [1628502905.678415]: Chao moi nguoi
[INFO] [1628502906.179231]: Chao moi nguoi
[INFO] [1628502906.678328]: Chao moi nguoi
[INFO] [1628502907.179654]: Chao moi nguoi
[INFO] [1628502907.679769]: Chao moi nguoi
[INFO] [1628502908.178955]: Chao moi nguoi
[INFO] [1628502908.679460]: Chao moi nguoi
[INFO] [1628502909.178482]: Chao moi nguoi
.
.
.

```

Open a new Terminal and run the following command to run the subscriber node
```sh
$ rosrun ros_basic_pkg subscriber.py
```

Output:
```
[INFO] [1628502926.681869]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
[INFO] [1628502927.180874]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
[INFO] [1628502927.681803]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
[INFO] [1628502928.181726]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
[INFO] [1628502928.682879]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
[INFO] [1628502929.181091]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
[INFO] [1628502929.680744]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
[INFO] [1628502930.181226]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
[INFO] [1628502930.680463]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
[INFO] [1628502931.181085]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
[INFO] [1628502931.680665]: /subsriber_5570_1628502926177Receive: Chao moi nguoi
.
.
.

```

