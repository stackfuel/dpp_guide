# UV-Python-Paketmanagement-Leitfaden

In diesem Leitfaden zeige ich dir, wie du UV für dein Data-Science-Projekt nutzen kannst. UV ist ein moderner und schneller Paketmanager für Python, der dir hilft, deine Projektumgebung sauber und übersichtlich zu halten.

## Was ist ein Virtual Environment?

Bei der Arbeit mit Python sind wir oft auf externe Pakete wie Pandas, Matplotlib, Scikit-Learn etc. angewiesen, die zusätzlich zu Python auf unserem System installiert werden müssen. Üblicherweise können diese Pakete mit dem in Python eingebauten Paketmanager `pip` installiert werden. Beispielsweise würde der Befehl `pip install pandas` das Paket Pandas auf unserem Rechner in einer globalen Umgebung installieren, sodass alle Python-Skripte direkt damit arbeiten können.

Wenn wir jedoch an mehreren Projekten gleichzeitig arbeiten oder unser Projekt mit anderen teilen möchten, stoßen wir schnell auf ein Problem. Die global installierten Pakete von `pip` werden in einer bestimmten Version installiert. Projekte können jedoch aufgrund ihrer Historie auf unterschiedliche Versionen der Pakete angewiesen sein. Daher ist es nicht ratsam, diese immer global zu installieren. An dieser Stelle kommen virtuelle Umgebungen oder Virtual Environments ins Spiel, bei denen Pakete in einem speziellen Ordner für jedes Projekt individuell installiert werden.

## Was ist UV?

UV ist ein Paketmanager für Python, ein kleines Hilfsprogramm, das zusätzlich zu Python installiert wird und uns bei der Arbeit mit virtuellen Umgebungen unterstützt. Mit UV können wir unsere Python-Projekte aufsetzen und beliebige Pakete für diese Projekte installieren. UV sorgt dafür, dass alle Pakete kompatibel zueinander sind und dokumentiert die verwendeten Pakete in einer eigenen Datei namens `pyproject.toml`. Dies hat den Vorteil, dass unsere Projekte sauber voneinander getrennt sind. Zudem hilft es dabei, unsere Projekte mit anderen auf GitHub zu teilen, da wir nicht alle Pakete mit unserem Projekt ausliefern müssen. Da UV die installierten Pakete in der `pyproject.toml`-Datei dokumentiert, reicht es aus, diese Datei in unserem Projekt vorzuhalten. Wenn andere nun die gleichen Pakete installieren möchten, kann UV diese automatisch in der richtigen Konfiguration installieren.

UV legt dabei einen `.venv`-Ordner in deinem Projektverzeichnis an. Dieser Ordner enthält alle installierten Pakete und die Python-Umgebung. Da dieser Ordner sehr groß werden kann und für jedes System neu erstellt werden sollte, gehört er nicht ins Git-Repository. Wir werden später noch sehen, wie wir ihn in der `.gitignore`-Datei ausschließen können.

Es gibt neben UV noch weitere Paketmanager, die für diesen Zweck genutzt werden können. `pip` ist der bekannteste von ihnen, da er mit Python geliefert wird und nicht zusätzlich installiert werden muss. Anaconda ist ebenfalls ein beliebter Paketmanager und vor allem im Bereich Data Science sehr verbreitet. Wir haben uns hier für UV entschieden, weil es deutlich moderner und schneller ist als die genannten Alternativen.

## Installation von UV

Zunächst müssen wir verstehen, dass UV ein rein terminalbasiertes Programm ist. Es bietet also keine grafische Benutzeroberfläche, sondern wird über ein sogenanntes Terminal bedient. Das bedeutet, dass wir alle Aktionen in Form von Textbefehlen ausführen müssen. Dazu kannst du unter Windows die **PowerShell** und unter macOS/Linux das **Terminal** verwenden. Solltest du noch keine Erfahrung mit dem Terminal haben, kannst du dir in unserem [Leitfaden zum Terminal](terminal_guide.md) die Grundlagen anschauen.

