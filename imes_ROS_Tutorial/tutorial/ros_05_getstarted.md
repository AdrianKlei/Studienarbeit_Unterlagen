Jetzt haben Sie eine Node mit Publisher und Subscriber für die benötigten Topics und können anfangen, eigenen Code einzubauen. Ziel ist es, die empfangenen Joy-Messages des Gamepads in sinnvolle Geschwindigkeits-Befehle für den youBot umzuwandeln.
{F21337, layout=center, float, size=full}


---

NOTE: Die Autovervollständigung von Qt Creator kann die Programmierung sehr vereinfachen.

Gehen Sie in die Callback-Methode des Subscribers und tippen Sie

  msg.

{F21358, layout=center, float, size=full}

Die Auto-Vervollständigung ({key Strg  Leertaste}) sollte Ihnen die verfügbaren Felder der Joy-Message anzeigen. Hier sollten Sie die aus [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/tutorials_ros_kommandozeile/ | Tutorial 02 ]] bekannten Elemente ##header##, ##axes## und ##buttons## wiederfinden.

---
Die Subscriber-Callback-Methode wird jedes Mal aufgerufen, wenn eine neue Message eintrifft. Der einfachste Ansatz ist es also, die Message direkt in der Callback-Methode zu verarbeiten und als Geschwindigkeiten direkt weiter zu publishen. 

(WARNING) Beachten Sie, dass Sie innerhalb von Subscriber-Callbacks nur einfache Berechnungen/Zuweisungen, wie in diesem Beispiel, implementieren sollten. Callbacks mit aufwendigen Berechnungen können den Programmablauf blockieren. In der Regel sollten Sie in einem Callback nur den Inhalt einer Message speichern (z.B. in eine Member-Variable) und die Verarbeitung an anderer Stelle (z.B. durch einen Timer) ausführen.

Füllen Sie die Subscriber-Callback-Methode nach dem folgenden Schema mit Inhalt:
  lang=c++
  void MyNode::subscriberCallback(const sensor_msgs::Joy &msg)
  {
  geometry_msgs::Twist twist_msg;
 
  twist_msg.linear.x = factor * msg.axes[index];
  twist_msg.linear.y = ...;
  twist_msg.angular.z = ...;
 
  my_publisher_.publish(twist_msg);
  }
Wählen Sie für ##factor## und ##index## selber passende Werte. Beachten Sie, dass Indices von Arrays bei null beginnen.

---

(NOTE) **Hinweise**

  - Die Einheit der Geschwindigkeit ist m/s bzw. rad/s
  - Da Sie zuerst nur in der Simulation fahren werden (und somit nichts kaputt machen können), können Sie die maximalen Geschwindigkeiten zunächst frei wählen.
  - Die Indizes sollten Sie in Tutorial 02 ermittelt haben.
  - Für die Geschwindigkeiten wird das folgende Koordinatensystem verwendet:

{F21366, layout=center, float, size=full}

---

Wenn Sie fertig sind, kompilieren Sie die Node mit {key Strg B}

Stellen Sie sicher, dass ein ##roscore## läuft. Starten Sie dann in jeweils einem Terminal die Joy-Node
  $ rosrun joy joy_node
und Ihre Node:
  $ rosrun joy_ctrl joy_ctrl_node

Öffnen Sie noch ein Terminal und überprüfen Sie das Ergebnis:
  $ rostopic echo cmd_vel
Betätigen Sie das Gamepad und beobachten Sie die Ausgaben.

Stimmen die Ergebnisse mit den Erwartungen überein? Wenn nicht, passen Sie den Quellcode an und wiederholen Sie die letzten Schritte.

NOTE: Wenn sie Im Terminal {key Strg C} drücken, können Sie eine Node wieder beenden.


  - Nächstes Tutorial: [[ https://phabricator.imes.uni-hannover.de/w/robotchallenge/tutorials_youbot_steuern/ | Den youBot in der Simulation steuern ]]
