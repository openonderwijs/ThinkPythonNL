[community/ThinkPython/HoofdstukTien - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTien)

> # Hoofdstuk 10 Lijsten
> 
> ## 10.1 Een lijst is een reeks
> 
> Net zoals een string is een **lijst** een reeks waarden. Bij een string zijn de waarden karakters, bij een lijst is ieder type toegestaan. De waarden in een lijst worden **elementen** genoemd en soms **items**.
> 
> Er bestaan verschillende manieren om een nieuwe lijst aan te maken; de eenvoudigste manier is de elementen insluiten tussen vierkante haken (\[ en \]):
> 
> \[10, 20, 30, 40\]
> \['goud', 'zilver', 'brons'\]
> 
> Het eerste voorbeeld is een lijst met 4 gehele getallen. Het tweede is een lijst met 3 strings. De elementen van een lijst hoeven niet van hetzelfde type te zijn. De volgende lijst bevat een string, een float, een geheel getal en een lijst:
> 
> \['spam', 2.0, 5, \[10, 20\]\]
> 
> Een lijst binnen een andere lijst heet **genest**.
> 
> Een lijst zonder elementen wordt een lege lijst genoemd; zo'n lijst wordt aangemaakt door niets tussen de haakjes te plaatsen \[\].
> 
> Zoals te verwachten was, kunt u een lijst met waarden aan een variabele toekennen:
> 
> \>>> kazen = \['Cheddar', 'Edam', 'Gouda'\]
> \>>> getallen = \[17, 123\]
> \>>> leeg = \[\]
> \>>> print kazen, getallen, leeg
> \['Cheddar', 'Edam', 'Gouda'\] \[17, 123\] \[\]
> 
> ## 10.2 Lijsten zijn aan te passen
> 
> De zinsbouw voor het benaderen van elementen in een lijst komt overeen met zinsbouw voor het benaderen van een karakter in een string. De expressie tussen de haakjes geeft de index weer. Denk eraan dat de indices met 0 beginnen:
> 
> \>>> print kazen\[0\]
> Cheddar
> 
> Anders dan bij strings zijn lijsten aan te passen. Wordt met haken gewerkt aan de linkerkant van een toewijzing, dan wordt daarmee het element aangewezen, dat zal worden gewijzigd.
> 
> \>>> getallen = \[17, 123\]
> \>>> getallen\[1\] = 5
> \>>> print getallen
> \[17, 5\]
> 
> Het 1ste element van getallen, dat 123 bevatte, is nu 5.
> 
> Denk aan een lijst als aan een relatie tussen indices en elementen. Deze relatie wordt een **positionering** genoemd; elke index is te "positioneren" op één van de elementen. Hierbij een statusdiagram dat kazen, getallen en leeg weergeeft:
> 
> -   ![boek013_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTien?action=AttachFile&do=get&target=boek013_nl.png "boek013_nl.png")
>     
> 
> Lijsten worden weergegeven door blokken met het woord "lijst" aan de buitenkant en elementen van de lijst erin. kazen verwijst naar een lijst met drie elementen, geïndexeerd 0, 1 en 2. getallen bevat twee elementen; het diagram geeft aan dat de waarde van het tweede element gewijzigd is van 123 naar 5. leeg verwijst naar een lijst zonder elementen.
> 
> Indices van een lijst werken op dezelfde manier als indices van strings:
> 
> -   Iedere integer expressie (die dus een geheel getal oplevert) kan dienen als index.
> -   Lezen en/of schrijven van niet bestaande elementen levert een foutboodschap op: IndexError.
>     
> -   Krijgt een index een negatieve waarde dan zal deze terugtellen vanaf het einde van de lijst.
> 
> De in operator werkt ook op lijsten.
> 
> \>>> kazen = \['Cheddar', 'Edam', 'Gouda'\]
> \>>> 'Edam' in kazen
> True
> \>>> 'Brie' in kazen
> False
> 
> ## 10.3 Een lijst doorlopen
> 
> De meest gebruikelijke manier om door de elementen van een lijst te lopen, is met een for lus. De zinsbouw komt overeen met die voor strings:
> 
> for kaas in kazen:
>       print kaas 
> 
> Dit werkt prima als u alleen de elementen uit een lijst wilt lezen. Maar als u de elementen wilt wegschrijven of bijwerken, hebt u de indices nodig. Een gebruikelijke manier om dit te bereiken, is door de functies range en len te combineren:
> 
> for i in range(len(getallen)):
>       getallen\[i\] = getallen\[i\] \* 2
> 
> Deze lus doorloopt de lijst en werkt elk element bij. len geeft het aantal elementen in de lijst terug. range geeft een lijst met indices van 0 tot _n_ − 1 terug; hierbij is _n_ de lengte van de lijst. Bij iedere omloop van de lus krijgt i de index van het volgende element. De toewijsinstructie in de body gebruikt i om de oude waarde van het element te lezen en de nieuwe waarde toe te kennen.
> 
> Een for lus toegepast op een lege lijst zal nooit bij de body komen om deze uit te voeren:
> 
> for x in leeg:
>       print 'Dit komt nooit voor.'
> 
> Hoewel een lijst een andere lijst kan bevatten zal die lijst slechts als een enkel element tellen. De lengte van deze lijst is vier:
> 
> \['spam', 1, \['Brie', 'Roquefort', 'Pol le Veq'\], \[1, 2, 3\]\]
> 
> ## 10.4 Bewerkingen op een lijst
> 
> De + operator voegt lijsten samen:
> 
> \>>>   a = \[1, 2, 3\]
> \>>>   b = \[4, 5, 6\]
> \>>>   c = a + b
> \>>>   print c
> \[1, 2, 3, 4, 5, 6\]
> 
> Op dezelfde manier, herhaalt de \* operator een lijst het gegeven aantal malen:
> 
> \>>>   \[0\] \* 4
> \[0, 0, 0, 0\]
> \>>>   \[1, 2, 3\] \* 3
> \[1, 2, 3, 1, 2, 3, 1, 2, 3\]
> 
> Het eerste voorbeeld herhaalt \[0\] vier keer. Het tweede voorbeeld herhaalt de lijst \[1, 2, 3\] drie keer.
> 
> ## 10.5 Partjes uit een Lijst
> 
> De operator die een partje uit een string haalt, werkt ook op een lijst:
> 
> \>>> t = \['a', 'b', 'c', 'd', 'e', 'f'\]
> \>>> t\[1:3\]
> \['b', 'c'\]
> \>>> t\[:4\]
> \['a', 'b', 'c', 'd'\]
> \>>> t\[3:\]
> \['d', 'e', 'f'\]
> 
> Laat u de eerste index achterwege, dan start het partje aan het begin. Laat u de tweede index achterwege, dan zal het partje tot aan het einde doorlopen. Dus als u beide weglaat, is het partje een kopie van de lijst.
> 
> \>>> t\[:\]
> \['a', 'b', 'c', 'd', 'e', 'f'\]
> 
> Omdat lijsten aan te passen zijn, is het meestal handig om een kopie te maken voordat allerlei bewerkingen de lijst gaan verbouwen.
> 
> Een operator voor partjes aan de linkerzijde van de toewijzing kan meerdere elementen bijwerken:
> 
> \>>> t = \['a', 'b', 'c', 'd', 'e', 'f'\]
> \>>> t\[1:3\] = \['x', 'y'\]
> \>>> print t
> \['a', 'x', 'y', 'd', 'e', 'f'\]
> 
> ## 10.6 Methoden voor een lijst
> 
> Python levert methoden die werken op lijsten. Bijvoorbeeld: append voegt een nieuw element toe aan het einde van een lijst:
> 
> \>>> t = \['a', 'b', 'c'\]
> \>>> t.append('d')
> \>>> print t
> \['a', 'b', 'c', 'd'\]
> 
> extend krijgt een lijst mee als een argument en voegt alle elementen toe:
> 
> \>>> t1 = \['a', 'b', 'c'\]
> \>>> t2 = \['d', 'e'\]
> \>>> t1.extend(t2)
> \>>> print t1
> \['a', 'b', 'c', 'd', 'e'\]
> 
> Dit voorbeeld laat t2 ongewijzigd.
> 
> sort ordent de elementen uit de lijst van laag naar hoog:
> 
> \>>> t = \['d', 'c', 'e', 'b', 'a'\]
> \>>> t.sort()
> \>>> print t
> \['a', 'b', 'c', 'd', 'e'\]
> 
> Lijstmethoden zijn lege methoden; ze wijzigen de lijst en geven niets None terug. Als u per ongeluk t = t.sort() opschrijft, zult u teleurgesteld zijn over het resultaat.
> 
> ## 10.7 Positioneer, filter en reduceer
> 
> U kunt de onderstaande lus gebruiken voor het ophogen van alle getallen in een lijst:
> 
> def alles\_ophogen(t):
>       totaal = 0
>       for x in t:
>             totaal += x
>       return totaal
> 
> totaal krijgt de begin waarde 0. Ieder keer dat de lus doorlopen wordt, krijgt x het volgende element uit de lijst. De += operator is een verkorte manier om een variabele bij te werken:
> 
>  totaal += x
> 
> komt overeen met:
> 
>  totaal = totaal + x
> 
> Bij het doorlopen van de lus zal totaal de som van de elementen opeenstapelen; een variabele op deze manier gebruiken, wordt ook wel een **opeenstapelaar** (accumulator) genoemd. Het optellen van elementen uit een lijst is zo'n veelgebruikte bewerking dat Python deze levert als een ingebouwde functie, sum:
> 
> \>>> t = \[1, 2, 3\]
> \>>> sum(t)
> 6
> 
> Een bewerking zoals deze, die een reeks elementen samenvoegt tot één enkele waarde, wordt ook wel **reduceren** genoemd.
> 
> Soms wilt u een lijst doorlopen en gelijktijdig een andere lijst opbouwen. Bijvoorbeeld: de volgende functie krijgt een lijst met strings en geeft een nieuwe lijst terug met strings in hoofdletters:
> 
> def hoofdletters(t):
>       resultaat = \[\]
>       for s in t:
>             resultaat.append(s.capitalize())
>       return resultaat
> 
> resultaat is bij aanvang een lege lijst; elke keer dat de lus wordt doorlopen, voegen we het volgende element toe. Dus resultaat is een soort opeenstapelaar.
> 
> Een bewerking zoals hoofdletters wordt ook wel een **positie** (map) genoemd, omdat deze een functie (in dit voorbeeld de methode capitalize) over elk element in de reeks legt.
> 
> Een andere gemeenschappelijke bewerking is het selecteren van enkele elementen uit de lijst en een sublijst teruggeven. Bijvoorbeeld: de volgende functie krijgt een lijst met strings en geeft er één terug met alleen die strings, die uit hoofdletters bestaan:
> 
> def alleen\_hoofdletters(t):
>       resultaat = \[\]
>       for s in t:
>            if s.isupper():
>                 resultaat.append(s)
>       return resultaat 
> 
> isupper is een stringmethode die True teruggeeft als de string alleen hoofdletters bevat.
> 
> Een dergelijke bewerking alleen\_hoofdletters wordt een **filter** genoemd, omdat deze sommige elementen uit de lijst filtert.
> 
> De gebruikelijke bewerkingen op een lijst kunnen als combinatie van positioneren, filteren en reduceren optreden. Omdat deze bewerkingen zo'n gemeengoed zijn, levert Python hiervoor ondersteuning in zijn taal, inclusief de ingebouwde functie map en een operator "list comprehension" genoemd.
> 
> **Oefening 10.1** Schrijf een functie die een lijst met getallen meekrijgt en de cumulatieve optelsom teruggeeft, dus een nieuwe lijst waarbij het _i_ste element de som is van de eerste _i_ + 1 elementen van de oorspronkelijke lijst. Bijvoorbeeld: de cumulatieve optelsom van \[1, 2, 3\] is \[1, 3, 6\].
> 
> ## 10.8 Elementen verwijderen
> 
> Het verwijderen van elementen uit een lijst kan op verschillende manieren. Kent u de index van een element, dan kunt u pop gebruiken:
> 
> \>>> t = \['a', 'b', 'c'\]
> \>>> x = t.pop(1)
> \>>> print t
> \['a', 'c'\]
> \>>> print x
> b
> 
> pop wijzigt de lijst en geeft het element terug dat verwijderd is. Geeft u geen index op dan wordt het laatste element teruggegeven en verwijderd.
> 
> Hebt u het verwijderde element niet nodig dan kunt u del gebruiken:
> 
> \>>> t = \['a', 'b', 'c'\]
> \>>> del t\[1\]
> \>>> print t
> \['a', 'c'\]
> 
> Kent u wel het element maar niet de index dan kunt u remove gebruiken:
> 
> \>>> t = \['a', 'b', 'c'\]
> \>>> t.remove('b')
> \>>> print t
> \['a', 'c'\]
> 
> De antwoordwaarde van remove is None.
> 
> Voor het verwijderen van meerdere elementen kunt u del gebruiken met de index voor partjes:
> 
> \>>> t = \['a', 'b', 'c', 'd', 'e', 'f'\]
> \>>> del t\[1:5\]
> \>>> print t
> \['a', 'f'\]
> 
> Zoals gebruikelijk selecteert een partje alle elementen tot aan de tweede index, deze telt dus niet mee.
> 
> ## 10.9 Lijsten en strings
> 
> Een string is een serie karakters en een lijst is een reeks waarden maar een lijst met karakters is niet hetzelfde als een string. Voor het omzetten van een string naar een lijst met karakters gebruikt u list:
> 
> \>>> s = 'spam'
> \>>> t = list(s)
> \>>> print t
> \['s', 'p', 'a', 'm'\]
> 
> Omdat list de naam is van een ingebouwde functie moet u deze naam niet als een variabele gebruiken. Ook het gebruik van l is niet handig omdat deze erg veel op 1 lijkt. Daarom wordt hier t gebruikt.
> 
> De list functie breekt een string op in individuele letters. Wilt u een string omzetten in woorden, maak dan gebruik van de methode split:
> 
> \>>> s = 'de bal is rond'
> \>>> t = s.split()
> \>>> print t
> \['de', 'bal', 'is', 'rond'\]
> 
> Een optioneel argument scheidingsteken (delimiter) genoemd, geeft aan welk karakter als onderscheiding tussen de woorden moet worden gebruikt. Het volgende voorbeeld gebruikt een verbindingsstreepje als **scheidingsteken**:
> 
> \>>> s = 'spam-spam-spam'
> \>>> scheidingsteken = '-'
> \>>> s.split(scheidingsteken)
> \['spam', 'spam', 'spam'\]
> 
> join is het tegenovergestelde van split. Deze krijgt een lijst met strings en schakelt de elementen aaneen. join is een stringmethode, dus moet u een beroep doen op het scheidingsteken en de lijst doorgeven als een parameter:
> 
> \>>> t = \['de', 'bal', 'is', 'rond'\]
> \>>> scheidingsteken = ' '
> \>>> scheidingsteken.join(t)
> 'de bal is rond'
> 
> In dit geval is het scheidingsteken een spatie, dus join plaatst een spatie tussen de woorden. Een string aaneenschakelen zonder spaties kan door een lege string '' als scheidingsteken mee te geven.
> 
> ## 10.10 Objecten en waarden
> 
> Voeren we een toewijsinstructie uit zoals:
> 
> a = 'banaan'
> b = 'banaan'
> 
> Weten we dat a en b beide verwijzen naar een string maar we weten niet of deze naar dezelfde string verwijzen. Er bestaan twee opties voor de status:
> 
> -   ![boek014_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTien?action=AttachFile&do=get&target=boek014_nl.png "boek014_nl.png")
>     
> 
> In het ene geval verwijzen a en b naar twee verschillende objecten met dezelfde waarde. In het tweede geval verwijzen zij naar hetzelfde object.
> 
> De controle, of de twee variabelen naar hetzelfde object verwijzen, wordt met de is operator uitgevoerd.
> 
> \>>> a = 'banaan'
> \>>> b = 'banaan'
> \>>> a is b
> True
> 
> In dit voorbeeld maakt Python maar één string object aan en beide a en b verwijzen hiernaar.
> 
> Maar maakt u twee lijsten aan dan krijgt u ook twee objecten:
> 
> \>>> a = \[1, 2, 3\]
> \>>> b = \[1, 2, 3\]
> \>>> a is b
> False
> 
> Het statusdiagram lijkt hierop:
> 
> -   ![book015.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTien?action=AttachFile&do=get&target=book015.png "book015.png")
>     
> 
> In dit geval zeggen we dan dat de lijsten gelijkwaardig, **equivalent**, zijn, omdat deze dezelfde elementen bevatten maar niet identiek zijn want ze zijn niet hetzelfde object. Zijn twee objecten identiek, dan zijn deze ook gelijkwaardig maar zijn deze gelijkwaardig, dan zijn ze niet noodzakelijkerwijs identiek.
> 
> Tot nu toe hebben we "object" en "waarde" door elkaar heen gebruikt maar het is nauwkeuriger om te zeggen dat een object een waarde heeft. Voert u a = \[1,2,3\] uit, dan verwijst a naar een lijstobject met een specifieke reeks van elementen als waarde. Heeft een andere lijst dezelfde elementen dan zeggen we dat deze dezelfde waarde heeft.
> 
> ## 10.11 Aliassen
> 
> Verwijst a naar een object en u voert b = a uit, dan verwijzen beide variabelen naar hetzelfde object:
> 
> \>>> a = \[1, 2, 3\]
> \>>> b = a
> \>>> b is a
> True
> 
> Het statusdiagram lijkt hierop:
> 
> -   ![book016.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTien?action=AttachFile&do=get&target=book016.png "book016.png")
>     
> 
> De connectie van een variabele aan een object wordt een **verwijzing** genoemd. In dit voorbeeld bestaan twee verwijzingen naar hetzelfde object.
> 
> Een object met meer dan één verwijzing heeft meer dan één naam dus we kunnen zeggen dat het object een **alias** heeft.
> 
> Kunt u het object met een alias wijzigen dan heeft een verandering, aangebracht door een alias, effect op de andere:
> 
> \>>> b\[0\] = 17
> \>>> print a
> \[17, 2, 3\]
> 
> Hoewel dit gedrag bruikbaar is, is het daarnaast foutgevoelig. In het algemeen is het veiliger om aliassen te voorkomen bij objecten die te wijzigen zijn. Bij objecten die niet te wijzigen zijn, zoals strings, is het hebben van een alias niet echt een probleem. In dit voorbeeld:
> 
> a = 'banaan'
> b = 'banaan'
> 
> Maakt het bijna nooit iets uit of a dan wel b naar dezelfde string verwijzen.
> 
> ## 10.12 Argumenten van een lijst
> 
> Geeft u een lijst door aan een functie dan krijgt de functie een verwijzing naar de lijst. Wijzigt de functie een parameter van de lijst dan ziet de aanroeper de verandering. Bijvoorbeeld: verwijder\_kop verwijdert het eerste element uit een lijst:
> 
> def verwijder\_kop(t):
>       del t\[0\]
> 
> Hier hoe het wordt gebruikt:
> 
> \>>> letters = \['a', 'b', 'c'\]
> \>>> verwijder\_kop(letters)
> \>>> print letters
> \['b', 'c'\]
> 
> De parameter t en de variabele letters zijn aliassen voor hetzelfde object. Het stapeldiagram ziet er als volgt uit:
> 
> -   ![boek017_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTien?action=AttachFile&do=get&target=boek017_nl.png "boek017_nl.png")
>     
> 
> Omdat de lijst wordt gedeeld door twee blokken tekende ik die ook.
> 
> Het is belangrijk om onderscheid te maken tussen bewerkingen die een lijst aanpassen en bewerkingen die een nieuwe lijst aanmaken. Bijvoorbeeld: de append methode wijzigt een lijst maar de + operator maakt een nieuwe lijst aan:
> 
> \>>> t1 = \[1, 2\]
> \>>> t2 = t1.append(3)
> \>>> print t1
> \[1, 2, 3\]
> \>>> print t2
> None
> \>>> t3 = t1 + \[3\]
> \>>> print t3
> \[1, 2, 3\]
> \>>> t2 is t3
> False
> 
> Dit verschil is belangrijk als u zelf functies schrijft die tot doel hebben een lijst aan te passen. Bijvoorbeeld: deze functie verwijdert _niet_ de kop van een lijst:
> 
> def kop\_slecht\_verwijderen(t):
>        t = t\[1:\]                      # FOUT!
> 
> De operator voor partjes maakt een nieuwe lijst aan; de toewijzing laat t hiernaar verwijzen maar niets daarvan heeft effect op de lijst die als argument was meegegeven.
> 
> Een alternatief is om een functie te schrijven die een nieuwe lijst aanmaakt en deze ook teruggeeft. Bijvoorbeeld: staart geeft alles terug behalve het eerste element uit de lijst:
> 
> def staart(t):
>        return t\[1:\]
> 
> Deze functie laat de originele lijst ongewijzigd. Zie hierbij hoe deze wordt gebruikt:
> 
> \>>> letters = \['a', 'b', 'c'\]
> \>>> rest = staart(letters)
> \>>> print rest
> \['b', 'c'\]
> 
> **Oefening 10.2** Schrijf een functie genaamd hak die een lijst meekrijgt en deze aanpast zodanig dat het eerste en laatste element verwijderd wordt en niets (None) teruggeeft.
> 
> Schrijf daarna een functie genaamd midden die een lijst meekrijgt en een nieuwe lijst teruggeeft die alles behalve het eerste en het laatste element bevat.
> 
> ## 10.13 Debuggen
> 
> Het op onzorgvuldige manier gebruiken van lijsten (en andere te wijzigen objecten) kan leiden tot vele uren debuggen. Hierbij enkele valkuilen en de manier om ze te omzeilen:
> 
> 1.  Vergeet niet dat de meeste methoden voor lijsten het argument aanpassen en niets (None) teruggeven. Dit is het tegenovergestelde van methoden voor strings, die een nieuwe string teruggeven en het origineel intact laten. Bent u gewoon code voor strings te schrijven die hierop lijkt:
>     
>     -   woord = woord.strip()
>         
>         Het is verleidelijk om dergelijke code te schrijven:
>         
>         t = t.sort()                    # FOUT!
>         
>         Omdat sort niets None teruggeeft, zal de volgende bewerking op t vermoedelijk fout lopen.
>         
>         Voordat u methoden en operatoren voor lijsten gaat gebruiken moet u de documentatie zorgvuldig lezen en de werking in een interactieve modus testen. De methoden en operatoren die lijsten met andere reeksen delen (zoals strings) zijn gedocumenteerd in [docs.python.org/lib/typesseq.html](http://docs.python.org/lib/typesseq.html). De methoden en operatoren die alleen gelden voor aanpasbare reeksen zijn gedocumenteerd in [docs.python.org/lib/typesseq-mutable.html](http://docs.python.org/lib/typesseq-mutable.html).
>         
> 2.  Kies één manier van werken en blijf daar bij. Een deel van het probleem met lijsten is dat er teveel manieren zijn om er mee te werken. Bijvoorbeeld: het verwijderen van een element uit een lijst kan met pop, remove en del en ook nog met behulp van het toewijzen van een partje. Een element toevoegen, kan met de methode append of de + operator. Maar vergeet niet dat deze goed gaan:
>     
>     -   t.append(x)
>         t = t + \[x\]
>         
>         En deze gaan fout:
>         
>         t.append(\[x\])                   #  FOUT!
>         t = t.append(x)                 #  FOUT!
>         t + \[x\]                         #  FOUT!
>         t = t + x                       #  FOUT!
>         
>         Probeer elk voorbeeld uit in de interactive modus en begrijp goed wat ze doen. Merk op dat de laatste instructie een "runtime error" veroorzaakt, de anderen zijn geldig, maar doen het verkeerde ding.
> 3.  Maak kopieën om te voorkomen dat een alias wordt gemaakt. Wilt u een methode zoals sort gebruiken, die een argument aanpast, en u hebt de originele lijst ook nog nodig, maak dan een kopie.
>     
>     -   originel = t\[:\]
>         t.sort()
>         
>         In dit voorbeeld kunt u ook de ingebouwde functie sorted toepassen; deze geeft een nieuwe gesorteerde lijst terug en laat het origineel intact. Maar in dat geval moet u voorkomen dat u sorted als een variabelenaam gebruikt!
>         
> 
> ## 10.14 Woordenlijst
> 
> **lijst**: Een reeks van waarden.
> 
> **element**: Eén van de waarden uit de lijst (of een andere reeks) ook wel item genoemd.
> 
> **index**: Een "integer" waarde waarmee een element uit de lijst wordt aangewezen.
> 
> **geneste lijst**: Een lijst die onderdeel uitmaakt van een andere lijst.
> 
> **Een lijst doorlopen**: Het op volgorde doorlopen van een lijst.
> 
> **positioneren**: Een relatie waarbij elk element van één set overeenkomt met een element uit een andere set. Bijvoorbeeld: een lijst is een positionering van indices op elementen.
> 
> **opeenstapelaar**: Een variabele die in een lus wordt gebruikt om het resultaat te sommeren of opeen te stapelen, ook **accumulator**.
> 
> **reduceren**: Een verwerkingspatroon dat een reeks doorloopt en de elementen opeenstapelt tot een enkel resultaat.
> 
> **map**: Een verwerkingspatroon dat een reeks doorloopt en bewerkingen op ieder element uitvoert.
> 
> **filter**: Een verwerkingspatroon dat een reeks doorloopt en een element selecteert dat aan een bepaald criterium voldoet.
> 
> **object**: Iets waarnaar een variabele kan verwijzen. Een object heeft een type en een waarde.
> 
> **equivalent**: Het hebben van dezelfde waarde.
> 
> **identiek**: Hetzelfde object zijn en dus gelijkwaardig.
> 
> **verwijzing**: De verbinding tussen een variabele en zijn waarde.
> 
> **alias**: De omstandigheid dat twee variabelen verwijzen naar hetzelfde object.
> 
> **scheidingsteken**: Een karakter of een string die wordt gebruikt om aan te geven waar een string moet worden opgesplitst.
> 
> ## 10.15 Oefeningen
> 
> **Oefening 10.3** Schrijf een functie genaamd is\_gesorteerd die een lijst als parameter meekrijgt en True teruggeeft als de lijst in oplopende volgorde is gesorteerd en anders False. U mag als gegeven aannemen, dat de elementen uit de lijst met elkaar vergeleken kunnen worden met de vergelijkingsoperatoren <, >, enz.
> 
> Bijvoorbeeld: is\_gesorteerd(\[1,2,2\]) moet True teruggeven en is\_gesorteerd(\['b','a'\]) moet False teruggeven.
> 
> **Oefening 10.4** Twee woorden vormen een anagram als u met het herschikken van de letters uit het ene woord een ander woord kunt spellen. Schrijf een functie genaamd is\_anagram die twee strings meekrijgt en True teruggeeft als ze een anagram vormen.
> 
> **Oefening 10.5** De zogenaamde geboortedag paradox:
> 
> 1.  Schrijf een functie genaamd heeft\_dubbelen die een lijst meekrijgt en True teruggeeft als enig element vaker voorkomt. De originele lijst mag niet gewijzigd worden.
>     
> 2.  Stel een klas heeft 23 studenten; wat is de kans dat twee studenten dezelfde verjaardag hebben? U kunt deze waarschijnlijkheid schatten door willekeurig 23 verjaardagen aan te maken en deze te controleren op dubbelen. Tip: u kunt willekeurige verjaardagen aanmaken met behulp van de randint functie in de random module.
>     
> 
> Meer over dit probleem is te lezen in [nl.wikipedia.org/wiki/Verjaardagenparadox](http://nl.wikipedia.org/wiki/Verjaardagenparadox) en mijn oplossing is te lezen in [thinkpython.com/code/birthday.py](http://www.thinkpython.com/code/birthday.py).
> 
> **Oefening 10.6** Schrijf een functie genaamd verwijder\_dubbelen die een lijst meekrijgt en een nieuwe lijst teruggeeft met alleen de unieke elementen uit de originele lijst. Tip: ze hoeven niet in dezelfde volgorde te staan.
> 
> **Oefening 10.7** Schrijf een functie die een bestand woorden.txt inleest en bouw een lijst met één element per woord. Schrijf twee versies van deze functie, één die gebruik maakt van de append methode en de andere moet gebruik maken van idiom t = t + \[x\]. Welke van de twee doet er het langst over om uitgevoerd te worden? en waarom? mijn oplossing is te lezen in [thinkpython.com/code/wordlist.py](http://thinkpython.com/code/wordlist.py).
> 
> **Oefening 10.8** Om te controleren of een woord in een lijst voorkomt, kunt u de in operator gebruiken maar dit gaat niet snel omdat deze de lijst van voor naar achteren doorzoekt.
> 
> Omdat de woorden in alfabetische volgorde staan kunnen we één en ander versnellen met een binaire zoekmethode, deze komt overeen met het zoeken in een woordenboek. U begint in het midden, kijkt of het woord voor of na de bladzijde komt waar het woordenboek is opengeslagen. Zoek verder in dat deel waar het woord voor moet komen en herhaal deze methode totdat het woord gevonden is.
> 
> Op deze manier wordt het te doorzoeken gedeelte gehalveerd. Heeft een woordenlijst zeg 113.809 woorden dan kost deze methode ongeveer 17 stappen om het woord te vinden of te concluderen dat het woord niet voorkomt.
> 
> Schrijf een functie genaamd binair\_zoeken die een gesorteerde lijst meekrijgt en een doelwaarde en geef de index terug van die waarde in de lijst als deze voorkomt en anders niets None als de waarde niet voorkomt.
> 
> Of u kunt de documentatie van de bisect module lezen en deze gebruiken!
> 
> **Oefening 10.9** Twee woorden zijn een "omkeerbaar paar" als elk woord het omgekeerde is van de andere. Schrijf een functie die alle omkeerbare woordparen uit een woordenlijst vindt.
> 
> **Oefening 10.10** Twee woorden zijn samen te voegen als de opeenvolgende letters van beide woorden een nieuw woord opleveren1. Bijvoorbeeld: "ntb" en "ntb" is samen te voegen tot "ntb".
> 
> 1.  Schrijf een functie die woordparen vindt die samen te voegen zijn. Tip: som niet alle woordparen op!
> 2.  Kunt u woordparen vinden die op drie manieren samen te voegen zijn, dat wil zeggen, om de drie letters is een woord te vormen?
> 
> * * *
> 
> 1 Deze oefening is geïnspireerd door een voorbeeld uit [puzzlers.org](https://wiki.ubuntu-nl.org/puzzlers.org).