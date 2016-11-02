# GitTraining


Gliederung:

1. Änderungen commiten
2. Commits zurücknehmen
3. Zu alten Versionen zurückkehren
4. Branches erstellen und löschen
5. Rebase Fallbeispiel
6. Merge Fallbeispiel
7. Fehler finden und beheben
8. git push und Optionen
9. git pull und Optionen

##0.Clone des Repository

Lokale Kopie des Repositories ziehen mit:

```
git clone https://github.com/PKnittel/GitTraining.git
```


##1.Änderungen commiten


Hinzufügen der Änderungen zum Commit

```
  git add [filename]
```

Hinzufügen aller Änderungen

```
  git add .
```

Commiten der Änderungen mit message

```
  git commit -m [message]
```

##2. Commits zurücknehmen


X-commits zurückgehen

```
  git reset HEAD~x
```

Achtung: Reset Ändert die History. Der HEAD meines aktuellen Branches wir hier verschoben. Um zu altem Stand zurückzukehren nutzen wir daher checkout  (siehe nächstes Kapitel)


Optionen für reset

  --hard
  reset der History und des working dir


  --soft (Standard)
  reset der History


Vorgehen bei falschem commit ohne push

```
  reset --soft
```
Anschließend neu commiten

oder

```
  git reset --hard 
```
um Änderungen zu verwerfen


Möchte man zu einem bestimmten commit zurückgehen kann man auch

```
  git reset [hash]
```

verwenden.

##3. Zu alten Versionen zurückkehren

```
  git checkout [hash]
```

Bringt das working dir auf den Stand des gewählten commits. Die History bleibt hiervon unberührt.


Es ist möglich an dieser Stelle anschließend einen neuen Branch zu erstellen um von diesem Commit aus weiter zu arbeiten. (Siehe nächstes Kapitel)


##4. Branches erstellen und löschen

```
  git branch [branchname]
```

Erstellt einen neuen Branch auf dem aktuellen Commit

```
  git checkout [branchname]
```

Bringt das working-dir auf den angegebenen Branchzustand

```
  git checkout -d [branchname]
```

Wechselt zum angegebenen Branch und erstellt ihn falls er noch nicht existiert

```
  git push origin [branchname]
```

erstellt eine Remotekopie des Branches (wenn man sich im Branch befindet)


##5. Rebase Fallbeispiel

Der Rebase ist ein Rebase onto. Es werden also alle Änderungen im eigenen Branch auf den Fremdbranch angewendet. Dazu muss man sich im eigenen Branch befinden.

```
  git checkout [eigenbranch]
```

Der Rebase geschieht mit dem folgenden Befehl:

```
  git rebase [fremdbranch]
```

Nun müssen Konflikte pro Commit einzeln aufglöst werden.

##6. Merge Fallbeispiel

Bei einem Merge werden alle Änderungen innerhalb eines Commits bereinigt. Dieser Commit wird auf den eigenen Branch angewendet. 

```
  git checkout [eigenbranch]
```

```
  git merge [fremdbranch]
```

##7. Fehler finden und beheben
Git-Tasks Skript

```
  cd dbf/frontend/web

  npm run git-tasks
```

Prüft die History auf doppelte Commits.




Das Reflog

```
  git reflog
```

Zeigt eine nummerierte Liste aller lokalen git Operationen an.


Mit 
```
  git reset HEAD@{[Zustandsnummer]} 
```
kehrte man zum gewählten Zustand zurück.


Dabei ändert man mit --soft nur die Historie und mit --hard auch das working dir.




QGit


QGit bietet die Möglichkeit die eigene Historie übersichtlicher anzeigen zu lassen.


Installieren:

```
  sudo apt-get install qgit
```
Starten:
```
  qgit
```

##8. git push und Optionen

```
  git push 
```
(mit default config)
Ersetzt die remote History durch die eigene, wenn es sich um einen Fast-Forward handelt.

```
  git push origin [branchname] 
```
(default für git push)

```
  git push origin [branchname] --force
```
Überschreibt die remote History in jedem Fall

```
  git push origin [branchname] --force-with-lease 
```
überschreibt die remote History nur wenn die sich seit dem letzten pull nicht geändert hat.


##9. git pull und Optionen

```
  git pull
```

Ist Kurzform von

```
  git fetch && git merge
```


(git fetch lädt alle Änderungen von remote)

```
  git pull --rebase
```

Ist Kurzform von
```
  git fetch && git rebase
```

In der git-Config lässt sich das Standardverhalten einstellen

```
  git config --list
```
zeigt die config

```
  git config --global pull.rebase true
```
Setzt pull.rebase auf trueueue