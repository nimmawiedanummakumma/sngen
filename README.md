# sngen
Neuer Seriennummer-Generator für KDG

Gut 11 Jahre nachdem ich mit meinem ersten Generator viel Zuspruch fand, habe ich mich wieder mit dem Thema 
befasst, denn mein Generator auf einem FreeHoster-Account hatte vor Jahren das Zeitliche gesegnet. 

Gott sei Dank gab es im KDG-Forum und anderswo bereits Ersatz und auch der Algorithmus zum Erzeugen der
Prüfziffer ist mittlerweile Allgemeingut.

Mir persönlich gefielen die erhältlichen Lösungen nicht. Denn alle Lösungen erfordern entweder zwingend einen 
Webserver oder man muss Programme, deren Quellcode und Absichten man nicht kennt, auf den eigenen Rechner laden.

Daher habe ich mal wieder einen Generator programmiert, ich brauchte mal wieder selber eine Seriennnummer.
Diesmal ist er auch optisch ansprechender, der Spielteufel ritt mich ein wenig.

Dieser Seriennummerngenerator ist so konzipiert, dass er (hoffentlich fast) überall funktioniert.
Er liegt im Quelltext vor (OpenSource) und funktioniert im Browser ohne dass man zwingend einen Server benötigt.
Ich habe Wert darauf gelegt, dass sämtliche Daten und Programme direkt in der HTML-Datei integriert sind.

Man braucht deswegen nicht einmal einen Webserver, damit der Generator funktioniert, er läuft komplett im Browser. 
Daher genügt es, wenn man ihn auf dem eigenen Rechner ablegt und mit dem Browser die Datei öffnet.

Natürlich kann man die Datei auf beliebigen Server ablegen und dann aufrufen, auch dann funktioniert sie ebenso.

Bitte macht Kopien von der HTML-Datei und legt sie ab, falls dieser Account mal geschlossen wird.
Ich selbst werde dieses Projekt übrigens nicht groß weiter verfolgen.

