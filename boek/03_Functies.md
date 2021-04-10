[community/ThinkPython/HoofdstukDrie - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukDrie)

> # Hoofdstuk 3 Functies
> 
> ## 3.1 Functie aanroepen
> 
> In de context van programmeren, is een **functie** een reeks instructies die een bewerking uitvoert en van een naam is voorzien. U definieert een functie door de naam en de reeks instructies te specificeren. Op een later moment "roept" u de functie aan op naam. We hebben al een voorbeeld van een **functieaanroep** gezien:
> 
> \>>> type(32)
> <type 'int'>
> 
> De naam van de functie is type. De expressie tussen ronde haken wordt het **argument** genoemd van de functie. Het resultaat van deze functie is het type van het argument.
> 
> Het is gebruikelijk om te zeggen dat een functie het argument "neemt" en het resultaat "terug" geeft. Het resultaat wordt de **antwoordwaarde** genoemd.
> 
> ## 3.2 Type omzetfuncties
> 
> Python levert ingebouwde functies die waarden van het ene type omzetten naar een ander type. De int functie neemt een willekeurige waarde en zet deze, als het lukt, om naar een integer (geheel getal). Zo niet dan protesteert de functie wel met een foutmelding:
> 
> \>>> int('32')
> 32
> \>>> int('Hallo')
> ValueError: invalid literal for int(): Hallo
> 
> int kan floating-point (drijvende komma) waarden omzetten naar gehele getallen maar deze worden niet afgerond, de breuk wordt afgehakt.
> 
> part:
> \>>> int(3.99999)
> 3
> \>>> int(-2.3)
> \-2
> 
> float zet gehele getallen en strings om naar floating-point getallen:
> 
> \>>> float(32)
> 32.0
> \>>> float('3.14159')
> 3.14159
> 
> Tenslotte, str zet zijn argument om naar een string:
> 
> \>>> str(32)
> '32'
> \>>> str(3.14159)
> '3.14159'
> 
> ## 3.3 Wiskundige functies
> 
> Python heeft een wiskundige module die het merendeel van de bekende wiskundige functies bevat. Een **module** is een bestand dat een verzameling van verwante functies bevat.
> 
> Voordat we de module kunnen gebruiken moeten we deze importeren:
> 
> \>>> import math
> 
> Deze instructie maakt een **moduleobject** aan die 'math' heet. Print u het moduleobject dan krijgt u hierover de nodige informatie:
> 
> \>>> print math
> <module 'math' from '/usr/lib/python2.5/lib-dynload/math.so'>
> 
> Het moduleobject bevat de functies en variabelen zoals gedefinieerd in de module. U benadert een functie door de naam van de module en de naam van de functie op te geven, gescheiden door een punt (ook wel een dot genoemd). Dit formaat heet **dot notatie**.
> 
> \>>> verhouding = signaal\_sterkte / ruis\_sterkte
> \>>> decibels = 10 \* math.log10(verhouding)
> \>>> radialen = 0.7
> \>>> hoogte = math.sin(radialen)
> 
> Het eerste voorbeeld berekent het logaritmische grondtal 10 van de signaal-ruis-verhouding. De math-module levert ook een functie genaamd log; berekening van de logaritme met grondtal e. Het tweede voorbeeld vindt de sinus van radiaal. De naam van de variabele is een aanwijzing dat sin en de andere trigonometrische functies (cos, tan, etc.) argumenten in radialen aannemen. Omzetten van graden naar radialen gebeurt door te delen door 360 en te vermenigvuldigen met 2π:
> 
> \>>> graden = 45
> \>>> radialen = graden / 360.0 \* 2 \* math.pi
> \>>> math.sin(radialen)
> 0.707106781187
> 
> De expressie math.pi krijgt de variabele pi vanuit de math module. De waarde van deze variabele is een benadering van π, met een nauwkeurigheid van 15 cijfers achter de komma.
> 
> Bent u (nog) niet bekend met trigonometry, dan is het voorgaande antwoord te controleren door dit te vergelijken met de wortel uit 2 gedeeld door 2:
> 
> \>>> math.sqrt(2) / 2.0
> 0.707106781187
> 
> ## 3.4 Compositie
> 
> Tot nu toe hebben we gekeken naar elk van de onderdelen van een programma ( variabelen, expressies en instructies ) afzonderlijk, en niet gesproken over hoe deze te combineren.
> 
> Een van de meest nuttige kenmerken van programmeertalen is hun mogelijkheid om kleine bouwblokken te maken en deze samen te voegen. Te vergelijken met Lego. Bijvoorbeeld: het argument van een functie kan elke soort expressie zijn, inclusief rekenkundige operatoren:
> 
> x = math.sin(graden / 360.0 \* 2 \* math.pi)
> 
> Maar ook functieaanroepen:
> 
> x = math.exp(math.log(x+1))
> 
> Bijna overal waar u een waarde kunt plaatsen, kunt u ook een willekeurige expressie plaatsen, er is één uitzondering: de linkerkant van een toewijsinstructie moet de naam van een variabele zijn. Iedere andere expressie aan de linkerkant levert een syntax error1 op.
> 
> \>>> minuten = uren \* 60                # goed
> \>>> uren \* 60 = minuten                # fout  
> SyntaxError: can't assign to operator
> 
> ## 3.5 Nieuwe functies toevoegen
> 
> Tot nu toe hebben we alleen functies gebruikt die zijn meegeleverd met Python, maar het is ook mogelijk om nieuwe functies toe te voegen. Een **functiedefinitie** omschrijft de naam van de nieuwe functie en de volgorde van de instructies die uitgevoerd worden tijdens de aanroep.
> 
> Hierbij een voorbeeld:
> 
> def print\_gedicht():
>      print "Berend Botje ging uit varen"
>      print "met zijn scheepje naar Zuidlaren."
> 
> def is een sleutelwoord dat aangeeft dat dit een functiedefinitie is. De naam van de functie is print\_gedicht. De regels voor functienamen zijn dezelfde als die voor namen van variabelen: letters, cijfers en een aantal interpunctietekens zijn toegestaan maar het eerste karakter mag geen cijfer zijn. U kunt geen sleutelwoord als functienaam gebruiken en het gebruik van een variabele en een functie met dezelfde naam moet u vermijden.
> 
> De lege haakjes achter de naam geven aan dat deze functie geen argumenten neemt.
> 
> De eerste regel van de functiedefinitie wordt de header (kop); de rest wordt de body genoemd. De kop moet eindigen met een dubbelepunt en de body moet worden ingesprongen. De afspraak is dat het inspringen altijd vier spaties groot is. (zie [sectie 3.13](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukDrie#A3.13Debuggen)). De body kan een willekeurig aantal instructies bevatten.
> 
> De strings in de printinstructies zijn tussen dubbele aanhalingstekens geplaatst. Enkele aanhalingstekens en dubbele aanhalingstekens hebben hetzelfde effect. De meeste mensen gebruiken enkele aanhalingstekens behalve in die gevallen waarbij een enkel aanhalingsteken in de string voorkomt (dit is ook een apostrof).
> 
> Typt u een functiedefinitie tijdens de interactieve modus, dan print de interpreter een ovaal (...) om aan te geven dat de definitie niet compleet is:
> 
> \>>> def print\_gedicht():
> ...        print "Berend Botje ging uit varen"
> ...        print "met zijn scheepje naar Zuidlaren."
> ...
> 
> Voeg een lege regel toe om de functie af te sluiten (dit is niet nodig in een script).
> 
> Door het definiëren van een functie wordt een variabele met dezelfde naam aangemaakt.
> 
> \>>> print print\_gedicht
> <function print\_gedicht at 0xb7e99e9c>
> \>>> print type(print\_gedicht)
> <type 'function'>
> 
> De waarde van print\_gedicht is een **functieobject**, met als type 'function'.
> 
> De zinsbouw voor het aanroepen van de nieuwe functie is dezelfde als voor ingebouwde functies:
> 
> \>>> print\_gedicht()
> Berend Botje ging uit varen
> met zijn scheepje naar Zuidlaren.
> 
> Zodra u een functie hebt gedefinieerd, kunt u deze gebruiken binnen een andere functie. Bijvoorbeeld: om het vorige refrein te herhalen kunnen we een functie schrijven die heet herhaal\_gedicht:
> 
> def herhaal\_gedicht():
>      print\_gedicht()
>      print\_gedicht()
> 
> Roep vervolgens herhaal\_gedicht aan:
> 
> \>>> herhaal\_gedicht()
> Berend Botje ging uit varen
> met zijn scheepje naar Zuidlaren.
> Berend Botje ging uit varen
> met zijn scheepje naar Zuidlaren.
> 
> Maar dat is niet hoe het liedje eigenlijk gaat.
> 
> ## 3.6 Definities en gebruik
> 
> Als u de codefragmenten uit de vorige sectie bij elkaar zet lijkt het complete programma hier op:
> 
> def print\_gedicht():
>      print "Berend Botje ging uit varen"
>      print "met zijn scheepje naar Zuidlaren."
> def herhaal\_gedicht():
>       print\_gedicht()
>       print\_gedicht()
> herhaal\_gedicht()
> 
> Dit programma bevat twee functiedefinities: print\_gedicht en herhaal\_gedicht. Functiedefinities worden net als andere instructies uitgevoerd, maar het effect is het aanmaken van functieobjecten. De instructies in de functie worden niet uitgevoerd totdat de functie wordt aangeroepen. Functiedefinities produceren geen uitvoer.
> 
> Zoals te verwachten, moet een functie eerst aangemaakt worden voordat deze uitgevoerd kan worden. Met andere woorden: de functiedefinitie moet eerst uitgevoerd zijn voordat deze voor de eerste keer wordt aangeroepen.
> 
> **Oefening 3.1** Verplaats de laatste regel van dit programma naar de bovenkant zodat de aanroep van de functie vóór de functiedefinitie staat. Draai het programma en bekijk welke foutmelding verschijnt.
> 
> **Oefening 3.2** Verplaats de aanroep van de functie terug naar het einde en plaats de definitie van print\_gedicht onder de definitie van herhaal\_gedicht. Wat gebeurt er als dit programma wordt uitgevoerd?
> 
> ## 3.7 Volgorde van uitvoering
> 
> Om er zeker van te zijn dat een functie gedefinieerd is voordat deze voor de eerste keer wordt gebruikt, moet u de volgorde kennen waarin instructies worden uitgevoerd, dit wordt de **volgorde van uitvoering** genoemd.
> 
> De uitvoering begint altijd bij de eerste instructie van een programma. Instructies worden één voor één en van boven naar beneden uitgevoerd.
> 
> Functiedefinities veranderen de volgorde van uitvoering van een programma niet, maar denk eraan dat instructies in een functie niet eerder worden uitgevoerd dan op het moment dat de functie wordt aangeroepen.
> 
> Een functieaanroep lijkt op een omleiding in de volgorde van uitvoering. In plaats van naar de volgende instructie over te gaan stapt het programma naar de body van de functie en voert alle instructies op die plaats uit. Vervolgens keert het programma terug naar de plek waar de functie werd aangeroepen.
> 
> Dat klinkt eenvoudig, totdat het u te binnen schiet dat functies elkaar kunnen aanroepen. Dus midden in een functie moet het programma mogelijk instructies uitvoeren van een andere functie. Maar terwijl deze functie wordt uitgevoerd moet het programma misschien nog instructies van een andere functie uitvoeren!
> 
> Gelukkig is Python goed in het bijhouden van de regel die hij momenteel uitvoert, dus iedere keer als een functie klaar is gaat het programma verder op de plek waar het was gebleven bij het aanroepen van de functie. Zodra het programma aan het einde is gekomen stopt de uitvoering.
> 
> Wat is de moraal van dit verhaal? Een programma moet u niet altijd van boven naar beneden lezen, u moet het programma lezen volgens de volgorde van uitvoering.
> 
> ## 3.8 Parameters en argumenten
> 
> Enkele van de ingebouwde functies, die we zagen, hebben argumenten nodig. Bijvoorbeeld: zodra u math.sin aanroept geeft u een getal mee als argument. Sommige functies krijgen meerdere argumenten: math.pow gebruikt er twee : namelijk het grondtal en de exponent.
> 
> Binnenin de functie, worden de argumenten toegewezen aan variabelen genaamd **parameters**. Hierbij een voorbeeld van een zelf gedefinieerde functie die een argument meekrijgt:
> 
> def print\_dubbel(jan):
>       print jan
>       print jan
> 
> Deze functie wijst het argument toe aan een parameter genaamd jan. Zodra de functie wordt aangeroepen print het de waarde van de parameter (wat het ook is) twee keer uit.
> 
> Deze functie werkt voor iedere waarde die te printen is.
> 
> \>>> print\_dubbel('Spam')
> Spam
> Spam
> \>>> print\_dubbel(17)
> 17
> 17
> \>>> print\_dubbel(math.pi)
> 3.14159265359
> 3.14159265359
> 
> Dezelfde regels die gelden voor het samenstellen van ingebouwde functies gelden ook voor zelf gedefinieerde functies, dus kunnen we iedere vorm van een expressie als argument voor print\_dubbel gebruiken:
> 
> \>>> print\_dubbel('Spam '\*4)
> Spam Spam Spam Spam
> Spam Spam Spam Spam
> \>>> print\_dubbel(math.cos(math.pi))
> \-1.0
> \-1.0
> 
> Het argument wordt geëvalueerd voordat de functie wordt aangeroepen, dus in deze voorbeelden worden de expressies, 'Spam '\*4 en math.cos(math.pi) maar één keer geëvalueerd.
> 
> U kunt ook een variabele als argument gebruiken:
> 
> \>>> michael = 'Eric, the half a bee.'
> \>>> print\_dubbel(michael)
> Eric, the half a bee.
> Eric, the half a bee.
> 
> De naam van de variabele, die we doorgeven als een argument (michael) heeft niets te maken met de naam van de parameter (jan). Het doet er niet toe welke variabele onze functie mee krijgt (in het aanroepen); hier in print\_dubbel, noemen we de variabele die het argument bevat, jan.
> 
> ## 3.9 Variabelen en parameters zijn lokaal
> 
> Zodra u een variabele aanmaakt in een functie, is deze **lokaal**; dit houdt in dat deze alleen bestaat binnen de functie. Bijvoorbeeld:
> 
> def samen\_dubbel(deel1, deel2):
>      samen = deel1 + deel2
>      print\_dubbel(samen)
> 
> Deze functie krijgt twee argumenten, voegt die samen en print het resultaat twee keer. Hierbij een voorbeeld in de praktijk:
> 
> \>>> regel1 = 'Oze wiezewoze'
> \>>> regel2 = 'wieze walla kristalla.'
> \>>> samen\_dubbel(regel1, regel2)
> Oze wiezewoze wieze walla kristalla.
> Oze wiezewoze wieze walla kristalla.
> 
> Zodra samen\_dubbel stopt, wordt de variabele samen verwijderd.
> 
> Als we die variabele willen printen buiten de functie samen\_dubbel, krijgen we een foutmelding :
> 
> \>>> print samen
> NameError: name 'samen' is not defined
> 
> Parameters zijn ook lokaal. Bijvoorbeeld: buiten de functie samen\_dubbel bestaan de variabelen "deel1" en "deel2" niet.
> 
> ## 3.10 Stapeldiagrammen
> 
> Het is over het algemeen nuttig om een **stapeldiagram** te tekenen en daarin bij te houden waar welke variabele kan worden gebruikt. Net als toestandsdiagrammen tonen stapeldiagrammen de waarde van iedere variabele, maar laten ze ook zien bij welke functie een variabele behoort.
> 
> Elke functie is weergegeven als een blok. Een **blok** is een omlijnd gebied met ervoor de naam van de functie en de parameters en variabelen van de functie daarbinnen. Het stapeldiagram van het vorige voorbeeld lijkt hierop:
> 
> -   ![boek004_nl_2.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukDrie?action=AttachFile&do=get&target=boek004_nl_2.png "boek004_nl_2.png")
>     
> 
> De blokken zijn geordend als een stapel zodat duidelijk wordt wie een functie aanroept. In dit voorbeeld: print\_dubbel wordt aangeroepen door samen\_dubbel, en samen\_dubbel wordt aangeroepen door \_\_main\_\_; dit is een speciale naam voor het hoogste blok. Maakt u een variabele buiten enige functie om dan behoort deze tot \_\_main\_\_.
> 
> Elke parameter verwijst naar dezelfde waarde als zijn overeenkomstige argument. Dus, deel1 heeft dezelfde waarde als regel1, deel2 heeft dezelfde waarde als regel2, en jan heeft dezelfde waarde als samen.
> 
> Geeft een functieaanroep een foutmelding dan zal Python de naam van de functie printen en de naam van de functie die de aanroep verzorgde en de naam van de functie die deze weer aanriep enzovoorts tot we terug zijn bij \_\_main\_\_.
> 
> Bijvoorbeeld: probeert u samen aan te roepen vanuit print\_dubbel, dan krijgt u een NameError:
> 
> vind\_oorsprong(binnenste laatste):
>    File "test.py", line 13, in \_\_main\_\_
>      samen\_dubbel(regel1, regel2)
>    File "test.py", line 5, in samen\_dubbel
>      print\_dubbel(samen)
>    File "test.py", line 9, in print\_dubbel
>      print samen
> NameError: name 'samen' is not defined
> 
> Deze lijst van functies wordt **vind\_oorsprong** genoemd. Het maakt duidelijk in welke functie de fout optreedt, op welke regel dit gebeurde en welke functies werden uitgevoerd op dat moment. De volgorde van de functies in de 'vind\_oorsprong' is hetzelfde als de volgorde van de blokken in het stapeldiagram. De functie die op dat moment uitgevoerd wordt staat onderaan.
> 
> ## 3.11 Productieve functies en lege functies
> 
> Enkele van de gebruikte functies, zoals de wiskundige functies, leveren een resultaat; voor het gemak noemen we deze **productieve functies**. Andere functies, zoals print\_dubbel, voeren een actie uit maar geven geen resultaat of waarde terug. Deze worden **lege functies** genoemd.
> 
> Roept u een productieve functie aan, dan wilt u bijna altijd iets doen met het resultaat. Bijvoorbeeld: u zou het aan een variabele kunnen toekennen of het gebruiken als onderdeel van een expressie:
> 
> x = math.cos(radialen)
> gouden = (math.sqrt(5) + 1) / 2
> 
> Roept u een functie aan in interactieve modus, dan zal Python het resultaat weergeven:
> 
> \>>> math.sqrt(5)
> 2.2360679774997898
> 
> Zodra u een productieve functie op zichzelf aanroept in een script, raakt het resultaat verloren!
> 
> math.sqrt(5)
> 
> Dit script berekent de wortel van vijf, maar omdat het de uitkomst niet opslaat of weergeeft, is dit niet erg zinvol.
> 
> Lege functies kunnen iets weergeven op het scherm of een ander effect teweegbrengen, maar ze geven geen waarde terug. Probeert u het resultaat toe te kennen aan een variabele, dan krijgt u een speciale waarde genaamd 'None' (niets).
> 
> \>>> resultaat = print\_dubbel('Oze')
> Oze
> Oze
> \>>> print resultaat
> None
> 
> De waarde None is niet hetzelfde als de string 'None'. Het is een speciale waarde die zijn eigen type heeft:
> 
> \>>> print type(None)
> <type 'NoneType'>
> 
> De functies die we tot nu toe hebben gemaakt zijn allemaal lege functies. We zullen over enkele hoofdstukken starten met het maken van productieve functies.
> 
> ## 3.12 Waarom functies?
> 
> Het kan zijn dat het nog niet duidelijk voor u is waarom we zoveel moeite doen om een programma in functies op te delen. We doen dit om de volgende redenen:
> 
> -   Het maken van een nieuwe functie biedt de mogelijkheid om een groep instructies van een naam te voorzien, dit maakt dat het programma makkelijker te lezen is.
> -   Functies kunnen een programma kleiner maken doordat zich herhalende code geschrapt wordt. Later, bij het aanbrengen van wijzigingen aan de reeks instructies, hoeft dit maar op één plek te gebeuren.
> -   Een lang programma opdelen in functies maakt het mogelijk om de delen stuk voor stuk te debuggen en deze vervolgens tot een werkend geheel samen te voegen.
> -   Goed ontworpen functies zijn vaak nuttig voor meerdere programma's. Als u eenmaal een functie hebt gemaakt en getest, kunt niet alleen u ze steeds weer gebruiken, maar ook anderen in hun programma's.
> 
> ## 3.13 Debuggen
> 
> Gebruikt u een tekstverwerker bij het maken van uw scripts, dan kunt u in de problemen komen met spaties en tabstops. De beste manier om deze problemen te vermijden, is om alleen spaties te gebruiken (dus geen tabstops). De meeste tekstverwerkers die Python kennen, doen dit standaard, maar sommige ook niet.
> 
> Tabstops en spaties zijn normaal gesproken niet zichtbaar en zijn daardoor moeilijk te debuggen; zoek dus naar en gebruik een tekstverwerker die het inspringen voor u afhandelt.
> 
> Vergeet ook niet om uw programma op te slaan voordat u dit uitvoert. Een aantal ontwikkelomgevingen doen dit automatisch maar sommigen ook niet. In dat geval kan het zijn dat het programma waar u naar kijkt in de tekstverwerker, niet hetzelfde is als het programma dat u uitvoert.
> 
> ![Info (!)](https://wiki.ubuntu-nl.org/static/light/img/icon_cool.png "Info (!)") Debuggen kan heel lang duren als u steeds hetzelfde, verkeerde, programma keer op keer uitvoert!
> 
> Verzeker u ervan dat de code waar u naar kijkt ook de code is die u uitvoert. Bent u hiervan niet zeker, plaats dan zoiets als print 'hallo' aan het begin van het programma en voer het opnieuw uit. Ziet u hallo niet verschijnen, dan voert u niet het juiste programma uit!
> 
> ## 3.14 Woordenlijst
> 
> **functie:** Een benoemde reeks instructies die een zinvolle actie uitvoert. Functies mogen argumenten meekrijgen en mogen een resultaat teruggeven, maar u bent daar niet toe verplicht.
> 
> **functiedefinitie:** Een instructie waarmee een nieuwe functie wordt aangemaakt; specificeert zijn naam, eventuele parameters en de instructies die het uitvoert.
> 
> **functieobject:** Een waarde aangemaakt door een functiedefinitie. De naam van de functie is een variabele die verwijst naar een functieobject.
> 
> **kop:** De eerste regel van een functiedefinitie.
> 
> **body:** De reeks instructies binnen een functiedefinitie.
> 
> **parameter:** Een naam gebruikt binnen een functie die verwijst naar de waarde doorgegeven als een argument.
> 
> **functieaanroep:** Een instructie die een functie uitvoert. Deze bestaat uit de functienaam die eventueel gevolgd wordt door een lijst met argumenten tussen haken, of lege haken.
> 
> **argument:** Een waarde doorgegeven aan een functie op het moment dat de functie aangeroepen wordt. Deze waarde is toegewezen aan de overeenkomstige parameter in de functie.
> 
> **lokale variabele:** Een variabele gedefinieerd binnen een functie. Een lokale variabele kan alleen binnen een functie worden gebruikt.
> 
> **antwoordwaarde:** Het resultaat van een functie. Wordt een functieaanroep gebruikt in een expressie, dan is de antwoordwaarde de uitkomst van de expressie.
> 
> **productieve functie:** Een functie die een waarde teruggeeft.
> 
> **lege functie:** Een functie die geen waarde teruggeeft.
> 
> **module:** Een bestand dat een verzameling van gerelateerde functies en andere definities bevat.
> 
> **importinstructie:** Een instructie die een modulebestand inleest en een moduleobject aanmaakt.
> 
> **moduleobject:** Een waarde aangemaakt door een importinstructie die toegang geeft aan de waarden gedefinieerd in een module.
> 
> **puntnotatie:** De zinsbouw voor het aanroepen van een functie in een andere module door een modulenaam te specificeren gevolgd door een punt en de functienaam.
> 
> **compositie:** Gebruik maken van een expressie als onderdeel van een grotere expressie, of een instructie als onderdeel van een grotere instructie.
> 
> **volgorde van uitvoering:** De volgorde waarin instructies worden uitgevoerd gedurende de werking van het programma.
> 
> **stapeldiagram:** De grafische weergave van functies in de vorm van gestapelde blokken, met de bijbehorende variabelen en waarden waarnaar deze verwijzen.
> 
> **blok:** Een omlijnd gebied in een stapeldiagram dat een functieaanroep weergeeft. Het bevat de lokale variabelen en parameters van die functie.
> 
> **vind\_oorsprong:** Een lijst van de functies die worden uitgevoerd, geprint op het moment dat zich een fout voordoet.
> 
> ## 3.15 Oefeningen
> 
> **Oefening 3.3** Python levert een ingebouwde functie genaamd len die de lengte van een string teruggeeft, dus de waarde van len('allen') is 5.
> 
> Schrijf een functie genaamd rechts\_opvullen die de string, genaamd 's', als parameter oppakt en de string afdrukt met voldoende voorloopspaties, zodanig dat de laatste letter van de string op positie 70 staat van het scherm.
> 
> \>>> rechts\_opvullen('allen')  allen
> 
> **Oefening 3.4** Een functieobject is een waarde die u kunt toewijzen aan een variabele of als argument kunt doorgeven. Bijvoorbeeld: doe\_twee\_keer is een functie die een functieobject oppakt als een argument en deze twee keer aanroept:
> 
> def doe\_twee\_keer(f):
>       f()
>       f()
> 
> Hier is een voorbeeld dat doe\_twee\_keer gebruikt om een functie genaamd print\_spam twee keer aan te roepen.
> 
> def print\_spam():
>     print 'spam'
> doe\_twee\_keer(print\_spam)
> 
> 1.  Neem dit voorbeeld over in een script en test het.
> 2.  Wijzig doe\_twee\_keer zodanig dat het twee argumenten meekrijgt, een functieobject en een waarde, en de functie twee keer aanroept, waarbij de waarde als een argument wordt doorgegeven.
>     
> 3.  Maak een generieke versie van print\_spam, genaamd print\_dubbel, die een string oppakt als een parameter en deze twee keer afdrukt.
>     
> 4.  Gebruik de gewijzigde versie van doe\_twee\_keer om de print\_dubbel twee keer aan te roepen, daarbij 'spam' als een argument door te geven.
>     
> 5.  Definieer een nieuwe functie genaamd doe\_vier\_keer die een functieobject oppakt en een waarde en de functie vier keer aanroept, en daarbij de waarde als parameter doorgeeft. Er moeten maar twee instructies in de body van deze functie voorkomen, geen vier.
>     
> 
> U kunt mijn oplossing bekijken bij [thinkpython.com/code/do\_four.py](http://thinkpython.com/code/do_four.py).
> 
> **Oefening 3.5** Deze oefening2 kan gemaakt worden met gebruikmaking van de instructies en andere functies die u tot nu toe hebt geleerd.
> 
> 1.  Schrijf een functie die een raster tekent dat lijkt op het onderstaande:
>     -   ![h3o15.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukDrie?action=AttachFile&do=get&target=h3o15.png "h3o15.png")
>         
>           
>         ![Info (!)](https://wiki.ubuntu-nl.org/static/light/img/icon_cool.png "Info (!)") Tip: om meer dan één waarde op een regel te printen kunt u een reeks printen, gescheiden door een komma:
>         
>         print '+', '-'
>         
>           
>         Eindigt de reeks met een komma, dan laat Python de regel staan, dus de eerstvolgende waarde verschijnt op dezelfde regel.
>         
>         print '+', print '-'
>         
>           
>         De uitvoer van deze instructies is '+ -'.  
>         Een print instructie op zichzelf beëindigt de huidige regel en gaat over in een nieuwe regel.
>         
> 2.  Schrijf met gebruik van de voorgaande functie een functie om een gelijksoortig raster te tekenen met vier rijen en vier kolommen.
> 
> U kunt een uitwerking vinden op [thinkpython.com/code/grid.py](http://thinkpython.com/code/grid.py).
> 
> * * *
> 
> 1 We zullen later uitzonderingen op deze regel zien.  
> 2 Gebaseerd op een oefening Oualline, Practical C Programming, Third Edition, O’Reilly (1997)