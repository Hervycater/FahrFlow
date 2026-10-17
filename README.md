# FahrFlow

Prototyp einer Plattform für Fahrzeugüberführungen. Auftraggeber legen Überführungsaufträge an, Fahrer nehmen sie an und führen sie durch, die Disposition behält den Überblick.

**Stand:** Prototyp in Vorbereitung · Spezifikationen im Status *Entwurf* · Produktrahmen Version 0.3 in Überarbeitung

---

## Zweck dieses Repositories

Dieses Repository ist die gemeinsame Arbeitsgrundlage für alle Beteiligten, Menschen wie Agenten. Es dokumentiert:

- **Was** gebaut werden soll (`specs/`).
- **Wer** woran arbeiten darf (diese README und `agents/`).
- **Wie** die Anwendung technisch aufgebaut werden soll (`docs/architecture.md`).
- **Welche technischen Entscheidungen** getroffen wurden (`docs/decisions.md`).
- **Den Anwendungscode** (`app/`).
- **Die Qualitätssicherung** (`tests/`).
- **Die Berichte aller Agenten, die unabhängigen Prüfungen und die Abschlussberichte** (`reports/`).

Wer neu einsteigt, soll anhand dieser Dateien den Projektstand, die verbindlichen Regeln, die eigenen Zuständigkeiten und die offenen Fragen nachvollziehen können. Produktentscheidungen und technische Festlegungen dürfen nicht aus Vermutungen oder aus nicht dokumentiertem Kontext abgeleitet werden.

## Lesereihenfolge

1. Diese Datei (`README.md`)
2. `specs/product.md`: Produktrahmen, Umfang, Nicht-Ziele und Querschnittsregeln
3. Die für die eigene Aufgabe relevanten Schnittstellenspezifikationen in `specs/`
4. Die eigene Rollenanweisung in `agents/`
5. `docs/decisions.md`: fachliche und technische Entscheidungen; für den Product Manager immer, für die anderen Rollen, soweit ihre Aufgabe betroffen ist. `docs/architecture.md` bei technischen Fragen.
6. Bei der Übernahme bestehender Arbeit: zuerst die letzten Einträge der eigenen Berichtsdatei in `reports/`, danach die relevanten Einträge der Berichtsdateien der anderen Agenten und, falls vorhanden, der letzte Abschlussbericht

Verbindliche Dateien werden von `main` gelesen; die eigene Arbeit (eigener Schreibbereich einschließlich der eigenen Berichtsdatei) vom eigenen Branch (siehe „Branches und Zusammenführung“).

## Ordnerstruktur und Zuständigkeiten

```text
fahrflow/
├── README.md
├── specs/
│   ├── product.md
│   ├── auth.md
│   ├── orders.md
│   ├── assignments.md
│   ├── status.md
│   ├── trips.md
│   └── handover.md
├── agents/
├── app/
│   ├── backend/
│   └── frontend/
├── tests/
├── docs/
│   ├── architecture.md
│   └── decisions.md
├── reports/
│   ├── product-manager-berichte.md
│   ├── backend-berichte.md
│   ├── frontend-berichte.md
│   ├── qa-berichte.md
│   ├── assistent-berichte.md
│   └── abschlussberichte/
└── .github/
```

| Bereich | Zweck | Schreibzugang |
|---|---|---|
| `README.md` | Projektübersicht und Arbeitsregeln | Projektinhaber |
| `specs/` | Produktrahmen und Spezifikationen | Projektinhaber (Änderungen und Freigabe); neue Dateien im Status *Entwurf*: Product Manager, nur im Arbeitsauftrag |
| `agents/` | Rollenanweisungen | Projektinhaber |
| `app/backend/` | API, Datenhaltung, Berechtigungen und Statuslogik | Backend-Agent |
| `app/frontend/` | Oberflächen für Auftraggeber, Disposition und Fahrer | Frontend-Agent |
| `tests/` | Abnahmetests | QA-Agent |
| `docs/architecture.md` | Architekturentwurf; Freigabe durch den Projektinhaber | Product Manager, nur im Arbeitsauftrag |
| `docs/decisions.md` | Dokumentation technischer und fachlicher Entscheidungen | Projektinhaber; Agenten schlagen Einträge in ihren Berichten vor |
| `reports/product-manager-berichte.md` | Sitzungsberichte des Product Managers | Product Manager |
| `reports/backend-berichte.md` | Sitzungsberichte des Backend-Agenten | Backend-Agent |
| `reports/frontend-berichte.md` | Sitzungsberichte des Frontend-Agenten | Frontend-Agent |
| `reports/qa-berichte.md` | Sitzungsberichte des QA-Agenten | QA-Agent |
| `reports/assistent-berichte.md` | Gesprächszusammenfassungen, Rollenprüfungen und Rollenentwürfe des Assistenten | Assistent |
| `reports/abschlussberichte/` | Abschlussberichte je Phase | Product Manager, nur im Arbeitsauftrag |
| `.github/` | Repository- und Workflow-Konfiguration | Projektinhaber |

Die Ordnerstruktur dokumentiert Zuständigkeiten, nicht automatisch den Fertigstellungsgrad der darin enthaltenen Dateien. Maßgeblich für den Bearbeitungsstand sind die Dateien selbst und die dazugehörigen Berichte. Bereits vorhandene Einzelberichte in `reports/` bleiben als Altbestand unverändert.

## Grundregeln

0. **Rangfolge.** Bei Widerspruch zwischen README und Rollenanweisung gilt die README. Widersprüche zwischen README und Spezifikationen löst kein Agent selbst. In beiden Fällen hält der Agent im betroffenen Punkt an, meldet den Widerspruch in seinem Bericht und arbeitet im unstrittigen Teil weiter.

1. **Ein Bereich, eine Zuständigkeit.** Jeder Agent arbeitet ausschließlich in dem Bereich, den die Zuständigkeitstabelle ihm zuweist. Diese Tabelle ist die Obergrenze, ein Arbeitsauftrag erweitert sie nicht. Änderungen außerhalb dieses Bereichs werden vorgeschlagen und nicht eigenständig vorgenommen.

