Dies ist eine Kurzanleitung zur Installation und Einrichtung von ROS und des youBot OS. Detailliertere Erklärungen zur ROS-Installation gibt es unter [[ http://wiki.ros.org/ | wiki.ros.org ]]. Je nach Version von Ubuntu und ROS gibt es leichte Abweichungen in den Befehlen. Besondere Aufmerksamkeit ist gefragt, wenn die Versionsnamen in einem Befehl auftauchen - bitte ggf. anpassen! Die hier verwendete Kombination ist:

Ubuntu 16 mit ROS Kinetic [[ http://wiki.ros.org/kinetic/Installation/Ubuntu | Ubuntu install of ROS Kinetic ]]
NOTE: Drücken Sie {key Strg Alt T} um ein Terminal zu öffnen

NOTE: Wenn Sie mit Linux nicht vertraut sind, werfen Sie einen Blick auf das [[ https://files.fosswire.com/2007/08/fwunixref.pdf | Linux Cheat Sheet  ]] oder fangen Sie mit einem [[ http://linuxcommand.org/lc3_learning_the_shell.php | Linux-Tutorial an. ]]

(WARNING) Das $-Zeichen signalisiert, dass es sich um einen Shell-Befehl handelt und ist kein Teil des Befehls selbst.

= Automatische Installation =
Für die automatische Installation von ROS haben wir ein Skript erstellt, welches alle erforderlichen Packages installiert. Dieses kann über das R169 Repository heruntergeladen werden:

   $ git clone https://phabricator.imes.uni-hannover.de/source/rc_installation.git

Gestartet wird die Installation über den Befehl
  $ rc_installation/install_ros_kinetic.sh 
Die Installation nimmt einige Minuten in Anspruch. War die Installation erfolgreich, sollte im Terminal die folgende Ausgabe angezeigt werden:
  ROS Installation Done!
  You can create your ROS workspace now.

Sollte die Installation über das Skript fehlschlagen, muss ROS manuell installiert werden.
== Manuelle Installation ==
Die manuelle Installation ist auf der [[  http://wiki.ros.org/kinetic/Installation/Ubuntu | offiziellen ROS Webseite ]] erläutert.

== Einrichten des Workspaces ==
Um eigene Packages für das ROS-Framework kompilieren zu können, muss ein Catkin-Workspace angelegt werden.
Catkin-Workspace namens catkin_ws erstellen (der Name darf abweichen):
  $ mkdir -p ~/catkin_ws/src
  $ cd ~/catkin_ws
  $ catkin init
  $ catkin build
Neue Umgebung in .bashrc speichern um sie automatisch zu laden:
  $ echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
  $ source ~/.bashrc
Damit wird die Umgebung bei jedem Start eines Terminals automatisch geladen.
Eigene Packages können dann in dem Verzeichnis ##~/catkin_ws/src## oder einem Unterverzeichnis angelegt werden.

== Download der RobotChallenge Vorgaben ==
Zu einigen Hausaufgaben werden Sie Quellcode-Vorgaben bekommen. Jedes Team hat einen Projektordner auf Phabricator. Sie finden die Projektordner unter:

  - Team A: #rca 
  - Team B: #rcb 

Die Vorgaben-Repositories für die RobotChallenge sind in Ihrem Projektordner verlinkt und werden regelmäßig aktualisiert. Laden Sie die Vorgabe herunter (in Ihren ROS-Workspace)
  $ cd ~/catkin_ws/src
  $ git clone https://phabricator.imes.uni-hannover.de/source/rc_vorgaben.git

== Installation des youBot OS ==
Das youBot OS enthält alle notwendigen Programmbibliotheken um mit dem youBot zu arbeiten und stellt weiterhin eine Simulationsumgebung zur Verfügung. Das youBot OS kann über den folgenden Befehl herunter geladen werden:
  $ git clone https://phabricator.imes.uni-hannover.de/diffusion/102/rc_youbot_os.git
Um das youBot OS kompilieren zu können, werden einige Packages benötigt die über ##rosdep## nachinstalliert werden müssen.
  $ cd ~/catkin_ws
  $ rosdep update
  $ rosdep install --from-paths src --ignore-src -r -y
Anschließend kann der ROS-Workspace kompiliert werden
  $ catkin build
- Nächstes Tutorial: [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/tutorials_ros_kommandozeile/ | ROS in der Kommandozeile ]]

