[community/ThinkPython/HoofdstukTwaalf - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwaalf)

> # Hoofdstuk 12 Tupels
> 
> ## 12.1 Tupels zijn onveranderbaar
> 
> Een tupel is een opeenvolging van waarden. De waarden kunnen van elk type zijn en ze zijn geïndexeerd door integers. In dat opzicht lijken tupels veel op lijsten. Het belangrijkste verschil is dat tupels onveranderbaar zijn. Syntactisch gezien is een tupel een lijst met waarden door komma's gescheiden :
> 
> \>>> t = 'a', 'b', 'c', 'd', 'e'
> 
> Hoewel niet noodzakelijk, is het gebruikelijk om tupels tussen haakjes te plaatsen:
> 
> \>>> t = ('a', 'b', 'c', 'd', 'e')
> 
> Om een tupel te maken met één enkel element moet het eindigen op komma:
> 
> \>>> t1 = ('a',)
> \>>> type(t1)
> <type 'tuple'>
> 
> Zonder deze komma behandelt Python ('a') als een string tussen haakjes:
> 
> \>>> t2 = ('a')
> \>>> type(t2)
> <type 'str'>
> 
> Een andere manier om een tupel te maken loopt via de ingebouwde tuplefunctie. Zonder argumenten maakt deze een lege tupel aan:
> 
> \>>> t = tuple()
> \>>> print t
> ()
> 
> Als het argument een reeks is (string, lijst of tupel), dan is het resultaat een tupel met de elementen van de reeks:
> 
> \>>> t = tuple('lupins')
> \>>> print t
> ('l', 'u', 'p', 'i', 'n', 's')
> 
> Omdat tuple de naam is van een ingebouwde functie moet het gebruik ervan als naam van een variabele vermeden worden. De meeste lijst operators werken ook op tupels. De vierkante haken operator indexeert een element:
> 
> \>>> t = ('a', 'b', 'c', 'd', 'e')
> \>>> print t\[0\]
> 'a'
> 
> En de selectie (slice) operator selecteert een gedeelte van de elementen.
> 
> \>>> print t\[1:3\]
> ('b', 'c')
> 
> Maar wordt geprobeerd om één van de elementen van een tupel te wijzigen, dan zal een foutmelding weergegeven worden:
> 
> \>>> t\[0\] = 'A'
> TypeError: object doesn't support item assignment
> 
> Elementen van een tupel kunnen niet worden gewijzigd, maar de ene tupel kan vervangen worden door een andere:
> 
> \>>> t = ('A',) + t\[1:\]
> \>>> print t
> ('A', 'b', 'c', 'd', 'e')
> 
> ## 12.2 Tupels toewijzen
> 
> Het is vaak handig om de waarden van twee variabelen om te wisselen. Met conventionele toewijzingen wordt gebruik gemaakt van een tijdelijke variabele. Bijvoorbeeld om a en b om te wisselen:
> 
> \>>> temp = a
> \>>> a = b
> \>>> b = temp
> 
> Deze oplossing is omslachtig; **tupel toewijzing** is eleganter:
> 
> \>>> a, b = b, a
> 
> De linkerkant is een tupel met variabelen; de rechterkant is een tupel met expressies. Elke waarde is toegewezen aan zijn respectievelijke variabele. Alle expressies aan de rechterkant worden geëvalueerd voordat enige toewijzing plaats vindt.
> 
> Het aantal variabelen aan de linkerkant en het aantal waarden aan de rechterkant moeten overeenkomen:
> 
> \>>> a, b = 1, 2, 3
> ValueError: too many values to unpack
> 
> Over het algemeen kan de rechterkant elk soort reeks zijn (string, lijst of tupel). Bijvoorbeeld: een e-mail adres opdelen in een gebruikersnaam en een domein, kan als volgt worden geschreven:
> 
> \>>> adres = 'monty@python.org'
> \>>> naam, domein = addr.split('@')
> 
> De antwoordwaarde van split is een lijst met twee elementen; het eerste element is toegekend aan naam, het tweede aan domein.
> 
> \>>> print naam
> monty
> \>>> print domein
> python.org
> 
> ## 12.3 Tupels als antwoordwaarde
> 
> Strikt genomen kan een functie maar één waarde teruggeven, echter is de waarde een tupel dan is het effect hetzelfde als het teruggeven van meerdere waarden. Bijvoorbeeld: u wilt twee getallen delen en het quotiënt en de rest berekenen, dan is het inefficiënt om eerst x/y te berekenen en vervolgens x%y. Het is beter om ze beide op hetzelfde moment te berekenen.
> 
> De ingebouwde functie divmod krijgt twee argumenten en geeft een tupel van twee waarden terug, het quotiënt en de rest. Het resultaat kan als een tupel opgeslagen worden:
> 
> \>>> t = divmod(7, 3)
> \>>> print t
> (2, 1)
> 
> Of gebruik tupel toewijzing om de elementen afzonderlijk op te slaan:
> 
> \>>> quot, rest = divmod(7, 3)
> \>>> print quot
> 2
> \>>> print rest
> 1
> 
> Hierbij een voorbeeld van een functie die een tupel teruggeeft:
> 
> def min\_max(t):
>       return min(t), max(t)
> 
> max en min zijn ingebouwde functies die het grootste en het kleinste element in een reeks vinden. min\_max berekent beide en geeft een tupel van twee waarden terug.
> 
> ## 12.4 Tupels met een variabel aantal argumenten
> 
> Functies kunnen een variabel aantal argumenten meekrijgen. Een parameternaam die begint met een \* **verzamelt** argumenten in een tupel. Bijvoorbeeld: printalles krijgt een willekeurig aantal argumenten mee en print deze:
> 
> def printalles(\*args):
>       print args
> 
> De verzamelparameter kan een willekeurige naam hebben maar args is gebruikelijk. Zie hier hoe de functie werkt:
> 
> \>>> printalles(1, 2.0, '3')
> (1, 2.0, '3')
> 
> U kunt de verzameloperator combineren met verplichte en optionele argumenten:
> 
> def puntloos(verplicht, optioneel=0, \*args):
>       print verplicht, optioneel, args
> 
> Voer deze functie uit met 1, 2, 3 en 4 of meer argumenten en wees er zeker van dat u begrijpt wat er gebeurt.
> 
> Het complement van verzamelen is **'uitstrooien**. U hebt een reeks van waarden en u wilt deze doorgeven aan een functie als meerdere argumenten, dan kunt u de \* operator gebruiken. Bijvoorbeeld: divmod krijgt precies twee argumenten mee, dit werkt niet met een tupel:
> 
> \>>> t = (7, 3)
> \>>> divmod(t)
> TypeError: divmod expected 2 arguments, got 1
> 
> Maar strooit u de tupel uit dan gaat het werken:
> 
> \>>> divmod(\*t)
> (2, 1)
> 
> **Oefening 12.1** Veel van de ingebouwde functies gebruiken tupels met een variabel aantal argumenten. Bijvoorbeeld max en min kunnen een willekeurig aantal argumenten meekrijgen:
> 
> \>>> max(1,2,3)
> 3
> 
> Maar sum doet dat niet.
> 
> \>>> sum(1,2,3)
> TypeError: sum expected at most 2 arguments, got 3
> 
> Schrijf een functie genaamd allesoptellen die een willekeurig aantal argumenten meekrijgt en hun som teruggeeft.
> 
> ## 12.5 Lijsten en tupels
> 
> zip is een ingebouwde functie die twee of meer reeksen meekrijgt en "ritst" (zips), deze in een lijst1 van tupels zet, waarbij elke tupel één element bevat van elke reeks.
> 
> Dit voorbeeld ritst een string en een lijst:
> 
> \>>> s = 'abc'
> \>>> t = \[0, 1, 2\]
> \>>> zip(s, t)
> \[('a', 0), ('b', 1), ('c', 2)\]
> 
> Het resultaat is een lijst met tupels waarbij elke tupel een teken bevat van de string en een overeenkomstig element uit de lijst.
> 
> Hebben reeksen niet dezelfde lengte dan heeft het resultaat de lengte van de kortste reeks.
> 
> \>>> zip('Anne', 'Mus')
> \[('A', 'M'), ('n', 'u'), ('n', 's')\]
> 
> U kunt een tupel toewijzing en een for lus gebruiken om een lijst met tupels te doorlopen:
> 
> t = \[('a', 0), ('b', 1), ('c', 2)\]
> for letter, getal in t:
>       print getal, letter
> 
> Iedere keer dat de lus doorlopen wordt, selecteert Python de volgende tupel uit de lijst en wijst de elementen toe aan letter en getal. De uitvoer van deze lus is:
> 
> 0 a
> 1 b
> 2 c
> 
> Combineert u zip, for en tupel toewijzing, dan krijgt u een handig idioom voor het doorlopen van twee (of meer) reeksen op hetzelfde moment. Bijvoorbeeld: heeft\_gelijke krijgt twee reeksen mee, t1 en t2 en geeft Waar terug als er een index i is zodanig dat t1\[i\] == t2\[i\]:
> 
> def heeft\_gelijke(t1, t2):
>       for x, y in zip(t1, t2):
>           if x == y:
>                 return True
>       return False
> 
> Wilt u door de elementen van een reeks en hun indices heenlopen, dan kunt u de ingebouwde functie enumerate gebruiken:
> 
> for index, element in enumerate('abc'):
>       print index, element
> 
> De uitvoer van deze lus is:
> 
> 0 a
> 1 b
> 2 c
> 
> Nogmaals.
> 
> ## 12.6 Woordenboeken en tupels
> 
> Woordenboeken hebben een methode genaamd items die een lijst met tupels teruggeven, waarbij elke tupel een sleutel-waarden paar is2.
> 
> \>>> d = {'a':0, 'b':1, 'c':2}
> \>>> t = d.items()
> \>>> print t
> \[('a', 0), ('c', 2), ('b', 1)\]
> 
> Zoals te verwachten van een woordenboek zijn de items in willekeurige volgorde. Omgekeerd kunt u een lijst met tupels gebruiken om een nieuw woordenboek te initialiseren:
> 
> \>>> t = \[('a', 0), ('c', 2), ('b', 1)\]
> \>>> d = dict(t)
> \>>> print d
> {'a': 0, 'c': 2, 'b': 1}
> 
> Het combineren van dict met zip geeft een korte, maar krachtige manier om een woordenboek aan te maken:
> 
> \>>> d = woordenboek(zip('abc', range(3)))
> \>>> print d
> {'a': 0, 'c': 2, 'b': 1}
> 
> De woordenboek methode update krijgt ook een lijst met tupels mee en voegt deze als sleutel-waarden paar aan een bestaand woordenboek toe.
> 
> Het combineren van items, tupel toewijzing en for geeft u een idioom voor het doorlopen van de sleutels en waarden in een woordenboek:
> 
> for sleutel, waarde in d.items():
>       print waarde, sleutel
> 
> De uitvoer van deze lus is:
> 
> 0 a
> 2 c
> 1 b
> 
> Opnieuw.
> 
> Het is gebruikelijk om tupels als sleutels van een woordenboek te gebruiken (voornamelijk omdat u geen lijsten kunt gebruiken). Bijvoorbeeld een telefoonboek koppelt een achter- en voornaamcombinatie aan een telefoonnummer. Stel voor dat we achter, voor en nummer gedefinieerd hebben; we kunnen dan schrijven:
> 
> directory\[achter,voor\] = nummer
> 
> De expressie tussen vierkante haken is een tupel. We kunnen de tupel toewijzing gebruiken om door het telefoonboek te bladeren.
> 
> for achter, voor in telefoonboek:
>       print voor, achter, directory\[voor,achter\]
> 
> Deze lus doorloopt de sleutels in het telefoonboek, dit zijn dus tupels. Het wijst de elementen van elke tupel toe aan achter en voor en print vervolgens de naam en het bijbehorende telefoonnummer.
> 
> Tupels weergeven in een status diagram kan op twee manieren. De meer gedetailleerde versie geeft indices en elementen weer, precies zoals deze voorkomen in de lijst. Bijvoorbeeld: ('Jansen', 'Jan') verschijnt als:
> 
> -   ![boek020_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwaalf?action=AttachFile&do=get&target=boek020_nl.png "boek020_nl.png")
>     
> 
> Maar in een groter diagram wilt u wellicht de details niet meenemen. Bijvoorbeeld: een diagram van het telefoonboek kan verschijnen als:
> 
> -   ![boek021_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwaalf?action=AttachFile&do=get&target=boek021_nl.png "boek021_nl.png")
>     
> 
> Hierbij worden de tupels grafisch verkort weergegeven met behulp van de Python zinsbouw.
> 
> Het telefoonnummer in het diagram is de klachtenlijn van de BBC; bel ze aub niet op.
> 
> ## 12.7 Tupels vergelijken
> 
> De vergelijkingsoperatoren werken met tupels en andere reeksen, Python begint met het vergelijken van het eerste element van elke reeks. Zijn deze gelijk dan gaat het door met de volgende elementen, enzovoorts, totdat een element wordt gevonden dat afwijkt. De daarop volgende elementen worden niet meer vergeleken (zelfs niet als ze erg groot zijn).
> 
> \>>> (0, 1, 2) < (0, 3, 4)
> True
> \>>> (0, 1, 2000000) < (0, 3, 4)
> True
> 
> De sort functie werkt op dezelfde manier. Deze sorteert hoofdzakelijk op het eerste element. Maar in het geval van een gelijkspel wordt gesorteerd op het tweede element enzovoorts.
> 
> Dit kenmerk leent zich voor een patroon genaamd DSU. Dit staat voor:
> 
> **Decoreer** een reeks door het aanmaken van een lijst met tupels met daarin één of meer sorteersleutels die voorafgaan aan de elementen van de reeks,
> 
> **Sorteer** de lijst met tupels en
> 
> **Undecoreer** door het onttrekken van de gesorteerde elementen uit de reeks.
> 
> Bijvoorbeeld: stel u hebt een lijst met woorden en u wilt deze sorteren van de langste naar de kortste:
> 
> def sorteer\_op\_lengte(woorden):
>       t = \[\]
>       for word in woorden:
>           t.append((len(woord), woord))
>       t.sort(reverse=True)
>       resultaat = \[\]
>       for lengte, woord in t:
>            resresultaat.append(woord)
>       return resultaat 
> 
> De eerste lus maakt een lijst met tupels aan, waarbij iedere tupel een woord is, vooraf gegaan door zijn lengte.
> 
> sort vergelijkt eerst het eerste element op lengte, en bekijkt het tweede element alleen bij een gelijkspel. Het sleutelwoord argument reverse=True vertelt aan sort om in omgekeerde volgorde te sorteren.
> 
> De tweede lus doorloopt de lijst met tupels en maakt een lijst met woorden in omgekeerde volgorde qua lengte.
> 
> **Oefening 12.2** In dit voorbeeld wordt een gelijkspel doorbroken door woorden te vergelijken, dus woorden met dezelfde lengte worden weergegeven in alfabetische volgorde. Voor andere applicaties kunt u een gelijkspel willekeurig doorbreken. Pas dit voorbeeld aan zodat woorden met dezelfde lengte in willekeurige volgorde verschijnen. Tip: kijk bij de random functie in de random module.
> 
> ## 12.8 Reeks van reeksen
> 
> Ik heb me geconcentreerd op lijsten van tupels maar ongeveer alle voorbeelden in dit hoofdstuk werken ook op een lijst met lijsten, tupel met tupels en tupel met lijsten. Om een opsomming van alle mogelijke combinaties te voorkomen is het eenvoudiger te spreken van een reeks van reeksen.
> 
> In veel verbanden kunnen de verschillende soorten reeksen (strings, lijsten en tupels) onderling uitgewisseld worden. Dus hoe en waarom kies je voor de ene, ofwel voor de andere?
> 
> Om met de meest voor de hand liggende reden te beginnen, strings kennen meer beperkingen dan andere reeksen omdat de elementen karakters moeten zijn. Ze zijn ook nog eens onveranderbaar. Is het nodig om de karakters in een string te wijzigen (in tegenstelling tot het aanmaken van een nieuwe string) dan zou u een lijst met karakters kunnen gebruiken.
> 
> Lijsten zijn gebruikelijker dan tupels voornamelijk omdat ze veranderlijk zijn. Maar in een beperkt aantal gevallen zult u de voorkeur geven aan tupels:
> 
> 1.  In bepaalde verbanden, zoals een return instructie is het qua zinsbouw eenvoudiger om een tupel aan te maken dan een lijst. In andere verbanden zult u de voorkeur geven aan een lijst.
>     
> 2.  Wilt u een reeks als woordenboeksleutel, dan moet u een onveranderbaar soort zoals een tupel of een string gebruiken.
> 3.  Wilt u een reeks doorgeven als een argument aan een functie, dan reduceert het werken met tupels het onverwachte gedrag van aliassen.
> 
> Omdat tupels onveranderbaar zijn, leveren deze geen methoden zoals sort en reverse, want deze passen de bestaande lijst aan. Maar Python levert de ingebouwde functies sorted en reversed, die elke reeks accepteren als een parameter en een nieuwe lijst met dezelfde elementen teruggeven in een andere volgorde.
> 
> ## 12.9 Debuggen
> 
> Lijsten, woordenboeken en tupels staan over het algemeen bekend als **gegevensstructuren**; in dit hoofdstuk beginnen we te kijken naar samengestelde gegevensstructuren zoals lijsten, woordenboeken en tupels die tupels als een sleutel en lijsten als waarde bevatten. Samengestelde gegevensstructuren zijn handig maar ze zijn gevoelig voor wat men zou kunnen noemen **vormfouten**; dat zijn fouten die optreden als een gegevensstructuur het verkeerde type, omvang of samenstelling heeft. Bijvoorbeeld: Verwacht u een lijst met één geheel getal en ik geef u een rechttoe rechtaan geheel getal (niet in een lijst), dan gaat dat niet werken.
> 
> Om te helpen met het debuggen van dit soort fouten heb ik een module geschreven, structshape. Deze module bevat een functie, die ook structshape genoemd is, die elk soort gegevensstructuren als een argument meekrijgt en een string teruggeeft die de vorm samenvat. Deze module is te downloaden vanaf [thinkpython.com/code/structshape.py](http://www.thinkpython.com/code/structshape.py)
> 
> Hierbij het resultaat voor een eenvoudige lijst:
> 
> \>>> from structshape import structshape
> \>>> t = \[1,2,3\]
> \>>> print structshape(t)
> list of 3 int
> 
> Een eleganter programma zou "lijst van 3 ints" schrijven, maar het was gemakkelijker om meervoudsvormen niet te behandelen. Hierbij een lijst met lijsten:
> 
> \>>> t2 = \[\[1,2\], \[3,4\], \[5,6\]\]
> \>>> print structshape(t2)
> list of 3 list of 2 int
> 
> Als de elementen van een lijst niet van hetzelfde type zijn, groepeert structshape ze op volgorde en op type:
> 
> \>>> t3 = \[1, 2, 3, 4.0, '5', '6', \[7\], \[8\], 9\]
> \>>> print structshape(t3)
> list of (3 int, float, 2 str, 2 list of int, int)
> 
> Hierbij een lijst met tupels:
> 
> \>>> s = 'abc'
> \>>> lt = zip(t, s)
> \>>> print structshape(lt)
> list of 3 tuple of (int, str)
> 
> En hierbij een woordenboek met drie items dat getallen omzet naar strings.
> 
> \>>> d = dict(lt)
> \>>> print structshape(d)
> dict of 3 int->str
> 
> Hebt u problemen met het bijhouden van gegevensstructuren, dan kan structshape helpen.
> 
> ## 12.10 Woordenlijst
> 
> **tupel**: Een onveranderbare reeks van elementen.
> 
> **tupeltoewijzing**: Een toewijzing met een reeks aan de rechterkant en een tupel van variabelen aan de linkerkant. De rechterkant wordt geëvalueerd en zijn element wordt toegewezen aan de variabele aan de linkerkant.
> 
> **verzamelen**: De actie van het samenstellen van een tupel met een variabel aantal argumenten.
> 
> **verstrooien**: De actie van het behandelen van een reeks als een lijst met argumenten.
> 
> **DSU**: Afkorting van "decoreer-sorteer-undecoreer", een patroon dat het aanmaken van een lijst met tupels, sorteren en afscheiden van een deel van het resultaat met zich meebrengt.
> 
> **gegevensstructuren**: Een verzameling van verwante waarden, vaak georganiseerd in lijsten, woordenboeken, tupels, enz.
> 
> **vorm** (van een gegevensstructuur): Een samenvatting van het type, de omvang en samenstelling van een gegevensstructuur.
> 
> ## 12.11 Oefeningen
> 
> **Oefening 12.3** Schrijf een functie genaamd most\_frequent die een string meekrijgt en de letter in omgekeerde volgorde van frequentie print. Zoek tekst bestanden vanuit verschillende talen en bekijk hoe letterfrequenties variëren tussen talen. Vergelijk uw resultaten met tabellen op [wikipedia.org/wiki/Letter\_frequencies](http://www.wikipedia.org/wiki/Letter_frequencies).
> 
> **Oefening 12.4** Meer anagrammen!
> 
> 1.  Schrijf een programma dat een woordenlijst in een bestand leest (zie paragraaf 9.1) en alle setjes met woorden print die een anagram zijn. Hierbij een voorbeeld van hoe dat eruit kan zien:
>     -         \['deltas', 'desalt', 'lasted', 'salted', 'slated', 'staled'\]
>               \['retainers', 'ternaries'\]
>               \['generating', 'greatening'\]
>               \['resmelts', 'smelters', 'termless'\]
>               Tip: U zou een woordenboek kunnen aanmaken dat een serie letters en de woorden bevat, die daarmee te formeren zijn. De vraag is hoe kunt u een serie letters weergeven op zo'n manier dat deze als sleutel te gebruiken is?
>         
> 2.  Pas het voorgaande programma zo aan dat dit de grootste set met anagrammen als eerste print, gevolgd door de op één na grootste, enzovoorts.
> 3.  In Scrabble is een "bingo" wanneer alle 7 letterblokjes op uw bordje, samen met een letter op het bord een achtletter woord vormen. Welke setje van acht letters vormen de meeste potentiële bingo's? Hint: In het Engels zijn dat zeven setjes.
> 4.  Twee woorden vormen een "metathesis paar" als u het ene woord kan omzetten in het ander door twee letters te wisselen3. Bijvoorbeeld: "converse" en "conserve". Schrijf een programma die alle metathesis paren in een woordenboek vindt. Tip: test niet alle woordparen en test ook niet alle mogelijke letterwisselingen.
>     
> 
> De oplossing is te downloaden op [thinkpython.com/code/anagram\_sets.py](http://thinkpython.com/code/anagram_sets.py).
> 
> **Oefening 12.5** Hierbij een nieuwe Car Talk Puzzel4 :
> 
> -   Wat is het langste Engelse woord, dat een geldig Engels woord blijft als u één voor één zijn letters verwijdert? Letters mogen aan het einde, het begin of ergens tussenin verwijderd worden maar u mag de letters niet van plaats verwisselen. Iedere keer als een letter verwijderd is, blijft het een Engels woord. Als u zo doorgaat, blijft u met één letter zitten en ook dat moet een Engels woord zijn, te vinden in het woordenboek. Wat is het langste woord en uit hoeveel letters bestaat dit? Hierbij een bescheiden voorbeeldje: Sprite. Ok? U start met "sprite", verwijdert één letter, bijvoorbeeld de "r" en we houden het woord "spite" over. Nu verwijderen we de "e" aan het einde en houden "spit" over, nu de "s" en we hebben "pit", "it" en "I".
> 
> Schrijf een programma dat alle woorden vindt die op deze wijze verkleind kunnen worden en vindt het langste woord.
> 
> Deze oefening biedt iets meer uitdaging dan de meeste, dus hierbij een aantal suggesties:
> 
> 1.  U zou een functie kunnen schrijven die een woord meekrijgt en een lijst met alle woorden berekent die geformeerd kunnen worden door één letter te verwijderen. Deze zijn de "kinderen" van dat woord.
> 2.  Recursief; een woord is herleidbaar als één van zijn kinderen herleidbaar is. Als basis (base case) kunt u een lege string beschouwen als herleidbaar.
> 3.  De meegeleverde woordenlijst words.txt bevat geen éénletter woorden, dus u moet de a en dergelijke zelf toevoegen net als de lege string.
>     
> 4.  De snelheid van het programma zal toenemen als u onthoudt welke woorden herleidbaar zijn.
> 
> Mijn oplossing is te vinden op [thinkpython.com/code/reducible.py](http://thinkpython.com/code/reducible.py).
> 
> * * *
> 
> 1 In Python 3.0, geeft zip een iterator met tupels maar voor de meeste doeleinden gedraagt een iterator zich als een lijst.  
> 2 Dit gedrag is een beetje afwijkend in Python 3.0.  
> 3 Deze oefening is geïnspireerd door een voorbeeld op [puzzlers.org](http://puzzlers.org).  
> 4 [www.cartalk.com/content/puzzler/transcripts/200651](http://www.cartalk.com/content/puzzler/transcripts/200651)