2. **Spezifikationen sind verbindlich.** Die Umsetzung muss den freigegebenen Spezifikationen entsprechen. Wo eine Spezifikation keine Vorgabe macht, ist die technische Umsetzung frei, sofern sie keine nicht vereinbarten fachlichen Auswirkungen erzeugt. Seiteneffekte sind nur zulässig, wenn die Spezifikation sie unter „Zustandsänderungen“ vorsieht.

3. **Spezifikationen ändert nur der Projektinhaber.** Der Product Manager legt neue Spezifikationsdateien im Status *Entwurf* in `specs/` nur im Arbeitsauftrag an. Bestehende Spezifikationsdateien, auch die von ihm entworfenen, ändert er nicht; Änderungen schlägt er in seinem Bericht vor. Andere Agenten ändern keine Spezifikationsdateien und schlagen Änderungen in ihren Berichten vor.

4. **Entwurf ist nicht gleich Freigabe.** Eine vorhandene Spezifikationsdatei gilt nicht automatisch als verbindlich freigegeben. Spezifikationen im Status *Entwurf* dürfen nicht als alleinige Grundlage für die Implementierung behandelt werden. Der Projektinhaber erteilt die ausdrückliche Freigabe.

5. **Der Auftragsstatus gehört dem Backend.** *(projektspezifisch)* Kein anderer Teil des Systems setzt den Auftragsstatus eigenmächtig. Die zulässigen Statusübergänge sind ausschließlich in `specs/status.md` definiert.

6. **Querschnittsregeln gelten für alle Schnittstellenspezifikationen.** *(projektspezifisch)* Anmeldung, Fehlerformat, Eingaberegeln, Zeitangaben, Kennungen, Haltbarkeit und Gleichzeitigkeit sind in `specs/product.md`, Abschnitt 6, festgelegt. Sie gelten nicht für das Berichtswesen, das seine Zeitangaben und Kennungen selbst regelt.

7. **Keine stillschweigenden Produktentscheidungen.** Unklare, widersprüchliche oder fehlende Anforderungen werden im Bericht unter „Rückfragen und Folgeentscheidungen“ dokumentiert (Format B: unter „Widersprüche und Lücken in den Spezifikationen“ oder „Rückfragen“). Agenten dürfen sie nicht eigenmächtig durch fachliche Annahmen ersetzen.

8. **Technische Entscheidungen werden dokumentiert.** Entscheidungen zu Datenhaltung, Sitzungsverwaltung, Technologie, Hosting und Dateispeicherung werden in `docs/decisions.md` festgehalten. Agenten schlagen Einträge in ihren Berichten vor (Format A: unter „Annahmen und Vorschläge“; Format B: unter „Rückfragen“), der Projektinhaber trägt sie ein. Technische Vorschläge dürfen keine freigegebenen Produktanforderungen abschwächen.

9. **Nichts geht ungeprüft in `main`.** Änderungen der Agenten kommen ausschließlich über Pull Requests nach `main`. Ein Agent darf einen Pull Request von seinem Branch eröffnen; prüfen und zusammenführen darf ihn nur der Projektinhaber. Der Projektinhaber darf seine eigenen Bereiche direkt auf `main` ändern. Kein Agent darf die Freigabe des Projektinhabers ersetzen.

10. **Fertig heißt geprüft.** Eine Aufgabe gilt erst als erledigt, wenn ihre vereinbarten Akzeptanzkriterien erfüllt und die erforderlichen Tests erfolgreich ausgeführt wurden. QA berichtet unabhängig über Ergebnisse, Abweichungen und offene Risiken, im QA-Berichtsformat (Format B).

11. **Berichte entstehen während der Arbeit.** Jeder Agent führt seinen Bericht von Beginn der Sitzung an fortlaufend und hinterlegt ihn auch dann, wenn die Arbeit abgebrochen wird. Das Berichtswesen regelt Ablage, Benennung und Format verbindlich.

12. **Rollenanweisungen ändert nur der Projektinhaber.** Kein Agent schreibt oder ändert Rollenanweisungen, auch nicht die eines anderen Agenten. Jeder Agent liest nur seine eigene Rollenanweisung. Ausnahmen: Der Assistent liest alle Rollenanweisungen, das gehört zu seiner Rolle. Der Product Manager liest die der anderen Rollen nur, wenn ein Arbeitsauftrag es verlangt. Änderungen schlagen Agenten in ihren Berichten vor; der Assistent kann sie als Entwurf ausformulieren. Das Lesen lässt sich technisch nicht sperren, diese Regel bindet die Agenten.

13. **Arbeitsaufträge.** Jeder Agent arbeitet nur im Rahmen eines Arbeitsauftrags des Projektinhabers (siehe „Arbeitsaufträge“).

14. **Ein fester Branch je Rolle.** Jeder Agent schreibt nur auf seinem Branch; verbindliche Dateien liest er von `main` (siehe „Branches und Zusammenführung“).

## Rollen

| Rolle | Aufgabe | Zuständig für |
|---|---|---|
| Projektinhaber | Steuert das Projekt, erteilt Arbeitsaufträge, trifft Produktentscheidungen, erteilt Freigaben und führt Pull Requests zusammen | `README.md`, `agents/`, `specs/` (Änderungen und Freigabe), `docs/decisions.md`, `.github/`, `main` |
| Product Manager | Analysiert Anforderungen, wertet `docs/decisions.md` aus und schlägt darauf aufbauend strategische Anpassungen vor, entwirft neue Spezifikationen, schlägt Änderungen an bestehenden vor, entwirft die Architektur und schreibt den Abschlussbericht einer Phase | Neue Spezifikationsdateien in `specs/` (nur im Arbeitsauftrag); `docs/architecture.md` (nur im Arbeitsauftrag); `reports/product-manager-berichte.md`; `reports/abschlussberichte/` (nur im Arbeitsauftrag) |
| Backend-Agent | Implementiert API, Datenhaltung, Berechtigungen und Statuslogik gemäß freigegebenen Spezifikationen | `app/backend/`, `reports/backend-berichte.md` |
| Frontend-Agent | Implementiert Oberflächen für Auftraggeber, Disposition und Fahrer gemäß freigegebenen Spezifikationen | `app/frontend/`, `reports/frontend-berichte.md` |
| QA-Agent | Prüft unabhängig die Anforderungen, erstellt und führt Abnahmetests aus und dokumentiert Abweichungen | `tests/`, `reports/qa-berichte.md` |
| Assistent | Führt allgemeine Gespräche mit dem Projektinhaber und hält sie in Berichten fest; entwirft Rollenanweisungen als Vorschlag und prüft, ob die Agenten ihre Rolle erfüllen | Schreiben: `reports/assistent-berichte.md`. Lesen: alle Dateien und Branches |

