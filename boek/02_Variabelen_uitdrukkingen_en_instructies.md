[community/ThinkPython/HoofdstukTwee - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwee)

# Hoofdstuk 2 Variabelen, uitdrukkingen en instructies

## 2.1 Waarden en typen

Een **waarde** (value) is één van de basisfuncties waarmee een programma werkt, zoals een letter of een cijfer. De waarden die we tot nu toe hebben gezien waren: 1, 2, en 'Hello, World!'.

Deze waarden zijn van verschillende **types**: 2 is een integer, en 'Hello, World!' is een **string**. Deze is zo genoemd omdat het een "koord" (string) van letters bevat. U kunt (en de interpreter kan) strings identificeren omdat zij tussen aanhalingstekens staan.

De print instructie werkt ook voor integers.

\>>> print 4
4

Als u niet zeker weet wat het type van de waarde is kan de interpreter het u vertellen.

\>>> type('Hello, World!')
<type 'str'>
\>>> type(17)
<type 'int'>

Het is geen verrassing dat strings tot het type str behoren en dat integers tot het type int behoren. Getallen met een decimale punt behoren tot het type float, omdat deze getallen in het formaat **floating-point** (drijvende komma) worden gepresenteerd.

\>>> type(3.2)
<type 'float'>

Hoe zit het met waarden als: '17' en '3.2'? Ze lijken op getallen, maar ze staan tussen aanhalingstekens zoals strings.

\>>> type('17')
<type 'str'>
\>>> type('3.2')
<type 'str'>

Dit zijn strings.

Als u een groot getal typt, zou u kunnen overwegen om komma's te gebruiken, tussen groepen van drie tekens, zoals in 1,000,000. Dit is geen correct getal in Python, maar het is toegestaan.

\>>> print 1,000,000
1 0 0

Goed, maar dat is niet wat we hadden verwacht! Python vertaalt 1,000,000 als een komma-gescheiden opeenvolging van getallen, die worden weergegeven met een ruimte ertussen.

Dit is het eerste voorbeeld dat we hebben gezien van een semantische fout; de code is bezig zonder dat er een fout wordt getoond, echter het functioneert niet "goed".

## 2.2 Variabelen

Een van de meest krachtige functies van een programmeertaal is de capaciteit om **variabelen** te bewerken. Een variabele is een naam die verwijst naar een waarde.

Een **assignment statement** (toewijzingsinstructie) maakt nieuwe variabelen aan en geeft ze een waarde:

\>>> boodschap= 'En nu iets totaal anders'
\>>> n = 17
\>>> pi = 3.1415926535897931

Dit voorbeeld maakt drie toewijzingen. De eerste wijst een string toe aan een nieuwe variabele, genaamd: boodschap. De tweede wijst de integer 17 toe aan n; de derde wijst de (benadering van de) waarde van π aan pi toe.

Een veel voorkomende manier om variabelen op papier weer te geven, is om de naam op te schrijven met een pijl die wijst naar de waarde van de variabele. Zo'n figuur wordt **state diagram** (toestandsdiagram) genoemd omdat het laat zien wat de toestand van elke verwijzing is. (stel het je voor als de gemoedstoestand van een variabele). Dit diagram toont het resultaat uit het (vorige) voorbeeld:

-   ![boek003_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwee?action=AttachFile&do=get&target=boek003_nl.png "boek003_nl.png")
    

Om weer te geven wat de waarde van een variabele is, kunt u de print instructie gebruiken:

\>>> print n
17
\>>> print pi
3.14159265359

Het type van een variabele is het type van de waarde waar de variabele naar verwijst.

\>>> type(boodschap)
<type 'str'>
\>>> type(n)
<type 'int'>
\>>> type(pi)
<type 'float'>

**Oefening 2.1** Als u een integer typt die begint met een nul, zou u misschien een confusing error (verwarrende fout) kunnen krijgen:

\>>> postcode = 02492
                  ˆ
SyntaxError: invalid token

Andere nummers lijken te werken, maar de resultaten zijn vreemd:

\>>> postcode = 02132
\>>> print postcode 
1114

Begrijpt u wat er gebeurt? Tip: print de waarden 01, 010, 0100 en 01000.

## 2.3 Variabelenamen en sleutelwoorden

Programmeurs kiezen meestal zinvolle namen voor hun variabelen. Ze documenteren waarvoor de variabelen worden gebruikt. Namen van variabelen kunnen een willekeurige lengte hebben. Ze kunnen veel letters en nummers bevatten. Maar ze beginnen altijd met een letter. Het is toegestaan om hoofdletters te gebruiken, maar het is een goed idee om de namen van variabelen met een kleine letter te laten beginnen (later zal duidelijk worden waarom).

