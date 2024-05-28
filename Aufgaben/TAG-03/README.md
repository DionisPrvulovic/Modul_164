![TBZ Logo](../x_res/tbz_logo.png)
![m164 Picto](../x_res/m164_picto.jpg)

# m164 - Datenbanken erstellen und Daten einfügen

[TOC]

---

# Tag 3

> Recap / Q&A Tag 2: Generalisierung/Spezialisierung, Identifying Relationships

## Datentypen

> Lehrerinput: M162 [Datentypen](https://gitlab.com/ch-tbz-it/Stud/m162/-/blob/main/Daten_Formate/Datentypen.md)

### Auftrag 

![ToDo](../x_res/ToDo.png) *Zeit: ca. 35 Min*

![Learn](../x_res/Train_R1.png)

**Tabelle Datentypen**

| Datentyp | MariaDB (MySQL) | Beispiel | Bemerkung / Einstellungen |
|----|----|----|----| 
| Ganze Zahlen | INT | 123 | Standardmäßig SIGNED, kann UNSIGNED sein |
| Natürliche Zahlen | INT UNSIGNED | 123 | Nur positive Werte |
| Festkommazahlen (Dezimalzahlen) | DECIMAL(10,2) | 123.45 | Präzision und Skala angeben |
| Aufzählungstypen | ENUM('small', 'medium', 'large') | 'medium' | Feste Werte definieren |
| Boolean (logische Werte) | BOOLEAN (TINYINT(1)) | 0 oder 1 | TRUE/FALSE sind Alias |
| Zeichen (einzelnes Zeichen) | CHAR(1) | 'A' | Feste Länge |
| Gleitkommazahlen | FLOAT | 123.45 | Weniger präzise als DECIMAL |
| Zeichenkette fester Länge | CHAR(n) | 'abc' | Feste Länge, rechtsbündig mit Leerzeichen |
| Zeichenkette variabler Länge | VARCHAR(n) | 'abc' | Variable Länge bis n |
| Datum und/oder Zeit | DATE, TIME, DATETIME | '2023-05-28' | Verschiedene Formate für Datum/Zeit |
| Zeitstempel | TIMESTAMP | '2023-05-28 12:34:56' | Automatische Aktualisierung möglich |
| Binäre Datenobjekte variabler Länge (z.B. Bild) | BLOB | | Speicherung großer Binärdaten |
| Verbund | SET('a', 'b', 'c') | 'a,b' | Mehrere Werte möglich |
| JSON | JSON | {"key": "value"} | Speichern von JSON-Daten |

---

![Learn](../x_res/Learn.png)

# Mehrfachbeziehungen

Bei Mehrfachbeziehungen haben zwei Tabellen mehrere Beziehungen, die unabhängig voneinander sind und jeweils einen anderen Sachverhalt repräsentieren. Um die verschiedenen Beziehungen eindeutig zu kennzeichnen, müssen sie möglichst aussagekräftig beschriftet werden (Rolle). Die Kardinalitäten können natürlich verschieden sein, da die Beziehungen voneinander unabhängig sind. In den Beispielen unten gibt es drei unabhängige Beziehungen zwischen den Entitätstypen *tbl_Fahrten* und *tbl_Orte*. Eine dieser Beziehungen ist die Auflistung der Orte, die bei einer Tour angefahren werden können. Dies ist eine mc:mc-Beziehung und benötigt daher eine Transformationstabelle.

![Mehrfachbeziehungen](./media/5c72d6a1875a0b2936a49acd3776bb29.png)

---

# Rekursion

Bis jetzt haben wir Beziehungen zwischen zwei verschiedenen Entitätstypen betrachtet. Es gibt aber auch die Möglichkeit, dass an einer Assoziation nur ein einziger Entitätstyp beteiligt ist. Konkret bedeutet das, dass ein Datensatz dieser Tabelle mit einem anderen Datensatz aus der gleichen Tabelle in Beziehung steht. Eine reine Hierarchie können wir innerhalb der gleichen Tabelle erledigen. Sie erhält also einen Fremdschlüssel, der auf den Identifikationsschlüssel der eigenen Tabelle verweist. Das klassische Beispiel hierfür ist eine Firmenorganisation, bei der jede Person genau eine andere Person als Vorgesetzten hat. Da die in der Hierarchie höchste Person natürlich keinen Vorgesetzten mehr haben kann, ist es eine c:mc Beziehung. Würden wir dieses Fremdschlüsselattribut auf „not null“ setzen (im Access: „Eingabe erforderlich“), könnten wir die „höchste Person nicht erfassen.

![Rekursion](./media/90ba7e5d574d9a6447020c521ab3b61f.png)

Abbildung: Darstellung einer einfachen Hierarchie in der Workbench

Mit dieser einfachen Variante kommen wir aber nicht weiter, wenn aus der klaren Hierarchie (einmal-Rekursion – nur ein Vorgesetzter ist möglich) eine Netzwerkstruktur wird. In diesem konkreten Beispiel bedeutet das, dass eine Person auch mehrere Vorgesetzte haben kann.

## Einfache Hierarchie

Dann handelt es sich um eine mc:mc Beziehung und wir benötigen eine Transformationstabelle. Speziell daran ist, dass die beiden Fremdschlüssel der Transformationstabelle jeweils auf einen Identifikationsschlüssel der gleichen Tabelle zeigen, aber in unterschiedlichen Rollen. Im Beispiel sind das die Rollen „ist Vorgesetzter von“ und „ist_Mitarbeiter_von“.

![Einfache Hierarchie](./media/Einfache_Hierarchie.png)

Abbildung: Hierarchie-Darstellung einer netzwerkförmigen Struktur

Einfache Hierarchien können mit Rekursionen innerhalb der gleichen Tabelle abgebildet werden. Solange jedes Element nur maximal ein Oberelement hat, reicht ein Fremdschlüssel, der auf die Identifikationsschlüssel der eigenen Tabelle verweist. Lediglich das Wurzelelement oder Topelement hat einen NULL-Wert, da die Hierarchie ja irgendwo enden (oder anfangen) muss. Es handelt sich hierbei um eine c:mc Beziehung.

Wenn aber mehrere Oberelemente zugelassen sind (z. B. mehrere Projektleiter), dann handelt es sich um eine mc:mc-Beziehung und es wird eine Transformationstabelle benötigt, die für jeden Beziehungsgraphen einen Datensatz enthält, der angibt welches Oberelement zu welchem Unterelement gehört.

## Stücklistenproblem

Eine klassische Anwendung der Rekursion in der Datenmodellierung ist die Stücklistenproblematik. Es gibt eine Tabelle mit Produkten und deren Eigenschaften. Jetzt kann sich aber auch ein Produkt aus mehreren anderen Produkten zusammensetzen (modulare Produkte). Beides – die zusammengesetzten Produkte (Aggregate) sowie die einzelnen Bestandteile – befindet sich in unserer Produkte- oder Artikeltabelle und wird auch einzeln verkauft. Das Problem besteht nun darin, eine Liste mit Einzelteilen zu erzeugen, die alle Artikel auf elementarer Ebene enthält (die also nicht mehr aus mehreren Produktteilen bestehen).

Ein gutes Beispiel – sogar mit SQL-Code – finden Sie hier:

[Parts Explosion with CTEs in SQL](https://infocenter.sybase.com/help/index.jsp?topic=/com.sybase.help.sqlanywhere.12.0.1/dbusage/parts-explosion-cte-sqlug.html)

![Stücklistenproblem](./media/a23bd48e09ca11406474760f63e8d173.png)

Abbildung: Das Beispiel beschreibt die Artikel einer Elementmöbelfabrik.

Lösung mit Rekursion: Da es sich im Modell ja nicht um eine einfache Hierarchie handelt (c:mc), reicht die Erstellung eines Fremdschlüsselattributs in der Produktetabelle nicht aus. Neben der Produktetabelle benötigen wir eine weitere Tabelle, die die Zusammensetzungen enthält. Also welche Komponente (Einzelteil oder Aggregat) fließt in welches Aggregat und mit welcher Menge ein?

### Auftrag 

![ToDo](../x_res/ToDo.png) *Zeit: ca. 25 Min*

![Learn](../x_res/Train_R1.png)

  - Bauen Sie die obigen Beziehungen (Mehrfachbeziehungen, Rekursion, einfache Hierarchie) in ihr Tourenplaner-Schema ein.
  - Erstellen Sie die Struktur in der Datenbasis auf ihrem DBMS-Server. (Forward Engineering)
  - Studieren Sie das Stücklistenproblem und tauschen Sie mit ihrem(r) SitznachbarIn darüber aus: Wie ist die Tabelle "component and subcomponent" aufgebaut?

*Hinweis: Wir brauchen die neue Tourenplanerstruktur in Zukunft. also nicht wieder löschen!*

---

# Datenbearbeitung der Datenbasis (Repetition ÜK Modul 106)

![Learn](../x_res/Learn.png)

Nun wollen wir Daten in die Struktur einfügen und bearbeiten.

![Konzept](./media/Konzept_DML.png)

> Für diejenigen, die den ÜK noch nicht hatten: [Insert Präsentation](./insert-into.pdf) und [DML_Befehle](./DML_Intro.md)

### Aufträge DML

1. Setzen Sie den [Auftrag Insert](insert.md) um.
2. Setzen Sie den [Auftrag update delete alter drop](update_delete_alter_drop.md) um.

---

# Daten auslesen (Repetition ÜK Modul 106)

![Learn](../x_res/Learn.png)

Der SQL-Befehl Select gehört je nach Einteilung zur Gruppe DML oder zu der eigenen Gruppe DQL (Data-Query-Language).

**Studieren** Sie die ausführliche **Syntax** des Select-Befehls:

[MariaDB](https://mariadb.com/kb/en/select/), [MySQL](https://dev.mysql.com/doc/refman/8.0/en/select.html) und diese [Präsentation](select.pdf)! 

> Hinweis: Mit Select können auch die internen Funktionen ausgeführt werden! *(Siehe Script Beispiele)*

Der SELECT-Befehl:

![SELECT Konzept](./media/Select_Konzept.png)

```sql
-- Select Beispiele:
-- -----------------

-- SELECT Wertet aus und zeigt in angeschriebenen Spalten an
SET @var = 12;               -- User Var setzen
SELECT @var as 'Var Inhalt'; 
SELECT 23647 / 2 AS Division, 214649 * 2 AS Multiplikation, 12+123.3 AS Addition;
SELECT IF(0 = FALSE, 'true', 'false') AS Logik, IF(1 = TRUE, 'true', 'false') AS Logik ;
SELECT ROUND(1234.5,0) AS Ganze, ROUND(12345.5678,2) AS Rappen, ROUND(1234.5,-2) AS Hundert; -- Funktion Runden
SELECT pi() AS PI, SIN(90) AS Sinus, POWER(2,3) AS '2^3', ABS(-1.5) AS 'Ohne -';             -- Mathe Funktion 

-- Ausgabe ALLER Attribute (*) einer Tabelle 
SELECT * FROM filmedatenbank.dvd_sammlung;   
-- auch ohne  "filmedatenbank."  wenn vorher "USE filmedatenbank" verwendet wurde!

USE filmedatenbank;

-- SELECT * : Horizontale Einschränkuung
SELECT film FROM filmedatenbank.dvd_sammlung;
SELECT film, regisseur FROM filmedatenbank.dvd_sammlung;
SELECT id, film, nummer, laenge_minuten, regisseur FROM dvd_sammlung;

-- WHERE: Vertikale Einschränkung
SELECT * FROM dvd_sammlung WHERE film = 'Angst';

-- o findet auch ö's   'ö' = 'oe'
Select * FROM dvd_sammlung WHERE regisseur like '%Tar%' AND ( film = '%a%' OR film like '%o%');