Die Zuständigkeit eines Agenten berechtigt ihn nicht dazu, Produktentscheidungen zu treffen, Spezifikationsänderungen freizugeben oder die Zuständigkeit anderer Rollen zu überschreiben.

### Besonderheiten des QA-Agenten

- Bei Prüfaufträgen prüft er, soweit prüfbar, ob Backend und Frontend dieselbe Spezifikation übereinstimmend interpretieren. Dafür liest er die Branches, die der Arbeitsauftrag als Prüfgegenstand nennt.
- Er dokumentiert die Konsistenzprüfung in Format B unter „Prüfumfang“; festgestellte Unterschiede führt er unter „Abweichungen“ mit Bezug auf die Spezifikation auf.
- Er berichtet, korrigiert aber nicht. Welche Interpretation gilt, entscheidet der Projektinhaber.

### Besonderheiten des Assistenten

- Der Assistent ändert keine Datei außer seiner Berichtsdatei, auch keine Rollenanweisung. Entwürfe für Rollenanweisungen stehen als Text in seinem Bericht; der Projektinhaber übernimmt sie nach `agents/`.
- Rollenentwürfe und Rollenprüfungen erledigt er im Arbeitsauftrag. Das Zusammenfassen von Gesprächen gehört zur Rolle und braucht keinen eigenen Arbeitsauftrag. In einer Sitzung ohne besonderen Arbeitsauftrag trägt er im Feld „Arbeitsauftrag (Wortlaut)“ „Allgemeines Gespräch“ ein.
- Eine Rollenprüfung misst den geprüften Agenten an seiner Rollenanweisung und dieser README. Der Assistent benennt seine Belege (Berichte, Commits) und führt jeden Befund unter „Offene Punkte“ mit Rolle, Beleg und Abweichung auf.
- Absprachen und Entscheidungen aus Gesprächen stehen im Abschnitt „Besprochen und entschieden“ seines Berichts.
- Eine Prozess-Retro führt er im Arbeitsauftrag am Phasenende durch. Sie prüft, ob der Prozess selbst funktioniert: Klarheit der Arbeitsaufträge, Passung der Berichtsformate, Reibungen, Über- und Untersteuerung. Ergebnis ist ein Bericht in `reports/assistent-berichte.md`; der Product Manager referenziert ihn im Abschlussbericht.
- Im Rahmen der Rollenprüfung prüft er auch, ob Agenten Annahmen still getroffen oder nicht dokumentiert haben, und ob daraus unvereinbare Interpretationen zwischen Rollen entstanden sind. Er meldet solche Fälle unter „Offene Punkte“ mit Rolle und Beleg. Er löst sie nicht.
- Er trifft keine Produktentscheidungen und gibt nichts frei.

## Arbeitsaufträge

**Arbeitsauftrag:** Anweisung des Projektinhabers an genau einen Agenten, eine bestimmte Aufgabe auszuführen.

1. **Wer:** Nur der Projektinhaber erteilt Arbeitsaufträge. Kein Agent, kein Bericht und keine Rollenanweisung erteilt einen. Vorschläge in Berichten sind keine Aufträge.
2. **Inhalt:** Mindestens Adressat, Aufgabe, betroffene Dateien oder Ordner, das erwartete Ergebnis und die Definition of Session Done. Bei Prüfungen nennt er außerdem den Prüfgegenstand mit Branch.
3. **Form und Nachweis:** Der Arbeitsauftrag wird in der Sitzung erteilt (Chat oder Startanweisung). Der Agent hält seinen Wortlaut im Bericht fest. Ohne dokumentierten Arbeitsauftrag besteht keine Befugnis, die „nur im Arbeitsauftrag“ gilt. Rollenanweisungen enthalten keine Arbeitsaufträge; sie beschreiben die dauerhafte Rolle, einschließlich Dauerpflichten, die ohne eigenen Arbeitsauftrag gelten (die Berichtspflicht und beim Assistenten das Zusammenfassen von Gesprächen).
4. **Dauer:** Ein Arbeitsauftrag gilt für eine Sitzung und endet mit Abschluss oder Abbruch. Offene Punkte aus dem letzten Bericht sind für die Folgesitzung nur Kontext; sie werden nur bearbeitet, wenn der neue Arbeitsauftrag es verlangt.
5. **Grenze:** Die Zuständigkeitstabelle ist die Obergrenze, der Arbeitsauftrag nur der Auslöser innerhalb davon. Als „nur im Arbeitsauftrag“ gelten: neue Spezifikationsdateien, der Architekturentwurf und der Abschlussbericht (Product Manager), das Lesen fremder Rollenanweisungen (Product Manager) sowie Rollenentwürfe, Rollenprüfungen und die Prozess-Retro (Assistent). Kein Arbeitsauftrag verleiht Schreibrechte auf `README.md`, `agents/`, `.github/` oder `docs/decisions.md`.
6. **Unklarheit:** Ist ein Arbeitsauftrag unklar, fragt der Agent nach. Ist niemand erreichbar, wählt er die engste Lesart und vermerkt das im Bericht unter „Annahmen und Vorschläge“.

### Definition of Session Done

Die Definition of Session Done legt fest, wann eine Sitzung als abgeschlossen gilt. Sie ist Bestandteil des Arbeitsauftrags und enthält mindestens:

- das erwartete Ergebnis (Datei, Bericht, Pull Request, Analyse),
- die Akzeptanzkriterien,
- erforderliche Tests oder Prüfungen,
- ob ein Pull Request zu eröffnen ist.

