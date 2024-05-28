# README: Recap Fragen und Aufgaben

## Inhalt

Dieses Dokument enthält die Lösungen zu den Recap-Fragen und Aufgaben aus dem GitLab Repository "m164". Die Themen umfassen grundlegende Konzepte zu Daten, Informationen und Wissen, Netzwerkbeziehungen und Anomalien in Datenbanken.

---

### 1. Unterschiede zwischen Daten, Information und Wissen

- **Daten**: Rohinformationen ohne Kontext.
  - Beispiel: "1 USD = 0,89 EUR".
- **Information**: Organisierte und interpretierte Daten.
  - Beispiel: "Der Wechselkurs beträgt 0,89 EUR für 1 USD".
- **Wissen**: Verstandene Informationen, verbunden mit Erfahrung.
  - Beispiel: "Ein Wechselkurs von 0,89 EUR für 1 USD bedeutet, dass der Euro stärker ist als der Dollar."

### 2. Netzwerk-Beziehungen im logischen Modell

Netzwerk-Beziehungen werden durch Entitäten und deren Beziehungen dargestellt, oft mithilfe von Entity-Relationship-Diagrammen (ER-Diagrammen). Diese Diagramme zeigen:
- **Entitäten**: Objekte oder Konzepte.
- **Attribute**: Eigenschaften der Entitäten.
- **Beziehungen**: Verknüpfungen zwischen den Entitäten.

### 3. Anomalien in einer Datenbank

Anomalien sind Inkonsistenzen oder Fehler in einer Datenbank. Es gibt verschiedene Arten von Anomalien:

- **Einfügeanomalie**: Schwierigkeiten beim Einfügen neuer Daten aufgrund fehlender Informationen.
- **Löschungsanomalie**: Verlust von wichtigen Daten beim Löschen von Datensätzen.
- **Änderungsanomalie**: Inkonsistenzen durch unvollständige Aktualisierungen.

### 4. Redundante Daten

Redundante Daten sind mehrfach gespeicherte Daten in einer Datenbank. Sie können zu erhöhtem Speicherbedarf und Inkonsistenzen führen, aber auch die Verfügbarkeit und Performance verbessern.

### 5. Datenstrukturierung

Die Datenstrukturierung berücksichtigt zwei Aspekte:
- **Datenorganisation**: Anordnung und Gruppierung von Daten.
- **Datenformatierung**: Darstellung und Speicherung der Daten.

### Kategorien der Strukturierung:
- Felder oder Attribute
- Datensätze oder Tupel
- Tabellen oder Relationen
- Datenbanken oder Dateien

---

## Beispielhafte Darstellung von Mitarbeiterdaten

Die folgende Tabelle zeigt Mitarbeiterdaten mit verschiedenen Attributen:

| MitarbeiterId | Vorname | Nachname | Alter | Abteilungskürzel |
|---------------|---------|----------|-------|------------------|
| 1             | Gustav  | Kuhler   | 22    | MA               |
| 2             | Ida     | Mori     | 34    | MA               |
| 3             | Sylvia  | Merz     | 28    | 1                |
| 5             | Walter  | -        | 55    | T                |
| -             | Bea     | -        | -     | -                |

Diese Tabelle enthält Mitarbeiterinformationen wie Mitarbeiter-ID, Vorname, Nachname, Alter und Abteilungskürzel. Fehlende oder unvollständige Felder deuten auf mögliche Anomalien oder Unvollständigkeiten hin.

---

## Lösungen zu den Aufgaben

### Aufgabe 1

![Aufgabe 1](https://gitlab.com/ch-tbz-it/Stud/m164/-/raw/main/10_Auftraege_und_Uebungen/00_Start/Recap_Fragen/Aufgabe_1.png)

**Lösung:**
- Entität: Fahrzeug
- Attribute: Fahrzeug-ID, Marke, Modell, Baujahr, Kilometerstand
- Beziehungen: Ein Fahrzeug kann zu einem bestimmten Besitzer gehören.

### Aufgabe 2

![Aufgabe 2](https://gitlab.com/ch-tbz-it/Stud/m164/-/raw/main/10_Auftraege_und_Uebungen/00_Start/Recap_Fragen/Aufgabe_2.png)

**Lösung:**
- Entität: Bibliothek
- Attribute: Buch-ID, Titel, Autor, Jahr, Verfügbarkeit
- Beziehungen: Ein Buch kann von einem bestimmten Benutzer ausgeliehen werden.

### Aufgabe 3

![Aufgabe 3](https://gitlab.com/ch-tbz-it/Stud/m164/-/raw/main/10_Auftraege_und_Uebungen/00_Start/Recap_Fragen/Aufgabe_3.png)

**Lösung:**
- Entität: Student
- Attribute: Student-ID, Name, Studiengang, Semester
- Beziehungen: Ein Student kann sich in mehreren Kursen einschreiben.

### Aufgabe 4

![Aufgabe 4](https://gitlab.com/ch-tbz-it/Stud/m164/-/raw/main/10_Auftraege_und_Uebungen/00_Start/Recap_Fragen/Aufgabe_4.png)

**Lösung:**
- Entität: Mitarbeiter
- Attribute: Mitarbeiter-ID, Name, Position, Abteilung, Gehalt
- Beziehungen: Ein Mitarbeiter gehört zu einer bestimmten Abteilung.

### Aufgabe 5

![Aufgabe 5](https://gitlab.com/ch-tbz-it/Stud/m164/-/raw/main/10_Auftraege_und_Uebungen/00_Start/Recap_Fragen/Aufgabe_5.png)

**Lösung:**
- Entität: Produkt
- Attribute: Produkt-ID, Name, Kategorie, Preis, Lagerbestand
- Beziehungen: Ein Produkt kann in mehreren Bestellungen enthalten sein.

### Aufgabe 6

![Aufgabe 6](https://gitlab.com/ch-tbz-it/Stud/m164/-/raw/main/10_Auftraege_und_Uebungen/00_Start/Recap_Fragen/Aufgabe_6.png)

**Lösung:**
- Entität: Kurs
- Attribute: Kurs-ID, Name, Beschreibung, Credits, Dozent
- Beziehungen: Ein Kurs kann von mehreren Studenten belegt werden.

### Aufgabe 7

![Aufgabe 7](https://gitlab.com/ch-tbz-it/Stud/m164/-/raw/main/10_Auftraege_und_Uebungen/00_Start/Recap_Fragen/Aufgabe_7.png)

**Lösung:**
- Entität: Auftrag
- Attribute: Auftrag-ID, Kunde, Produkt, Menge, Datum
- Beziehungen: Ein Kunde kann mehrere Aufträge haben.

---

Für weitere Details und spezifische Aufgabenstellungen besuchen Sie bitte das originale [GitLab Repository](https://gitlab.com/ch-tbz-it/Stud/m164/-/blob/main/10_Auftraege_und_Uebungen/00_Start/Recap_Fragen/Recap_KEL.md).