Het onderstrepingsteken (\_) kan voorkomen in een naam. Het wordt veel gebruikt in namen met veel woorden, zoals mijn\_naam of luchtsnelheid\_van\_een\_ongeladen\_vliegtuig.

Als u een variabele een foutieve naam geeft, krijgt u een syntaxis fout:

\>>> 76trombones = 'grote optocht'
SyntaxError: invalid syntax
\>>> more@ = 1000000
SyntaxError: invalid syntax
\>>> class = 'Geadvanceerde theoretische zymurgie'
SyntaxError: invalid syntax

76trombones is foutief omdat het niet begint met een letter. more@ is ook niet correct omdat het een verkeerd teken bevat, @. Maar wat is er dan verkeerd aan class?

class is één van Python's **keywords** (sleutelwoorden). De interpreter gebruikt sleutelwoorden om de structuur van het programma te verbeteren, en deze kunnen niet worden gebruikt als namen voor variabelen. Python heeft 31 sleutelwoorden1 :

and      del     from   not    while
as       elif    global or     with
assert   else    if     pass   yield
break    except  import print
class    exec    in     raise
continue finally is     return
def      for     lambda try

Het is misschien handig om dit lijstje te bewaren. Als de interpreter klaagt over de naam van één van de variabelen en u weet niet waarom, kijk dan op deze lijst.

## 2.4 Instructies

Een instructie is een stukje code dat de Python interpreter kan uitvoeren. We hebben twee soorten instructies gezien: print en toewijzing.

Wanneer u een instructie in interactieve modus typt, voert de interpreter deze uit en geeft het resultaat weer, mits er een resultaat is.

Een script bevat meestal meerdere instructies. Als er meerdere instructies zijn verschijnen de resultaten één voor één, zolang de instructies worden uitgevoerd. Bijvoorbeeld: het script

print 1
x = 2
print x

geeft de volgende uitvoer

1
2

De toewijzingsinstructie geeft geen uitvoer weer.

## 2.5 Operators en operanden

**Operators** zijn speciale symbolen die berekeningen vertegenwoordigen zoals optellen en vermenigvuldigen. De waarden waar de operator op wordt toegepast heten **operanden**.

De operators +, -, \*, / en \*\* voeren een optelling, aftrekking, vermenigvuldiging, deling en een kwadratering uit, zoals in de volgende voorbeelden:

20+32       hour-1      hour\*60+minute        minute/60    5\*\*2     (5+9)\*(15-7)

