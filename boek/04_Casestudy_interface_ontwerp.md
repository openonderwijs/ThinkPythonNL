[community/ThinkPython/HoofdstukVier - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVier)

> # Hoofdstuk 4 Casestudy: interface ontwerp
> 
> ## 4.1 TurtleWorld
> 
> Als bijlage bij dit boek zijn een set modules geschreven genaamd Swampy. Een van deze modules is [TurtleWorld](https://wiki.ubuntu-nl.org/TurtleWorld), die een set functies levert voor het tekenen van lijnen met behulp van schildpadden die over het beeldscherm worden gedirigeerd.
> 
> U kunt Swampy downloaden bij [thinkpython.com/swampy](http://www.thinkpython.com/swampy), volg de instructies daar voor het installeren van Swampy op uw systeem.
> 
> Ga naar de map waar TurtleWorld.py staat, maak een bestand genaamd polygoon.py (veelhoek) en typ de volgende code:
> 
> from TurtleWorld import \*
> wereld = TurtleWorld()
> jan = Turtle()
> print jan
> wait\_for\_user()
> 
> De eerste regel is een variatie van de import instructie die we eerder zagen; in plaats van een moduleobject aan te maken worden de functies direct uit de module geïmporteerd en zijn dus te gebruiken zonder de puntnotatie.
> 
> De volgende regels kennen een [TurtleWorld](https://wiki.ubuntu-nl.org/TurtleWorld) toe aan wereld en kennen een Turtle toe aan jan. Het printen van jan levert iets als:
> 
> <TurtleWorld.Turtle instance at 0xb7bfbf4c>
> 
> Dit betekent dat jan verwijst naar een **instantie** van een Turtle zoals gedefinieerd in de module TurtleWorld. In deze context betekent "instantie" een lid van een set; deze Turtle is één van een set van mogelijke Turtles.
> 
> wait\_for\_user vertelt aan [TurtleWorld](https://wiki.ubuntu-nl.org/TurtleWorld) te wachten totdat de gebruiker iets doet, hoewel in dit geval de gebruiker niet veel meer kan doen dan het venster sluiten.
> 
> [TurtleWorld](https://wiki.ubuntu-nl.org/TurtleWorld) levert verschillende besturingsfuncties voor een turtle: fd en bk voor voorwaarts en achterwaarts, lt en rt voor links en rechts afslaan. Iedere Turtle heeft een pen vast, deze staat omlaag of omhoog. Staat de pen naar beneden dan laat de Turtle een spoor achter tijdens het bewegen. De functies pu en pd staan voor "pen omhoog" en "pen naar beneden".
> 
> Voeg de onderstaande regels toe aan het programma, na het toekennen van Turtle() aan jan en voor het aanroepen van wait\_for\_user:
> 
> fd(jan, 100)
> rt(jan)
> fd(jan, 100)
> 
> De eerste regel vertelt jan om 100 stappen naar voren te lopen. De tweede regel vertelt hem om rechtsaf te slaan.
> 
> Zodra u het programma uitvoert zult u zien dat jan naar het oosten loopt en daarna naar het zuiden en daarbij twee lijnen trekt.
> 
> Wijzig het programma zo dat het een vierkant tekent. Stop niet voordat u het programma werkend hebt gekregen!
> 
> ## 4.2 Eenvoudige herhaling
> 
> Grote kans dat u iets geschreven hebt zoals hieronder (met weglating van de code voor het toekennen van [TurtleWorld](https://wiki.ubuntu-nl.org/TurtleWorld)() en wachten op de gebruiker):
> 
> fd(jan, 100)
> lt(jan)
> fd(jan, 100)
> lt(jan)
> fd(jan, 100)
> lt(jan)
> fd(jan, 100)
> 
> We kunnen hetzelfde doen maar dan beknopter met een for instructie. Voeg dit voorbeeld toe aan polygoon.py en voer het opnieuw uit:
> 
> for i in range(4):
>       print 'Hallo!'
> 
> Zo iets als hieronder moet verschijnen:
> 
> Hallo!
> Hallo!
> Hallo!
> Hallo!
> 
> Dit is de eenvoudigste manier van het gebruik van de for instructie, later gaan we nog verder. Maar dit is genoeg om het programma voor het vierkant te herschrijven.
> 
> Hierbij een for instructie die een vierkant tekent:
> 
> for i in range(4):
>       fd(jan, 100)
>       lt(jan)
> 
> De opbouw van een for instructie is gelijk aan die van een functiedefinitie. Het bestaat uit een kop die eindigt met een dubbelepunt en een ingesprongen body. De body kan een willekeurig aantal instructies bevatten.
> 
> Een for instructie wordt ook wel een **lus** genoemd omdat de volgorde van uitvoering door de body loopt en dan terugkeert naar het begin. In dit geval wordt de body vier keer doorlopen.
> 
> Deze versie is eigenlijk een beetje anders dan de voorgaande code voor een vierkant, omdat weer linksaf wordt geslagen na het tekenen van de laatste zijde van het vierkant. De extra afslag kost wat meer tijd maar het vereenvoudigt de code als we iedere herhaling gelijk houden. Deze versie heeft ook het effect dat de turtle terugkeert in de start positie, dus weer kijkt in de richting waarin hij vertrokken is.
> 
> ## 4.3 Oefeningen
> 
> De volgende serie oefeningen gebruiken [TurtleWorld](https://wiki.ubuntu-nl.org/TurtleWorld). Deze zijn gewoon leuk maar hebben ook nut. Probeer, terwijl u ermee bezig bent, het nut te ontdekken.
> 
> De volgende paragrafen bevatten de oplossingen van de oefeningen; kijk daar nog niet naar totdat u de oefeningen hebt afgemaakt of op zijn minst geprobeerd hebt om ze af te maken.
> 
> 1.  Schrijf een functie genaamd vierkant die de parameter genaamd t krijgt, dat is een turtle. De functie moet de turtle gebruiken om een vierkant te tekenen. Schrijf een functieaanroep die jan doorgeeft als een argument aan vierkant en voer het programma opnieuw uit.
>     
> 2.  Voeg een andere parameter toe, genaamd lengte, aan vierkant. Wijzig de body zodat de lengte van de zijden lengte is en wijzig de functieaanroep om een tweede argument te gebruiken. Voer het programma opnieuw uit. Test het programma met verschillende waarden voor lengte.
>     
> 3.  De functies lt en rt maken standaard een 90-graden afslag maar het is mogelijk om een tweede argument op te geven die het aantal graden aangeeft. Bijvoorbeeld: lt(jan, 45) draait jan 45 graden naar links. Maak een kopie van vierkant en wijzig de naam in polygoon. Voeg een andere parameter toe genaamd n en wijzig de body zodat het een regelmatige polygoon met n zijden tekent. Tip: de middelpuntshoeken van een regelmatige polygoon met n zijden zijn 360.0/_n_ graden.
>     
> 4.  Schrijf een functie genaamd cirkel die een turtle t en straal (radius) r als parameters krijgt en daarmee bij benadering een cirkel tekent door het aanroepen van polygoon met een geschikte lengte en aantal zijden. Test uw functie met een serie waarden voor r. Tip: zoek de omtrek van de cirkel uit en zorg ervoor dat lengte \* n = omtrek. Een andere tip: als jan te langzaam is, voer hem dan op door jan.delay aan te passen, dit is de tijd tussen twee bewegingen in seconden. jan.delay = 0.01 krijgt hem in beweging.
>     
> 5.  Maak een meer generieke versie van cirkel genaamd boog die een extra parameter hoek mee krijgt; deze bepaalt welk fragment van een cirkel moet worden getekend. hoek wordt uitgedrukt in aantal graden, dus als hoek=360 is moet boog een volledige cirkel tekenen.
>     
> 
> ## 4.4 Inkapseling
> 
> De eerste oefening vraagt om de code voor het tekenen van een vierkant in een functiedefinitie te plaatsen en vervolgens om deze functie aan te roepen en daarbij turtle als een parameter door te geven. Hierbij een oplossing:
> 
> def vierkant(t):
>       for i in range(4):
>             fd(t, 100)
>             lt(t)
> vierkant(jan)
> 
> De binnenste instructies, fd en lt zijn twee maal ingesprongen om aan te geven dat deze tot de for behoren, Dat is binnen de functiedefinitie. De volgende regel, vierkant(jan), begint op de linker kantlijn; dus dit is het einde van zowel de for lus als de functiedefinitie.
> 
> Binnen de functie verwijst t naar dezelfde turtle als waar jan naar verwijst, dus lt(t) heeft hetzelfde effect als lt(jan). Waarom heet de parameter dan niet jan? Het idee is dat t iedere willekeurige parameter turtle kan zijn, niet alleen jan; u kunt een tweede turtle maken en deze als een argument doorgeven aan vierkant:
> 
> piet = Turtle()
> vierkant(piet)
> 
> Een stuk code in een functie samenvatten wordt **inkapselen** genoemd. Eén van de voordelen van inkapselen is dat het een naam aan de code geeft en dat is een vorm van documentatie. Een ander voordeel is dat de code opnieuw kan worden gebruikt; het is beknopter om een functie twee keer aan te roepen dan om de body te kopiëren!
> 
> ## 4.5 Generalisatie
> 
> De volgende stap is het toevoegen van de parameter lengte aan vierkant. Hierbij een oplossing:
> 
> def vierkant(t, lengte):
>       for i in range(4):
>             fd(t, lengte)
>             lt(t)
> vierkant(jan, 100)
> 
> Het toevoegen van een parameter aan een functie wordt generalisatie genoemd omdat dit de functie meer algemeen toepasbaar maakt: in de voorgaande versie heeft het vierkant altijd dezelfde omvang; in deze versie kan het ieder formaat aannemen.
> 
> De volgende stap heet ook generalisatie. In plaats van vierkantjes tekenen, tekent polygoon regelmatige polygonen met een willekeurig aantal zijden. Hierbij een oplossing:
> 
> def polygoon(t, n, lengte):
>       hoek= 360.0 / n
>       for i in range(n):
>             fd(t, lengte)
>             lt(t, hoek)
> polygoon(jan, 7, 70)
> 
> Deze code tekent een polygoon met 7 zijden en een lengte van 70. Bestaan er meer dan een paar numerieke argumenten dan wordt gemakkelijk vergeten waar deze voor staan of in welke volgorde ze moeten voorkomen. Het is toegestaan en soms nuttig om de namen van de parameters op te nemen in de lijst met argumenten:
> 
> polygoon(jan, n=7, lengte=70)
> 
> Deze worden **sleutelwoordargumenten** genoemd omdat ze de parameter namen als "sleutelwoorden" doorgeven (niet te verwarren met Python sleutelwoorden zoals while en def).
> 
> Deze zinsbouw maakt het programma beter te lezen. Dit is ook een herinnering aan de manier waarop argumenten en parameters werken: bij het aanroepen van een functie worden de argumenten aan parameters toegewezen.
> 
> ## 4.6 Interfaceontwerp
> 
> De volgende stap is het schrijven van cirkel, die de straal r krijgt als parameter. Hierbij een eenvoudige oplossing die gebruik maakt van polygoon om een polygoon te tekenen met 50 zijden:
> 
> def cirkel(t, r):
>        omtrek= 2 \* math.pi \* r
>        n = 50
>        lengte = omtrek/ n
>        polygoon(t, n, lengte)
> 
> De eerste regel berekent de omtrek van een cirkel met straal r door middel van de formule 2πr. Omdat we math.pi gebruiken moeten we math importeren. De afspraak is dat import instructies, normaal gesproken, aan het begin van een script staan.
> 
> n is het aantal lijn segmenten van onze benadering van een cirkel, dus lengte is de lengte van ieder segment. polygoon tekent een polygoon met 50 zijden die daarmee een cirkel benadert met straal r.
> 
> Eén begrenzing van deze oplossing is dat n een constante is, dit houdt in dat voor heel grote cirkels de lijnsegmenten te lang worden en dat we voor kleine cirkels tijd verspillen aan het tekenen van hele kleine segmenten. Een oplossing zou zijn om de functie te generaliseren door n als een parameter op te nemen. Dit geeft de gebruiker of iedereen die cirkel) aanroept meer richting, maar de interface is dan niet zo netjes meer..
> 
> De **interface** van een functie is een samenvatting van hoe die wordt gebruikt: wat zijn de parameters? Wat voert de functie uit? En wat is de antwoordwaarde? Een interface is "netjes" als deze "as simple as possible, but not simpler" (Einstein) is.
> 
> In dit voorbeeld behoort r tot de interface omdat deze de te tekenen cirkel specificeert. n is minder geschikt omdat het betrekking heeft op de details van _hoe_ de cirkel moet worden weergegeven.
> 
> Inplaats van de interface vol te stoppen is het beter om een geschikte waarde voor n te kiezen afhankelijk van de omtrek:
> 
> def cirkel(t, r):
>        omtrek= 2 \* math.pi \* r
>        n = int(omtrek/ 3) + 1
>        length = omtrek/ n
>        polygoon(t, n, lengte)
> 
> Het aantal segmenten is (ongeveer) omtrek/3, dus de lengte van elk segment is (ongeveer) 3, dit is klein genoeg om de cirkel rond te laten lijken en groot genoeg om efficiënt te zijn en geschikt voor elke cirkelgrootte.
> 
> ## 4.7 Refactoren
> 
> Bij het schrijven van cirkel, wordt het programma polygoon hergebruikt omdat een veelzijdige polygoon een goede benadering is van een cirkel. Maar boog werkt niet zo goed mee; zowel polygoon als cirkel kunnen niet gebruikt worden om een boog te tekenen.
> 
> Een alternatief is om te beginnen met een kopie van polygoon en deze om te zetten in een boog. Het resultaat zou hierop kunnen lijken:
> 
> def boog(t, r, hoek):
>       boog\_lengte = 2 \* math.pi \* r \* hoek / 360
>       n = int(boog\_lengte / 3) + 1
>       stap\_lengte = boog\_lengte / n
>       stap\_hoek= float(hoek) / n
>       for i in range(n):
>            fd(t, stap\_lengte)
>            lt(t, stap\_hoek)
> 
> Het tweede gedeelte van deze functie lijkt op polygoon maar we kunnen polygoon niet hergebruiken zonder de interface aan te passen. We zouden polygoon meer generiek kunnen maken door de hoek als derde argument te benutten maar dan is polygoon niet langer een zinvolle naam! In plaats daarvan zou deze dan polylijn moeten heten:
> 
> def polylijn(t, n, lengte, hoek):
>       for i in range(n):
>            fd(t, lengte)
>            lt(t, hoek)
> 
> Nu kunnen we polygoon en boog herschrijven door met polylijn te werken:
> 
> def polygoon(t, n, lengte):
>       hoek= 360.0 / n
>       polylijn(t, n, lengte, hoek)
> def boog(t, r, hoek):
>       boog\_lengte = 2 \* math.pi \* r \* hoek / 360
>       n = int(boog\_lengte / 3) + 1
>       stap\_lengte = boog\_lengte / n
>       stap\_hoek= float(hoek) / n
>       polylijn(t, n, stap\_lengte, stap\_hoek)
> 
> Uiteindelijk kunnen we cirkel herschrijven door boog te gebruiken:
> 
> def cirkel(t, r):
>       boog(t, r, 360)
> 
> Dit herstructureren van processen in een programma om de interface van de functie te verbeteren en het hergebruiken van code te bevorderen wordt **Refactoren** genoemd1. In dit voorbeeld valt op te merken dat er overeenkomstige code zit in boog en polygoon, dus zetten we deze om naar polylijn.
> 
> Hadden we vooruit gepland dan zouden we polylijn eerst hebben geschreven en daarmee refactoren hebben vermeden maar vaak weet u in het begin van een project te weinig om alle interfaces te ontwerpen. Zodra u met het coderen start ontstaat een beter inzicht in het probleem. Soms is refactoren een teken dat u iets hebt geleerd.
> 
> ## 4.8 Een ontwikkelplan
> 
> Een **ontwikkelplan** is een proces voor het schrijven van programma's. Het proces dat we hebben gebruikt in deze casestudy is "inkapseling en generalisatie ". De stappen van dit proces zijn:
> 
> 1.  Begin met het schrijven van een klein programmaatje zonder functiedefinities.
> 2.  Zodra u het programma werkend hebt, kapsel het in, in een functie en geef het een naam.
> 3.  Generaliseer de functie door de juiste parameters toe te voegen.
> 4.  Herhaal de stappen 1–3 totdat u een set met werkende functies hebt. Knip en plak de werkende code om overtypen (en opnieuw testen) te voorkomen.
> 5.  Zoek naar kansen om het programma te verbeteren door refactoren. Bijvoorbeeld: hebt u overeenkomstige code op verschillende plaatsen, overweeg dan deze te herstructureren in een toepasselijke algemene functie.
> 
> Dit proces heeft een aantal nadelen —we zullen verderop de alternatieven bekijken— maar is handiger nu we nog niet weten hoe u een programma kunt opdelen in functies. Deze aanpak laat u al werkend verder ontwerpen.
> 
> ## 4.9 docstring
> 
> Een **docstring** is een tekstregel aan het begin van een functie die de interface uitlegt ("doc" is een afkorting van "documentatie"). Hierbij een voorbeeld:
> 
> def polylijn(t, lengte, n, hoek):
>       """Teken n lijn segmenten met de gegeven lengte en
>       hoek (in graden) ertussen. t is een turtle.
>       """
>       for i in range(n):
>             fd(t, lengte)
>             lt(t, hoek)
> 
> Deze docstring is voorzien van driedubbele aanhalingstekens, daardoor kan de stringtekst over meerdere regels lopen.
> 
> De tekst is bondig maar deze bevat de essentiële informatie die iemand nodig heeft om deze functie te gebruiken. Het beschrijft beknopt wat de functie doet (zonder in details over het hoe te treden). Het legt uit wat het effect is van elke parameter op het gedrag van de functie en wat elke parameter is (als dat al niet voor de hand ligt).
> 
> Dit soort documentatie schrijven is een belangrijk onderdeel van het interface ontwerp. Een goed ontworpen interface moet eenvoudig uit te leggen zijn. Is het moeilijk om uit te leggen wat een functie doet, dan is dat een aanwijzing dat de interface verbetering behoeft.
> 
> ## 4.10 Debuggen
> 
> Een interface is zoiets als een contract tussen een functie en de aanroeper. De aanroeper levert bepaalde parameters aan en de functie gaat akkoord met het uitvoeren van het werk.
> 
> Bijvoorbeeld: polylijn vereist vier argumenten. Het eerste moet een Turtle zijn (of een ander object dat werkt met fd en lt). Het tweede moet een getal zijn, waarschijnlijk positief, hoewel de functie anders ook werkt. Het derde argument moet een geheel getal zijn, range piept anders (afhankelijk van de versie van Python die u gebruikt). Het vierde moet een getal zijn, zo te zien in graden.
> 
> Deze eisen worden **pre-condities** genoemd omdat deze correct worden verondersteld voordat de functie zijn werk doet. Omgekeerd, condities aan het einde van de functie zijn **post-condities**. Post-condities bevatten het beoogde effect van de functie (zoals het tekenen van lijnsegmenten) en enige neveneffecten (zoals verplaatsen van de Turtle of aanbrengen van veranderingen in de World).
> 
> Pre-condities zijn de verantwoordelijkheid van de aanroeper. Vergist de aanroeper zich in de (goed gedocumenteerde!) pre-conditie en de functie doet zijn werk niet goed, dan zit de fout in de aanroep en niet in de functie. Echter voor doelgericht debuggen is het vaak een goed idee om een functie op zijn pre-condities te controleren in plaats van aan te nemen dat deze correct zijn. Als iedere functie op zijn pre-condities vooraf wordt gecontroleerd, dan is duidelijk wie de schuldige is als één en ander fout gaat.
> 
> ## 4.11 Woordenlijst
> 
> **instantie**: Een lid van een set. De [TurtleWorld](https://wiki.ubuntu-nl.org/TurtleWorld) in dit hoofdstuk is een lid van de set van [TurtleWorlds](https://wiki.ubuntu-nl.org/TurtleWorlds).
> 
> **lus**: Een deel van een programma dat herhaald kan worden uitgevoerd.
> 
> **inkapselen**: Het proces van het omzetten van een reeks instructies in een functiedefinitie.
> 
> **generalisatie**: Het proces van het vervangen van iets onnodig specifieks (zoals een getal) door iets dat algemeen toepasbaar is (zoals een variabele of een parameter).
> 
> **sleutelwoordargument**: Een argument die de naam van de parameter bevat als een "sleutelwoord".
> 
> **interface**: Een beschrijving van hoe een functie te gebruiken, inclusief de naam en de beschrijving van de argumenten en antwoordwaarde.
> 
> **ontwikkelplan**: Een proces voor het schrijven van programma's.
> 
> **docstring**: Een regel tekst (string) die in een functiedefinitie voorkomt om de interface van de functie te documenteren.
> 
> **pre-conditie**: Een vereiste waaraan de aanroeper moet voldoen voordat de functie uitgevoerd wordt.
> 
> **post-conditie**: Een vereiste waaraan de functie moet voldoen voordat de functie eindigt.
> 
> ## 4.12 Oefeningen
> 
> **Oefening 4.1** Download de code in dit hoofdstuk bij [thinkpython.com/code/polygon.py](http://www.thinkpython.com/code/polygon.py).
> 
> 1.  Schrijf de juiste docstrings voor polygoon, boog en cirkel.
>     
> 2.  Teken een stapeldiagram dat de status van het programma laat zien tijdens het uitvoeren van cirkel(jan, straal). U kunt de berekening handmatig uitvoeren of een print instructie aan de code toevoegen.
>     
> 3.  De versie van boog in paragraaf 4.7 is niet erg nauwkeurig omdat de lineaire benadering van de cirkel zich altijd buiten een echte cirkel bevindt. Als resultaat eindigt de turtle een paar eenheden verder dan de juiste bestemming. Mijn oplossing toont een manier om dit effect te reduceren. Lees de code en kijk of u er wijs uit kunt worden. Als u een diagram tekent kunt u ontdekken hoe het werkt.
>     
> 
> **Oefening 4.2** Schrijf een algemeen toepasbare set van functies die bloemen, zoals de onderstaande, kan tekenen:
> 
> ![book005.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVier?action=AttachFile&do=get&target=book005.png "book005.png")
> 
> Een oplossing is te vinden op [thinkpython.com/code/flower.py](http://www.thinkpython.com/code/flower.py).
> 
> **Oefening 4.3** Schrijf een algemeen toepasbare set van functies die de onderstaande patronen kan tekenen:
> 
> ![book006.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVier?action=AttachFile&do=get&target=book006.png "book006.png")
> 
> Een oplossing is te vinden op [thinkpython.com/code/pie.py](http://www.thinkpython.com/code/pie.py).
> 
> **Oefening 4.4** De letters van het alfabet kunnen geconstrueerd worden uit een beperkt aantal basis elementen, zoals verticale en horizontale lijnen en een paar bogen. Ontwerp een tekenset die met een minimum aan basiselementen kan worden getekend en schrijf functies die de letters van het alfabet tekenen.
> 
> U kunt een functie per letter schrijven met de namen teken\_a, teken\_b, enzovoorts en plaats uw functies in een bestand genaamd letters.py. U kunt een "turtle typemachine" downloaden bij [thinkpython.com/code/typewriter.py](http://www.thinkpython.com/code/typewriter.py) om te helpen bij het testen van uw code.
> 
> Een oplossing is te vinden op [thinkpython.com/code/letters.py](http://www.thinkpython.com/code/letters.py).
> 
> * * *
> 
> 1 [nl.wikipedia.org/wiki/Refactoring](http://nl.wikipedia.org/wiki/Refactoring)