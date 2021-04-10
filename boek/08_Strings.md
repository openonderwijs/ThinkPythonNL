[community/ThinkPython/HoofdstukAcht - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht)

> # Hoofdstuk 8 Strings
> 
> ## 8.1 Een string is een rij
> 
> Een string is een **rij** van karakters. U kunt de karakters één voor één benaderen met de vierkante haken operator:
> 
> \>>> fruit = 'banaan'
> \>>> letter = fruit\[1\]
> 
> De tweede instructie selecteert karakter nummer 1 uit fruit en kent deze toe aan letter.
> 
> De expressie tussen vierkante haken wordt een **index** genoemd. De index wijst aan welk karakter uit de rij u wilt hebben (vandaar de naam).
> 
> Maar het kan zijn dat u niet krijgt wat u zou verwachten:
> 
> \>>> print letter
> a
> 
> Voor de meeste mensen is de eerste letter van 'banaan' de b en niet a. Maar voor computerwetenschappers is de index een uitloper van het begin van de string en uitloper van de eerste letter is nul.
> 
> \>>> letter = fruit\[0\]
> \>>> print letter
> b
> 
> Dus b is de 0de letter (“nulde”) van 'banaan', a is de 1ste letter (“eerste”) en n is de 2de (“tweede”) letter.
> 
> U kunt iedere expressie, inclusief variabelen en operatoren, als een index gebruiken, maar de waarde van de index moet altijd een integer (geheel getal) zijn. Anders krijgt u:
> 
> \>>> letter = fruit\[1.5\]
> TypeError: string indices must be integers
> 
> ## 8.2 len
> 
> len is een ingebouwde functie die het aantal karakters van een string teruggeeft:
> 
> \>>> fruit = 'banaan'
> \>>> len(fruit)
> 6
> 
> Om de laatste letter van een string op te halen, zou u geneigd zijn zoiets als dit te proberen:
> 
> \>>> lengte = len(fruit)
> \>>> laatste = fruit\[lengte\]
> IndexError: string index out of range
> 
> De reden voor de IndexError is dat in 'banaan’ geen letter voorkomt met de index 6. Omdat we beginnen te tellen met nul, zijn de zes letters genummerd 0 tot en met 5. Om de laatste letter te krijgen moet u 1 aftrekken van de lengte:
> 
> \>>> laatste = fruit\[length-1\]
> \>>> print laatste
> a
> 
> Een alternatief is het gebruik van negatieve indices, deze tellen dan terug vanaf het einde van de string. De expressie fruit\[-1\] brengt de laatste letter voort, fruit\[-2\] de op één na laatste, enzovoorts.
> 
> ## 8.3 Passage met een 'for' lus
> 
> Veel berekeningen hebben betrekking op het verwerken van één karakter per keer uit een string. Deze starten vaak aan het begin en selecteren elk karakter één voor één, doen er iets mee en gaan hiermee door tot aan het einde van de string. Dit patroon van verwerken wordt een **passage** genoemd. Eén manier om een passage te schrijven is met behulp van een while lus:
> 
> index = 0
> while index < len(fruit):
>      letter = fruit\[index\]
>      print letter
>      index = index + 1
> 
> Deze lus doorloopt de string en geeft elke letter op een eigen regel weer. De conditie van de lus is index < len(fruit), dus zodra de index gelijk is aan de lengte van de string, wordt de conditie 'false', en de body van de lus wordt niet uitgevoerd. Het laatste karakter dat wordt benaderd is degene met de index len(fruit)-1, dit is het laatste karakter in de string.
> 
> **Oefening 8.1** Schrijf een functie die een string oppakt als een argument en de letters achterstevoren weergeeft, één letter per regel.
> 
> Een andere manier om een passage te maken is met behulp van een for lus:
> 
> for karakter in fruit:
>      print karakter
> 
> Iedere omloop van de lus wordt het volgende karakter toegewezen aan de variabele karakter. De lus gaat door totdat er geen karakters meer over zijn.
> 
> Het volgende voorbeeld toont hoe aaneenrijging te gebruiken (optellen van een string) en een for lus bij het maken van een alfabetische reeks. In Robert [McCloskey](https://wiki.ubuntu-nl.org/McCloskey)’s boek _Make Way for Ducklings_, de namen van de eendjes zijn Jack, Kack, Lack, Mack, Nack, Ouack, Pack, en Quack.
> 
> Deze lus plaatst deze namen in de juiste volgorde:
> 
> voorvoegsels = 'JKLMNOPQ'
> achtervoegsel = 'ack'
> for letter in voorvoegsels :
>      print letter + achtervoegsel 
> 
> The output is:
> 
> Jack
> Kack
> Lack
> Mack
> Nack
> Oack
> Pack
> Qack
> 
> Dit is natuurlijk niet echt goed omdat "Ouack" en "Quack" verkeerd zijn gespeld.
> 
> **Oefening 8.2** Pas het programma aan om deze fout te herstellen.
> 
> ## 8.4 String plakjes
> 
> Een onderdeel van een string wordt een **plakje** genoemd. Het selecteren van een plakje gaat op dezelfde manier als het selecteren van een karakter:
> 
> \>>> s = 'Monty Python'
> \>>> print s\[0:5\]
> Monty
> \>>> print s\[6:13\]
> Python
> 
> De operator \[n:m\] geeft het deel van de string terug van het "n-de" karakter tot het "m-de" karakter, inclusief het eerste maar exclusief het laatste karakter. Dit gedrag druist in tegen de intuïtie, maar het kan helpen om te bedenken dat de indices iets tussen de karakters in aanwijzen, zoals te zien in het volgende diagram:
> 
> -   ![boek011_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht?action=AttachFile&do=get&target=boek011_nl.png "boek011_nl.png")
>     
> 
> Als u de eerste index (voor de komma) weglaat, start het partje bij het begin van de string. Laat u de tweede index weg dan gaat het plakje tot het einde van de string:
> 
> \>>> fruit = 'banaan'
> \>>> fruit\[:3\]
> 'ban'
> \>>> fruit\[3:\]
> 'aan'
> 
> Als de eerste index groter of gelijk is aan de tweede zal het resultaat een **lege string** zijn, weergegeven door twee aanhalingstekens:
> 
> \>>> fruit = 'banaan'
> \>>> fruit\[3:3\]
> ''
> 
> Een lege string bevat geen karakters en heeft een lengte 0; behalve dat, is deze gelijk aan iedere andere string.
> 
> **Oefening 8.3** Gegeven dat fruit een string is, wat betekent fruit\[:\]?
> 
> ## 8.5 Strings zijn onveranderbaar
> 
> Het is verleidelijk om de \[\] operator aan de linker zijde van een toewijzing te gebruiken met de intentie om een karakter te wijzigen in een string. Bijvoorbeeld:
> 
> \>>> begroeting = 'Hello, world!'
> \>>> begroeting\[0\] = 'J'
> TypeError: object does not support item assignment
> 
> Het "object" in deze zaak is de string en het "item" is het karakter dat u probeerde toe te wijzen. Voor dit moment geldt: een **object** is hetzelfde ding als een waarde maar we zullen dit later nuanceren. Een **item** is één van de waarden in een reeks.
> 
> De reden voor de fout is dat strings **onveranderbaar** zijn; dit betekent dat u niets kunt veranderen aan een bestaande string. Het beste wat u kunt doen, is een nieuwe string aanmaken die een variatie is op het origineel:
> 
> \>>> begroeting = 'Hello, world!'
> \>>> nieuwe\_begroeting = 'J' + begroeting\[1:\]
> \>>> print nieuwe\_begroeting
> Jello, world!
> 
> Dit voorbeeld rijgt een nieuwe eerste letter aan een plakje van begroeting. Dit heeft geen effect op de originele string.
> 
> ## 8.6 Zoeken
> 
> Wat doet de volgende functie?
> 
> function isnumbered(obj) { return obj.childNodes.length && obj.firstChild.childNodes.length && obj.firstChild.firstChild.className == 'LineNumber'; } function nformat(num,chrs,add) { var nlen = Math.max(0,chrs-(''+num).length), res = ''; while (nlen>0) { res += ' '; nlen-- } return res+num+add; } function addnumber(did, nstart, nstep) { var c = document.getElementById(did), l = c.firstChild, n = 1; if (!isnumbered(c)) { if (typeof nstart == 'undefined') nstart = 1; if (typeof nstep == 'undefined') nstep = 1; var n = nstart; while (l != null) { if (l.tagName == 'SPAN') { var s = document.createElement('SPAN'); var a = document.createElement('A'); s.className = 'LineNumber'; a.appendChild(document.createTextNode(nformat(n,4,''))); a.href = '#' + did + '\_' + n; s.appendChild(a); s.appendChild(document.createTextNode(' ')); n += nstep; if (l.childNodes.length) { l.insertBefore(s, l.firstChild); } else { l.appendChild(s); } } l = l.nextSibling; } } return false; } function remnumber(did) { var c = document.getElementById(did), l = c.firstChild; if (isnumbered(c)) { while (l != null) { if (l.tagName == 'SPAN' && l.firstChild.className == 'LineNumber') l.removeChild(l.firstChild); l = l.nextSibling; } } return false; } function togglenumber(did, nstart, nstep) { var c = document.getElementById(did); if (isnumbered(c)) { remnumber(did); } else { addnumber(did,nstart,nstep); } return false; } document.write('<a href="#" onclick="return togglenumber(\\'CA-3429344ad0eabf87cc3c5eb58b89cc0a7fb9b733\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3429344ad0eabf87cc3c5eb58b89cc0a7fb9b733_1) def vinden(woord, letter):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3429344ad0eabf87cc3c5eb58b89cc0a7fb9b733_2)      index = 0
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3429344ad0eabf87cc3c5eb58b89cc0a7fb9b733_3)      while index < len(woord):
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3429344ad0eabf87cc3c5eb58b89cc0a7fb9b733_4)            if woord\[index\] == letter:
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3429344ad0eabf87cc3c5eb58b89cc0a7fb9b733_5)                 return index
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3429344ad0eabf87cc3c5eb58b89cc0a7fb9b733_6)            index = index + 1
>  [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3429344ad0eabf87cc3c5eb58b89cc0a7fb9b733_7)      return -1
> 
> In zekere zin is vinden het tegenovergestelde van de \[\] operator. In plaats van met behulp van de index een overeenkomstig karakter op te halen, gebruikt deze functie een karakter om de index te zoeken die daarmee overeenkomt. Wordt het karakter niet gevonden dan geeft de functie \-1 terug.
> 
> Dit is het eerste voorbeeld van een return instructie binnenin een lus. Zodra {{{woord\[index\] == letter}}} waar is, breekt de functie uit de lus en keert de functie onmiddellijk terug.
> 
> Komt het karakter niet voor in de string dan zal het programma de lus normaal doorlopen en een \-1 teruggeven.
> 
> Dit patroon waarbij een reeks tijdens het passeren wordt berekend en terugkeert zodra gevonden is wat wordt gezocht, wordt een zoektocht genoemd.
> 
> **Oefening 8.4** Verander vinden zodanig dat deze over een derde parameter beschikt, de index in woord waar deze zou moeten beginnen met zoeken.
> 
> ## 8.7 Lussen en tellen
> 
> Het volgende programma telt het aantal keren dat een letter voorkomt in een string:
> 
> woord = 'banaan'
> teller = 0
> for letter in woord:
>       if letter == 'a':
>            teller = teller+ 1
> print teller
> 
> Dit programma demonstreert een ander patroon van verwerken, genaamd een **teller**. De variabele teller is geïnitialiseerd op 0 en vervolgens iedere keer opgehoogd zodra een a is gevonden. Zodra de lus afloopt, bevat teller het resultaat: namelijk het totaal aantal a’s.
> 
> **Oefening 8.5** breng deze code onder in een functie genaamd teller en generaliseer deze zodanig dat het de string en een letter als argumenten accepteert.
> 
> **Oefening 8.6** Herschrijf deze functie zodanig dat in plaats van het laten passeren van de string, deze de drie-parameter versie uit de voorgaande versie van vinden gebruikt.
> 
> ## 8.8 String methodes
> 
> Een **methode** is gelijk aan een functie — deze krijgt argumenten en geeft een waarde terug — maar de zinsbouw is anders. Bijvoorbeeld: de methode upper krijgt een string en geeft een nieuwe string terug, die de originele string is in hoofdletters; in het Engels heet zo'n string een string in 'uppercase':
> 
> In plaats van de functie zinsbouw upper(woord), gebruikt de methode de zinsbouw woord.upper().
> 
> \>>> woord = 'banaan'
> \>>> nieuw\_woord = woord.upper()
> \>>> print nieuw\_woord
> BANAAN
> 
> Deze manier van punt notatie specificeert de naam van de methode, kapitaal en de naam van de string om aan de methode toe te kennen woord. De lege haakjes geven aan dat deze methode geen argumenten krijgt.
> 
> Een methodeaanroep wordt een **aanroeping** genoemd, in dit geval kunnen we zeggen dat we upper aanroepen met woord.
> 
> Er is ook een methode genaamd find, deze is uiteraard gelijk aan de functie die we hebben gemaakt:
> 
> \>>> woord = 'banaan'
> \>>> index = woord.find('a')
> \>>> print index
> 1
> 
> In dit voorbeeld roepen we find aan met woord en geven de letter, die we zoeken, door als parameter.
> 
> Eigenlijk is de find methode meer generiek dan onze functie; de methode kan ook substrings vinden en niet alleen karakters:
> 
> \>>> woord.find('na')
> 2
> 
> Het kan een tweede argument mee krijgen, namelijk de index waarop moet worden gestart met zoeken:
> 
> \>>> woord.find('na', 3)
> 4
> 
> En als derde argument de index waar het zoeken moet eindigen:
> 
> \>>> naam = "bob"
> \>>> naam.find('b', 1, 2)
> \-1
> 
> Deze doorzoeking gaat fout omdat 'b' niet voorkomt in de index reeks van 1 tot 2 ( (2 hoort er niet bij ).
> 
> **Oefening 8.7** Er bestaat een string methode genaamd count die hetzelfde doet als de functie in de voorgaande oefening. Lees de documentatie over deze methode en doe een aanroep die de a's in 'banaan' telt.
> 
> ## 8.9 De 'in' operator
> 
> Het woord in is een booleaanse operator die twee strings krijgt en True teruggeeft als de eerste string als substring voorkomt in de tweede string:
> 
> \>>> 'a' in 'banaan'
> True
> \>>> 'zaad' in 'banaan'
> False
> 
> Bijvoorbeeld: de volgende functie print alle letters van woord1 die ook voorkomen in woord2:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-3a550a0581d8c6788fc8b879de4a9b752e43d038\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3a550a0581d8c6788fc8b879de4a9b752e43d038_1) def in\_beide(woord1, woord2):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3a550a0581d8c6788fc8b879de4a9b752e43d038_2)       for letter in woord1:
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3a550a0581d8c6788fc8b879de4a9b752e43d038_3)            if letter in woord2:
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-3a550a0581d8c6788fc8b879de4a9b752e43d038_4)                  print letter
> 
> Met goed gekozen namen voor variabelen, leest Python soms net als Nederlands met een Engels accent. U kunt de lus lezen als, “for (voor iedere) letter in (het eerste) woord, if (als de) letter (voorkomt) in (het tweede) woord, print (deze) letter.”
> 
> Dit is wat u krijgt als u appels met peren vergelijkt:
> 
> \>>> in\_beide('appels', 'peren')
> p
> e
> 
> ## 8.10 String vergelijking
> 
> De vergelijkingsoperatoren werken ook op strings. Om te kijken of twee strings gelijk zijn:
> 
> if woord == 'banaan':
>      print 'Oké, bananen!'
> 
> Andere vergelijkingshandelingen zijn nuttig om woorden in alfabetische volgorde te zetten:
> 
> if woord < "banaan":
>      print "Uw woord," + woord + ", komt voor banaan."
> elif woord > "banaan":
>      print "Uw woord," + woord + ", komt na banaan."
> else:
>      print "Goed, bananen."
> 
> Python behandelt hoofd- en kleine letters niet op dezelfde manier zoals mensen dat doen. Alle hoofdletters komen voor de kleine letters, dus:
> 
> Uw woord, Mandarijn, komt voor banaan.
> 
> Een gebruikelijke manier om dit probleem te omzeilen, is de strings naar een standaardformaat om te zetten, bijvoorbeeld allemaal kleine letters, voordat een vergelijking wordt uitgevoerd. Houdt dit in gedachten om u te verdedigen tegen een man met een Mandarijn.
> 
> ## 8.11 Debuggen
> 
> Gebruikt u indices om de waarden te laten passeren in een reeks, dan is het lastig om het begin en het einde van een passage goed te kiezen. Hier is een functie waarbij het de bedoeling is om twee woorden te vergelijken en True terug te geven als een van de woorden het omgekeerde is van de ander, maar deze functie bevat twee fouten:
> 
> def is\_omgekeerde(woord1, woord2):
>     if len(woord1) != len(woord2):
>         return False
>     i = 0
>     j = len(woord2)
>     while j > 0:
>         if woord1\[i\] != woord2\[j\]:
>             return False
>         i = i+1
>         j = j-1
>     return True
> 
> De eerste if instructie controleert of de woorden even lang zijn. Zo niet, dan geven we onmiddellijk False terug en voor de rest van de functie nemen we aan dat de woorden even lang zijn. Dit is een voorbeeld van het wachter patroon in Sectie 6.8.
> 
> i en j zijn indices: i laat woord1 naar voren lopen terwijl j woord2 naar achteren laat lopen. Vinden we twee letters die niet gelijk zijn, dan geven we direct een False terug. Komen we door de hele lus en alle letters zijn gelijk, dan geven we True terug.
> 
> Als we deze functie testen met de woorden “pots” en “stop”, dan verwachten we de waarde True terug te krijgen maar we krijgen een [IndexError](https://wiki.ubuntu-nl.org/IndexError):
> 
> \>>> is\_omgekeerde('pots', 'stop')
> ...
>     File "reverse.py", line 15, in is\_omgekeerde
>         if woord1\[i\] != woord2\[j\]:
> IndexError: string index out of range
> 
> Om dit soort fouten te debuggen, is onze eerste actie het printen van de waarden van de indices direct voor de regel waar de fout optreedt.
> 
>     while j > 0:
>         print i, j              # print here
>         if woord1\[i\] != woord2\[j\]:
>             return False
>         i = i+1
>         j = j-1
> 
> Voer ik het programma nu opnieuw uit dan krijg ik meer informatie:
> 
> \>>> is\_omgekeerde('pots', 'stop')
> 0 4
> ...
> IndexError: string index out of range
> 
> In de eerste ronde door de lus is de waarde van j 4; dit is buiten het bereik van de string 'pots'. De index van het laatste karakter is 3, dus de beginwaarde voor j moet len(woord2)-1 zijn.
> 
> Als ik deze fout oplos en het programma opnieuw uitvoer krijg ik:
> 
> \>>> is\_omgekeerde('pots', 'stop')
> 0 3
> 1 2
> 2 1
> True
> 
> Deze keer krijgen we het goede antwoord, maar het lijkt erop dat de lus maar drie keer wordt doorlopen; dat is verdacht. Om een beter idee te krijgen van wat er gebeurt, is het handig om een statusdiagram te tekenen. Tijdens de eerste passage lijkt het blok voor is\_omgekeerde op het volgende:
> 
> i 0 j 3
> woord1 "pots" woord2 "stop"
> 
> Ik veroorloofde mij om de variabelen in het blok netjes te rangschikken en via het stippellijntje is te zien dat de waarden van i en j aangeven waar het karakter in woord1 en woord2 zit.
> 
> **Oefening 8.8** Begin met dit diagram, voer het programma uit op papier, verander de waarden van i en j gedurende elke herhaling. Zoek de fout in de functie en verbeter deze.
> 
> ## 8.12 Woordenlijst
> 
> **object:** Iets waar een variabele naar kan verwijzen. Voor dit moment kunt u een "object" en een "waarde" door elkaar gebruiken.
> 
> **reeks:** Een geordende set; dat wil zeggen een set waarden waarbij elke waarde is geïdentificeerd door een integer index.
> 
> **item:** Een van de waarden in een reeks.
> 
> **index:** Een integer waarde gebruikt om een item te selecteren uit een reeks, zoals een karakter uit een string.
> 
> **plakje:** Een deel van een string gespecificeerd door het bereik van indices.
> 
> **lege string:** Een string zonder karakter en met lengte 0, weergegeven door twee aanhalingstekens.
> 
> **onveranderbaar:** De eigenschap van een reeks waarbij zijn items niet toegewezen kunnen worden.
> 
> **traverse:** Sequentieel alle items doorlopen en een operatie op alle items uitvoeren.
> 
> **zoek:** Een patroon van een passage die stopt zodra het gezochte gevonden is.
> 
> **teller:** Een variabele die wordt gebruikt om iets te tellen; wordt normaal gesproken op nul gezet en daarna opgehoogd.
> 
> **methode:** Een functie die verwant is aan een object en wordt aangeroepen met puntnotatie.
> 
> **aanroeping:** Een instructie die een methode aanroept.
> 
> ## 8.13 Oefeningen
> 
> **Oefening 8.9** Een plakje van een string kan een derde index krijgen waarmee de "stapgrootte" gespecificeerd wordt, dat wil zeggen het aantal spaties tussen de opeenvolgende karakters. Een stapgrootte van 2 betekent elk tweede karakter en 3 betekent elk derde enzovoorts.
> 
> \>>> fruit = 'banaan'
> \>>> fruit\[0:5:2\]
> 'bna'
> 
> Een stapgrootte van -1 gaat achterwaarts door het woord, dus het plakje \[::-1\] genereert een omgekeerde string. Gebruik deze taaleigenaardigheid van Python om een eenregelige versie van is\_palindroom te maken uit oefening 6.6.
> 
> **Oefening 8.10** Lees de documentatie over de string methoden op [docs.python.org/lib/string-methods.html](http://docs.python.org/lib/string-methods.html). Het is de overweging waard om wat te experimenteren met deze methoden om er zeker van te zijn dat u begrijpt hoe deze werken. Bijzonder nuttig zijn strip en replace.
> 
> De documentatie gebruikt een zinsbouw die mogelijk verwarring schept. Bijvoorbeeld: in find(sub\[, start\[, end\]\]), De haakjes geven aan dat parameters optioneel zijn. Dus sub is verplicht maar start is optioneel en als u start toevoegt, is end optioneel.
> 
> **Oefening 8.11** De volgende functies zijn allemaal _bedoeld_ om te controleren of een string kleine letters bevat maar enkelen zijn zeker fout. Beschrijf voor elke functie wat deze eigenlijk doet (aangenomen dat de parameter een string is).
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_1) def kleingletters1(s):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_2)     for c in s:
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_3)         if c.islower():
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_4)             return True
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_5)         else:
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_6)             return False
>  [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_7) 
>  [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_8) def kleingletters2(s):
>  [9](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_9)     for c in s:
>  [10](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_10)         if 'c'.islower():
>  [11](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_11)             return 'True'
>  [12](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_12)         else:
>  [13](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_13)             return 'False'
>  [14](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_14) 
>  [15](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_15) def kleingletters3(s):
>  [16](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_16)     for c in s:
>  [17](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_17)         flag = c.islower()
>  [18](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_18)     return flag
>  [19](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_19) 
>  [20](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_20) def kleingletters4(s):
>  [21](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_21)     flag = False
>  [22](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_22)     for c in s:
>  [23](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_23)         flag = flag or c.islower()
>  [24](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_24)     return flag
>  [25](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_25) 
>  [26](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_26) def kleingletters5(s):
>  [27](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_27)     for c in s:
>  [28](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_28)         if not c.islower():
>  [29](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_29)             return False
>  [30](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAcht#CA-8f15b0d673f218cbcde6aacd9bb9924d248edfaa_30)     return True
> 
> **Oefening 8.12** ROT13 is een zwakke vorm van encryptie (versleuteling) die niets anders doet dan elke letter in een woord 13 plaatsen “verwisselen”1 . Een letter verwisselen, houdt in dat we door het alfabet moeten schuiven en dan terug keren naar het begin, dus een ’A’ doorschuiven met 3 is ’D’ en ’Z’ doorschuiven met 1 is ’A’.
> 
> Schrijf een functie genaamd roteer\_woord die een string en een integer als parameters krijgt en die een nieuwe string teruggeeft waarbij de letters van de originele string doorgeschoven zijn met een gegeven aantal.
> 
> Bijvoorbeeld: “cheer” doorgeschoven met 7 is “jolly” en “melon” doorgeschoven met -10 is “cubed”.
> 
> U wilt mogelijk de ingebouwde functies gebruiken zoals ord, die een karakter omzet naar een numerieke code en chr, die een numerieke code omzet naar karakters.
> 
> Mogelijk beledigende grappen zijn soms versleuteld met ROT13. Voelt u zich niet zo snel beledigd, zoek dan een aantal op en decodeer deze.
> 
> * * *
> 
> 1 Zie [nl.wikipedia.org/wiki/Rot13](http://nl.wikipedia.org/wiki/Rot13)