Je nachdem, welches Betriebssystem du verwendest, gibt es verschiedene Wege, UV zu installieren. Für eine genauere Beschreibung schaue in die [Dokumentation](https://docs.astral.sh/uv/getting-started/installation/) von UV.

Führe folgende Befehle, je nach Betriebssystem, in deinem Terminal aus.

### Windows

Windows hat einen eigenen Paketmanager für Programme namens Winget. Öffne eine PowerShell-Konsole und gib folgenden Befehl ein:

```bash
winget install --id=astral-sh.uv -e
```

Sollte das nicht funktionieren, ist Winget auf deinem System noch nicht verfügbar. Versuche alternativ folgenden Befehl:

```bash
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### macOS / Linux

Für macOS- und Linux-Systeme können wir UV über `curl` herunterladen und direkt installieren:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

---

Solltest du Probleme mit der Installation haben, schaue in die [Dokumentation](https://docs.astral.sh/uv/getting-started/installation/) oder melde dich beim Mentoring-Team von StackFuel.

Nach der Installation kannst du prüfen, ob alles geklappt hat. Starte dein Terminal/PowerShell erneut und gib den folgenden Befehl ein:

```bash
uv --version
```

Wir können in diesem Leitfaden nur die Grundlagen von UV behandeln. Falls du dich dafür interessierst, was mit UV noch alles möglich ist, lege ich dir die offizielle [Dokumentation](https://docs.astral.sh/uv/getting-started/) der Entwickler ans Herz.

<!---
TODO: uv --help
-->

## Projekt erstellen `uv init`

Lass uns ein neues Data-Science-Projekt erstellen! Lege zunächst einen neuen Ordner an und wechsle hinein:

```bash
mkdir mein-data-projekt
cd mein-data-projekt
```

Jetzt initialisieren wir das Projekt mit UV:

```bash
uv init
```

**Wichtige Parameter für `uv init`:**

- `--python`: Legt die Python-Version fest, z. B. `uv init --python=3.12`
- `--name`: Setzt den Projektnamen, z. B. `uv init --name="mein-data-projekt"`

UV hat jetzt ein neues Projekt in unserem Ordner angelegt und dabei einige Dateien und Ordner erstellt.

Zunächst wurden die Dateien `.git` `.gitignore`, `.python-version`, `main.py`, `pyproject.toml`, und `README.md` angelegt. Falls du die Ordner mit einem vorangestellen Punkt nicht sehen kannst, musst du in deinem Dateiexplorer versteckte Elemente einblenden. Das ist unter Windows und macOS unterschiedlich. In der Regel findest du diese Option im Menü "Ansicht" oder "Darstellung".

Ich gehe gleich auf die einzelnen Dateien ein aber noch ist die Arbeit nicht ganz erledigt. UV hat noch keinen virtuelles Environment angelegt da wir es bislang noch nicht benutzt haben. 

Lass uns zunächst versuchen die von UV erstellte `main.py` auszuführen. Dazu führe fogenden Befehl aus:

```bash
uv run main.py
```

Wenn alles geklappt hat sollte eine Ausgabe wie diese erscheinen:

```
Hello from mein-data-projekt!
```

Zusätzlich hat UV einen Ordner `.venv` sowie die Datei `uv.lock` angelegt. Lass uns nun die wichtigsten Dateien und Ordner durchgehen.


**`pyproject.toml`**: Dies ist deine Projekt-Konfigurationsdatei. Sie sieht etwa so aus:

```toml
[project]
name = "mein-data-projekt"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.12"
dependencies = []
```

In dieser Datei werden wichtige Informationen zu unserem Projekt abgelegt. Programme wie UV nutzen diese Datei, um Einstellungen für das Projekt zu verwalten. Wenn du dich dafür interessierst, wie diese Datei aufgebaut ist und funktioniert, kannst du gerne einen Blick in den offiziellen [Python Packaging Guide](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/) werfen. Für den Anfang musst du aber nur wissen, dass UV hier einige Metadaten für unser Projekt angelegt hat und unter dem Punkt `dependencies` die Namen der benötigten Pakete für unser Projekt hinterlegen wird.

Fühl dich frei, die Datei zu bearbeiten und den Projektnamen sowie die Beschreibung zu ändern. Das ist wichtig, wenn du dein Projekt später auf GitHub veröffentlichen möchtest. Wenn du das Projekt mit anderen teilst, wird diese Datei automatisch mit dem Projekt ausgeliefert.


**`.python-version`**: Enthält die Python-Version für dein Projekt, z. B.:

```
3.12
```

**`uv.lock`**: Diese Datei speichert die exakten Versionen aller installierten Pakete. UV wird versuchen, diese stets mit der `pyproject.toml` und den tatsächlich installierten Paketen im `.venv`-Ordner synchron zu halten.

Darüber hinaus hat UV wahrscheinlich die Dateien `README.md`, `hello.py`, `.gitignore` sowie ein Git-Repository im Ordner `.git` angelegt. Falls du die letzten beiden nicht finden kannst, musst du vermutlich in deinem Dateiexplorer versteckte Elemente einblenden. Die `README.md` dient dazu, dein Projekt zu beschreiben und zu dokumentieren. Diese Datei wird unter GitHub standardmäßig auf der Startseite deines Projekts angezeigt. Die `hello.py`-Datei kannst du zum Testen deines Setups verwenden. Falls du mit dem `.git`-Ordner oder der `.gitignore`-Datei nichts anfangen kannst, schau dir unseren [Git-Leitfaden](git_guide.md) an.


Zudem hat UV einen Ordner `.venv` angelegt. Dies ist das virtuelle Environment, in dem alle Pakete für dein Projekt installiert werden. UV wird versuchen diesen Ordner immer mit der `pyproject.toml`-Datei und der `uv.lock`-Datei zu synchronisieren wenn du änderungen am Environment vornimmst. Du kanns diesen vorgang auch mit dem Befehl `uv sync` manuell anstoßen. Wir werden später noch darauf eingehen.


## Pakete installieren `uv add`

Für ein Data-Science-Projekt brauchst du typischerweise einige Bibliotheken. Um mit Jupyter Notebooks zu arbeiten, kannst du das Paket `jupyter` installieren. Dieses bietet dir den Jupyter-Kernel, der für die Ausführung der Zellen im Notebook zuständig ist, und den Jupyter-Server, der eine einfache webbasierte Benutzeroberfläche für einen Internetbrowser bietet. Du kennst den Jupyter-Server wahrscheinlich schon in Form des DataLabs von StackFuel. Wenn du deine Notebooks mit VSCode bearbeiten möchtest, reicht es aus, wenn du nur das Paket `ipykernel` installierst, da VSCode selbst die Benutzeroberfläche darstellt.

Darüber hinaus können wir einige Bibliotheken gebrauchen, die du bereits aus unseren Trainings kennst. Zu nennen wären hier `pandas`, `matplotlib`, `seaborn`, `scikit-learn` etc.

Um ein Paket mit UV zu installieren, kannst du den Befehl `uv add` gefolgt von einem oder mehreren Paketnamen verwenden.

```bash
uv add ipykernel pandas matplotlib
```

Nach diesem Befehl hat sich deine `pyproject.toml` verändert:

```toml
[project]
name = "mein-data-projekt"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.12"
dependencies = [
    "ipykernel>=6.29.5",
    "matplotlib>=3.10.1",
    "pandas>=2.2.3",
]
```

**Hinweis:** Die oben stehenden Versionsnummern können in deinem Fall vom Beispiel abweichen. Das liegt daran, dass UV stets versucht, die aktuellsten Versionen der Pakete zu installieren, und diese regelmäßig aktualisiert und weiterentwickelt werden.

In der `pyproject.toml` finden wir die Pakete, welche wir explizit durch `uv add` als Abhängigkeit für unser Projekt definiert haben. Damit ist klar, dass unser Projekt auf diesen Bibliotheken aufbaut und jeder, der unser Projekt selbst ausführen möchte, diese Pakete installiert haben muss. Allerdings haben diese Pakete selbst ebenfalls Abhängigkeiten von anderen Paketen, die wir nicht explizit angegeben haben. So sind die Pakete `pandas` und `matplotlib` beispielsweise von `numpy` abhängig. UV installiert diese zusätzlichen Abhängigkeiten automatisch für uns mit und dokumentiert alle installierten Pakete in der `uv.lock`-Datei. UV hat also `numpy` ebenfalls installiert, und wir können dieses Paket in unseren Notebooks verwenden. Allerdings sollten wir, falls wir `numpy` explizit in unserem Quellcode verwenden, dieses auch in unserer `pyproject.toml`-Datei auflisten bzw. mit `uv add` hinzufügen und uns nicht darauf verlassen, dass es durch `pandas` oder `matplotlib` installiert wird.


Du kannst nun in VSCode dein erstes Notebook, z. B. `test.ipynb`, anlegen. Nachdem du diese Datei geöffnet hast, solltest du als Erstes den Kernel oben rechts in der Ecke definieren. Hier wähle einfach das `.venv` aus, welches UV gerade für uns angelegt hat. Mehr dazu in unserem [Projekt Guide](project_guide.md).

## Pakete entfernen `uv remove`

Wenn du versehentlich ein Paket installiert hast, welches du nicht benötigst, kannst du dieses mit dem Befehl `uv remove` wieder deinstallieren. UV wird es dann aus der `pyproject.toml`-Datei entfernen und das Paket inklusive aller Abhängigkeiten, die nicht von anderen Paketen verwendet werden, löschen.

```bash
uv remove matplotlib
```

## Virtuelle Umgebung synchronisieren `uv sync`

Wir haben gesehen, dass UV die Bibliotheken, die wir über `uv add` installieren, in der `pyproject.toml` sowie der `uv.lock`-Datei einträgt. Aber was, wenn wir uns das Projekt frisch von GitHub geklont haben und nun das Environment komplett neu aufsetzen wollen? In diesem Fall sind die Bibliotheken bereits in der `pyproject.toml` und `uv.lock` eingetragen, allerdings noch nicht installiert. Für diesen Fall gibt es den Befehl `uv sync`. Mit diesem Befehl versucht UV, die entsprechenden Dateien und das Environment zu synchronisieren. Das bedeutet, alles, was in der `pyproject.toml`-Datei steht, aber noch nicht im Environment existiert, wird nachinstalliert.

Dieser Befehl ist immer dann wichtig, wenn das Environment von jemand anderem geändert wurde. Stell dir vor, ein Kollege arbeitet gerade an einem neuen Feature und braucht dafür eine Bibliothek, welche noch nicht Teil des Environments ist. Er installiert dieses Paket bei sich durch `uv add`, und UV aktualisiert seine Version der `pyproject.toml`-Datei. Wenn er fertig ist, pusht er seinen neuen Code zusammen mit der aktualisierten `pyproject.toml` auf GitHub. Wenn du dir nun das Projekt pullst, wirst du ein Paket in deiner `pyproject.toml` haben, welches nicht Teil deines Environments ist, da das Environment selbst nicht Teil des Git-Repositorys ist. In dieser Situation kannst du einfach `uv sync` im Terminal eingeben, und UV kümmert sich darum, dass alles korrekt installiert wird.

**`uv add`:**

- Fügt neue Pakete hinzu und aktualisiert `pyproject.toml`
- Installiert die Pakete direkt

**`uv sync`:**

- Synchronisiert das virtuelle Environment mit `pyproject.toml`
- Nützlich, wenn du das Projekt frisch geklont oder gepullt hast

**Tipp:** Führe `uv sync` aus, wenn deine Teammitglieder neue Pakete hinzugefügt haben und du die Änderungen übernehmen möchtest.

## Code ausführen `uv run`

Wir haben nun ein Environment und können dort Pakete installieren und unseren Programmcode schreiben. Doch was, wenn wir diesen Code nun ausführen wollen? Üblicherweise rufen wir im Terminal das Programm `python` bzw. unter Linux `python3` auf und übergeben dem Programm unser Skript zur Ausführung.

```bash
python hello.py
```

Allerdings bekommen wir hier ein Problem. Unser virtuelles Environment ist unserem Betriebssystem nicht bekannt. Es wird versuchen, eine global installierte Python-Version auf dem System zu finden und diese auszuführen. Diese Version wird aber nicht mit den Bibliotheken aus unserem Environment vertraut sein.

Die konventionelle Lösung für das Problem ist es, das virtuelle Environment zunächst zu "aktivieren". Im `.venv/Scripts`-Ordner (unter Windows) bzw. `.venv/bin` (unter macOS/Linux) liegen mehrere Skripte, welche für unterschiedliche Terminals vorgesehen sind. Bei der Ausführung des richtigen Skripts wird nun dem Betriebssystem die richtige Python-Version samt aller installierten Bibliotheken bekannt gemacht, sodass, solange das Environment aktiv ist, die richtige Python-Version mit `python hello.py` aufgerufen wird.

UV macht die ganze Sache ein wenig einfacher. Da UV selbst ein Programm ist, das unser Environment kennt, solange wir es im richtigen Pfad aufrufen, können wir den Befehl `uv run` für die Ausführung von Python-Code verwenden.

```bash
uv run hello.py
```

UV kümmert sich dann darum, dass die richtige Python-Version unseres Environments für die Ausführung verwendet wird.

---

Du hast nun die wichtigsten Befehle und Funktionen von UV kennengelernt, um dein Projekt aufzusetzen und `.py`-Dateien sowie Jupyter Notebooks auszuführen. UV bietet noch einige weitere Möglichkeiten, die du dir gerne bei Bedarf anschauen kannst. Dafür empfehlen wir die offizielle [Dokumentation](https://docs.astral.sh/uv/) der Entwickler.

Ich wünsche dir viel Spaß mit deinem Python-Projekt!