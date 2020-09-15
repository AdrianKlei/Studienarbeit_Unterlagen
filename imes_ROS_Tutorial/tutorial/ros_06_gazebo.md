Als Simulationsumgebung wird [[ http://gazebosim.org/ | Gazebo ]] verwendet. F�r ROS kinetic wird Version 7.x empfohlen. Alles ben�tigte sollte mit der aktuellen ROS-Version bereits installiert sein.

Starten Sie die Simulation:
  $ roslaunch launcher gazebo.launch

Der Befehl besteht aus drei Teilen:
 ##roslaunch##: Befehl zum Ausf�hren eines launch files 
 ##launcher##: Name des Packages
 ##gazebo.launch##: Name des launch files

Das folgende Fenster sollte sich jetzt �ffnen:
{F21368,layout=center,size=full}
---
NOTE: Gazebo stellt als Physiksimulator recht hohe Anforderungen an die Hardware des Systems. Falls die Systemgeschwindigkeit nach dem Start von Gazebo deutlich abnimmt, k�nnen zun�chst die Schatten in der 3D-Darstellung deaktiviert werden. Klicken sie hierf�r unter dem Reiter ##World## auf ##Scene## und setzen sie bei //shadows// den Wert auf //false//. Falls diese Ma�nahme nicht ausreicht, kann Gazebo auch ohne eine grafische Ausgabe gestartet werden. Die Simulation wird dann im Hintergrund ausgef�hrt und kann mit Ausnahme der grafischen Anzeige normal genutzt werden. Um Gazebo ohne GUI zu starten, muss ein Argument bei dem Aufruf von Gazebo in der Kommandozeile gesetzt werden:

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
Jetzt k�nnen Sie mit dem Gamepad den youBot in der Simulation bewegen.
Falls etwas nicht funktionieren sollte, k�nnen Sie auch erst einmal zum n�chsten Abschnitt gehen. Dort lernen Sie ein wichtiges Tool zum Debuggen von ROS kennen.

N�chstes Tutorial: [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/tutorials_debug_viz/ | Debugging und Visualisierung ]]