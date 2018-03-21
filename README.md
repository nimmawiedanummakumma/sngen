# sngen
Neuer Seriennummer-Generator für KDG

Beinahe 10 Jahre nachdem ich mit meinem ersten Generator viel Zuspruch fand, habe ich mich wieder mit dem Thema 
befasst, denn mein Generator auf einem FreeHoster-Account hatte vor Jahren das Zeitliche gesegnet. 

Gott sei Dank gab es im KDG-Forum und anderswo bereits Ersatz und auch der Algorithmus zum Erzeugen der
Prüfziffer ist mittlerweile Allgemeingut.

Mir persönlich gefielen die erhältlichen Lösungen nicht. Denn alle Lösungen erfordern entweder zwingend einen 
Webserver odr ich muss Programme deren Quellcode und Absichten ich nicht kenne, auf meinen Rechner laden.

Daher habe ich mal wieder einen programmiert, ich brauchte mal wieder selber eine Seriennnummer.

Dieser Seriennummerngenerator ist so konzipiert, dass er (hoffentlich fast) überall funktioniert.
Er liegt im Quelltext vor (OpenSource) und funktioniert im Browser ohne dass man zwingend einen Server benötigt.
Ich habe Wert darauf gelegt, dass sämtliche Daten und Programme direkt in der HTML-Datei integriert sind.

Man braucht deswegen nicht einmal einen Webserver, damit der Generator funktioniert, er läuft komplett im Browser. 
Daher genügt es wenn man sie auf dem eigenen Rechner ablegt und mit dem Browser die Datei öffnet.

Natürlich kann man die Datei auf beliebigen Server ablegen und dann aufrufen, auch dann funktioniert sie ebenso.

Bitte macht Kopien von der HTML-Datei und legt sie ab, falls dieser Account mal geschlossen wird.
Ich selbst werde dieses Projekt übrigens nicht groß weiter verfolgen.
ür 
Der Generator wird im KDG-Forum beschrieben ( https://www.kdgforum.de/viewtopic.php?f=5&t=3140&start=850 ) dort 
sollte man sich informieren.

Die Datei existiert in 2 Varianten einer komprimierten und eine unkomprimierten.
Die komprimierte sollte verwendet werden um Seriennummern zu generieren.
Die unkomprimierte sollte verwendet werden, wenn der Code modifiziert werden soll (da sind auch Kommentare drin).
Nach erfolgter Modifikation komprimiert man dan wieder.
Zum Komprimieren kann man https://htmlcompressor.com/compressor/ verwenden, da kann man den Code auch gleich validieren.

