<html>
  <body>
    <h1>Hobbylos search engine</h1>
    Die neue Hobbylos Suche.<br><br>
    <h3>Was ist neu?</h3>
    <b>- Design</b><br>
    Komplett neues, modernes Design mit Dark/Light Mode.<br>
    <b>- Backend</b><br>
    Das Backend setzt auf einen Indexsuchansatz (ähnlich wie Google und Co).<br>
    Vorteile: <br>
    - wesentlich schneller <br>
    - genauer <br>
    - Sortierung nach Relevanz <br>
    - Suche nach Sätzen besser möglich <br>
    - Folgen-Filter <br>
    <br>
    <h3>API:</h3>
    <h4>GET Request</h4>
    URL: https://api.hobbylos.online/ <br>
    word = str (gesuchtes wort / satz)<br>
    offset = int (response offset)(optional)<br>
    limit = int (response limit)(optional)<br>
    sort_by_time = str "forward" (neueste zuerst) oder "reverse" (älteste zuerst)(optional, default: Sortierung nach Relevanz)<br>
    folge_id = str (Spotify Episoden id, filtert Ergebnisse auf eine bestimmte Folge)(optional)
    <h4>Response</h4>
    b = int (current limit)(optional)<br>
    v = int (current offset)(optional)<br>
    count_all = str "... wurde ... Mal in Hobbylos gefunden."<br>
    next = str (next api request)(optional)<br>
    previous = str (previous api request)(optional)<br>
    search = array [<br>
    ... L = float (Relevanz-Score),<br>
    ... f = str (Spotify Episoden id),<br>
    ... n = str (Name der Hobbylos Episode),<br>
    ... s = int (Delay des Wortes/Satzes in der Episode),<br>
    ... text = str (Text mit dem Wort/Satz drin)<br>
    ]
    <h4>GET Request /folgen</h4>
    URL: https://api.hobbylos.online/folgen <br>
    Gibt eine Liste aller Hobbylos-Folgen (von Spotify) inkl. Indexierungs-Status zurück. Keine Parameter.
    <h4>Response</h4>
    total_indexed = int (Anzahl bereits indexierter Folgen)<br>
    total_on_spotify = int (Gesamtanzahl Folgen auf Spotify)<br>
    folgen = array [<br>
    ... id = str (Spotify Episoden id),<br>
    ... name = str (Name der Folge),<br>
    ... release_date = str (Veröffentlichungsdatum, YYYY-MM-DD),<br>
    ... indexed = bool (true wenn durchsuchbar),<br>
    ... status = str (optional, nur bei nicht-indexierten Folgen: pending, queued, transcribing, processing, error),<br>
    ... status_message = str (optional, Zusatzinfo zum Status)<br>
    ]
  </body>
</html>