Bei Erkundungs-, Analyse- oder Entwurfsaufträgen darf sie lauten: „Ergebnis ist ein Bericht mit Optionen; keine Implementierung.“

Fehlt die Definition of Session Done, wählt der Agent die engste Lesart, vermerkt das im Bericht unter „Annahmen und Vorschläge“ und arbeitet nicht über den erkennbaren Auftrag hinaus.

## Arbeitsablauf

1. **Anforderungen prüfen:** Der Product Manager analysiert im Arbeitsauftrag den bestehenden Produktrahmen, die Schnittstellenspezifikationen, Prüfberichte und offenen Fragen.

2. **Entwerfen und vorschlagen:** Beauftragt der Projektinhaber neue Spezifikationen, entwirft der Product Manager sie als neue Dateien im Status *Entwurf* in `specs/`. Notwendige Änderungen an bestehenden Spezifikationsdateien, Widersprüche, fehlende Akzeptanzkriterien und technische Abhängigkeiten dokumentiert er in seinem Bericht (`reports/product-manager-berichte.md`). Bestehende Spezifikationsdateien verändert er nicht. Im Arbeitsauftrag entwirft er außerdem `docs/architecture.md`.

3. **Produktentscheidungen treffen:** Der Projektinhaber prüft die Vorschläge und Entwürfe, entscheidet über offene fachliche Fragen und überarbeitet beziehungsweise genehmigt die betroffenen Spezifikationen.

4. **Spezifikationen freigeben:** Die für den Hauptablauf relevanten Spezifikationen müssen vollständig genug, widerspruchsfrei und ausdrücklich freigegeben sein, bevor die Implementierung beginnt.

5. **Abnahmetests vorbereiten:** QA leitet aus den freigegebenen Spezifikationen reproduzierbare Abnahmetests ab. Die Tests sollen möglichst vor der Implementierung existieren.

6. **Implementieren:** Backend und Frontend setzen die freigegebenen Anforderungen auf ihren Branches um. Abweichungen, unklare Anforderungen und technische Hindernisse werden dokumentiert, statt eigenmächtig fachliche Regeln zu verändern.

7. **Unabhängig prüfen:** QA führt die Abnahmetests aus und prüft insbesondere Berechtigungen, Fehlerfälle, Zustandsübergänge, gleichzeitige Anfragen und die vollständige Durchführung des Hauptablaufs.

8. **Berichten und freigeben:** Jeder Agent führt seinen Bericht von Sitzungsbeginn an (siehe „Berichtswesen“) und schließt ihn am Ende der Sitzung ab: erledigte Aufgaben, offene Punkte, Testergebnisse und notwendige Folgeentscheidungen. Der Projektinhaber entscheidet über die Freigabe und führt die Pull Requests zusammen.

9. **Phase abschließen:** Erklärt der Projektinhaber eine Phase für beendet, beauftragt er zuerst den Assistenten mit der Prozess-Retro und danach den Product Manager mit dem Abschlussbericht. Voraussetzung ist, dass die Berichte der Phase einschließlich der Prozess-Retro per Pull Request in `main` sind. Der Abschlussbericht dient als Vorlage für die Vorführung und als Grundlage für die Arbeitsaufträge der nächsten Phase. Der Projektinhaber nimmt die Phase ab.

Begleitend prüft der Assistent im Arbeitsauftrag, ob die Agenten ihre Rolle erfüllen, und entwirft Anpassungen der Rollenanweisungen als Vorschlag.

## Branches und Zusammenführung

### 1. Modell

`main` ist die einzige verbindliche Fassung. Der Projektinhaber legt je Rolle einmal einen festen Branch von `main` aus an. Agenten legen keine Branches an. Außer `main` und den Agenten-Branches gibt es keine dauerhaften Branches.

| Rolle | Branch |
|---|---|
| Product Manager | `agent/product-manager` |
| Backend-Agent | `agent/backend` |
| Frontend-Agent | `agent/frontend` |
| QA-Agent | `agent/qa` |
| Assistent | `agent/assistent` |

### 2. Schreiben

- Ein Agent schreibt nur auf seinem Branch und nur in den Pfaden seiner Zeile der Zuständigkeitstabelle. In `main` und in anderen Branches schreibt er nie.
- Kein Force-Push, kein Rebase, kein Löschen von Branches.
- Fehlt sein Branch, legt er keinen an. Er meldet das dem Projektinhaber in der Sitzung und arbeitet nicht auf einem anderen Branch weiter.
- Pro Rolle läuft nur eine Sitzung gleichzeitig.

### 3. Lesen

- Verbindliche Dateien (README, Rollenanweisung, Spezifikationen, Entscheidungen, Berichte anderer Agenten) liest ein Agent ausschließlich von `main`. Entwürfe auf anderen Branches sind keine Arbeitsgrundlage.
- Den eigenen Branch liest und schreibt er. Andere Branches ignoriert er.
- Es gelten folgende Ausnahmen:
  1. **QA-Agent:** Darf die Branches lesen, die im jeweiligen Prüfauftrag ausdrücklich als Prüfgegenstand genannt sind. QA liest den Branch, den der Arbeitsauftrag als Prüfgegenstand nennt, zum Beispiel `agent/backend`. Ist der Prüfbereich unklar, muss er vor der Prüfung Rückfrage halten.
  2. **Assistent:** Darf alle Branches des Repositories lesen, soweit dies für seine Aufgaben erforderlich ist. Dies umfasst insbesondere rollenübergreifende Analysen und die Prüfung, ob Agenten ihre Rollenanweisungen einhalten.
- Verbindliche Referenz bei Prüfungen: QA verwendet den ausdrücklich genannten Branch als Prüfgegenstand für die zu prüfende Implementierung. main bleibt die Referenz für verbindliche Regeln und ausdrücklich freigegebene Anforderungen. Entwürfe oder Änderungen auf anderen Branches werden nicht allein dadurch verbindlich, dass QA sie liest.
- **Technische Absicherung:** Repository-Berechtigungen sollen die festgelegten Zugriffsgrenzen unterstützen und, soweit technisch möglich, absichern. Die tatsächlichen technischen Möglichkeiten und Einschränkungen sind bei der Einrichtung zu berücksichtigen.

