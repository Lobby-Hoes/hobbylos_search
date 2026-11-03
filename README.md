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
    <h3>Higher-Lower-Spiel (/game):</h3>
    Welches Wort wurde öfter im Podcast gesagt? Die Zahl eines Wortes ist dieselbe wie count_all der Suche. Alle POST-Routen nehmen form-encoded Bodies. Fehler kommen wie bei der Suche als HTTP 200 mit error = str. Ein Spiel verfällt nach 2 Stunden.<br>
    <h4>POST Request /game/start</h4>
    URL: https://api.hobbylos.online/game/start <br>
    Startet ein neues Spiel. Keine Parameter. Höchstens 60 Starts pro IP in 10 Minuten (error "rate limited").
    <h4>Response</h4>
    id = str (Spiel-ID für alle weiteren Requests)<br>
    score = int (0)<br>
    a = object { word = str, count = int }<br>
    b = object { word = str } (Zahl bleibt bis zum Tipp verborgen)
    <h4>POST Request /game/guess</h4>
    URL: https://api.hobbylos.online/game/guess <br>
    id = str (Spiel-ID)<br>
    guess = str "higher" (b öfter als a) oder "lower" (b seltener als a), bei Gleichstand zählt beides als richtig<br>
    round = int (aktueller score, schützt vor doppelt abgeschickten Tipps, sonst error "stale round")
    <h4>Response</h4>
    correct = bool<br>
    b_count = int (Zahl von b)<br>
    score = int<br>
    next = object { word = str } (nur bei richtigem Tipp: neues Wort, das bisherige b wird zu a)<br>
    over = bool (nur bei falschem Tipp: true, Spiel beendet)
    <h4>POST Request /game/state</h4>
    URL: https://api.hobbylos.online/game/state <br>
    id = str (Spiel-ID). Aktueller Stand, z. B. nach einem Verbindungsfehler.
    <h4>Response</h4>
    score = int<br>
    over = bool<br>
    submitted = bool (schon in die Rangliste eingetragen)<br>
    a = object { word = str, count = int }<br>
    b = object { word = str, count = int (nur wenn over) }
    <h4>POST Request /game/submit</h4>
    URL: https://api.hobbylos.online/game/submit <br>
    id = str (Spiel-ID)<br>
    name = str (2 bis 20 Zeichen, Buchstaben, Ziffern, Leerzeichen und . _ -, mindestens ein Buchstabe oder eine Ziffer)<br>
    Trägt ein beendetes Spiel mit score ab 1 in die Rangliste ein, einmal pro Spiel. Der Score kommt vom Server.
    <h4>Response</h4>
    rank = int (Platz in der Rangliste, null außerhalb der Top 100)<br>
    score = int
    <h4>GET Request /game/leaderboard</h4>
    URL: https://api.hobbylos.online/game/leaderboard <br>
    Top 20. Bei gleichem Score steht der frühere Eintrag oben. Keine Parameter.
    <h4>Response</h4>
    leaderboard = array [<br>
    ... name = str,<br>
    ... score = int,<br>
    ... date = str (YYYY-MM-DD),<br>
    ... ts = int (Unix-Zeit des Eintrags)<br>
    ]
    <h4>Fehler (error)</h4>
    "unknown game", "stale round", "game over", "invalid guess", "invalid round", "game not over", "already submitted", "score too low", "invalid name", "rate limited", "conflict" (paralleler Zug auf dasselbe Spiel), "game unavailable"
  </body>
</html>