Der Generator wird im KDG-Forum beschrieben ( https://www.kdgforum.de/viewtopic.php?f=5&t=3140&start=850 ) dort 
sollte man sich informieren.

Die Datei existiert in 2 Varianten einer komprimierten und eine unkomprimierten.
Die komprimierte sollte verwendet werden um Seriennummern zu generieren.
Die unkomprimierte sollte verwendet werden, wenn der Code modifiziert werden soll (da sind auch Kommentare drin).
Nach erfolgter Modifikation komprimiert man dann wieder.
Zum Komprimieren kann man https://htmlcompressor.com/compressor/ verwenden, da kann man den Code auch gleich validieren.

{::nomarkdown}
<!DOCTYPE html>
<html lang="de">
 <head>
  <meta charset="utf-8">
  <title>Seriennummern-Generator</title>
<!-- 
 The goal of this serial-number generator was to be self-contained in one
 single HTML-file. This makes the generator even work when the HTML file
 is just downloaded to the user's directory and accessed locally with the
 browser. It does not need a webserver to work.

 To achieve this goal some tricks had to be used, the most tricky was
 to have both, the favicon and the icon on the page to be comimg from
 the same svg image. For this to work the image needs to be base64 encoded
 and created on the fly, which was a bit tricky for the favicon.
 To see the plaintext svg code you can double-click the icon that will create
 an alert-box showing the SVG source code.
 To get it back into the code - if modified - you have to base64-encode it
 and put that code into the function svgiconb64.

 For performance-reasons the code should be compressed. Here's how to do it:
  1. Use your browser to go to://htmlcompressor.com/compressor/
  2. Upload this HTML file
     MAKE SURE TO SET CHARSET TO UTF8 BEFORE YOU UPLOAD!
  3. Compress it
  4. While at it, it might be a good idea to also use the HTML-validator
  5. Download the compressed code
  6. Always deliver compressed code, but also keep and offer uncompressed
     code for easier modifications 
-->
  <style media="all">
body {
  padding:0px;
  margin:0px;
  font-family:Verdana,Arial,Helvetica,sans-serif;
}
a:link{
  text-decoration: none;
  color: black;
}
a:visited{
  text-decoration: none;
  color: black;
}
a:hover{
  text-decoration: none;
  color: #e60000;
}
#vorkopf {
  margin-top:5px;
  position:absolute;
  top:0px;
  font-size: 8pt;
  right:180px;
  left:180px;
  height:30px;
  text-align:center;
}
#kopf {
  position:absolute;
  top:40px;
  right:180px;
  left:180px;
  height:50px;
  text-align:left;
  border-radius: 3px;
  background-color: #e60000;
  box-shadow: 0 1px 2px rgba(50,50,50,0.75);
}
#inhalt {
  position:relative;
  top: 20px;
  min-width:600px;
  padding:0px;
  margin:0px 180px;
}
#links {
  position:relative;
  top: 35px;
  left:10px;
  width:140px;
  bottom: 40px;
  text-align:right;
}
#rechts {
  position:absolute;
  top: 40px;
  right:10px;
  width:170px;
  text-align:left;
}
.spalte1 {
  margin-right: 2%;
  width: 48%;
  float: left;
}
.spalte2 {
  margin-left: 2%;
  float: left;
  width: 48%;
}
.vollbreit {
  margin-right: 2%;
  width: 98%;
  float: left;
}
.center {
  text-align: center;
}
#fuss {
  font-size:0.8em;
  position:relative;
  text-align: center;
  margin-top: 30px;
  margin-bottom: 50px;
  padding: 20px;
  background-color: #f4f4f4;
}
p {
  font-size:0.8em;
  padding:10px 15px;
  font-family:Verdana,Arial,Helvetica,sans-serif;
}
pre {
  font-size:12px;
  padding:10px 15px;
}
#back {
  padding:15px;
  text-align:center;
}
#back a {
  color:white;
  font-size:0.8em;
  font-weight:600;
}
h2,h3,h4,h5,h6 {
  margin: 0.3em 0 0.2em 0;
  color:#e60000;
}
h1,h2,h3,h4,h5,h6,body,div,p,span {
  font-family:DejaVu-Sans,Verdana,Arial,Helvetica,sans-serif;
  font-weight: normal;
}
h1 {
  margin: 1em 0em 0.2em 0em;
  color:#e60000;
}
.fett {
  font-family:DejaVu-Sans,Verdana,Arial,Helvetica,sans-serif;
  font-weight: bold;
}
.unterstrichen {
  font-family:DejaVu-Sans,Verdana,Arial,Helvetica,sans-serif;
  text-decoration: underline;
}
.receiver {
  color: #00aa00;
}
.checksum {
  color: #0000aa;
}
.serial {
  font-family:DejaVu-Sans,Verdana,Arial,Helvetica,sans-serif;
  color: #e60000;
}
.bold {
  font-weight: bold;
}
.italic {
  font-style: italic;
}
.spacing {
    margin-left: 20px;
    margin-right: 20px;
}
.clear {
  clear: both;
}
.tiny {
  font-size: 0.6em;
}
  </style>
 </head>
 <body>
  <noscript>
   <p>
    <br>
    <br>
    <br>
    <br>
    <br>
    <h1 class="center">Sie haben JavaScript deaktiviert, dann funktioniert der Generator nicht!</h1>
    <h2 class="center">Sie müssen JavaScript aktivieren, damit sie den Generator nutzen können.</h2>
    <p>
    Die Seriennummer wird auf Ihrem Rechner errechnet bzw. erzeugt.
    Dazu benötigt diese Seite JavaScript.<br>
    Der Vorteil ist, dass der Generator ohne Server funktioniert.<br>
    Er funktioniert also auch, wenn Sie diese Seite bzw. den Quelltext
    in einer lokalen Datei abspeichern und mit dem Browser die Datei öffnen.<br>
    Dies erleichert es auch, ihn auf beliebigen Servern zur Verfügung zu
    stellen, denn es werden keinerlei Anforderungen an den Server gestellt.
   </p>
  </noscript>
  <div id="vorkopf">
   Produktberatung & Bestellung: <span class="fett">0080 - 643 626 332</span>
  </div>
  <div id="kopf">
  </div>
  <div id="links">
   <span id="iconref">
   <!-- svg-image will be added by JS -->
   </span>
  </div>
  <div id="rechts">
  </div>
  <div id="inhalt">
   <div class="vollbreit">
    <h1>Seriennummern-Generator</h1>
    <h2>für Vodafone Kabel Deutschland</h2> 
    <h3>1. Gerät auswählen</h3>
   </div>
   <div class="spalte1">
    <span class="fett unterstrichen">Entweder</span> CI+ Modul <br>bzw. Reveiver wählen<br>
    <select id="snstart" onchange="snstartchg();">
     <option value="39015">Smart CI+ (NDS) - 39015</option>
     <option value="39010">Smart CI+ (NDS) - 39010</option>
     <option value="33502" selected>SMiT CI+ (NDS)</option>
     <option value="39210">Neotion CI+ (NDS)</option><!-- G03/G09-->
     <option value="11135">Humax PR HD3000 C (NDS)</option>
     <option value="35510">Technicrypt CI+ (NDS)</option>
     <option value="13716">Nokia dbox2 (betacrypt)</option>
    </select>
   </div>
   <div class="spalte2">
    <span class="fett unterstrichen">oder</span>
    eigenen, fünfstelligen,<br>
    numerischen Gerätecode eingeben<br>
    <input type="number" id="ownrec" size="10" min="10000" max="99999" onchange="ownrecchg();">
   </div>
   <div class="vollbreit">
    <h3>2. Gerätenummer wählen</h3>
   </div>
   <div class="spalte1">
    <span class="fett unterstrichen">Entweder</span> Nummer generieren<br><span class="tiny">Anzahl der Stellen auswählen (zwischen 3 und 7)</span><br>
    <input type="number" id="digits" value="5" size="1" min="3" max="7" onchange="digitschg();">
   </div>
   <div class="spalte2">
     <span class="fett unterstrichen">oder</span> selbst eine Nummer wählen<br><span class="tiny">wobei maximal sieben Stellen möglich sind</span><br>
     <input type="number" id="ownsn" value="" size="10" onchange="ownserchg();"><br>
   </div>
   <div class="vollbreit">
    <h3>3. Los geht's</h3>
     <button type="button" id="los">Seriennummer erzeugen</button><br>
   </div>
   <div class="vollbreit center">
     <span class="tiny"><br>Seriennummer bestehend aus <span class="receiver">Receiver-/Modulkennung</span>, <span class="serial">Gerätenummer</span> und <span class="checksum">Prüfsumme</span>.<br></span>
    <div id="result">
     <br>
    </div><br>
    <small>Alle Angaben ohne Gewähr.</small>
   </div>
  </div>
   <div class="vollbreit">
     <div id="fuss">
        <a href="https://www.kdgforum.de/viewtopic.php?f=62&t=16390&start=30&hilit=Pr%C3%BCfziffer" class="spacing" target="_blank">KDG Forum</a>
       <a href="https://www.vuplussupport.org/wbb4/index.php?thread/40813-how-to-vodafone-kabel-deutschland-mit-der-vu/" class="spacing" target="_blank">VUplus Support Forum</a>
       <a href="https://forum.digitalfernsehen.de/threads/kabel-deutschland-g09-karte-emms-per-oscam.338181/