### 4. Vertrauen und Regelkonformität
Die Zugriffs- und Schreibregeln sind verbindliche Arbeitsregeln. Jeder Agent ist verpflichtet, die README und seine eigene Rollenanweisung einzuhalten.

Technische Repository-Berechtigungen und Schutzregeln unterstützen die Einhaltung dieser Vorgaben, ersetzen aber weder die Regelbeachtung noch die Prüfung der tatsächlichen technischen Absicherung. Aus einer beschriebenen Schutzmaßnahme darf nicht geschlossen werden, dass sie bereits eingerichtet oder wirksam ist.

Der Assistent prüft im Rahmen seiner Rollenprüfungen, soweit anhand der verfügbaren Informationen möglich, ob Agenten die festgelegten Zugriffs- und Schreibregeln einhalten. Festgestellte Abweichungen dokumentiert er mit nachvollziehbaren Belegen in seinem Bericht und legt sie dem Projektinhaber zur Entscheidung vor.

Der Assistent darf festgestellte Verstöße nicht eigenmächtig durch Änderungen an fremden Dateien oder Branches korrigieren. Über notwendige Korrekturen und Änderungen am Regelwerk entscheidet der Projektinhaber.

### 5. Zusammenführung

- Zu Sitzungsbeginn holt der Agent `main` per Merge in seinen Branch.
- Ein Agent darf einen Pull Request von seinem Branch nach `main` eröffnen (Vorlage: `.github/pull_request_template.md`). Prüfen und zusammenführen darf nur der Projektinhaber, mit „Merge commit“ ohne Squash, damit die Agenten-Branches mit `main` verträglich bleiben.

### 6. Technische Absicherung (vom Projektinhaber einzurichten)

Die GitHub-Einstellungen ergänzen die Arbeitsregeln und ersetzen sie nicht. Eine beschriebene Schutzmaßnahme gilt erst dann als eingerichtet, wenn sie im Repository tatsächlich konfiguriert und ihre Wirkung geprüft wurde.

Der Projektinhaber führt die folgenden Aufgaben schrittweise aus und dokumentiert den Einrichtungsstand:

1. **Schutz von `main`:** Pull Request verpflichtend; Force-Push und Löschen gesperrt. Die Einstellungen müssen so geprüft werden, dass der Projektinhaber den vorgesehenen Freigabeprozess weiterhin ausführen kann.
2. **Pfadprüfung für Pull Requests:** Ein automatisierter Check bestimmt anhand des Branchnamens die Rolle und schlägt fehl, wenn ein Pull Request Dateien außerhalb der für diese Rolle erlaubten Pfade ändert. Für `agent/product-manager` sind in `specs/` nur neu hinzugefügte Dateien erlaubt. `README.md`, `agents/`, `.github/` und `docs/decisions.md` sind für alle Agenten gesperrt.
3. **Workflow einrichten:** Der Check wird unter `.github/workflows/` abgelegt und vom Projektinhaber eingerichtet und getestet.
4. **Schreibzugriff prüfen:** Der Projektinhaber prüft, welche Repository-Berechtigungen und Branch-Regeln für die tatsächlich verwendeten Agenten zur Verfügung stehen. Ziel ist, Schreibzugriffe auf fremde Branches und unzulässige Änderungen an geschützten Bereichen so weit wie technisch möglich zu verhindern.
5. **Einrichtungsstand dokumentieren:** Nicht eingerichtete oder nicht erfolgreich geprüfte Schutzmaßnahmen bleiben ausdrücklich offene Aufgaben. Die Arbeitsregeln gelten unabhängig davon weiterhin für alle Agenten.

Branch Protection Rules allein garantieren nicht, dass jeder Agent ausschließlich in seinen eigenen Branch schreiben kann. Die tatsächliche Schutzwirkung hängt von der eingerichteten Konfiguration und den Zugriffsrechten ab.

## Berichtswesen

### 1. Grundsatz

Jeder Agent berichtet über jede Sitzung. Der Bericht ist Teil der Arbeit und kein Nachtrag. Agenten haben kein Gedächtnis an frühere Sitzungen. Die eigene Berichtsdatei ist deshalb die Übergabe zwischen Sitzungen und gegenüber dem Projektinhaber.

Übergabe-Minimum. Jeder Bericht muss so vollständig sein, dass die nächste Sitzung ohne nicht dokumentierten Kontext arbeiten kann. Das umfasst mindestens: aktueller Stand, nächster konkreter Schritt, blockierende Rückfragen, getroffene Annahmen und offene Risiken. Was die nächste Sitzung nicht wissen muss, muss der Bericht nicht enthalten. Der Bericht ersetzt keine Spezifikation und keine Entscheidung des Projektinhabers.

### 2. Ablage

Jeder Agent hat genau eine Berichtsdatei. Sie gehört zu seinem Schreibbereich (Zuständigkeitstabelle).

| Agent | Berichtsdatei | Sitzungsbericht |
|---|---|---|
| Product Manager | `reports/product-manager-berichte.md` | Format A; zusätzlich Format C für Abschlussberichte |
| Backend-Agent | `reports/backend-berichte.md` | Format A |
| Frontend-Agent | `reports/frontend-berichte.md` | Format A |
| QA-Agent | `reports/qa-berichte.md` | Format B |
| Assistent | `reports/assistent-berichte.md` | Format A |

Dazu gelten diese Regeln:

- Von den Berichtsdateien schreibt jeder Agent nur in seine eigene. Die der anderen liest er von `main`.
- Jeder Bericht ist ein Eintrag in der Berichtsdatei. Neue Einträge werden unten angehängt.
- Frühere Einträge werden nicht verändert. Einzige Ausnahme ist der Eintrag der laufenden Sitzung des Agenten.
- Existiert die Berichtsdatei noch nicht, legt der Agent sie mit der Überschrift `# Berichte: [Rolle]` an.
- Die Berichtsdatei liegt auf dem Branch des Agenten und gelangt wie alles andere per Pull Request nach `main` (Grundregel 9).