In sommige andere talen wordt de "ˆ" gebruikt voor het kwadraat maar in Python is dit een bitwise operator genaamd XOR. Ik behandel bitwise operatoren niet in dit boek maar u kunt informatie daarover nalezen op [wiki.python.org/moin/BitwiseOperators](http://wiki.python.org/moin/BitwiseOperators).

De operator voor delen is misschien niet degene die u zou verwachten:

\>>> minute = 59
\>>> minute/60
0

De waarde voor minute is 59 en in conventionele rekenkunde is 59 gedeeld door 60 0.98333, geen 0. De reden voor deze afwijking is dat Python een **"floor division"**2 uitvoert.

Wanneer beide operanden integers zijn, dan is het resultaat ook een integer; "floor division" hakt de rest af, dus in dit voorbeeld wordt het resultaat afgerond naar nul.

Zijn beide operanden een floating-point getal, dan voert Python een floating-point deling uit en het resultaat is een float:

\>>> minute/60.0
0.98333333333333328

## 2.6 Expressies

Een **expressie** is een combinatie van waarden, variabelen en operatoren. Een waarde op zichzelf wordt beschouwd als een expressie, net als een variabele, dus de onderstaande expressies zijn alle rechtmatig (aangenomen dat aan de variabele x een waarde is toegekend):

17
x
x + 17

Typt u in interactieve modus een expressie in, dan zal de interpreter deze **evalueren** en het volgende resultaat weergeven:

\>>> 1 + 1
2

In een script echter doet een expressie op zichzelf niets! Dit is een gebruikelijke verwarring bij beginners.

**Oefening 2.2** Typ de volgende instructies in de Python interpreter om zien wat er gebeurt:

5
x = 5
x + 1

Plaats nu dezelfde instructies in een script en draai dit af. Wat is de uitkomst? Verander het script door iedere expressie om te vormen naar een print instructie en draai het opnieuw af.

## 2.7 Volgorde van bewerkingen

Wanneer meerdere operatoren in een expressie voorkomen, hangt de volgorde van de evaluatie af van de **voorrangsregels**. Voor wiskundige operatoren volgt Python de conventie uit de wiskunde:

-   **H**aakjes hebben de hoogste voorrang en worden gebruikt om een expressie te forceren om de door u gewenste volgorde te hanteren. Omdat expressies tussen haakjes als eerste worden geëvalueerd, 2 \* (3-1) is 4 en (1+1)\*\*(5-2) is 8. Haakjes zijn ook nuttig om een expressie gemakkelijker leesbaar te maken, zoals in (minute \* 100) / 60, ook al verandert het resultaat niet.
    
-   **M**achtsverheffen heeft de daarop volgende voorrang, dus 2\*\*1+1 is 3 en niet 4, 3\*1\*\*3 is 3 en niet 27.
    
-   **V**ermenigvuldigen en **D**elen hebben dezelfde rang, deze is hoger dan **O**ptellen en **A**ftrekken, deze beiden hebben ook dezelfde rang. Dus 2\*3-1 is 5 en niet 4, 6+4/2 is 8 en niet 5.
    
-   Operatoren met dezelfde rang worden van links naar rechts geëvalueerd. Dus in de expressie graden / 2 \* pi wordt de deling eerst uitgevoerd en het resultaat vermenigvuldigd met pi. Om te delen door 2π verwisselt u de operand of u gebruikt haakjes.
    

## 2.8 String bewerkingen

In het algemeen is het mogelijk om wiskundige bewerkingen toe te passen op strings, ook als strings op getallen lijken, dus het volgende is niet foutief:

'2'-'1'           'eggs'/'easy'           'third'\*'a charm'

De "+" operator werkt met strings maar zal waarschijnlijk niet dat doen wat u verwacht: deze voert een **samentrekken** uit, wat inhoudt dat de beide strings samengevoegd worden, van begin tot het eind. Bijvoorbeeld:

eerste = 'keel'
tweede = 'zanger'
print eerste + tweede 

De uitkomst van dit programma is keelzanger.

De "\*" operator werkt ook op strings, deze voert herhalingen uit. Bijvoorbeeld, 'Spam'\*3 is 'SpamSpamSpam'. Als één operand een string is moet de andere een integer zijn.

Dit gebruik van de "+" en de "\*" is zinnig door de overeenkomst met optellen en vermenigvuldigen. Net zoals 4\*3 gelijk is aan 4+4+4, verwachten we dat 'Spam'\*3 gelijk is aan 'Spam'+'Spam'+'Spam' en dat is zo. Aan de andere kant bestaat een significant onderscheid tussen het samentrekken en herhalen van een string en het optellen en vermenigvuldigen van een integer. Kunt u een eigenschap van een optelling bedenken die een string samentrekken niet heeft?

## 2.9 Commentaar

Met dat programma's groeien en gecompliceerder worden, is het ook moeilijker om ze te lezen. Formele talen zijn compact en het is vaak moeilijk om te bepalen wat een stukje code doet en waarom.

Om die reden is het een goed idee om notities toe te voegen aan uw programma waarin wordt uitgelegd wat het programma doet, in een natuurlijke taal. Deze notities worden **commentaar** genoemd en beginnen met het "#" symbool:

\# bereken het percentage van het uur dat is verlopen
percentage = (minute \* 100) / 60

In dit geval staat het commentaar op een eigen regel, u kunt ook commentaar aan het einde van een regel plaatsen:

percentage = (minute \* 100) / 60     # percentage van een uur

Alles vanaf het "#" tot aan het einde van de regel wordt genegeerd en heeft geen effect op de werking van het programma.

Commentaar is pas echt waardevol wanneer de niet voor de hand liggende kenmerken van de code gedocumenteerd worden. Het is redelijk om aan te nemen dat de lezer snapt _wat_ de code doet; het is dus zeker zinvol om uit te leggen _waarom_ deze code nodig is.

Het volgende commentaar is dubbelop met de code en nutteloos:

v = 5          # ken 5 toe aan v

Het volgende commentaar is wel zinvol, want het legt iets uit wat we niet meteen uit de regel code kunnen afleiden, namelijk de betekenis van de variabele "v":

v = 5          # snelheid in meters/seconde.

Zinvolle namen van variabelen kunnen de noodzaak van commentaar verminderen maar lange namen maken complexe expressies moeilijk leesbaar; er is dus een wisselwerking.

## 2.10 Debuggen

Op dit punt aangekomen zijn de syntax fouten waarschijnlijk te wijten aan foutieve namen van variabelen, zoals class en yield, dit zijn namelijk sleutelwoorden. race~baan en US$ bevatten verboden karakters.

Plaatst u een spatie in de naam van een variabele, dan neemt Python aan dat het om twee operanden gaat zonder een operator:

\>>> verkeerde naam = 5
SyntaxError: invalid syntax

Bij syntax fouten is de boodschap niet echt helder. De meest voorkomende boodschappen zijn SyntaxError: invalid syntax and SyntaxError: invalid token, geen van tweeën geeft veel informatie.

De runtime fouten die u waarschijnlijk het meest maakt is een “use before def;” dat wil zeggen: u probeert een variabele te gebruiken voordat hieraan een waarde is toegekend. Dit kan voorkomen als u de naam van de variabele verkeerd spelt:

\>>> kapitaal = 327.68
\>>> rente = kapiteel \* koers
NameError: name 'kapiteel' is not defined

Namen van variabelen zijn hoofdletter gevoelig, dus LaTeX is niet hetzelfde als latex. Op dit punt aangekomen zijn de meest waarschijnlijke oorzaken van een semantische fout de volgorde van operaties. Bijvoorbeeld, om 1/2 π te berekenen zou je geneigd zijn dit op te schrijven:

\>>> 1.0 / 2.0 \* pi

Maar de deling wordt als eerste uitgevoerd, dus krijgt u π/2 en dat is niet hetzelfde! Python kan op geen enkele wijze weten wat u bedoelde, dus in dit voorbeeld krijgt u geen fout boodschap maar gewoon het verkeerde antwoord.

## 2.11 Woordenlijst

**waarde**: Een van de basiseenheden van een gegeven, zoals een getal of string waarmee een programma bewerkingen uitvoert.

**type**: De categorie van een waarde. De types die we tot nu toe hebben gezien zijn: integers (type int), floating-point nummers (type float) en strings (type str).

**integer**: Een type dat gehele getallen vertegenwoordigt.

**floating-point**: Een type dat getallen met cijfers achter de komma vertegenwoordigt.

**string**: Een type dat een serie karakters vertegenwoordigt.

**variabele**: Een naam die verwijst naar een waarde.

**statement**: Een deel van de code die een instructie of een opdracht vertegenwoordigt. Tot nu toe zijn de instructies die we hebben gezien toewijzingen en print instructies.

**toewijzing**: Een instructie waarmee een waarde aan een variabele wordt toegewezen.

**toestandsdiagram (state diagram)**: Een grafische voorstelling van een aantal variabelen en de waarden waarnaar ze verwijzen.

**sleutelwoord (keyword)**: Een gereserveerd woord dat door de interpreter wordt gebruikt om het programma te ontleden; u mag geen sleutelwoorden gebruiken zoals "if", "def" en "while" als naam voor een variabele.

**operator**: Een special symbool dat een eenvoudige bewerking beschrijft zoals optellen, vermenigvuldigen of samentrekken van een string.

**operand**: Eén van de waarden die door een operator wordt bewerkt.

**floor division**: De bewerking die twee getallen deelt en de rest afhakt.

**expressie**: Een combinatie van variabelen, operatoren en waarden die één enkele waarde weergeeft.

**evalueren**: Vereenvoudigen van de expressie door het uitvoeren van de bewerkingen en zo te komen tot één enkele waarde.

**voorrangsregels**: De set aan regels die de volgorde bepalen waarin een expressie met meerdere operatoren en operanden geëvalueerd wordt.

**samentrekken**: Voeg twee operanden samen van begin tot het eind.

**commentaar**: Informatie in een programma die bedoeld is voor andere programmeurs of wie dan ook die de broncode leest. Commentaar heeft geen effect op de werking van het programma.

## 2.12 Oefeningen

**Oefening 2.3** Stel je voor dat we de volgende toewijsinstructies uitvoeren:

breedte = 17
hoogte = 12.0
scheidingsteken = '.'

Schrijf voor elk van de volgende expressies de waarde van de expressie op en het type (van de waarde van de expressie).

   1. breedte/2
   2. breedte/2.0
   3. hoogte/3
   4. 1 + 2 \* 5
   5. scheidingsteken \* 5

Gebruik de Python interpreter om uw antwoorden te controleren.

**Oefening 2.4** training in het gebruik van de Python interpreter als rekenmachine:

1.  Het volume van een bol met straal r is 4/3 π r3. Wat is het volume van een bol met straal 5? Aanwijzing: 392.6 is fout!
    
2.  Veronderstel dat de adviesverkoopprijs van een boek €24.95 is maar boekwinkels krijgen 40% korting. Verzendkosten bedragen €3 voor het eerste exemplaar en 75 cent voor elk volgend exemplaar. Wat is de totale inkoopsprijs voor 60 exemplaren?
3.  Als ik om 6:52 uur 's ochtend het huis uit ga en 1 km hard loop in een rustig tempo (5:25 minuten per km), dan 3 km in een tempo van (4:48 minuten per km) en daarna 1 km opnieuw in een rustig tempo, op welk tijdstip ben ik thuis voor het ontbijt?

\---

1 In Python 3.0, is "exec" niet langer een sleutelword maar "nonlocal" wel.  
2 In Python 3.0, is het resultaat van deze deling een float. De nieuwe operator // voert een integer deling uit.

