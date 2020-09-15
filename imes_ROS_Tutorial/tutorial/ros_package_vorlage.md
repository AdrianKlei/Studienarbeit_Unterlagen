Diese Package Vorlage enthält die beispielhafte Implementierung von
  - Subscriber
  - Publisher
  - Service Server
  - Service Client
  - Timer
  - ROS Parametern

Sie kann daher als Grundlage für neue Packages verwendet werden

---

**Package Vorlage herunterladen**
{F22284}

---

Mit dem Skript ##rename.bash## kann das Package umbenannt werden.

  $ rosrun my_pkg rename.bash new_package_name new_node_name

**Inhalt**
```
my_pkg/
    cfg/
        params.yaml
    include/
        my_pkg/
            my_node.h
    launch/
        my_launchfile.launch
    src/
        my_node.cpp
    CMakeLists.txt
    package.xml
    rename.bash
```
**my_node.h**
```
lang=c++
#ifndef MY_NODE_H
#define MY_NODE_H
 
#include "ros/ros.h"
#include "std_msgs/String.h"
#include "std_srvs/Empty.h"
 
class MyNode
{
public:
    MyNode(ros::NodeHandle &node_handle);
 
private:
    // node handle
    ros::NodeHandle *node_;
 
    // ros communication
    ros::Subscriber my_subscriber_;
    ros::Publisher my_publisher_;
    ros::ServiceServer my_service_server_;
    ros::ServiceClient my_service_client_;
    ros::Timer my_timer_;
 
    // parameters
    double my_double_parameter_;
    std::string my_string_parameter_;
    int my_int_parameter_;
    bool my_bool_parameter_;
 
    // callbacks
    void subscriberCallback(const std_msgs::String &msg);
    bool serviceCallback(std_srvs::Empty::Request &req, std_srvs::Empty::Response &res);
    void timerCallback(const ros::TimerEvent &evt);
};
 
#endif // MY_NODE_H
```
**my_node.cpp**
```
lang=c++
#include "my_pkg/my_node.h"
 
//########## CONSTRUCTOR #####################################################################################
MyNode::MyNode(ros::NodeHandle &node_handle):
    node_(&node_handle)
{
    // === PARAMETERS ===
    node_->param("my_pkg/my_double_param", my_double_parameter_, 0.0);
    node_->param("my_pkg/my_string_param", my_string_parameter_, std::string(""));
    node_->param("my_pkg/my_int_param", my_int_parameter_, 0);
    node_->param("my_pkg/my_bool_param", my_bool_parameter_, false);
 
    // === SUBSCRIBERS ===
    my_subscriber_ = node_->subscribe("some_topic", 10, &MyNode::subscriberCallback, this);
 
    // === PUBLISHERS ===
    my_publisher_ = node_->advertise<std_msgs::String>("my_namespace/my_topic", 10);
 
    // === SERVICE SERVERS ===
    my_service_server_ = node_->advertiseService("my_namespace/my_service", &MyNode::serviceCallback, this);
 
    // === SERVICE CLIENTS ===
    my_service_client_ = node_->serviceClient<std_srvs::Empty>("some_service");
 
    // === TIMER ===
    my_timer_ = node_->createTimer(ros::Duration(0.1), &MyNode::timerCallback, this);
}
 
//########## CALLBACK: SUBSCRIBER ############################################################################
void MyNode::subscriberCallback(const std_msgs::String &msg)
{
    ROS_INFO("Message received: %s", msg.data.c_str());
}
 
//########## CALLBACK: SERVICE SERVER ########################################################################
bool MyNode::serviceCallback(std_srvs::Empty::Request &req, std_srvs::Empty::Response &res)
{
    ROS_INFO("Service call received.");
    return true;
}
 
//########## CALLBACK: TIMER #################################################################################
void MyNode::timerCallback(const ros::TimerEvent &evt)
{
    // === PUBLISH A MESSAGE ===
    std_msgs::String msg;
    msg.data = "Hello World.";
    my_publisher_.publish(msg);
 
    // === CALL A SERVICE ===
    std_srvs::Empty srv;
    my_service_client_.call(srv);
}
 
//########## MAIN ############################################################################################
int main(int argc, char** argv)
{
    ros::init(argc, argv, "my_node_name");
 
    ros::NodeHandle node_handle;
    MyNode my_node(node_handle);
 
    ROS_INFO("Node is spinning...");
    ros::spin();
 
    return 0;
}
```
**package.xml**
```
lang=xml
<?xml version="1.0"?>
<package format="2">
  <name>my_pkg</name>
  <version>0.1.0</version>
  <description>IMES Node Template</description>

  <maintainer email="my_name@todo.todo">My Name</maintainer>
  <license>TODO</license>

  <buildtool_depend>catkin</buildtool_depend>
  <depend>roscpp</depend>
  <depend>std_msgs</depend>
  <depend>std_srvs</depend>

</package>
```
**CMakeLists.txt**
```
lang=c++
cmake_minimum_required(VERSION 2.8.3)
project(my_pkg)
set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
  std_srvs
)
 
catkin_package()
 
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)
 
add_executable(my_node
  src/my_node.cpp
  include/my_pkg/my_node.h
)
 
target_link_libraries(my_node
  ${catkin_LIBRARIES}
)

```
**my_launchfile.launch**
```
lang=xml
<?xml version="1.0"?>
<launch>
	<!-- LOAD PARAMETERS -->
	<rosparam file="$(find my_pkg)/cfg/params.yaml" command="load" ns="my_pkg" />	
 
	<!-- LAUNCH NODE -->
	<node name="my_node" pkg="my_pkg" type="my_node" output="screen" />
</launch>
```
**params.yaml**
```
lang=yaml
my_double_param: 0.5
my_string_param: "This is a string"
my_int_param: 2
my_bool_param: true
```
**rename.bash**
```
lang=bash
#!/bin/bash
 
if (( $# != 2 )); then
    echo "Error: Wrong number of arguments"
    echo "Usage: rename.sh package_name node_name"
    exit
fi
 
cd "$(dirname "$0")"
 
package_name=$(echo $1 | tr '[:upper:]' '[:lower:]')
node_name=$(echo $2 | tr '[:upper:]' '[:lower:]')
include_guard=${1}_${2}
include_guard=$(echo $include_guard | tr '[:lower:]' '[:upper:]')
class_name=$(echo $2 | sed -r 's/(^|_)([a-z])/\U\2/g' )
 
# CMakeLists.txt
sed -i -- "s/my_pkg/$package_name/g" ./CMakeLists.txt
sed -i -- "s/my_node/$node_name/g" ./CMakeLists.txt
 
# package.xml
sed -i -- "s/my_pkg/$package_name/g" ./package.xml
sed -i -- "s/IMES Node Template/$package_name/g" ./package.xml
 
# launchfile
sed -i -- "s/my_pkg/$package_name/g" ./launch/my_launchfile.launch
sed -i -- "s/my_node/$node_name/g" ./launch/my_launchfile.launch
 
# header
sed -i -- "s/MyNode/$class_name/g" ./include/my_pkg/my_node.h
sed -i -- "s/MY_NODE/$include_guard/g" ./include/my_pkg/my_node.h
sed -i -- "s/my_pkg/$package_name/g" ./include/my_pkg/my_node.h
 
# src
sed -i -- "s/my_node_name/$node_name/g" ./src/my_node.cpp
sed -i -- "s/MyNode/$class_name/g" ./src/my_node.cpp
sed -i -- "s/my_pkg/$package_name/g" ./src/my_node.cpp
sed -i -- "s/my_namespace/$package_name/g" ./src/my_node.cpp
sed -i -- "s/my_node/$node_name/g" ./src/my_node.cpp
 
# rename files
mv ./launch/my_launchfile.launch ./launch/$node_name.launch
mv ./include/my_pkg/my_node.h ./include/my_pkg/$node_name.h
mv ./src/my_node.cpp ./src/$node_name.cpp
mv ./include/my_pkg ./include/$package_name
cd ..
mv ./my_pkg ./$package_name
cd $package_name
```