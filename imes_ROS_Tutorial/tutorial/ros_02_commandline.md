Das Ziel der Tutorials ist es, den youBot mit einem Gamepad fernzusteuern. Gegeben sind eine Gamepad-Node, die dessen Eingaben in das Topic ##/joy## leitet, und der youBot, der im Topic ##/cmd_vel## auf Fahrbefehle wartet.
Gebraucht wird eine ROS Node, die die Informationen zwischen diesen beiden Topics vermittelt.

In diesem Abschnitt werden Sie damit anfangen, die Treiber-Node für das Gamepad zu starten. Anschließend werden Sie Kommandozeilen-Tools verwenden, um die Node zu untersuchen und herauszufinden, wie Sie auf die Ausgaben des Gamepads zugreifen können.
{F21335, layout=center, float, size=full}

NOTE: Im [[ http://wiki.ros.org/ | ROS-Wiki ]] findet man für viele Anwendungen bereits fertige Packages. Die meisten dieser Packages können bequem über die Paketverwaltung installiert werden: ##$ sudo apt-get install ros-<distro>-<package_name>## Für die Verwendung von Gamepads (und Joysticks) gibt es z.B. das Package joy: [[ http://wiki.ros.org/joy | http://wiki.ros.org/joy. ]]

Installieren Sie das Joy-Package
  $ sudo apt-get install ros-kinetic-joy

Bevor eine Node gestartet werden kann, muss ein roscore laufen. Öffnen Sie ein Terminal und starten Sie einen roscore:
  $ roscore

Starten Sie anschließend in einem neuen Terminal die joy-Node:
  $ rosrun joy joy_node
Der Befehl besteht aus drei Teilen:


  - ##rosrun##: Befehl zum Ausführen einer Node
  - ##joy##: Name des Packages
  - ##joy_node##: Name der Node

NOTE: Wenn das Gamepad angeschlossen ist, sollte die Node jetzt laufen. Falls Probleme auftreten, gibt es hier weitere Hinweise zur Konfiguration des Treibers: [[ http://wiki.ros.org/joy/Tutorials/ConfiguringALinuxJoystick | http://wiki.ros.org/joy/Tutorials/ConfiguringALinuxJoystick ]]

Jetzt läuft der Gamepad-Treiber. Aber was genau tut die Node? Um das herauszufinden stellt ROS einige Tools (u.a. rostopic) zur Verfügung.
  $ rostopic list
  $ rostopic info <Topic-Name>
  $ rostopic echo <Topic-Name>
Beantworten Sie die folgenden Fragen:

  - Auf welchem Topic werden die Gamepad-Ausgaben gesendet?
  - Welcher Message-Typ wird verwendet?

(NOTE)Mit dem Zusatz ##-h## wird eine Hilfe zur Verwendung des Befehls angezeigt. Z.B.: ##rostopic -h## oder ##rostopic list -h##

Jetzt können Sie die Buttons und Achsen des Gamepads betägigen und die resultierenden Ausgaben im Terminal beobachten.
Finden Sie die richtige Zuordnung der Buttons und Achsen zu den angezeigten Werten. Diese Zuordnung werden Sie in späteren Abschnitten benötigen.
NOTE: Weitere nützliche Kommandozeilen-Tools finden Sie im ROS-Wiki: [[ http://wiki.ros.org/ROS/CommandLineTools | http://wiki.ros.org/ROS/CommandLineTools ]]

  - Nächstes Tutorial: [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/tutorials_package_erstellen/ | Ein Package erstellen ]]



