<!--

author:   Sebastian Zug & André Dietrich & Galina Rudolf
email:    sebastian.zug@informatik.tu-freiberg.de & andre.dietrich@ovgu.de & Galina.Rudolf@informatik.tu-freiberg.de
version:  0.0.1
language: de
narrator: Deutsch Female

import: https://raw.githubusercontent.com/LiaTemplates/Rextester/master/README.md

-->

# Vorlesung Softwareprojekt

Der vorliegende Kurs realisiert die Vorlesung "Softwareprojekt" an der TU Bergakademie
Freiberg auf der Basis von LiaScript. Die
Veranstaltung richtet sich an Informatiker und Mathematiker und adressiert die folgenden Punkte:

* aufbauend auf dem vorangegangenen Kurs Softwareentwicklung werden die Konzepte von C++ erläutert
* Einführung in das Robot Operating System (ROS)
* Elemente von Robotersystemen und deren Implementierung wie
  * Grundlagen der Sensoren und deren Einbettung in ROS
  * Aktoren und deren Regelung
  * Karten, deren Erzeugung und Nutzung


* Architekturkonzepte für Roboteranwendungen

Für den ersten Punkt wird der Quellcode direkt in das LiaScript-Dokument eingebettet und kann damit im Browser bearbeitet werden. Dabei ist ein "Versionssystem light" verfügbar, das Änderungen lokal im Browser abspeichert. Basis für die Ausführungsumgebung ist die API von Rextester https://rextester.com/. Vielen Dank für diesen Service!

Ausführbarer C++ Code sieht wie folgt aus, der Titel kann weggelassen werden.

```cpp                     HelloWorld.cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello, World!";
    return 0;
}
```
@Rextester.CPP

Der Markdown-Quellcodeblock wird dafür um den Makroaufruf `@Rextester.CPP` am
Ende ergänzt. Dabei können unterschiedliche Compiler (gcc, clang, Microsoft C++ Compiler) und Parametersets genutzt werden.

```
@Rextester.CPP
@Rextester.CPP_clang
@Rextester.CPP_vc
```

Im Weiteren ist es möglich "Kommandozeilenparameter" an die Rextester-Ausführungsumgebung
zu übergeben und diese dann auch im Browser zu variieren. In diesem Fall werden
die Parameter in einem separaten Codeblock angefügt, gefolgt von der Anweisung
`@Rextester.CPP(true,@input(1))`

```cpp                     HelloWorld.cpp
#include <iostream>
using namespace std;

int main()
{
    int input{};
    int output{};

    cout << "Bitte geben Sie eine Zahl ein!" << endl;
    cin >> input;
    output = input * 2;
    cout << "Das Doppelte dieser Zahl ist " << output << "." << endl;
    return 0;
}
```
```
5
```
@Rextester.CPP(false,`@input(1)`)

Der boolsche Parameter kann genutzt werden um eine knappe Statistik der Kompilierung
und der Ausführungsparameter abzurufen.

Darüber hinaus können auch komplette Parameterset an den Compiler übergeben werden, um zum Beispiel die verschiedenen C++ Versionen zu evaluieren. Wenn Sie zum Beispiel in folgendem Beispiel, dass mit dem Makroaufruf

```
@Rextester.eval(@CPP, false, ,`-Wall -std=c++98 -O2 -o a.out source_file.cpp`)
```

kompiliert wird, versuchen `auto` und die uniforme Initialisierung zu nutzen (jeweils ab C++11), generiert der Compiler einen Fehler.

```cpp                     HelloWorld.cpp
#include <iostream>
using namespace std;

int main()
{
    int output = 5;
    //auto output {5};
    cout << output;
    return 0;
}
```
@Rextester.eval(@CPP, false, ,`-Wall -std=c++98 -O2 -o a.out source_file.cpp`)
