# Visual Studio Code - Leitfaden für die Python-Entwicklung

In diesem Leitfaden zeige ich dir, wie du mit dem Code-Editor **Visual Studio Code** (VSCode) effektiv arbeiten kannst. VSCode ist ein leistungsstarker und vielseitiger Editor, der besonders für die Python-Entwicklung geeignet ist. Wir werden uns ansehen, wie du VSCode installierst, die Oberfläche navigierst, den Editor an deine Bedürfnisse anpasst und mit Python-Projekten, insbesondere unter Verwendung von UV und Jupyter Notebooks, arbeitest.

## Einführung

### Was ist Visual Studio Code?

**Visual Studio Code (VSCode)** ist ein kostenloser, plattformübergreifender Code-Editor von Microsoft. Er bietet zahlreiche Funktionen wie Code-Vervollständigung, Debugging, Git-Integration und Unterstützung für eine Vielzahl von Programmiersprachen durch Erweiterungen. Neben VSCode gibt es noch eine Vielzahl weiterer Entwicklungsumgebungen für Python, wie PyCharm, Spyder oder das aus dem DataLab bekannte JupyterLab. Grundsätzlich kannst du dein Projekt mit jedem dieser Tools aufsetzen.

### Vorteile von VSCode für die Python-Entwicklung

- **Leichtgewichtiger Editor** mit großer Funktionalität
- **IntelliSense**: intelligente Code-Vervollständigung
- **Integriertes Terminal** für die Ausführung von Befehlen (z. B. UV, Python, Git etc.)
- **Erweiterbar** durch eine Vielzahl von **Extensions** (Erweiterungen)
- **Unterstützung von Jupyter Notebooks** direkt im Editor
- **Plattformübergreifend**: verfügbar für Windows, macOS und Linux

### Download und Installation von VSCode

**Download**:

