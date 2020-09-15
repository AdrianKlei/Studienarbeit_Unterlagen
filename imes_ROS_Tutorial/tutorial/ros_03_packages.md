Damit der youBot mit dem Gamepad ferngesteuert werden kann, müssen die von der Joy-Node gesendeten Daten in Geschwindigkeiten für den Roboter übersetzt werden. Der Treiber des youBot benötigt dazu Messages vom Typ ##geometry_msgs/Twist## auf dem Topic ##cmd_vel##. In den folgenden Abschnitten werden Sie eine zunächst ein Package und dann eine Node erstellen, die das Gamepad mit dem youBot verbindet.
{F21337, layout=center, float, size=full}

Jede Node muss in einem Package untergebracht sein. Ein neues, leeres Package kann über den Befehl ##catkin_create_pkg## angelegt werden:
  $ catkin_create_pkg package_name [dependencies]
Wie genau das geht, können Sie im entsprechenden [[ http://wiki.ros.org/ROS/Tutorials/CreatingPackage | ROS-Tutorial ]] nachlesen.
== Installation von QtCreator ==
Um den Einstieg zu vereinfachen, wird das Package mit dem Programm QtCreator erstellt. QtCreator ist eine IDE, für die ein ROS-Plugin existiert und daher diverse nützliche Funktionen für die Arbeit mit ROS enthält.

Eine Anleitung für die Installation von QtCreator (inkl. ROS Plugin) findet sich unter dem folgenden Link:
[[ https://ros-qtc-plugin.readthedocs.io/en/latest/_source/How-to-Install-Users.html|https://ros-qtc-plugin.readthedocs.io/en/latest/_source/How-to-Install-Users.html ]]
Dabei ist der "Xenial Online Installer" im Abschnitt "Installation Procedure for Ubuntu 16.04" zu wählen.

NOTE: Die ##.run## Datei kann geöffnet werden, indem die Befehle ##sudo chmod +x qtcreator-ros-xenial-latest-online-installer.run## und anschließend ##./qtcreator-ros-xenial-latest-online-installer.run## verwendet werden.
Danach ist der Anleitung im Abschnitt [[ https://ros-qtc-plugin.readthedocs.io/en/latest/_source/How-to-Install-Users.html#qt-installer-procedure | Qt Installer Procedure ]] zu folgen.

Qt kann dann über den Befehl
  $ qtcreator-ros
gestartet werden.

---
== Öffnen eines Workspaces ==
Zunächst soll der catkin Workspace in Qt geöffnet werden. Dies erfolgt über {nav File > New File or Project... > Other Project > ROS Workspace} und über ##Browse...## die Auswahl des Ordners ##catkin_ws##. Als Name ein beliebiger Name, z.B. ##catkin_ws##, festgelegt werden. Bei ##Build System:## muss "CatkinTools" ausgewählt werden. Im nächsten Fenster kann der Öffnungsvorgang über ##Finish## abgeschlossen werden.

---
== Erstellen des Packages ==

Wechseln Sie nun zurück in die ##Edit## Ansicht und öffnen sie den ##catkin_ws## Ordner im Project Explorer.
Über einen Rechtsklick auf den Ordner ##src## wird ein neues Package über ##Add New...## hinzugefügt. 
{F21350,layout=center, float,size=full}
Als Name soll ##joy_ctrl## verwendet werden. Damit innerhalb des Packages die ROS Funktionalitäten verwendet und Nachrichten des Typs '##geometry_msgs/Twist## gesendet werden können, müssen einige Programmbibliotheken in das Package eingebunden werden. 
  roscpp std_msgs sensor_msgs geometry_msgs
Diese sind unter ##Dependencies## im Feld ##catkin## einzutragen.

{F21352,layout=center, float,size=full}
Im nächsten Schritt wird der Vorgang über ##Finish## beendet.
{F21354,layout=center, float,size=full}

---

(WARNING) **Hinweis:** Im weiteren Verlauf der Veranstaltung werden Sie diverse Packages bzw. Nodes erstellen müssen. Um diesen Vorgang zu vereinfachen, stellen wir eine Package-Vorlage bereit, in der die wichtigsten Komponenten einer Node enthalten sind. Sie können die Vorlage [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/ros_package_vorlage/ | hier ]] herunterladen.


- Nächstes Tutorial: [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/tutorials_node_erstellen/ | Eine Node erstellen ]]