### 3. Benennung: Datum_Zeit_Verfasser_Absicht

Jeder Bericht trägt eine Berichtskennung nach dem Schema `Datum_Zeit_Verfasser_Absicht`. Sie ist die Überschrift (Ebene 2) des Eintrags. Berichte, die dem Projektinhaber direkt vorgelegt werden, tragen dieselbe Kennung.

| Teil | Bedeutung | Schreibweise |
|---|---|---|
| Datum | Tag des Sitzungsbeginns | `JJJJ-MM-TT` |
| Zeit | Uhrzeit des Sitzungsbeginns, 24-Stunden-Zählung, in der Projektzeitzone | `HH-MM` |
| Verfasser | Rolle des berichtenden Agenten | `product-manager`, `backend`, `frontend`, `qa` oder `assistent` |
| Absicht | Was die Sitzung erreichen soll | ein bis vier Wörter, Kleinbuchstaben, durch Bindestriche getrennt, ohne Umlaute und Sonderzeichen |

Die Teile werden durch einen Unterstrich getrennt. Innerhalb eines Teils steht kein Unterstrich.

Beispiel: `2026-10-10_16-06_product-manager_berichtswesen-einfuehren`

Die Berichtskennung bleibt für die gesamte Sitzung unverändert, auch wenn der Eintrag fortgeschrieben wird. Ein Abschlussbericht trägt dieselbe Kennung als Dateiname, zum Beispiel `2026-12-01_10-00_product-manager_abschlussbericht-phase-1.md`.

### 4. Ablauf einer Sitzung

1. **Vorbereiten:** Der Agent arbeitet die Lesereihenfolge durch, einschließlich der letzten Einträge seiner Berichtsdatei, und holt `main` per Merge in seinen Branch. Hat der letzte Eintrag den Status *laufend* oder *abgebrochen*, nimmt er dessen offene Punkte als Kontext zur Kenntnis. Er bearbeitet sie nur, wenn der Arbeitsauftrag es verlangt.
2. **Anlegen:** Bevor die eigentliche Arbeit startet, legt der Agent seinen Eintrag an: Berichtskennung, Status *laufend*, Wortlaut des Arbeitsauftrags und Bezug.
3. **Fortschreiben:** Der Agent ergänzt den Eintrag nach jedem abgeschlossenen Arbeitsschritt und hält den Stand auf seinem Branch fest (Commit und Push). Eine getroffene Annahme, eine neue Rückfrage, ein festgestellter Widerspruch und jede Absprache oder Entscheidung des Projektinhabers werden sofort eingetragen und nicht erst am Ende der Sitzung.
4. **Abschließen:** Am Ende der Sitzung setzt der Agent den Status auf *abgeschlossen* und führt die Selbstprüfung durch.
5. **Abbruch:** Wird die Arbeit abgebrochen (Fehler, Zeit- oder Kontextgrenze, Entzug von Zugängen oder Anweisung des Projektinhabers), hält der Agent sofort den aktuellen Stand auf seinem Branch fest, setzt den Status auf *abgebrochen* und trägt Abbruchgrund und nächsten Schritt ein.
6. **Abbruch ohne Möglichkeit zur Meldung:** Konnte ein Agent den Status nicht mehr ändern, bleibt der letzte Eintrag auf *laufend* stehen. Die Folgesitzung und der Projektinhaber behandeln einen Eintrag mit Status *laufend*, auf den keine Fortsetzung folgt, als abgebrochen. Die Folgesitzung vermerkt das in ihrem eigenen Eintrag.

### 5. Berichtsformat A (Sitzungsbericht, Standardformat für alle Agenten außer QA)

Product Manager, Backend-Agent, Frontend-Agent und Assistent verwenden für Sitzungsberichte ausschließlich dieses Format. Ein Agent darf Abschnitte nicht weglassen, umbenennen oder umsortieren. Nur QA darf davon abweichen, und zwar ausschließlich durch Format B.

```markdown
## JJJJ-MM-TT_HH-MM_verfasser_absicht

**Status:** laufend | abgeschlossen | abgebrochen
**Arbeitsauftrag (Wortlaut) und Bezug:** [Wortlaut des Arbeitsauftrags, betroffene Dateien, Spezifikationen mit Version]
**Abbruchgrund und nächster Schritt:** [nur bei Status abgebrochen, sonst „Entfällt“]

### Erledigt
[Welche Dateien und Aufgaben, jeweils ein Satz]

### Besprochen und entschieden
[Absprachen mit dem Projektinhaber in dieser Sitzung in Sätzen. Getroffene Entscheidungen sind als „Entscheidung“ gekennzeichnet, damit der Projektinhaber sie in docs/decisions.md übernehmen kann. Oder: Keine.]

### Annahmen und Vorschläge
[Jede Annahme und jeder Vorschlag mit Begründung. Oder: Keine.]

### Offene Punkte
[Was nicht fertig ist, was als Nächstes zu tun ist und offene Risiken, soweit erkennbar. Oder: Keine.]

### Rückfragen und Folgeentscheidungen
[Nummeriert. Je Frage: blockierend oder zu klären, betroffene Datei oder Spezifikation, Frage. Oder: Keine.]

### Änderungsbedarf an bestehenden Dateien
[Nur Vorschläge für Dateien außerhalb des eigenen Bereichs. Der Agent hat dort nichts geändert. Oder: Keine.]

### Testergebnisse
[Ausgeführte Tests und ihr Ergebnis. Oder: Keine Tests ausgeführt, mit Begründung.]

### Selbstprüfung
[Ergebnis der Prüfliste aus der eigenen Rollenanweisung. Enthält sie keine, prüft der Agent gegen die Grundregeln und die Arbeitsaufträge dieser README und nennt, was er geprüft hat.]
```

Kein Abschnitt bleibt leer. Gibt es nichts zu berichten, steht dort ausdrücklich „Keine“. Solange der Status *laufend* ist, darf ein noch nicht bearbeiteter Abschnitt „Noch offen“ lauten. Bei Status *abgeschlossen* ist das nicht zulässig.

