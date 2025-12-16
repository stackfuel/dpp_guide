# Data Science Projektleitfaden

<!-- ## Inhaltsverzeichnis
1. [Einführung](#einführung)
2. [Projekterstellung und -struktur](#projekterstellung-und--struktur)
3. [Versionskontrolle mit Git und GitHub](#versionskontrolle-mit-git-und-github)
4. [Pakete und Abhängigkeiten mit UV verwalten](#pakete-und-abhängigkeiten-mit-uv-verwalten)
5. [Jupyter Notebooks vs. Python Skripte](#jupyter-notebooks-vs-python-skripte)
6. [Zusammenarbeit in Gruppen](#zusammenarbeit-in-gruppen)
7. [Best Practices für Data Science Projekte](#best-practices-für-data-science-projekte)
8. [Häufige Herausforderungen und Lösungen](#häufige-herausforderungen-und-lösungen)
9. [Nächste Schritte](#nächste-schritte) -->

## Einführung

Herzlich willkommen zum letzten Teil unserer Leitfadenreihe für den Projekt-Portfolio Kurs bei StackFuel! Nachdem du dich bereits mit VSCode, dem Terminal, dem Paketmanager UV und Git vertraut gemacht hast, geht es in diesem Leitfaden darum, all dieses Wissen zusammenzuführen und ein vollständiges Data Science Projekt aufzusetzen.

Ob du alleine oder in einer Gruppe arbeitest, ob du einen öffentlich verfügbaren Datensatz verwendest oder eigene Daten analysierst – dieser Leitfaden wird dir helfen, dein Projekt professionell zu strukturieren und zu verwalten, damit du dich auf das Wesentliche konzentrieren kannst: die Datenanalyse und die Erkenntnisse, die du daraus gewinnst.

## Projekterstellung und -struktur

### Projekt mit UV initialisieren

Der erste Schritt bei jedem neuen Projekt ist die Erstellung einer isolierten Python-Umgebung (virtual environment). Mit UV geht das besonders einfach:

1. Erstelle zunächst einen neuen Projektordner und öffne diesen mit VSCode

2. Initialisiere eine neue virtuelle Umgebung mit UV indem du im eingbauten Terminal von VSCode folgenden Befehl ausführst:

```bash
uv init
```

Dieser Befehl legt eine Reihe von Dateien und Ordner in deinem Projektverzeichnis an. Schaue in den [UV Guide](uv_guide.md) um mehr über die Funktionsweise von UV zu erfahren.

### Eine sinnvolle Projektstruktur erstellen

Eine gut durchdachte Ordnerstruktur hilft dir dabei, den Überblick zu behalten und macht es anderen leichter, deinen Code zu verstehen. Hier ist eine bewährte Struktur für Data Science Projekte:

```
mein-data-science-projekt/
│
├── .venv/                 # Virtuelle Umgebung (wird automatisch von UV erstellt)
│
├── data/                  # Alle Datendateien
│   ├── raw/               # Rohdaten (unverändert)
│   ├── processed/         # Bereinigte und vorverarbeitete Daten
│   └── external/          # Externe Datenquellen (optional)
│
├── notebooks/             # Jupyter Notebooks für Exploration und Präsentation
│
├── src/                   # Quellcode für die Verwendung im Projekt
│   ├── __init__.py        # Macht src zu einem Python-Paket
│   ├── data/              # Skripte zum Herunterladen oder Generieren von Daten
│   ├── features/          # Skripte zur Feature-Erstellung/-Transformation
│   ├── models/            # Skripte zum Trainieren und Verwenden von Modellen
│   └── visualization/     # Skripte zur Visualisierung
│
├── tests/                 # Testcode für src
│
├── .gitignore             # Gibt an, welche Dateien nicht unter Versionskontrolle stehen
├── pyproject.toml         # Wird von UV erstellt und enthält Projektabhängigkeiten
├── README.md              # Projektbeschreibung und Nutzungsanleitung
├── .env                   # optional für Umgebungsvariablen (z.B. API-Keys, Passwörter, sollten nicht ins Repo)
└── setup.py               # Falls du eine Installation deines Pakets ermöglichen möchtest
```

Du kannst diese Struktur direkt über VSCode erstellen, indem du die Ordner und Dateien manuell anlegst. 

Diese Struktur ist flexibel – passe sie an die Bedürfnisse deines spezifischen Projekts an. Für kleine Projekte ist möglicherweise eine vereinfachte Version ausreichend.

## Versionskontrolle mit Git und GitHub

### .gitignore richtig einrichten

Die `.gitignore`-Datei ist entscheidend, um zu verhindern, dass unnötige oder sensible Dateien ins Repository gelangen. Hier kannst du beliebige Dateien und Ordner angeben, die Git ignorieren soll. Dies ist besonders wichtig für große Dateien, temporäre Dateien oder Umgebungsdateien.
Hier ist ein Beispiel für eine gute `.gitignore`-Datei für Data Science Projekte. Du musst nicht alle Einträge verstehen, aber sie geben dir eine Vorstellung davon, was du ignorieren solltest:

```
# Virtuelle Umgebung
.venv/
venv/
ENV/

# Byte-kompilierte / optimierte / DLL-Dateien
__pycache__/
*.py[cod]
*$py.class
*.so

# Distribution / Packaging
dist/
build/
*.egg-info/

# Jupyter Notebook
.ipynb_checkpoints

# Daten (optional, je nach Projektanforderungen)
data/raw/
data/processed/

# Modelle (können groß sein)
*.pkl
*.h5
*.joblib

# Logs
logs/
*.log

# Environment-spezifische Dateien
.env
.env.local
*.env

# IDE-spezifische Dateien
.idea/
.vscode/
*.swp
*.swo

# Betriebssystem-spezifische Dateien
.DS_Store
Thumbs.db
```

**Wichtig:** Die Entscheidung, ob du Daten und Modelle in das Repository aufnehmen möchtest, hängt von verschiedenen Faktoren ab:

- **Datengröße**: Git ist nicht für große Dateien optimiert. Dateien über 100MB sollten normalerweise nicht ins Repository.
- **Datenschutz**: Sensible oder private Daten sollten nie in ein öffentliches Repository.

Empfehlung: Erstelle Skripte, die deine Daten herunterladen oder generieren, anstatt die Rohdaten selbst zu speichern. Ein Beispiel für ein solches Script findest du in unserem [Referenzprojekt](https://github.com/stackfuel/DPP-Referenzprojekt).

## Pakete und Abhängigkeiten mit UV verwalten

UV vereinfacht die Installation und Verwaltung von Python-Paketen für dein Projekt erheblich. Hier sind die wichtigsten Befehle:

### Pakete installieren

Um ein neues Paket zu installieren und zur `pyproject.toml` hinzuzufügen:

```bash
uv add ipykernel pandas numpy matplotlib scikit-learn
```

Dieser Befehl installiert die angegebenen Pakete und aktualisiert automatisch deine `pyproject.toml`-Datei.

### Nützliche Data Science Bibliotheken

Hier ist eine Liste der gängigsten Bibliotheken für Data Science Projekte:

1. **Datenmanipulation und -analyse**:
   - `pandas`: Für Datenverarbeitung und -analyse
   - `numpy`: Für numerische Berechnungen

2. **Datenvisualisierung**:
   - `matplotlib`: Grundlegende Visualisierungen
   - `seaborn`: Statistik-Visualisierungen auf Basis von matplotlib
   - `plotly`: Interaktive Grafiken
   - `bokeh`: Interaktive Web-Visualisierungen

3. **Machine Learning**:
   - `scikit-learn`: Für klassische ML-Algorithmen
   - `tensorflow` oder `pytorch`: Für Deep Learning
   - `xgboost` oder `lightgbm`: Für Gradient Boosting

4. **Datenzugriff und -speicherung**:
   - `sqlalchemy`: Allgemeine SQL-Datenbankinteraktion
   - `duckdb`: Moderne SQL-Datenbank für Analytics
   - `pymongo`: MongoDB-Zugriff
   - `pyarrow` oder `fastparquet`: Parquet-Dateiformate

5. **Statistik und wissenschaftliche Berechnungen**:
   - `scipy`: Wissenschaftliche Berechnungen
   - `statsmodels`: Statistische Modelle und Tests

6. **Projektunterstützung**:
   - `jupyter`: Für Notebooks inklusive Jupyter Server
   - `ipykernel`: Für Jupyter Notebooks in VSCode
   - `ipywidgets`: Für interaktive Elemente in Notebooks
   - `pytest`: Für Testautomatisierung
   - `black` und `ruff`: Für Code-Formatierung und Linting

Du wirst nur einen kleinen Teil dieser Pakete in deinem Projekt benötigen. Installiere nur die Pakete, die du tatsächlich verwendest, um die Größe deines Projekts zu minimieren.

### Abhängigkeiten synchronisieren

Wenn du mit anderen zusammenarbeitest, ist es wichtig, dass alle Teammitglieder dieselben Pakete und Versionen verwenden.

- Installiere Pakete immer mit `uv add`, damit sie in der `pyproject.toml`-Datei gespeichert werden. Du findest im Internet oft Beispiele, wie du Pakete mit `pip` installierst. Diese werden nicht in der `pyproject.toml` gespeichert und sind daher nicht reproduzierbar.
- Wenn du neue Pakete installiert hast und deine `pyproject.toml`-Datei aktualisiert wurde, erstelle einen Commit zu dieser Änderung, pushe dein Projekt auf GitHub und teile dies deinem Team mit, damit sie ihre Umgebung synchronisieren können.
- Teammitglieder können ihre Umgebung mit dem folgenden Befehl synchronisieren:

```bash
uv sync
```

Dieser Befehl installiert alle Pakete, die in der `pyproject.toml`-Datei aufgeführt sind, und stellt sicher, dass alle Teammitglieder dieselben Versionen verwenden.

## Jupyter Notebooks vs. Python Skripte

Du bist mit der Arbeit an Jupyter Notebooks bereits aus unseren Trainings im DataLab vertraut. In der Softwareentwicklung und auch in der Data Science wird darüber hinaus mit *normalen* Python Scripten gearbeitet. Dies sind einfache Textdateien mit der Endung `.py` (Jupyter Notebooks haben die Endung `.ipynb`). Python Scripte können direkt vom Python Interpreter ausgeführt werden während für Jupyter Notebooks ein sogenannter **Kernel** installiert werden muss.

### Notebooks vs. Scripte

Jupyter Notebooks und Python-Skripte haben unterschiedliche Anwendungsbereiche und Vorteile. Hier ist ein Überblick, wann welches Format sinnvoll ist:

**Jupyter Notebooks eignen sich besonders für:**

- **Explorative Datenanalyse**: Wenn du Daten untersuchen und visualisieren möchtest, sind Notebooks ideal, da du Code und Ergebnisse direkt nebeneinander siehst.
- **Dokumentation**: Durch die Kombination von Markdown-Text und Code kannst du deine Analyse gut dokumentieren.
- **Präsentationen**: Notebooks eignen sich hervorragend, um Analysen und Ergebnisse zu präsentieren.
- **Lernen und Unterrichten**: Die interaktive Natur von Notebooks macht sie ideal für Lernzwecke.
- **Prototyping**: Schnelles Testen von Ideen und Konzepten.

**Python-Skripte (.py) sind besser geeignet für:**

- **Produktionscode**: Skripte lassen sich leichter in Produktionssysteme integrieren.
- **Wiederverwendbare Module**: Wenn du Code schreiben möchtest, der in anderen Projekten oder Scripten verwendet werden soll.
- **Größere Projekte**: Bei umfangreichen Projekten mit mehreren Dateien ist eine strukturierte Organisation mit Skripten übersichtlicher.
- **Performance**: Skripte werden in der Regel effizienter ausgeführt als Notebooks.
- **Versionskontrolle**: Python-Skripte sind einfacher mit Git zu verfolgen, da sie reiner Text sind.
- **Automatisierung**: Für regelmäßig laufende Tasks oder Batch-Verarbeitungen.

Für dein Projekt-Portfolio empfehlen wir einen hybriden Ansatz: Verwende Notebooks für die Exploration und Analyse deiner Daten und refaktoriere dann den Code in strukturierte Python-Module, wenn du eine wiederverwendbare Lösung erstellen möchtest.

### Wichtig: Notebook-Outputs vor dem Commit bereinigen

Wenn du Jupyter Notebooks mit Git versionierst, ist es wichtig, die Ausgaben vor dem Commit zu bereinigen. Hier sind die Gründe dafür:

1. **Dateigröße**: Notebooks mit vielen oder großen Ausgaben (besonders Grafiken) können das Repository unnötig aufblähen da die outputs mit in die Notebook-Datei geschrieben werden.
2. **Versionskontrolle**: Änderungen in den Ausgaben erschweren es, die tatsächlichen Codeänderungen zu erkennen.
3. **Saubere Diff-Ansicht**: Ohne Ausgaben sind die Unterschiede zwischen Versionen klarer erkennbar.

Es gibt mehrere Möglichkeiten, Notebook-Ausgaben zu bereinigen:

**Manuell in VSCode:**
1. Öffne das Notebook in VSCode
2. Klicke auf die drei Punkte (...) in der oberen Leiste
3. Wähle "Clear All Outputs"

<!--  TODO: Zu testen
**Mit nbstripout (empfohlen):**
1. Installiere nbstripout: `uv add nbstripout`
2. Konfiguriere Git, um es automatisch zu verwenden: `nbstripout --install`

Diese Einrichtung stellt sicher, dass Ausgaben automatisch vor jedem Commit entfernt werden.
-->

## Zusammenarbeit in Gruppen

### Git-Workflow für Teams

Wenn du in einer Gruppe arbeitest, ist ein strukturierter Git-Workflow besonders wichtig. Hier ist ein einfacher, aber effektiver Workflow:
> **Hinweis:** Alle folgenden Schritte lassen sich auch direkt in VSCode über das Source Control Panel durchführen, siehe dazu [hier](https://code.visualstudio.com/docs/sourcecontrol/overview). Zur einfacheren Dokumentation verwenden wir hier die Terminal-Befehle für Git.

1. **Repository einrichten**:
   - Ein Teammitglied erstellt das Repository auf GitHub
   - Dieses Mitglied fügt alle anderen als Collaborators hinzu (unter Settings > Collaborators)
   - Jeder klont das Repository: `git clone [repository-url]`

2. **Feature-Branch-Workflow (Optional)**:
   - Erstelle für jedes Feature oder jede Aufgabe einen neuen Branch: `git checkout -b feature/datenbereinigung`
   - Arbeite an deinen Änderungen und committe regelmäßig: `git commit -m "Beschreibender Commit-Text"`
   - Synchronisiere deinen Branch mit dem Remote-Repository: `git push origin feature/datenbereinigung`
   - Wenn das Feature fertig ist, erstelle einen Pull Request auf GitHub

3. **Code Review und Merge**:
   - Ein anderes Teammitglied überprüft den Code im Pull Request
   - Nach der Genehmigung wird der Branch in den Hauptbranch (main/master) gemergt
   - Alle Teammitglieder aktualisieren ihre lokalen Repositories: `git pull origin main`

> Solltest du alleine Arbeiten oder nur ein kleines Team haben, kannst du auch direkt im `main` Branch arbeiten. In diesem Fall ist es wichtig, dass du regelmäßig deine Änderungen committest und pushst um Merge-Konflikte zu vermeiden.

### Umgebungen synchronisieren

Um sicherzustellen, dass alle Teammitglieder mit denselben Paketversionen arbeiten:

- Wenn ein Teammitglied ein neues Paket installiert: `uv add paketname`
- `pyproject.toml` pushen: `git add pyproject.toml && git commit -m "Add new dependency" && git push`
- Andere Teammitglieder synchronisieren ihre Umgebung: `uv sync`

### Zusammenarbeit an Notebooks

Bei der gemeinsamen Arbeit an Jupyter Notebooks gibt es einige Herausforderungen:

- **Notebook-Konflikte vermeiden**:
   - Teile die Arbeit klar auf (z.B. verschiedene Notebooks für verschiedene Analysen)
   - Vermeide es, gleichzeitig am selben Notebook zu arbeiten

- **Dokumentation und Kommentare**:
   - Verwende Markdown-Zellen ausgiebig, um deinen Code zu dokumentieren
   - Füge Kommentare hinzu, die anderen Teammitgliedern helfen, deinen Code zu verstehen

- **Vermeide zu große Notebooks**:
   - Halte Notebooks klein und fokussiert
   - Teile große Analysen in mehrere Notebooks auf
   - Verwende Python-Skripte für wiederverwendbaren Code und importiere diese in Notebooks

## Best Practices für Data Science Projekte

### Code-Qualität sicherstellen (Optional)

Verwende Linting-Tools, um deinen Code sauber und konsistent zu halten:

```bash
uv add black ruff
```

- `black`: Formatiert deinen Code automatisch
- `ruff`: Prüft deinen Code auf Fehler und Verbesserungsmöglichkeiten

Diese Tools kannst du in VSCode einrichten, sodass sie automatisch beim Speichern ausgeführt werden.

### Reproduzierbarkeit gewährleisten

**Random Seeds setzen**:
   ```python
   import numpy as np
   import random
   import torch
   
   # Setze Seeds für Reproduzierbarkeit
   SEED = 42
   random.seed(SEED)
   np.random.seed(SEED)
   torch.manual_seed(SEED)
   ```

**Datenpipelines dokumentieren**:
   - Speichere Zwischen- und Endversionen deiner Daten
   - Dokumentiere jeden Transformationsschritt ausführlich
   - Verwende Download Scipte für die Rohdaten und speichere die Daten in `data/raw/`
   - Verwende Scripte zum verarbeiten der Daten und speichere die verarbeiteten Daten in `data/processed/`
   - auf diese weise können andere deine Datenpipelines nachvollziehen und reproduzieren auch wenn der `data` Ordner nicht im Repository ist.



### Dokumentation pflegen

Eine gute README.md Datei ist entscheidend. Sie sollte enthalten:

- **Projekttitel und -beschreibung**
- **Installation und Setup**:
   ```
   # Installation
   git clone https://github.com/username/projektname.git
   cd projektname
   uv init
   ```
- **Nutzung**: Beispiele, wie das Projekt verwendet wird
- **Datenquellen**: Woher stammen die Daten, wie kann man sie erhalten
- **Projektstruktur**: Kurze Erklärung der Ordnerstruktur
- **Teammitglieder**: Bei Gruppenprojekten

## Nächste Schritte (Optional für fortgeschrittene)

Nachdem du dein Projekt aufgesetzt hast, stehen dir viele Wege offen:

1. **Deployment deiner Modelle**:
   - Als REST-API mit FastAPI oder Flask
   - Als Streamlit- oder Dash-Anwendung

2. **Automatisierte Tests hinzufügen**:
   - Unit-Tests mit pytest
   - Integration Tests für Datenpipelines

3. **CI/CD-Pipeline einrichten**:
   - Automatisierte Tests bei jedem Push
   - Automatisches Deployment deiner Anwendung

4. **Kennzahlen und Monitoring**:
   - MLflow für Experiment-Tracking
   - Prometheus/Grafana für Monitoring

### Fazit

Ein gut strukturiertes Projekt ist der Grundstein für erfolgreiche Data Science Arbeit. Mit den in diesem Leitfaden vorgestellten Werkzeugen und Methoden kannst du von Anfang an professionell arbeiten – egal ob allein oder im Team.

Denk daran, dass die perfekte Projektstruktur nicht existiert. Passe die Vorschläge an deine spezifischen Bedürfnisse und an die Größe deines Projekts an. Das Wichtigste ist, dass du und dein Team produktiv arbeiten können und eure Ergebnisse leicht reproduzierbar und verständlich sind.

Viel Erfolg bei deinem Data Science Projekt!
