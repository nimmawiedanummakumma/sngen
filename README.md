# sngen
# Neuer Seriennummer-Generator für Vodafone KDG
Der funktionierende Generator auf github: https://nimmawiedanummakumma.github.io/sngen/

## Infos zum Programm

### Historie
Gut 11 Jahre nachdem ich mit meinem ersten Generator viel Zuspruch fand, habe ich mich wieder mit dem Thema 
befasst, denn mein Generator auf einem FreeHoster-Account hatte vor Jahren das Zeitliche gesegnet. 

Gott sei Dank gab es im KDG-Forum und anderswo bereits Ersatz und auch der Algorithmus zum Erzeugen der
Prüfziffer ist mittlerweile Allgemeingut.

## Praktische und ästethische Erwägungen
Mir persönlich gefielen die erhältlichen Lösungen nicht. Denn alle Lösungen erfordern entweder zwingend einen 
Webserver oder man muss binäre Programme, deren Quellcode und Absichten man nicht kennt, auf den eigenen Rechner laden.

Daher habe ich mal wieder einen Generator programmiert, ich brauchte mal wieder selber eine Seriennnummer.
Diesmal ist er auch optisch ansprechender, der Spielteufel ritt mich ein wenig.

Er sammelt und überträgt keinerlei Daten und läuft vollkommen lokal. Wenn man die HTML-Seite auf den eignenen Rechner herunterlädt und lokal mit dem Browser öffnet, funktioniert der Generator vollkommen offline.

### Konzeption
Dieser Seriennummerngenerator ist so konzipiert, dass er (hoffentlich fast) überall funktioniert.
Er liegt im Quelltext vor (OpenSource) und funktioniert im Browser ohne dass man zwingend einen Server benötigt.
Ich habe Wert darauf gelegt, dass sämtliche Daten und Programme direkt in der HTML-Datei integriert sind.

Man braucht deswegen nicht einmal einen Webserver, damit der Generator funktioniert, er läuft komplett im Browser. 
Daher genügt es, wenn man ihn auf dem eigenen Rechner ablegt und mit dem Browser die Datei öffnet.

Natürlich kann man die Datei auf beliebigen Server ablegen und dann aufrufen, auch dann funktioniert sie ebenso.

### Kopien erwünscht
Bitte macht Kopien von der HTML-Datei und legt sie ab, falls dieser Account mal geschlossen wird.

### Weitere Beteilung des Urhebers
Ich selbst werde dieses Projekt übrigens nicht groß weiter verfolgen.
Deswegen kann auch jeder Github-Benutzer den Code ändern. Ich hoffe mal,
dass das nicht ins Chaos führt.

### Änderungen
Bei Änderungen daran denken, die komprimierte Variante (siehe unten) auch in den Branch gh-pages als index.html zu übernehmen, denn von da kommt die Generatorseite https://nimmawiedanummakumma.github.io/sngen/
. 