Übergabe. Status und „Erledigt“ (aktueller Stand), „Offene Punkte“ (nächster Schritt und offene Risiken), „Rückfragen und Folgeentscheidungen“ (blockierende Rückfragen) und „Annahmen und Vorschläge“ (getroffene Annahmen) bilden zusammen die Übergabe an die nächste Sitzung. Beim Abschließen prüft der Agent, ob diese Abschnitte ausreichen, damit die nächste Sitzung ohne nicht dokumentierten Kontext arbeiten kann.

### 6. Berichtsformat B (Sitzungsbericht, ausschließlich für QA)

Der QA-Agent verwendet für jeden Sitzungsbericht, ob Prüfung oder Testerstellung, ausschließlich dieses Format. Kein anderer Agent darf Format B verwenden. QA berichtet unabhängig: Der QA-Agent beschreibt Abweichungen, korrigiert sie aber nicht und ändert keine Spezifikationen.

```markdown
## JJJJ-MM-TT_HH-MM_qa_absicht

**Status:** laufend | abgeschlossen | abgebrochen
**Arbeitsauftrag (Wortlaut):** [Wortlaut des Arbeitsauftrags]
**Prüfgegenstand:** [Spezifikationen mit Version, geprüfter Branch und Stand der Implementierung; bei Testerstellung die Spezifikationen, aus denen die Tests abgeleitet wurden]
**Abbruchgrund und nächster Schritt:** [nur bei Status abgebrochen, sonst „Entfällt“]

### Prüfumfang
[Was wurde geprüft: Spezifikationen, Abnahmebeispiele, Berechtigungen, Fehlerfälle, Zustandsübergänge, gleichzeitige Anfragen, Hauptablauf, bei Beauftragung die Konsistenz der Interpretation zwischen Backend und Frontend. Was wurde ausdrücklich nicht geprüft.]

### Testergebnisse
| Test | Bezug (Spezifikation, Abnahmebeispiel) | Erwartet | Tatsächlich | Ergebnis |
|---|---|---|---|---|

Ergebnis: bestanden | nicht bestanden | nicht ausführbar

### Abweichungen
[Nummeriert. Je Abweichung: Bezug, Schweregrad (kritisch | hoch | mittel | niedrig), erwartetes und tatsächliches Verhalten, Schritte zur Reproduktion. Oder: Keine.]

### Widersprüche und Lücken in den Spezifikationen
[Unklare, widersprüchliche oder fehlende Anforderungen. Sie werden berichtet, nicht gelöst; ein Korrekturvorschlag ist zulässig. Oder: Keine.]

### Offene Risiken und Prüflücken
[Was nicht prüfbar war oder unsicher bleibt. Oder: Keine.]

### Einschätzung zur Abnahme
[Empfehlung: abnahmefähig | bedingt abnahmefähig | nicht abnahmefähig, mit Begründung. Die Freigabe entscheidet der Projektinhaber.]

### Rückfragen
[Nummeriert. Je Frage: blockierend oder zu klären, betroffene Datei oder Spezifikation, Frage. Hier stehen auch Vorschläge für Einträge in docs/decisions.md. Oder: Keine.]
```

Auch bei Format B bleibt kein Abschnitt leer. Es gelten die Regeln zum Fortschreiben, zum Abschließen und zum Abbruch aus Abschnitt 4.

Übergabe. Die Abschnitte „Abweichungen“, „Offene Risiken und Prüflücken“ und „Rückfragen“ bilden zusammen die Übergabe an die nächste Sitzung. Beim Abschließen prüft QA, ob diese Abschnitte ausreichen, damit die nächste Sitzung ohne nicht dokumentierten Kontext arbeiten kann.

### 7. Berichtsformat C (Abschlussbericht, ausschließlich für den Product Manager)

Der Abschlussbericht ist ein eigenes Dokument und ersetzt keinen Sitzungsbericht. Der Product Manager schreibt ihn nur im Arbeitsauftrag, nachdem der Projektinhaber eine Phase für beendet erklärt hat. Er liegt unter `reports/abschlussberichte/` und trägt die Berichtskennung als Dateinamen. Die Sitzung, in der er entsteht, wird zusätzlich in Format A in der Berichtsdatei des Product Managers festgehalten.

Der Abschlussbericht stützt sich ausschließlich auf Dateien in `main`: Spezifikationen, Entscheidungen und Berichte. Jede Aussage zum Ergebnis verweist auf ihren Beleg. Testergebnisse übernimmt er aus den Berichten von QA und stellt keine eigenen auf. Er trifft keine Produktentscheidungen. Kurzfassung und Abschnitt 4 sind so geschrieben, dass sie ohne den Rest für eine Vorführung genutzt werden können. Der Vision-Check und die Lessons Learned stützen sich ausschließlich auf Dateien in `main` und auf die Prozess-Retro des Assistenten; eigene Erhebungen führt der Product Manager nicht durch.

