Jetzt sollten Sie den Aufbau eines ROS-Package und einer Node verstanden haben und in der Lage sein, Ihre Node aus den vorigen Abschnitten eigenständig zu erweitern.

---

**Aufgabe 1**

  - Legen sie ein Launchfile an, das Ihre Node und die Joy-Node gemeinsam startet.

  - Verwenden Sie in Ihrer Node ROS-Parameter für die maximalen Geschwindigkeiten. Definieren sie die Parameter dafür in einer Konfigurationsdatei, die im Launchfile geladen 
 wird. Ein beispielhafter Abruf von Parametern im Programm ist bereits im ##JoyCtrlNode## Konstruktor gegeben.

(NOTE) **Hinweis:** Beispiele für launch Dateien und das Schreiben von Parametern finden sie unter der [[ http://wiki.ros.org/roslaunch/XML | Beschreibung des XML Formats für roslaunch ]]. Die [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/ros_package_vorlage/ | ROS-Package-Vorlage ]] enthält auch eine Beispiel für eine launch- und cfg Datei.

---

**Aufgabe 2**

  - Überlegen Sie, was passieren kann, wenn die Verbindung zwischen Ihrer Node und der Joy-Node abbricht.
  - Nutzen Sie den Timer in Ihrer Node, um mögliche Probleme beim Verbindungsverlust zu vermeiden.
(NOTE)**Hinweis:** [[ http://wiki.ros.org/roscpp/Overview/Time | http://wiki.ros.org/roscpp/Overview/Time ]]

---

**Aufgabe 3**

  - Definieren sie einen Button des Gamepads als //Turbo//, mit dem sich die Geschwindigkeit kurzzeitig erhöhen lässt und bauen Sie diesen in Ihre Node ein.

---


  - Zurück zur Übersicht: [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/tutorials_ros_direkteinstieg/ | Tutorial Übersicht ]]