" class="spacing" target="_blank">Digital Fernsehen Forum</a>
       <a href="http://www.digitalfernsehen.de/Kabelkunden-tricksen-Kabel-Deutschland-mit-falschen-Receiver-Seriennummern-aus.news_749990.0.html" class="spacing" target="_blank">Digital Fernsehen Artikel</a>
     </div>
  </div>
   <script>
    function ownserchg() {
        var ownsn = document.getElementById('ownsn');
        if (ownsn.value.length > 7) {
          alert("Maximal 7 Stellen möglich - Nummer wird gekürzt");
	  ownsn.value = ownsn.value.substr(0,7);
        } else if ( isNaN(ownsn.value)) {
          alert("Seriennumer muss eine max. 7-stellige Zahl sein")
	  ownsn.value = 0;
        } else {
          if (ownsn.value < 0) {
	      alert("Seriennummer muss positiv oder leer sein.");
	      ownsn.value = '';
	  } else {	    
              serial();
	      return(true);
          }
        }
	return(false);
    }
    function digitschg() {
        var DigitsInp  = document.getElementById('digits');
        var digits  = DigitsInp.value;
	if ((digits > 7 ) || (digits < 3)) {		    
				       DigitsInp.value = 5;
				       alert("Die Anzahl der Stellen muss zwischen 3 und 7 liegen");
				       return(false);
				       } else {
	serial();
				       return(true);
				       }
    }
    function ownrecchg() {
        var ownrec = document.getElementById('ownrec');
        if (ownrec.value.length != 5) {
          alert("Receivercode muss fünfstellig sein.");
        } else if ( isNaN(ownrec.value)) {
          alert("Receivercode muss eine fünfstellige Zahl sein")
        } else {
          serial();
          return(true);
	}
        ownrec.value=snstart.value;
        return(false);
    }
    function snstartchg() {
      ownrec.value=snstart.value;
      serial();
    }
    function showsvgb64() {
      alert("SVG Quellcode des Icon in base64-codiert:\n"+svgiconb64());
    }
    function showsvg() {
      var Base64 = {
        _keyStr: "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=",
            encode: function(e) {
            var t = "";
            var n, r, i, s, o, u, a;
            var f = 0;
            e = Base64._utf8_encode(e);
            while (f < e.length) {
                n = e.charCodeAt(f++);
                r = e.charCodeAt(f++);
                i = e.charCodeAt(f++);
                s = n >> 2;
                o = (n & 3) << 4 | r >> 4;
                u = (r & 15) << 2 | i >> 6;
                a = i & 63;
                if (isNaN(r)) {
                    u = a = 64
                } else if (isNaN(i)) {
                    a = 64
                }
                t = t + this._keyStr.charAt(s) + this._keyStr.charAt(o) +
                    this._keyStr.charAt(u) + this._keyStr.charAt(a)
            }
            return t
        },
        decode: function(e) {
            var t = "";
            var n, r, i;
            var s, o, u, a;
            var f = 0;
            e = e.replace(/[^A-Za-z0-9\+\/\=]/g, "");
            while (f < e.length) {
                s = this._keyStr.indexOf(e.charAt(f++));
                o = this._keyStr.indexOf(e.charAt(f++));
                u = this._keyStr.indexOf(e.charAt(f++));
                a = this._keyStr.indexOf(e.charAt(f++));
                n = s << 2 | o >> 4;
                r = (o & 15) << 4 | u >> 2;
                i = (u & 3) << 6 | a;
                t = t + String.fromCharCode(n);
                if (u != 64) {
                    t = t + String.fromCharCode(r)
                }
                if (a != 64) {
                    t = t + String.fromCharCode(i)
                }
            }
            t = Base64._utf8_decode(t);
            return t
        },
        _utf8_encode: function(e) {
            e = e.replace(/\r\n/g, "\n");
            var t = "";
            for (var n = 0; n < e.length; n++) {
                var r = e.charCodeAt(n);
                if (r < 128) {
                    t += String.fromCharCode(r)
                } else if (r > 127 && r < 2048) {
                    t += String.fromCharCode(r >> 6 | 192);
                    t += String.fromCharCode(r & 63 | 128)
                } else {
                    t += String.fromCharCode(r >> 12 | 224);
                    t += String.fromCharCode(r >> 6 & 63 | 128);
                    t += String.fromCharCode(r & 63 | 128)
                }
            }
            return t
        },
        _utf8_decode: function(e) {
            var t = "";
            var n = 0;
            var r = c1 = c2 = 0;
            while (n < e.length) {
                r = e.charCodeAt(n);
                if (r < 128) {
                    t += String.fromCharCode(r);
                    n++
                } else if (r > 191 && r < 224) {
                    c2 = e.charCodeAt(n + 1);
                    t += String.fromCharCode((r & 31) << 6 | c2 & 63);
                    n += 2
                } else {
                    c2 = e.charCodeAt(n + 1);
                    c3 = e.charCodeAt(n + 2);
                    t += String.fromCharCode((r & 15) << 12 | (c2 & 63) <<
                        6 | c3 & 63);
                    n += 3
                }
            }
            return t
        }
      }
      /* var Ausgabe  = document.getElementById('result'); */
      /* Ausgabe.innerHTML = "SVG source-code of icon:<br><textarea>"+Base64.decode(svgiconb64())+"</textarea>"; */
      alert("SVG Quellcode des Icon (base64-codiert verwendet für Icon und favicon):\n"+Base64.decode(svgiconb64()));
    }
    function serial() {
      var Eingabe  = document.getElementById('Eingabe');
      var Ausgabe  = document.getElementById('result');
      var serialNum;
      var startval;
      var zeros = "0000000000";
      var sn1, sn2, pp, pps;
      var iconlink = document.getElementById('favicon');
      if ( ownrec.value == 0 ) {
          startval = snstart.value;
      } else {
          startval = ownrec.value;
      }
      if ( ownsn.value == 0 ) {
	  var digits = document.getElementById('digits').value;
          serialNum = Math.floor(Math.random()*(10**digits)).toString();
      } else {
          serialNum = ownsn.value;
      }
      serialNum = startval + zeros.substr(0,12-serialNum.length-5)+serialNum;
      sn1 = parseInt(serialNum/100);
      sn2 = serialNum-(sn1*100)
      pp = sn1%23+sn2;
      if (pp > 99) {
          pp = pp-100
      }
      pps = pp.toString();
      pps = zeros.substr(0,10-8-pps.length)+pps;
      Ausgabe.innerHTML = "Seriennummer ist <span class='receiver bold'>"+serialNum.substr(0,5)+"</span><span class='serial italic bold'>"+serialNum.substr(5,7)+"</span><span class='checksum bold'>"+pps+"</span>"
      /* Eingabe.value = 0; */
    }
    function svgiconb64 () {
      /* This is the icon in base64 encoding. To see the decoded source
         code double-click on the icon when you view the page in the browser
       */ 
      return("ICAgPHN2ZwogICAgICBpZD0iaWNvbiIKICAgICAgdmlld0JveD0iMCAwIDYxIDYxIgogICAgICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciCiAgICAgIHdpZHRoPSI2MSIKICAgICAgaGVpZ2h0PSI2MSIKICAgICAgdmVyc2lvbj0iMS4xIj4KICAgICA8ZGVmcz4KICAgICAgIDxzdHlsZT4uY2lyY2xle2ZpbGw6I2U2MDAwMDt9LmRyb3B7ZmlsbDojZmZmO308L3N0eWxlPgogICAgIDwvZGVmcz4KICAgICA8ZwogICAgICAgIHRyYW5zZm9ybT0ibWF0cml4KDAuMjExNjcwMDgsMCwwLDAuMjExNjcwMDgsLTIuNTAxNDgzNCwtMi41MDE0ODI1KSIKICAgICAgICBpZD0iZzgiPgogICAgICAgPGNpcmNsZQogICAgICAgICAgY2xhc3M9ImNpcmNsZSIKICAgICAgICAgIGN4PSIxNTUuOTEiCiAgICAgICAgICBjeT0iMTU1LjkxIgogICAgICAgICAgcj0iMTQxLjczIgogICAgICAgICAgc3R5bGU9ImZpbGw6I2U2MDAwMCIgLz4KICAgICAgIDxwYXRoCiAgICAgICAgICBjbGFzcz0iZHJvcCIKICAgICAgICAgIGQ9Im0gMTU0LjkyLDIzNS4wMyBjIDM4Ljk0LDAuMTMgNzkuNDYsLTMzLjExIDc5LjYzLC04Ni40OCAwLjA5LC0zNS4yOSAtMTguOTUsLTY5LjI2IC00My4yOSwtODkuNDYgLTIzLjc0LC0xOS42NiAtNTYuMjYsLTMyLjI3IC04NS43NiwtMzIuMzcgLTMuOCwwIC03Ljc3LDAuMyAtMTAuMiwxLjEzIDI1Ljc5LDUuMzUgNDYuMzIsMjkuMzUgNDYuMjMsNTYuNTggYSAxNC43OCwxNC43OCAwIDAgMSAtMC4xNywyLjMxIEMgOTguMjAsOTcuMjUgNzguNjEsMTIzLjI5IDc4LjQ5LDE1OS4zMiBjIC0wLjEyLDM2LjAzIDI4LjMyLDc1LjU1IDc2LjQzLDc1LjcxIHoiCiAgICAgICAgICBzdHlsZT0iZmlsbDojZmZmZmZmIgogICAgICAgICAgLz4KICAgICAgIDxwYXRoCiAgICAgICAgICBzdHlsZT0iZmlsbDojZmYwMDAwO3N0cm9rZTojZmYwMDAwO3N0cm9rZS13aWR0aDo1LjMwMjU4ODk0IgogICAgICAgICAgZD0ibSAxODcuNjcsMTc0LjY2IGEgMzEuNjEsMzEuNjMgMCAwIDEgLTMxLjQyLDMxLjYzIDMxLjYxLDMxLjYzIDAgMCAxIC0zMS43OSwtMzEuMjUgbCAzMS42MCwtMC4zNyB6IiAvPgogICAgICAgPHBhdGgKICAgICAgICAgIHN0eWxlPSJmaWxsOiNmZjAwMDA7c3Ryb2tlOiNmZjAwMDA7c3Ryb2tlLXdpZHRoOjQuNzI0MzMzMjkiCiAgICAgICAgICBkPSJtIC0xNjUuODAsLTE0MS41MyBhIDExLjc1LDQuNDIgMCAwIDEgLTExLjY4LDQuNDIgMTEuNzUsNC40MiAwIDAgMSAtMTEuODIsLTQuMzcgbCAxMS43NSwtMC4wNTIgeiIKICAgICAgICAgIHRyYW5zZm9ybT0ibWF0cml4KC0wLjk5OTk0MDA1LC0wLjAxMDk0OTQyLDAuMDEwOTQ5NDIsLTAuOTk5OTQwMDUsMCwwKSIgLz4KICAgICAgIDxwYXRoCiAgICAgICAgICBzdHlsZT0iZmlsbDojZmYwMDAwO3N0cm9rZTojZmYwMDAwO3N0cm9rZS13aWR0aDo0LjcyNDMzMzI5IgogICAgICAgICAgZD0ibSAtMTI0Ljk0LC0xNDEuOTMgYSAxMS43NSw0LjQyIDAgMCAxIC0xMS42OCw0LjQyIDExLjc1LDQuNDIgMCAwIDEgLTExLjgyLC00LjM3IGwgMTEuNzUsLTAuMDUgeiIKICAgICAgICAgIHRyYW5zZm9ybT0ibWF0cml4KC0wLjk5OTk0MDA1LC0wLjAxMDk0OTQsMC4wMTA5NDk0LC0wLjk5OTk0MDA1LDAsMCkiIC8+CiAgICAgPC9nPgogICA8L3N2Zz4K");
    }
    var los  = document.getElementById('los');
    /* Where to add the icon */
    var icon  = document.getElementById('iconref');
    /* Where to add the favicon */
    var head = document.getElementsByTagName("head")[0];
    /* Create link and image */
    var link = document.createElement("link");
    var iimg = document.createElement("img");
    /* Set up favicon image using base64-encoded svg */
    link.type = "image/svg+xml";
    link.rel  = "icon";
    link.href = "data:image/svg+xml;base64," + svgiconb64();
    head.appendChild(link);
    /* Set up image on page using base64-encoded svg */
    iimg.src = "data:image/svg+xml;base64," + svgiconb64();
    icon.appendChild(iimg);
    los.addEventListener ('click', serial, true);
    kopf.addEventListener ('dblclick',showsvgb64, true);
    iimg.addEventListener ('dblclick', showsvg, true);
    ownrec.value=snstart.value;
   </script>
  </body>
</html>
