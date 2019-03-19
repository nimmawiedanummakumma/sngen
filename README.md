# sngen
# Neuer Seriennummer-Generator für KDG
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

So kompxpirimiert man
  1. Mit dem Browser die Seite https://htmlcompressor.com/compressor/
  2. Wichtig: den Zeichensatz auf utf-8 stellen
  3. Die HTML-Datei hochladen und
  4. anschließend komprimieren
  5. Die Gelehenheit nutzen und den HTML-Code validieren
  6. Den komprimierten Code herunterladen und in github als sn-uncomprssed.html ablegen, ggf, auch im Branch gh-pages als index.html

= Ein paar Infos zum Icon

Das Icon liegt als sn.svg.b64 base64-kodiert im Quellcode vor, 
genauso wie es in den 
HTML-code integriert ist. Der Grund für die Kodierung ist, dass es nur 
auf diese Art so in den Code integriert werden konnte, 
dass es sowohl als favicon (das kleine Icon in der Adressleiste des Browsers) 
als auch innerhalb der Seite verwendet wird.

Soll das Icon Änderungen erfahren, geht man so vor:
1. Dekodieren z. B. mit `openssl base64 -d < sn.svg.b64 > sn.svg
2. Bearbeiten von sn.svg (mit einem Vectorgrakfik programm oder einem Text-Editor)
3. Kodieren z. B. mit `openssl base64 < sn.svg > sn.svg.b64
4. Im unkomprimierten HTML-Quellcode das Icon ersetzen (function svgiconb64)
Hierzu wird der Base64-code in einer einigen Zeile verlangt, das lässt sich mit
`awk '{printf "%s",$0}' sn.ico.b64` einfach erzeugen.
