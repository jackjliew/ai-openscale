---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: ai, artificial intelligence, high availability, disaster recovery, recovery, load-balancing, postgres

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Hochverfügbarkeit und Disaster-Recovery
{: #openscale-availability-recovery}

{{site.data.keyword.aios_full}} ist an mehreren {{site.data.keyword.cloud_notm}}-Standorten hoch verfügbar, wie zum Beispiel in Dallas und Washington, D. C. Die Wiederherstellung nach potenziellen Katastrophen, die einen ganzen Standort betreffen, erfordert jedoch Planung und Vorbereitung.
{: shortdesc}

Sie sind dafür verantwortlich, die Konfiguration, Anpassung und Nutzung Ihres Service zu verstehen. Sie sind ebenfalls dafür verantwortlich, ausreichend vorbereitet zu sein, um eine Instanz des Service an einem neuen Standort neu zu erstellen und Ihre Daten an einem beliebigen Standort wiederherzustellen. Weitere Informationen enthält [Wie kann sichergestellt werden, dass keine Ausfallzeiten auftreten? ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window}.

##Hochverfügbarkeit 
{: #openscale-high-availability}

{{site.data.keyword.aios_short}} wird in Rechenzentren der Region **us-south** mit Mehrzonenrouting (MZR) bereitgestellt und ist dort in drei Verfügbarkeitszonen verfügbar. Wenn eine Zone zu einer beliebigen Zeit nicht verfügbar ist, ist das System in anderen Verfügbarkeitszonen weiterhin verfügbar . Die globale Lastausgleichsfunktion und der DNS-Server leiten den Datenverkehr ohne jegliche Unterbrechung für die Benutzer an verfügbare Zonen weiter.

Daten, die in PostgreSQL-Datenbanken gespeichert sind, sind ebenfalls hoch verfügbar und sind in mehreren Verfügbarkeitszonen vorhanden. Es liegt jedoch in der Verantwortung des Kunden, Daten zur Unterstützung eines Disaster-Recovery-Plans zu sichern, damit Services neu erstellt werden können.

Für den {{site.data.keyword.aios_short}}-Datenverkehr wird eine Lastverteilung über mehrere Zonen in einer Region durchgeführt. Jede Zone ist ein Rechenzentrum in derselben Region. 

Compose-Datenbanken wie PostgreSQL und Datenbanken mit verteiltem <code>etc</code>-Verzeichnis (etcd-Datenbanken) werden regelmäßig gesichert, um eine hohe Verfügbarkeit sicherzustellen, und im Katastrophenfall kann das Einsatzteam für {{site.data.keyword.aios_short}} den Service innerhalb des Ziels in Bezug auf den maximal tolerierbaren Datenverlust bei einem Ausfall (Recovery Point Objective, RPO) wiederherstellen.
 
{{site.data.keyword.cloud_notm}} bietet Datenredundanz in der Region und ermöglicht dadurch Schutz durch Hochverfügbarkeit. IBM bietet ohne gesonderte Berechnung die automatische Datenreplikation für Kundendatenbanken, die Trainings- und/oder kundenspezifische Modelldaten enthalten. Die Replikation wird über die Verfügbarkeitszonen in den Regionen hinweg innerhalb der Rechenzentren von {{site.data.keyword.cloud_notm}} abgeschlossen.
 
## Sicherung (Backup) & Wiederherstellung
{: #openscale-restore}

Der Kunde ist für die Sicherung und Wiederherstellung seiner eigenen Daten verantwortlich, und zwar einschließlich der Daten von Trainings- und/oder angepassten Modellen sowie von jeglichen vom Kunden generierten angepassten Modellen. Anweisungen zur Sicherung und Wiederherstellung finden Sie in der Dokumentation zu {{site.data.keyword.cloud_notm}}.
 
##Disaster-Recovery
{: #openscale-disaster-recovery}

Die regionsinterne Business-Continuity wird durch die Nutzung der automatischen Replikation in den Verfügbarkeitszonen in den Regionen innerhalb der {{site.data.keyword.cloud_notm}}-Rechenzentren komplettiert. Der Kunde ist verantwortlich für die Disaster-Recovery in mehreren Regionen. Zu ihren Pflichten gehören unter anderem die Sicherung, Wiederherstellung und Synchronisierung ihrer eigenen Sicherheitsrichtlinien, Daten von Trainingsmodellen und/oder benutzerdefinierten Modellen sowie aller vom Kunden generierten angepassten Modellen. Darüber hinaus ist der Kunde für das Routing und/oder den Lastausgleich über die Regionen hinweg verantwortlich. Anweisungen zur Sicherung und Wiederherstellung des Clients enthält die Dokumentation zu {{site.data.keyword.cloud_notm}}.
