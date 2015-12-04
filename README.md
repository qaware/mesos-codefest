# Mesos Codefest
Fast alle modernen Softwaresysteme laufen auf einem Cluster. Wird das Cluster mit klassischen Mitteln betrieben, so sieht man immer wieder dieselben Probleme:
* Zu hohe Betriebskosten, da die Server kaum ausgelastet sind. Mit der geringen Auslastung erkauft man sich Kapazitäten für Spitzenlasten und Isolation von einzelnen Anwendungsteilen – klassische Opportunitätskosten.
* Zu hohe Betriebskosten durch den Overhead von Hardware-Virtualisierung.
* Standard-Betriebsprozeduren wie Installationen, Rolling Updates, Canary Releases und Rollbacks sind aufwändig,
fehleranfällig und nur schwer zu automatisieren.
* Zentrale Betriebsfunktionen wie Monitoring, Failover, Absicherung oder Skalierung müssen pro
Anwendung neu aufgesetzt und konfiguriert werden. Dies ist aufwändig und fehleranfällig.

Ein Cluster-Betriebssystem wie Apache Mesos / Mesosphere DCOS löst diese Probleme auf elegante Weise. Es überträgt das Prinzip eines klassischen Betriebssystems, das über einen einzigen Rechner herrscht, auf ein Rechen-Cluster aus vielen Rechnern. Es abstrahiert dabei viele Rechner zu einem großen Rechner. Damit werden Betriebsprozeduren so einfach wie auf nur einem Rechner. Die Betriebskosten sinken deutlich, da durch intelligentes Scheduling und durch den Einsatz von Betriebssystem-Virtualisierung die Auslastung deutlich steigt und der Overhead deutlich sinkt.
Cluster-Betriebssysteme werden bereits massiv im Sillicon Valley eingesetzt (z.B. bei Apple Siri, Twitter und Airbnb) aber auch bei eher klassischen IT-Nutzern wie CenturyLink, Verizon, Walmart und dem CERN. Es existiert eine Vielzahl an Erfahrungsberichten mit der neuartigen Betriebsumgebung, die i.W. von hohen Kosteneinsparungen und gesteigerter Flexibilität im Betrieb berichten.
Im folgenden Tutorial wollen wir die folgenden Fragestellungen vertiefen:
* Wie funktioniert ein Cluster-Betriebssystem am Beispiel Apache Mesos / Mesosphere DCOS?
* Was ist der Nutzen eines Cluster-Betriebssystems?
* Wie können Anwendungen so (um-)gebaut werden, dass sie auf einem Cluster-Betriebssystem
laufen?

Grundvoraussetzung ist ein Rechner mit Vagrant (https://www.vagrantup.com), VirtualBox (https://www.virtualbox.org) und MinGW (http://www.mingw.org/). Vor dem Tutorial bitte bereits eine Ubuntu Box für Vagrant herunterladen mit dem Befehl `vagrant box add ubuntu/trusty64`.
