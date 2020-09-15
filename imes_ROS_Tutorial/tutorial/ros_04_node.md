Nun soll dem Package eine Node hinzugefügt werden. Dies erfolgt über einen Rechtsklick auf ##joy_ctrl## im Project Explorer und die Auswahl von {nav Add New... > C++ > C++ Class}. Als Name der Klasse soll ##JoyCtrlNode## eingetragen werden. In dem Feld "Header File" muss dann noch ##include/joy_ctrl/joy_ctrl_node.h## und bei "Source File" ##src/joy_ctrl_node.cpp## eingetragen werden. 
{F21356,layout=center, float,size=full}
Bestätigen sie den Vorgang erneut über ##Finish##.

Anschließend muss die Datei ##CMakeLists.txt## im ##joy_ctrl## Package **am Ende** um die folgenden Zeilen ergänzt werden, damit die Node kompiliert werden kann:

  lang=cmake
  add_executable(joy_ctrl_node
    src/joy_ctrl_node.cpp
    include/joy_ctrl/joy_ctrl_node.h
  )

  target_link_libraries(joy_ctrl_node
    ${catkin_LIBRARIES}
  )
Außerdem muss in derselben Datei der Abschnitt
  lang=cmake
  include_directories(
  # include
  # ${catkin_INCLUDE_DIRS}
  )
zu
  lang=cmake
  include_directories(
   include
   ${catkin_INCLUDE_DIRS}
  )
geändert werden.

 ---

== Einfügen von Programmcode ==
Ersetzen sie den Inhalt der ##joy_ctrl_node.h## Datei mit dem folgenden Code:
  lang=c++, name=joy_ctrl_node.h, lines=12
  #ifndef JOY_CTRL_NODE_H
  #define JOY_CTRL_NODE_H
  #include "ros/ros.h"
  #include "std_msgs/String.h"
  #include "std_srvs/Empty.h"
 
  class JoyCtrlNode
  {
  public:
    JoyCtrlNode(ros::NodeHandle &node_handle);
 
  private:
    // node handle
    ros::NodeHandle *node_;
 
    // ros communication
    ros::Subscriber my_subscriber_;
    ros::Publisher my_publisher_;
    ros::Timer my_timer_;
 
    // parameters
    double my_double_parameter_;
    std::string my_string_parameter_;
    int my_int_parameter_;
    bool my_bool_parameter_;
 
    // callbacks
    void subscriberCallback(const std_msgs::String &msg);
    void timerCallback(const ros::TimerEvent &evt);
  };
  #endif // JOY_CTRL_NODE_H
Und ##joy_ctrl_node.cpp## wie folgt:
  lang=c++, name=joy_ctrl_node.cpp, lines=12
  #include "joy_ctrl/joy_ctrl_node.h"
 
  //########## CONSTRUCTOR #####################################################################################
  JoyCtrlNode::JoyCtrlNode(ros::NodeHandle &node_handle):
    node_(&node_handle)
  {
    // === PARAMETERS ===
    node_->param("my_pkg/my_double_param", my_double_parameter_, 0.0);
    node_->param("my_pkg/my_string_param", my_string_parameter_, std::string(""));
    node_->param("my_pkg/my_int_param", my_int_parameter_, 0);
    node_->param("my_pkg/my_bool_param", my_bool_parameter_, false);
 
    // === SUBSCRIBERS ===
    my_subscriber_ = node_->subscribe("some_topic", 10, &JoyCtrlNode::subscriberCallback, this);
 
    // === PUBLISHERS ===
    my_publisher_ = node_->advertise<std_msgs::String>("my_namespace/my_topic", 10);
 
    // === TIMER ===
    my_timer_ = node_->createTimer(ros::Duration(0.1), &JoyCtrlNode::timerCallback, this);
  }
 
  //########## CALLBACK: SUBSCRIBER ############################################################################
  void JoyCtrlNode::subscriberCallback(const std_msgs::String &msg)
  {
 
  }
 
  //########## CALLBACK: TIMER #################################################################################
  void JoyCtrlNode::timerCallback(const ros::TimerEvent &evt)
  {
 
  }
 
  //########## MAIN ############################################################################################
  int main(int argc, char** argv)
  {
    ros::init(argc, argv, "joy_ctrl_node");
 
    ros::NodeHandle node_handle;
    JoyCtrlNode joy_ctrl_node(node_handle);
 
    ROS_INFO("Node is spinning...");
    ros::spin();
 
    return 0;
  }

In dieser Form enthält das Programm einen Subscriber, um Messages zu empfangen, einen Publisher, um Messages zu versenden, sowie einen Timer und den beispielhaften Abruf von Parametern.
Um die Eingabe des Gamepads als ##geometry_msgs/Twist## Message an den youBot zu senden, muss das Programm erweitert werden. 

Binden Sie zunächst im Header (##joy_ctrl_node.h##) die Message-Definitionen ein:
  lang=c++
  #include <sensor_msgs/Joy.h>
  #include <geometry_msgs/Twist.h>
Ändern sie im Konstruktor der ##joy_ctrl_node.cpp## den Message-Typen und das Topic des Publishers:
  lang=c++
  my_publisher_ = node_->advertise<geometry_msgs::Twist>("cmd_vel", 10);
Ändern sie im Konstruktor das Topic des Subscribers
  lang=c++
  my_subscriber_ = node_->subscribe("joy", 10, &JoyCtrlNode::subscriberCallback, this);
Ändern sie anschließend des Message-Typen in der Callback-Methode des Subscribers.
In ##joy_ctrl_node.h##:
  lang=c++
  void subscriberCallback(const sensor_msgs::Joy &msg);
In ##joy_ctrl_node.cpp##:
  lang=c++
  void JoyCtrlNode::subscriberCallback(const sensor_msgs::Joy &msg)
  {
  }
Anschließend kann die Node über die Tastenkombination {key Strg B} kompiliert werden. Wenn keine Fehler auftreten, ist die Node soweit vorbereitet, dass damit begonnen werden kann eigenen Code zu schreiben.


  - Nächstes Tutorial: [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/tutorials_code_schreiben/ | Eigenen Code schreiben ]]