### Zusätzliche Informationen
Generatoren werden im KDG-Forum beschrieben ( https://www.kdgforum.de/viewtopic.php?f=5&t=3140&start=850 ) dort 
sollte man sich informieren.

### Varianten
Die Datei existiert in 2 Varianten einer komprimierten und eine unkomprimierten.
Die komprimierte sollte verwendet werden um Seriennummern zu generieren.
Die unkomprimierte sollte verwendet werden, wenn der Code modifiziert werden soll (da sind auch Kommentare drin).
Nach erfolgter Modifikation komprimiert man dann wieder.
Zum Komprimieren kann man https://htmlcompressor.com/compressor/ verwenden, da kann man den Code auch gleich validieren.
Wichtig ist, dass man vor dem Hochladen den Zeichensatz auf UTF-8 stellt, sonst werden die Umlaute ruiniert.

So komprimiert man
  1. Mit dem Browser die Seite https://htmlcompressor.com/compressor/
  2. Wichtig: den Zeichensatz auf utf-8 stellen
  3. Die HTML-Datei hochladen und
  4. anschließend komprimieren
  5. Die Gelegenheit nutzen und den HTML-Code validieren
  6. Den komprimierten Code herunterladen und in github als sn-uncomprssed.html ablegen, ggf, auch im Branch gh-pages als index.html

### Ein paar Infos zum Icon

Das Icon liegt in der Datei sn.svg.b64 base64-kodiert im Quellcode vor, 
genau so wie es in den 
HTML-code integriert ist. Der Grund für die Kodierung ist, dass es nur 
auf diese Art so in den Code integriert werden konnte, 
dass es sowohl als favicon (das kleine Icon in der Adressleiste des Browsers) 
als auch innerhalb der Seite verwendet werden kann.

Soll das Icon Änderungen erfahren, geht man so vor:
1. Dekodieren z. B. mit `openssl base64 -d < sn.svg.b64 > sn.svg
2. Bearbeiten von sn.svg (mit einem Vectorgrafikprogramm oder einem Text-Editor)
3. Kodieren z. B. mit `openssl base64 < sn.svg > sn.svg.b64
4. Im unkomprimierten HTML-Quellcode das Icon ersetzen (function svgiconb64)
Hierzu wird der Base64-code in einer einigen Zeile verlangt, das lässt sich mit
`awk '{printf "%s",$0}' sn.ico.b64` einfach erzeugen.
```javascript
    function svgiconb64 () {
      /* This is the icon in base64 encoding. To see the decoded source
         code double-click on the icon when you view the page in the browser
       */ 
      return("ICAgPHN2ZwogICAgICBpZD0iaWNvbiIKICAgICAgdmlld0JveD0iMCAwIDYxIDYxIgogICAgICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciCiAgICAgIHdpZHRoPSI2MSIKICAgICAgaGVpZ2h0PSI2MSIKICAgICAgdmVyc2lvbj0iMS4xIj4KICAgICA8ZGVmcz4KICAgICAgIDxzdHlsZT4uY2lyY2xle2ZpbGw6I2U2MDAwMDt9LmRyb3B7ZmlsbDojZmZmO308L3N0eWxlPgogICAgIDwvZGVmcz4KICAgICA8ZwogICAgICAgIHRyYW5zZm9ybT0ibWF0cml4KDAuMjExNjcwMDgsMCwwLDAuMjExNjcwMDgsLTIuNTAxNDgzNCwtMi41MDE0ODI1KSIKICAgICAgICBpZD0iZzgiPgogICAgICAgPGNpcmNsZQogICAgICAgICAgY2xhc3M9ImNpcmNsZSIKICAgICAgICAgIGN4PSIxNTUuOTEiCiAgICAgICAgICBjeT0iMTU1LjkxIgogICAgICAgICAgcj0iMTQxLjczIgogICAgICAgICAgc3R5bGU9ImZpbGw6I2U2MDAwMCIgLz4KICAgICAgIDxwYXRoCiAgICAgICAgICBjbGFzcz0iZHJvcCIKICAgICAgICAgIGQ9Im0gMTU0LjkyLDIzNS4wMyBjIDM4Ljk0LDAuMTMgNzkuNDYsLTMzLjExIDc5LjYzLC04Ni40OCAwLjA5LC0zNS4yOSAtMTguOTUsLTY5LjI2IC00My4yOSwtODkuNDYgLTIzLjc0LC0xOS42NiAtNTYuMjYsLTMyLjI3IC04NS43NiwtMzIuMzcgLTMuOCwwIC03Ljc3LDAuMyAtMTAuMiwxLjEzIDI1Ljc5LDUuMzUgNDYuMzIsMjkuMzUgNDYuMjMsNTYuNTggYSAxNC43OCwxNC43OCAwIDAgMSAtMC4xNywyLjMxIEMgOTguMjAsOTcuMjUgNzguNjEsMTIzLjI5IDc4LjQ5LDE1OS4zMiBjIC0wLjEyLDM2LjAzIDI4LjMyLDc1LjU1IDc2LjQzLDc1LjcxIHoiCiAgICAgICAgICBzdHlsZT0iZmlsbDojZmZmZmZmIgogICAgICAgICAgLz4KICAgICAgIDxwYXRoCiAgICAgICAgICBzdHlsZT0iZmlsbDojZmYwMDAwO3N0cm9rZTojZmYwMDAwO3N0cm9rZS13aWR0aDo1LjMwMjU4ODk0IgogICAgICAgICAgZD0ibSAxODcuNjcsMTc0LjY2IGEgMzEuNjEsMzEuNjMgMCAwIDEgLTMxLjQyLDMxLjYzIDMxLjYxLDMxLjYzIDAgMCAxIC0zMS43OSwtMzEuMjUgbCAzMS42MCwtMC4zNyB6IiAvPgogICAgICAgPHBhdGgKICAgICAgICAgIHN0eWxlPSJmaWxsOiNmZjAwMDA7c3Ryb2tlOiNmZjAwMDA7c3Ryb2tlLXdpZHRoOjQuNzI0MzMzMjkiCiAgICAgICAgICBkPSJtIC0xNjUuODAsLTE0MS41MyBhIDExLjc1LDQuNDIgMCAwIDEgLTExLjY4LDQuNDIgMTEuNzUsNC40MiAwIDAgMSAtMTEuODIsLTQuMzcgbCAxMS43NSwtMC4wNTIgeiIKICAgICAgICAgIHRyYW5zZm9ybT0ibWF0cml4KC0wLjk5OTk0MDA1LC0wLjAxMDk0OTQyLDAuMDEwOTQ5NDIsLTAuOTk5OTQwMDUsMCwwKSIgLz4KICAgICAgIDxwYXRoCiAgICAgICAgICBzdHlsZT0iZmlsbDojZmYwMDAwO3N0cm9rZTojZmYwMDAwO3N0cm9rZS13aWR0aDo0LjcyNDMzMzI5IgogICAgICAgICAgZD0ibSAtMTI0Ljk0LC0xNDEuOTMgYSAxMS43NSw0LjQyIDAgMCAxIC0xMS42OCw0LjQyIDExLjc1LDQuNDIgMCAwIDEgLTExLjgyLC00LjM3IGwgMTEuNzUsLTAuMDUgeiIKICAgICAgICAgIHRyYW5zZm9ybT0ibWF0cml4KC0wLjk5OTk0MDA1LC0wLjAxMDk0OTQsMC4wMTA5NDk0LC0wLjk5OTk0MDA1LDAsMCkiIC8+CiAgICAgPC9nPgogICA8L3N2Zz4K");
    }

```

Kleines Gimmick am Rande: Wenn man auf der Generatorseite das Icon doppelklickt,erscheint der SVG-Quellcode in einer Popup-Message. Sollte also die Datei sn.svg verloren gehen, kann man sie so wieder erstellen.

## Info zur verwendeten Telefonnummer
Die angegebene Telefonnummer ist natürlich Unfug, sie wurde nur wegen der optischen Ähnlichkeit zu gewissen Seiten eingebaut. Sie ist wie eine Vanitynummer aufgebaut.

`6436263 32` steht also für

`NIEMAND DA`

Die verwendete Ländervorwahl ist nicht vergeben, so dass ein Anrufversuch auch keine Kosten verursacht.
