<html>
  <body>
    <h1>Hobbylos search engine</h1>
    Die neue Hobbylos Suche.<br><br>
    <h3>Was ist neu?</h3>
    <b>- Designe</b><br>
    Für das neue Design hat <a href="https://instagram.com/claudia.sofia_02/" target="_blank">@claudia.sofia_02</a> ein Template erstellt, sodass ich nur noch die Funktionen hinzufügen musste. <br>
    Dabei musste ich leider auf ein paar schöne Details verzichten.<br>
    <b>- Backend</b><br>
    Das Backend ist komplett neu geschrieben und setzt auf einen Indexsuchansatz (ähnlich wie Google und Co).<br>
    Vorteile: <br>
    - wehsentlich schneller <br>
    - genauer <br>
    - Sortierung nach Relevanz <br>
    - Suche nach Sätzen besser möglich <br>
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