Besuche die offizielle Website von VSCode: [https://code.visualstudio.com/](https://code.visualstudio.com/) und lade die passende Version für dein Betriebssystem herunter.

**Installation auf Windows**:

- Führe die heruntergeladene `.exe`-Datei aus.
- Folge den Anweisungen des Installationsassistenten.
- Optional _empfohlen_: Aktiviere die Option **"Code zu PATH hinzufügen"**, um VSCode über die Kommandozeile zu starten.
- Optional _empfohlen_: Aktiviere die beiden Optionen **"In Code öffnen"** für das Kontextmenü.

**Installation auf macOS**:

- Öffne das heruntergeladene `.zip`-Archiv.
- Ziehe die Anwendung **Visual Studio Code** in den Ordner **Programme**.

Nachdem du VSCode installiert hast, solltest du dich mit der Oberfläche vertraut machen. Microsoft stellt dafür eine umfangreiche [Dokumentation](https://code.visualstudio.com/docs) zur Verfügung, in der alle wichtigen Features erklärt werden.

## Einrichtung

Im [Get Started](https://code.visualstudio.com/docs/getstarted/getting-started) Guide wirst du in die Grundlagen von VSCode eingeführt. Dir wird ein Überblick über das grundlegende Interface, die Einstellungen, das Arbeiten mit Source Control (Git) sowie die Erweiterung der Software mit Language Extensions (z. B. für Python) gegeben. Verschaffe dir hier einen Überblick. Du musst nicht das ganze Tutorial durcharbeiten, da du die wichtigsten Funktionen auch bei uns lernst.

### Erweiterungen

Der größte Vorteil von VSCode ist seine Erweiterbarkeit durch Extensions (Erweiterungen). Für unsere Python-Entwicklung benötigst du einige wichtige Erweiterungen, die dir die Arbeit erheblich erleichtern werden.

Um Erweiterungen zu installieren, klicke auf das Extensions-Symbol in der Activity Bar am linken Rand (oder drücke `Ctrl+Shift+X` auf Windows bzw. `Cmd+Shift+X` auf macOS).

Hier sind die empfohlenen Erweiterungen für dein Python-Projekt:

1. **Python Extension**:

   - Die offizielle Python-Erweiterung von Microsoft
   - Bietet IntelliSense, Linting, Debugging, Code-Navigation, Code-Formatierung und vieles mehr
   - Suche nach "Python" und installiere die Erweiterung von Microsoft

2. **Jupyter Extension**:

   - Ermöglicht die Arbeit mit Jupyter Notebooks direkt in VSCode
   - Unterstützt das Ausführen von Code-Zellen, das Anzeigen von Plots und die Integration mit dem Python-Interpreter
   - Suche nach "Jupyter" und installiere die Erweiterung von Microsoft

3. **Even Better TOML**:

   - Bietet Syntax-Highlighting und Unterstützung für TOML-Dateien
   - Besonders nützlich für die Arbeit mit `pyproject.toml`-Dateien, die für moderne Python-Projekte verwendet werden
   - Suche nach "Even Better TOML" und installiere die Erweiterung von tamasfe

4. **Ruff**:
   - Ein schneller Python Linter und Code-Formatter
   - Hilft dir, deinen Code sauber und nach den Python-Standards zu formatieren
   - Suche nach "Ruff" und installiere die entsprechende Erweiterung

Nach der Installation dieser Erweiterungen sollte VSCode automatisch deine Python-Umgebung erkennen (mehr dazu im [UV-Leitfaden](./uv_guide.md)) und die entsprechenden Funktionen zur Verfügung stellen. Falls du weitere Erweiterungen benötigst, kannst du jederzeit den [Extension Marketplace](https://code.visualstudio.com/docs/configure/extensions/extension-marketplace) durchsuchen.

### Terminal

Ein wichtiger Bestandteil der Arbeit mit VSCode ist das integrierte Terminal, das dir ermöglicht, Befehle direkt aus dem Editor heraus auszuführen, ohne zwischen verschiedenen Anwendungen wechseln zu müssen. Das Terminal wird im [Leitfaden zu UV](./uv_guide.md) wichtig, wenn es darum geht, mit dem Paketmanager UV zu arbeiten und Python sowie einige Pakete zu installieren. Aber auch für die Arbeit mit Git und anderen Entwicklungswerkzeugen ist das Terminal wichtig. Im [Leitfaden zum Terminal](./terminal_guide.md) werden wir uns genauer mit diesem Werkzeug beschäftigen und dir zeigen, wie du es effektiv nutzen kannst.

Hier sind einige grundlegende Funktionen und Tipps zur Verwendung des Terminals in VSCode:

**Öffnen des Terminals**:

- Drücke `Ctrl+Ö` (Windows/Linux) oder `Cmd+Ö` (macOS).
- Alternativ kannst du über das Menü "Terminal" > "New Terminal" ein neues Terminal öffnen.

**Grundlegende Terminal-Funktionen in VSCode**:

1. **Mehrere Terminals verwalten**:

   - Du kannst mehrere Terminal-Instanzen haben, zwischen denen du über das Dropdown-Menü in der Terminal-Leiste wechseln kannst.
   - Teile das Terminal-Fenster horizontal oder vertikal mit dem "Split"-Button.

2. **Terminal-Typ auswählen**:

   - In Windows kannst du zwischen PowerShell, Command Prompt und WSL wählen.
   - In macOS/Linux stehen verschiedene Shells wie Bash, Zsh oder Fish zur Verfügung.

3. **Befehle ausführen**:

   - Führe Python-Skripte aus: `python mein_skript.py`
   - Verwende UV für Paketmanagement (siehe [UV-Leitfaden](uv_guide.md))
   - Arbeite mit Git (siehe [Git-Leitfaden](git_guide.md))

4. **Terminal-Ausgabe durchsuchen**:

   - Nutze `Ctrl+F` (Windows/Linux) oder `Cmd+F` (macOS), um in der Terminal-Ausgabe zu suchen.

5. **Terminaleinstellungen anpassen**:
   - Passe Schriftart, Größe und andere Einstellungen über die VSCode-Einstellungen an.

Für eine ausführlichere Einführung in die Arbeit mit dem Terminal, lies bitte den [Terminal-Leitfaden](./terminal_guide.md), der detaillierte Informationen und Beispiele enthält.

## Tipps für effizientes Arbeiten mit VSCode

Hier sind einige zusätzliche Tipps, die dir helfen können, produktiver mit VSCode zu arbeiten:

### Tableiste

Wenn du im Explorer (Symbol mit den zwei Ordnern) eine Datei öffnest, geschieht dies in einem neuen Tab. Du kannst zwischen Tabs wechseln, indem du sie anklickst oder `Ctrl+Tab` (Windows/Linux) bzw. `Cmd+Tab` (macOS) nutzt. Dateien werden zunächst im temporären Modus geöffnet, was durch den kursiven Dateinamen erkennbar ist. Ein weiterer Dateiklick ersetzt die aktuelle Datei im Tab. Um eine Datei dauerhaft zu öffnen, klicke den Tab doppelt an.

Wenn eine Datei ungespeicherte Änderungen hat, wird ein kleiner schwarzer Kreis neben dem Dateinamen angezeigt. Du kannst die Datei speichern, indem du `Ctrl+S` (Windows/Linux) oder `Cmd+S` (macOS) drückst.

### Tastenkombinationen

**Datei- und Fenster-Management**

| Aktion                            | Windows/Linux  | MacOS         |
| --------------------------------- | -------------- | ------------- |
| **Schnelles Öffnen von Dateien**  | `Ctrl+P`       | `Cmd+P`       |
| Zwischen geöffneten Tabs wechseln | `Ctrl+Tab`     | `Cmd+Tab`     |
| Datei schließen                   | `Ctrl+W`       | `Cmd+W`       |
| Datei speichern                   | `Ctrl+S`       | `Cmd+S`       |
| Seitenleiste ein-/ausblenden      | `Ctrl+B`       | `Cmd+B`       |
| Explorer öffnen                   | `Ctrl+Shift+E` | `Cmd+Shift+E` |
| Erweiterungen öffnen              | `Ctrl+Shift+X` | `Cmd+Shift+X` |
| Git-Ansicht öffnen                | `Ctrl+Shift+G` | `Cmd+Shift+G` |
| Vollbildmodus ein-/ausschalten    | `F11`          | `Cmd+Ctrl+F`  |

**Bearbeiten**

| Aktion                                         | Windows/Linux | MacOS            |
| ---------------------------------------------- | ------------- | ---------------- |
| **Zeilen nach oben/unten verschieben**         | `Alt+Up/Down` | `Option+Up/Down` |
| **Zeile/Auswahl kommentieren/auskommentieren** | `Ctrl+/#`     | `Cmd+/#`         |
| Rückgängig machen                              | `Ctrl+Z`      | `Cmd+Z`          |
| Wiederholen                                    | `Ctrl+Y`      | `Cmd+Shift+Z`    |
| Ausschneiden, Kopieren, Einfügen               | `Ctrl+X/C/V`  | `Cmd+X/C/V`      |

**Suchen und Navigieren**

| Aktion                           | Windows/Linux  | MacOS         |
| -------------------------------- | -------------- | ------------- |
| Globale Suche                    | `Ctrl+Shift+F` | `Cmd+Shift+F` |
| Dateiweit suchen                 | `Ctrl+F`       | `Cmd+F`       |
| Zum nächsten Suchergebnis        | `F3`           | `Cmd+G`       |
| Zur vorherigen Position springen | `Ctrl+-`       | `Cmd+-`       |
| Zur nächsten Position springen   | `Ctrl+Shift+-` | `Cmd+Shift+-` |

**Allgemein**

| Aktion                       | Windows/Linux   | MacOS         |
| ---------------------------- | --------------- | ------------- |
| **Befehlspalette öffnen**    | `Ctrl+Shift+P`  | `Cmd+Shift+P` |
| Tastenkombinationen anzeigen | `Ctrl+K Ctrl+S` | `Cmd+K Cmd+S` |
| **Einstellungen öffnen**     | `Ctrl+,`        | `Cmd+,`       |

## Zusammenfassung

Visual Studio Code ist ein vielseitiger und leistungsstarker Editor, der dir alle Werkzeuge bietet, die du für die Python-Entwicklung benötigst. Mit den richtigen Erweiterungen und Einstellungen kannst du eine Umgebung schaffen, die perfekt auf deine Bedürfnisse zugeschnitten ist.

In diesem Leitfaden haben wir die grundlegende Installation und Einrichtung von VSCode für die Python-Entwicklung behandelt sowie die Arbeit mit Python-Skripten und Jupyter Notebooks. Nutze diese Grundlagen, um dein eigenes Projekt zu erstellen und damit zu experimentieren.

Für weitere Informationen zu spezifischen Themen, schau dir die anderen Leitfäden an:

- [Leitfaden für das Terminal](./terminal_guide.md)
- [Leitfaden für den Python-Paketmanager UV](./uv_guide.md)
- [Leitfaden für Git](./git_guide.md)

Viel Erfolg bei deinem Projekt-Portfolio!
