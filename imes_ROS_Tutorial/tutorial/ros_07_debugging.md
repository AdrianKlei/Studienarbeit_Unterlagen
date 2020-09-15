In diesem Abschnitt werden Sie Tools kennen lernen, mit denen Sie sich einen Überblick über aktive ROS-Nodes und den Zustand des Roboters verschaffen können.
Annahme: Gazebo und die Nodes aus den vorigen Abschnitten sind noch aktiv.

NOTE: Ein wichtiges Tool zum Debuggen haben Sie bereits kennengelernt: ##rostopic##.
Mit ##rostopic list## und ##rostopic echo## kann man schnell die vorhandenen Topics überprüfen.

Starten Sie ##rqt##
  $ rqt
und wählen Sie {nav Plugins > Introspection > Node Graph}
{F21370,layout=center,size=full}
Setzen Sie oben zunächst alle Haken und wählen {nav Nodes only}.

Dann sollten Sie den folgenden Graphen sehen:
{F21372,layout=center,size=full}
Dieser Node-Graph ist sehr nützlich, um sich einen Überblick über die aktiven Nodes und Topics zu verschaffen. Hier erkennt man auch schnell, wenn Verbindungen fehlen, weil z.B. Topics falsch benannt sind.

Wählen Sie jetzt oben links {nav Nodes/Topics (all)}.
{F21374,layout=center,size=full}
Hier sehen Sie unter anderem, dass Gazebo auch Odometrie und Laserscans publisht.
Als nächstest lernen Sie, wie diese Daten visualisiert werden können.

NOTE: Ein weiteres Tool, das Sie häufig verwenden werden, ist //rviz//.
Mit rviz lassen sich unterschiedliche Daten des Robotersystems visualisieren. Dazu zählen z.B. Laserscans, Punktwolken, Kamerabilder, Koordinatensysteme, Maps, und ein Modell des Roboters selbst. Damit lässt sich u.a. überprüfen, was der Roboter gerade „sieht“ und wo der Roboter glaubt, sich gerade zu befinden.
Bei rviz handelt es sich nicht um eine Simulationsumgebung, auch wenn es auf den ersten Blick ähnlich wie Gazebo aussieht. rviz stellt nur die Daten dar, die es vom Roboter bzw. von der Simulation empfängt.

Starten Sie rviz:
  $ rviz

Unten links können mit dem {nav Add}-Button Daten zur Visualisierung hinzugefügt werden.
{F21376,layout=center,size=full}

Fügen Sie zuerst das Roboter-Modell hinzu:
{F21378,layout=center,size=full}

Wählen Sie oben links {nav Fixed Frame > Odom}
{F21380,layout=center,size=full}

Fügen Sie jetzt nacheinander die beiden Laserscanner mit den Topics ##scan## und ##scan_back## hinzu.
Am einfachsten geht das über den Reiter {nav By Topic}:
{F21382,layout=center,size=full}

Jetzt sollten sie den youBot zusammen mit den Daten der Laserscanner sehen:
{F21384,layout=center,size=full}

Damit haben Sie die wichtigsten Komponenten von ROS kennengelernt. Als nächstes können Sie die Übungsaufgaben bearbeiten.


  - Nächstes Tutorial: [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/tutorials_aufgaben/ | Übungsaufgaben ]]

