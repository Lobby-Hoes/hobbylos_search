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
    limit = int (response limit)(optional)
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
  </body>
</html>
