Als Simulationsumgebung wird [[ http://gazebosim.org/ | Gazebo ]] verwendet. Für ROS kinetic wird Version 7.x empfohlen. Alles benötigte sollte mit der aktuellen ROS-Version bereits installiert sein.

Starten Sie die Simulation:
  $ roslaunch launcher gazebo.launch

Der Befehl besteht aus drei Teilen:
 ##roslaunch##: Befehl zum Ausführen eines launch files 
 ##launcher##: Name des Packages
 ##gazebo.launch##: Name des launch files

Das folgende Fenster sollte sich jetzt öffnen:
{F21368,layout=center,size=full}
---
NOTE: Gazebo stellt als Physiksimulator recht hohe Anforderungen an die Hardware des Systems. Falls die Systemgeschwindigkeit nach dem Start von Gazebo deutlich abnimmt, können zunächst die Schatten in der 3D-Darstellung deaktiviert werden. Klicken sie hierfür unter dem Reiter ##World## auf ##Scene## und setzen sie bei //shadows// den Wert auf //false//. Falls diese Maßnahme nicht ausreicht, kann Gazebo auch ohne eine grafische Ausgabe gestartet werden. Die Simulation wird dann im Hintergrund ausgeführt und kann mit Ausnahme der grafischen Anzeige normal genutzt werden. Um Gazebo ohne GUI zu starten, muss ein Argument bei dem Aufruf von Gazebo in der Kommandozeile gesetzt werden:

```
$ roslaunch launcher gazebo.launch gui:=false
```
---
Falls sie nicht mehr laufen, starten Sie noch einmal die beiden Nodes:
  
```
$ rosrun joy joy_node
```
```
$ rosrun joy_ctrl joy_ctrl_node
```
Jetzt können Sie mit dem Gamepad den youBot in der Simulation bewegen.
Falls etwas nicht funktionieren sollte, können Sie auch erst einmal zum nächsten Abschnitt gehen. Dort lernen Sie ein wichtiges Tool zum Debuggen von ROS kennen.

Nächstes Tutorial: [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/tutorials_debug_viz/ | Debugging und Visualisierung ]]