```markdown
# Abschlussbericht: [Phase oder Projekt]

**Berichtskennung:** JJJJ-MM-TT_HH-MM_product-manager_abschlussbericht-[phase]
**Phase:** [Name oder Nummer]
**Zeitraum:** [von – bis]
**Stand:** [Commit auf main, Versionen der Spezifikationen]
**Arbeitsauftrag (Wortlaut):** [Wortlaut des Arbeitsauftrags]
**Status:** Entwurf | abgenommen

## 1. Kurzfassung
[Höchstens fünf Sätze: Ziel, Ergebnis, Qualität, wichtigste offene Punkte, Empfehlung.]

## 2. Ziel und Ausgangslage
[Was die Phase erreichen sollte und wovon sie ausging.]

## 3. Ergebnis gegen Umfang und Erfolgskriterien
| Anforderung oder Erfolgskriterium | Quelle | Ergebnis (erfüllt / teilweise / nicht erfüllt) | Beleg |
|---|---|---|---|

## 4. Vorführung
[Zielgruppe, Voraussetzungen, Ablauf in Schritten mit erwartetem Ergebnis je Schritt, bekannte Einschränkungen. Für den Betrieb Verweis auf docs/architecture.md.]

## 5. Qualität und Prüfstand
[Ergebnisse der Abnahmetests laut QA-Berichten, Abweichungen, offene Risiken.]

## 6. Vision-Check
[Prüfung, ob Produktrahmen, Spezifikationen und Architektur noch zueinander passen. Abweichungen mit Beleg. Der Product Manager entscheidet nicht, er meldet und schlägt vor.]

## 7. Entscheidungen der Phase
[Verweise auf die Einträge in docs/decisions.md.]

## 8. Lessons Learned
[Was hat sich bewährt? Was hat nicht funktioniert? Was sollte die nächste Phase anders machen? Quellen: Berichte der Phase und die Prozess-Retro des Assistenten. Der Product Manager leitet ab, entscheidet nicht.]

## 9. Offene Punkte und Rückfragen
[Nummeriert. Oder: Keine.]

## 10. Übergang in die nächste Phase
[Empfohlener Umfang und Reihenfolge, Voraussetzungen, nötige Entscheidungen und Freigaben, Vorschlag für Arbeitsaufträge je Rolle.]

## 11. Quellen
[Berichtskennungen, Spezifikationen mit Version, Commit.]

## 12. Abnahme durch den Projektinhaber
[Vom Projektinhaber auszufüllen: abgenommen | bedingt abgenommen | nicht abgenommen, Datum, Auflagen.]
```

### 8. Änderungen am Berichtswesen

Ablage, Benennung und alle Berichtsformate ändert nur der Projektinhaber.

## Begriffe

### Allgemeine Begriffe

| Begriff | Bedeutung |
|---|---|
| Projektinhaber | Person, die das Projekt steuert, Arbeitsaufträge erteilt, Produktentscheidungen trifft und Freigaben erteilt |
| Agent | KI-gestützte Rolle, die Aufgaben in einem festgelegten Bereich ausführt; hat kein Gedächtnis an frühere Sitzungen, was er wissen muss, steht im Repository |
| Rolle | Aufgabe, Rechte und Grenzen eines Beteiligten, beschrieben in dieser README und, für Agenten, in der Rollenanweisung |
| Rollenanweisung | Datei in `agents/`, die Aufgabe, Rechte, Grenzen und Prüfliste einer Rolle beschreibt; ändert nur der Projektinhaber |
| Arbeitsauftrag | Anweisung des Projektinhabers an genau einen Agenten, eine bestimmte Aufgabe auszuführen (siehe „Arbeitsaufträge“) |
| Definition of Session Done | Festlegung im Arbeitsauftrag, wann eine Sitzung als abgeschlossen gilt; enthält erwartetes Ergebnis, Akzeptanzkriterien, erforderliche Tests, PR-Anforderung |
| Sitzung | Zusammenhängender Arbeitsabschnitt eines Agenten von Beginn bis zu Abschluss oder Abbruch |
| Phase | Abgegrenzter Abschnitt des Projekts mit eigenem Umfang und Ziel, den der Projektinhaber festlegt und für beendet erklärt |
| Spezifikation | Dokument, das festlegt, was gebaut wird (Verhalten, Umfang, Grenzen), ohne vorzuschreiben, wie |
| Produktrahmen | Spezifikation, die Umfang, Nicht-Ziele, Rollen, Querschnittsregeln und Erfolgskriterien des Produkts festlegt |
| Schnittstellenspezifikation | Spezifikation, die das Verhalten einer Schnittstelle einschließlich Eingaben, Ausgaben, Fehlerfällen und Zustandsänderungen beschreibt |
| Entwurf | Status eines Dokuments, das noch nicht freigegeben ist |
| Freigabe | Ausdrückliche Zustimmung des Projektinhabers zur verbindlichen Verwendung eines Entwurfs oder einer Änderung |
| Abnahmetest | Reproduzierbarer Test, mit dem QA überprüft, ob eine Anforderung erfüllt ist |
| Agenten-Branch | Fester Branch `agent/<rolle>`, auf dem ein Agent schreibt |
| Pull Request | Vorschlag, die Änderungen eines Branches nach `main` zu übernehmen; nur der Projektinhaber führt ihn zusammen |
| Bericht | Eintrag eines Agenten in seiner Berichtsdatei, der eine Sitzung dokumentiert |
| Berichtsdatei | Die einem Agenten zugewiesene Datei in `reports/`, in der er seine Berichte hinterlegt |
| Berichtskennung | Name eines Berichts nach dem Schema `Datum_Zeit_Verfasser_Absicht` |
| Format A | Sitzungsberichtsformat für alle Agenten außer QA |
| Format B | Sitzungsberichtsformat ausschließlich für QA |
| Format C | Format des Abschlussberichts, ausschließlich für den Product Manager |
| Abschlussbericht | Dokument des Product Managers am Ende einer Phase; Vorlage für die Vorführung und Grundlage der nächsten Phase |
| Übergabe-Minimum | Mindeststandard für Berichte: aktueller Stand, nächster konkreter Schritt, blockierende Rückfragen, Annahmen, offene Risiken |
| Prozess-Retro | Prüfung am Phasenende, ob der Prozess selbst funktioniert; durchgeführt vom Assistenten |

### Projektspezifische Begriffe (FahrFlow)

| Begriff | Bedeutung |
|---|---|
| Überführungsauftrag | Auftrag, ein Fahrzeug von einer Adresse zu einer anderen zu fahren; kein Arbeitsauftrag |
| Auftraggeber | Benutzerrolle, die Überführungsaufträge anlegt und die eigenen Überführungsaufträge einsehen darf |
| Disposition | Benutzerrolle, die Überführungsaufträge anlegt und alle einsehen darf |
| Fahrer | Benutzerrolle, die offene Überführungsaufträge annehmen und zugewiesene durchführen darf |
| Auftragsstatus | Zustand eines Überführungsauftrags; zulässige Werte und Übergänge stehen ausschließlich in `specs/status.md` |
| Hauptablauf | Der in `specs/product.md` beschriebene Durchlauf eines Überführungsauftrags vom Anlegen bis zum Abschluss |
| Projektzeitzone | Europe/Berlin |
