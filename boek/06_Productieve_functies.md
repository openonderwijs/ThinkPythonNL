[community/ThinkPython/HoofdstukZes - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZes)

# Hoofdstuk 6 Productieve functies

## 6.1 Antwoordwaarden

Een aantal van de ingebouwde functies die we gebruikt hebben, zoals de wiskundige functies, leveren resultaten. Door het aanroepen van de functie ontstaat een waarde die we doorgaans toekennen aan een variabele of gebruiken als onderdeel van een expressie.

e = math.exp(1.0)
hoogte  = straal \* math.sin(radians)

Alle functies die we tot nu toe hebben geschreven, zijn leeg. Ze drukken iets af of bewegen turtles (zie oefening 5.4 in [hfdst. 5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijf#A5.14Oefeningen)) rond maar hun antwoordwaarde is Niets.

In dit hoofdstuk gaan we eindelijk productieve functies schrijven. Het eerste voorbeeld is oppervlakte, die de oppervlakte teruggeeft van een cirkel met een gegeven straal:

def oppervlakte(straal):
      tijdelijk = math.pi \* straal\*\*2
      return tijdelijk 

We hebben de return instructie eerder gezien maar in een productieve functie bevat de return instructie een expressie. Deze instructie betekent: "Keer onmiddelijk terug uit deze functie en gebruik de volgende expressie als antwoordwaarde". De expressie kan onnodig ingewikkeld zijn, bijvoorbeeld als we deze functie beknopter zouden schrijven:

def oppervlakte(straal):
      return math.pi \* straal\*\*2

Aan de andere kant maken **tijdelijke variabelen** zoals tijdelijk het debuggen gemakkelijker.

Soms is het handig om meerdere return instructies te hebben en wel één in iedere tak van een voorwaarde:

def absolute\_waarde(x):
      if x < 0:
           return -x
      else:
           return x

Omdat deze return instructies elk in een eigen tak van een voorwaarde staan, zal er altijd maar één uitgevoerd worden..

Zodra een return instructie uitgevoerd wordt, stopt de functie zonder ook nog maar enige instructie uit te voeren. Code die na het return statement staat of op een andere plaats waar de volgorde van uitvoering deze niet kan bereiken wordt **dode code** genoemd.

In een productieve functie is het een goed idee om ervoor te zorgen dat iedere mogelijke weg door de functie een return instructie raakt. Bijvoorbeeld:

def absolute\_waarde(x):
       if x < 0:
             return -x
       if x > 0:
             return x

Deze functie is incorrect, omdat als x gelijk is aan 0, aan geen van de voorwaarden wordt voldaan en de functie eindigt zonder dat een return instructie wordt geraakt. Bereikt de volgorde van uitvoeren het einde van de functie, dan is de antwoordwaarde Niets (None) en dat is niet de absolute waarde 0.

\>>> print absolute\_waarde(0)
None

Overigens levert Python een ingebouwde functie genaamd abs die absolute waarden berekent.

**Oefening 6.1** Schrijf een vergelijkings functie die een 1 terug geeft als x > y, 0 als x == y en \-1 als x < y.

## 6.2 Incrementeel ontwikkelen

Zodra u grotere functies schrijft kan het zo zijn dat u meer tijd kwijt bent met debuggen.

Bij het omgaan met complexe programma's kunt u het zogenaamde proces van **incrementeel ontwikkelen** uitproberen. Het doel van incrementeel ontwikkelen is het vermijden van een langdurige debugsessie door het toevoegen en testen van kleine hoeveelheden code per keer.

Als voorbeeld, u wilt de afstand tussen twee punten berekenen met de gegeven coördinaten (x1 , y1 ) en (x2 , y2 ). Volgens de stelling van Pythagoras is de afstand:

-   ![formula001.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZes?action=AttachFile&do=get&target=formula001.png "formula001.png")
    

De eerste stap is te bedenken hoe een afstand functie in Python eruit moet zien. Met andere woorden wat is de invoer (parameters) en wat de uitvoer (antwoordwaarde)?

In dit geval is de invoer de twee punten die zijn weergegeven met vier getallen. De antwoordwaarde is de afstand en dat is een floating-point waarde.

Hiermee kunt u al een schets van de functie opschrijven:

def afstand(x1, y1, x2, y2):
       return 0.0

Natuurlijk berekent deze versie geen afstand en geeft zo altijd nul terug. Maar de zinsopbouw is correct en uitvoerbaar; dit houdt in dat deze functie te testen is voordat deze gecompliceerder wordt.

Test de nieuwe functie met enkele proef argumenten:

\>>> afstand(1, 2, 4, 6)
0.0

Deze waarden zijn zo gekozen dat de horizontale afstand 3 is, de verticale afstand 4 en het resultaat is dus 5. (de schuine zijde van een 3-4-5 driehoek). Bij het testen van een functie is het handig om het juiste antwoord te weten.

Op dit punt aangekomen is bevestigd dat de zinsbouw van de functie correct is en kunnen we meer code toe gaan voegen. Een verstandige vervolgstap is het vinden van het verschil van x2 − x1 en y2 − y1. De volgende versie slaat deze waarden op in tijdelijke variabelen en geeft ze weer.

def afstand(x1, y1, x2, y2):
      dx = x2 - x1
      dy = y2 - y1
      print 'dx is', dx
      print 'dy is', dy
      return 0.0

Als de functie werkt, geeft het 'dx is 3' en ’dy is 4’ weer. Zo ja, dan weten we dat de functie de juiste argumenten mee krijgt en de eerste berekening goed uitvoert. Zo niet, dan hoeven we maar een paar regels te controleren.

Vervolgens berekenen we de optelsom van kwadraten van dx en dy:

def afstand(x1, y1, x2, y2):
      dx = x2 - x1
      dy = y2 - y1
      dkwadraat = dx\*\*2 + dy\*\*2
      print 'd-kwadraat is: ', dkwadraat 
      return 0.0

En weer voeren we het programma uit en controleren we de uitvoer (deze moet 25 zijn). Uiteindelijk gebruiken we math.sqrt (vierkantswortel) om het resultaat te berekenen en terug te geven:

def afstand(x1, y1, x2, y2):
      dx = x2 - x1
      dy = y2 - y1
      dkwadraat = dx\*\*2 + dy\*\*2
      resultaat = math.sqrt(dkwadraat)
      return resultaat

Werkt dit correct, dan zijn we klaar. Zo niet, dan wilt u mogelijk de waarde van resultaat weergeven, voorafgaand aan de return instructie.

De uiteindelijke versie geeft niets weer als deze wordt uitgevoerd; het geeft alleen een waarde terug. De print instructies zijn handig bij het debuggen maar zodra de functie werkt, zijn deze overbodig. Dergelijke code wordt een **steiger** genoemd omdat dit helpt bij het bouwen maar geen onderdeel is van het eindproduct.

Wanneer u zelf gaat programmeren moet u een paar regels code per keer toevoegen. Krijgt u meer en meer ervaring dan schrijft en test u vanzelf grotere brokken code. Hoe dan ook, incrementeel ontwikkelen scheelt later veel tijd bij het debuggen.

De belangrijkste aspecten van het proces zijn:

1.  Start met een werkend programma en maak kleine incrementele wijzigingen. Treedt er op enig moment een fout op, dan hebt u een goed beeld waar deze optreedt.
2.  Gebruik tijdelijke variabelen die de tussenwaarden bevatten zodat u deze kunt weergeven en controleren.
3.  Werkt het programma eenmaal dan kunt u de **steigers** verwijderen of meerdere instructies samenvoegen tot samengestelde expressies maar alleen dan wanneer de leesbaarheid niet achteruit gaat.
    

**Oefening 6.2** Maak gebruik van incrementeel ontwikkelen bij het schrijven van een functie genaamd **schuine\_zijde** die de lengte van de schuine zijde (hypotenusa) van een rechthoekige driehoek teruggeeft en waarbij de lengten van de twee rechthoekszijden als argumenten worden meegegeven. Beschrijf iedere stap van het ontwikkelproces bij het uitwerken.

## 6.3 Compositie

Zoals beschreven kunt u dus een functie aanroepen vanuit een andere functie. Deze mogelijkheid wordt **compositie** genoemd.

Bijvoorbeeld: We gaan een functie schrijven die twee argumenten meekrijgt, namelijk het middelpunt en een punt op de omtrek van de cirkel, en die aan de hand van deze argumenten de oppervlakte van die cirkel berekent.

Stel dat het middelpunt is opgeslagen in de variabelen xc en yc, het punt op de omtrek is opgeslagen in xp en yp. De eerste stap is het vinden van de straal van de cirkel; dit is de afstand tussen twee punten. We hebben zojuist een functie afstand geschreven, die dit berekent:

straal= afstand(xc, yc, xp, yp)

De volgende stap is het vinden van de oppervlakte van de cirkel met die straal; we hebben dat ook opgeschreven :

resultaat = oppervlakte(straal)

voeg deze stappen samen in een functie en we krijgen:

def cirkel\_oppervlakte(xc, yc, xp, yp):
     straal= afstand(xc, yc, xp, yp)
     resultaat = oppervlakte(straal)
     return resultaat

De tijdelijke variabele straal en resultaat zijn nuttig bij het ontwikkelen en het testen maar zodra het programma werkt, kunnen we een compacte versie samenstellen:

def cirkel\_oppervlakte(xc, yc, xp, yp):
     return oppervlakte(afstand(xc, yc, xp, yp))

## 6.4 Booleaanse functies

Functies kunnen een booleanse uitkomst teruggeven; dit is vaak handig om gecompliceerde en vaker voorkomende tests in functies uit te voeren. Bijvoorbeeld:

def is\_deelbaar(x, y):
     if x % y == 0:
           return True
     else:
           return False

Het is een goed gebruik om booleaanse functies namen te geven die klinken als een ja/nee vraag, is\_deelbaar geeft of True (waar) of False (onwaar) terug om daarmee aan te geven of x deelbaar is door y.

Hierbij een voorbeeld:

\>>>      is\_deelbaar(6, 4)
False
\>>>      is\_deelbaar(6, 3)
True

Het resultaat van de == operator is een booleaan, dus we kunnen een functie schrijven die compacter is door direct het antwoord terug te geven:

def is\_deelbaar(x, y):
      return x % y == 0

Booleaanse functies worden vaak gebruikt in voorwaardelijke instructies:

if is\_deelbaar(x, y):
      print 'x is deelbaar door y'

Het is verleidelijk om het als volgt op te schrijven:

if is\_deelbaar(x, y) == True:
      print 'x is deelbaar door y'

Maar de extra vergelijking is niet nodig.

**Oefening 6.3** Schrijf een functie zit\_er\_tussenin(x, y, z) die True terug geeft als x ≤ y ≤ z en anders False.

## 6.5 Meer over recursie

We hebben nog maar een klein gedeelte behandeld van Python maar het is interessant om te weten dat dit gedeelte een _volledige_ programmeertaal is; dit betekent dat alles wat kan worden berekend, uitgedrukt kan worden in deze taal. Elk programma dat ooit is geschreven kan worden herschreven door alleen gebruik te maken van de tot nu toe geleerde taalonderdelen (we hebben nog een paar opdrachten nodig voor het aansturen van het toetsenbord, het scherm, schijven, enzovoorts, maar dat is het dan).

Deze bewering waarmaken is een niet alledaagse opgave en voor het eerst tot stand gebracht door Alan Turing, een van de eerste literatuurwetenschappers (sommigen zullen zeggen dat hij een wiskundige was maar veel van de eerste computerwetenschappers zijn gestart als wiskundigen). Dienovereenkomstig staat dit bekend als de Turing hypothese. In het boek _Introduction to the Theory of Computation_, van Michael Sipser, staat een meer volledige en zuivere discussie over de hypothese van Turing.

Om u een idee te geven wat u kunt doen met de gereedschappen, die u tot nu toe geleerd hebt, zullen we een aantal recursief gedefinieerde wiskundige functies evalueren. Een recursieve definitie komt overeen met een cirkel definitie, in die zin dat de definitie een verwijzing bevat naar het begrip dat wordt gedefinieerd. Een zuivere cirkel definitie is niet erg zinvol:

**verrukkelijk**: Een bijvoeglijk naamwoord dat wordt gebruikt om iets te omschrijven dat verrukkelijk is.

Als u een dergelijke definitie in een woordenboek zou terug vinden, zou u zich hier waarschijnlijk aan ergeren. Aan de andere kant, als u de definitie van de faculteitfunctie opzoekt, weergegeven met het teken !, kunt u het volgende te zien krijgen:

0! = 1
n! = n(n − 1)!

Deze definitie stelt dat de faculteit van 0 gelijk is aan 1 en dat de faculteit van enige andere waarde _n_ gelijk is aan _n_ vermenigvuldigd met de faculteit van _n_ − 1.

Dus 3! is 3 keer 2!, wat weer 2 keer 1! is, wat weer 1 keer 0! is. Samengevat: 3! is gelijk aan 3 keer 2 keer 1 keer 1 en dat is 6.

Kunt u een recursieve definitie van iets schrijven, dan is het normaal gesproken mogelijk een Python programma te schrijven om die definitie te evalueren. De eerste stap is te besluiten welke parameters we nodig hebben. In dit geval is het duidelijk dat faculteit een geheel getal mee krijgt:

def faculteit(n):

Is het argument 0 dan volstaat het terug geven van 1:

def faculteit(n):
      if n == 0:
           return 1

Zo niet, en dat is het interessante gedeelte, maken we een recursieve aanroep om de faculteit te vinden van _n_ − 1 en die te vermenigvuldigen met _n_:

def faculteit(n):
      if n == 0:
           return 1
      else:
           terugkeer= faculteit(n-1)
           resultaat = n \* terugkeer
           return resultaat

De volgorde van uitvoering van dit programma komt overeen met de volgorde van aftellen in paragraaf 5.8. We roepen faculteit aan met de waarde 3:

omdat 3 geen 0 is, nemen we de tweede tak en berekenen de faculteit van n-1...

-   omdat 2 geen 0 is, nemen we de tweede tak en berekenen de faculteit van n-1...
    
    -   omdat 1 geen 0 is, nemen we de tweede tak en berekenen de faculteit van n-1...
        
        -   omdat 0 _gelijk is aan_ 0, nemen we de eerste tak en geven 1 terug zonder nog enige recursieve aanroepen te maken.
            
        
        De antwoordwaarde (1) wordt met _n_ vermenigvuldigd, dat is 1 en het resultaat wordt teruggegeven.
        
    
    De antwoordwaarde (1) wordt met _n_ vermenigvuldigd, dat is 2 en het resultaat wordt teruggegeven.
    

De antwoordwaarde (2) wordt met _n_ vermenigvuldigd, dat is 3 en het resultaat: 6 wordt de antwoordwaarde van de functie aanroep die het proces heeft opgestart.

Onderstaand een stapeldiagram dat overeenkomt met deze serie functie aanroepen:

-   ![boek009_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZes?action=AttachFile&do=get&target=boek009_nl.png "boek009_nl.png")
    

De antwoordwaarden worden weergegeven van beneden naar boven. In elk blok is de antwoordwaarde de waarde van resultaat, dat weer het product is van n en terugkeer.

In het laatste blok bestaan de lokale variabelen terugkeer en resultaat niet, omdat de tak die deze aanmaakt niet wordt uitgevoerd.

## 6.6 Blind vertrouwen

Een manier om programma's te lezen, is het simpelweg volgen van de volgorde van uitvoering maar dit eindigt maar al te vaak in een doolhof.

Een alternatief is wat genoemd wordt "blind vertrouwen". Aangekomen bij een functieaanroep gaat u ervan uit dat de functie correct werkt en de juiste resultaten terug geeft, in plaats van de functie uit te pluizen.

In feite past u het principe van blind vertrouwen al toe bij het gebruiken van ingebouwde functies. Zodra u math.cos of math.exp aanroept, bestudeert u de werking van deze functies niet. U neemt aan dat deze werken omdat de mensen, die ze ooit hebben geschreven, goede programmeurs zijn.

Hetzelfde geldt voor het aanroepen van één van uw eigen functies. Bijvoorbeeld: in paragraaf 6.4, hebben we een functie genaamd is\_deelbaar geschreven, die bepaalt of een getal deelbaar is door een ander getal. Hebben we eenmaal onszelf overtuigd dat een functie correct werkt door de code te bestuderen en te testen, dan gebruiken we de functie zonder daar nog naar te kijken.

Dit principe geldt ook voor recursieve programma's. Komt u bij een recursieve aanroep dan nemen we aan dat de recursieve aanroep werkt (het juiste resultaat levert) en gaan we niet de volgorde van uitvoering nalopen. En onszelf afvragen: "Stel dat ik de faculteit van _n_ − 1 kan vinden, kan ik dan de faculteit van _n_ berekenen?" In dit geval is het duidelijk dat dit kan door vermenigvuldigen met _n_.

Het is natuurlijk wel wat vreemd om aan te nemen dat de functie correct werkt terwijl deze nog niet af is; juist daarom wordt dit blind vertrouwen genoemd!

## 6.7 Nog een voorbeeld

Na faculteit is het meest gebruikte voorbeeld van een recursief gedefinieerde wiskundige functie fibonacci, deze heeft de volgende definitie1 :

fibonacci(0) = 0
fibonacci(1) = 1
fibonacci(''n'') = fibonacci(''n'' − 1) + fibonacci(''n'' − 2);

Vertaald naar Python, ziet dit er als volgt uit:

def fibonacci (n):
      if n == 0:
           return 0
      elif n == 1:
           return 1
      else:
           return fibonacci(n-1) + fibonacci(n-2)

Als u de volgorde van uitvoering tracht te volgen, zelfs voor kleine waarden van _n_, dan begint het u te duizelen. Maar volgens het principe van blind vertrouwen neemt u aan dat de twee recursieve aanroepen correct werken; het is nu ook duidelijk dat u het juiste resultaat krijgt door de twee aanroepen op te tellen.

## 6.8 Typen controleren

Wat gebeurt er als we faculteit aanroepen en 1,5 als argument meegeven?

\>>> faculteit(1.5)
RuntimeError: Maximum recursion depth exceeded

Het lijkt op een oneindige recursie. Maar hoe kan dit? Er bestaat een basiscontrole — namelijk n == 0. Maar als n geen geheel getal is, dan missen we de basiscontrole en herhalen we eindeloos.

In de eerste recursieve aanroep is de waarde van n 0,5. In de volgende is deze -0,5. Vanaf daar wordt n kleiner (meer negatief), en zal n dus nooit de 0 bereiken.

We hebben twee keuzes. We kunnen de faculteit functie meer generiek maken zodat floating-point getallen ook werken of we laten faculteit controleren welk type argumenten mee komen. De eerste optie wordt de gammafunctie2 genoemd en valt een beetje buiten het aandachtsgebied van dit boek. Dus kiezen we voor de tweede optie.

We kunnen de ingebouwde functie isinstance gebruiken om het type van een argument te valideren. Nu we er toch mee bezig zijn kunnen we meteen controleren of het argument een positief getal is:

def faculteit(n):
      if not isinstance(n, int):
           print 'Faculteit is alleen gedefinieerd voor gehele getallen.'
           return None
      elif n < 0:
           print 'Faculteit is alleen gedefinieerd voor positieve gehele getallen.'
           return None
      elif n == 0:
           return 1
      else:
           return n \* faculteit(n-1)

De eerste basiscontrole handelt de niet gehele getallen af en de tweede controle handelt negatieve gehele getallen af. In beide gevallen geeft het programma een foutmelding weer en geeft None terug om aan te geven dat er iets fout ging:

\>>> faculteit('fred')
Faculteit is alleen gedefinieerd voor gehele getallen.
None
\>>> faculteit(-2)
Faculteit is alleen gedefinieerd voor positieve gehele getallen.
None

Komen we langs deze beide controles, dan weten we dat _n_ een positief geheel getal is en kunnen we bewijzen dat de recursie zal eindigen.

Dit programma vertoont een patroon dat soms een **wachter** wordt genoemd. De eerste twee condities treden op als "wachters" die de code beschermen tegen waarden die mogelijk een fout veroorzaken. De wachters maken het mogelijk om te bewijzen dat de code correct werkt.

## 6.9 Debuggen

Een groot programma opdelen in kleinere functies creëert, om het zo te zeggen, natuurlijke controlepunten voor het debuggen. Werkt een functie niet dan zijn er een drietal mogelijkheden:

-   1 Er is iets mis met de argumenten die de functie meekrijgt, aan een randvoorwaarde wordt niet voldaan.  
    2 Er is iets mis met de functie, er wordt niet aan een voorwaarde voor na de afloop voldaan.  
    3 Er is iets mis met de antwoordwaarde of de manier waarop deze wordt gebruikt.
    

Voeg een print instructie toe aan het begin van de functie en geef de waarden van de parameters van de functie weer (en mogelijk hun types). Of u kunt code schrijven die de randvoorwaarden expliciet controleert. Hiermee wordt het eerste punt uitgesloten.

Zien de parameters er goed uit, voeg dan een print instructie toe voor elke return instructie, die de antwoordwaarden weergeeft. Controleer, als het kan, de resultaten handmatig. Het is wellicht handig om de functie aan te roepen met waarden die makkelijk te controleren zijn, zoals in paragraaf 6.2.

Lijkt de functie te werken, kijk dan naar de functieaanroep en wees er zeker van dat de antwoordwaarde wordt gebruikt, of op de juiste manier wordt gebruikt.

print instructies toevoegen aan het begin en einde van een functie helpt om de volgorde van uitvoering te verduidelijken. Bijvoorbeeld: de onderstaande versie van faculteit is voorzien van print instructies:

def faculteit(n):
      space = ' ' \* (4 \* n)
      print space, 'faculteit', n
      if n == 0:
           print space, 'teruggave 1'
           return 1
      else:
           herhaling = faculteit(n-1)
           resultaat = n \* herhaling
           print space, 'teruggave', resultaat
           return resultaat

space is een string van spaties die het inspringen van de uitvoer controleert. Hierbij het resultaat van faculteit(5):

                            faculteit 5
                       faculteit 4
                 faculteit 3
            faculteit 2
      faculteit 1
  faculteit 0
  teruggave 1
      teruggave 1
            teruggave 2
                 teruggave 6
                       teruggave 24
                            teruggave 120

Als u niet wijs wordt uit de volgorde van uitvoering, dan is een dergelijke uitvoer nuttig. Het kost wel wat tijd om een effectieve steigerconstructie te ontwikkelen, maar een steigerconstructie scheelt de nodige tijd bij het debuggen.

## 6.10 Woordenlijst

**tijdelijke variabele**: Een variabele die wordt gebruikt om tussentijdse waarden van een complexe berekening op te slaan.

**dode code**: Onderdeel van een programma dat nooit zal worden uitgevoerd; het komt regelmatig voor dat deze code achter een return instructie staat.

**None**: Een speciale waarde teruggegeven door functies die geen return instructie hebben of die een return instructie hebben zonder een antwoordwaarde.

**incrementele ontwikkeling**: Een ontwikkelplan voor een programma bedoeld om het debuggen te vermijden, door het toevoegen en het testen van kleine stukjes code per keer.

**steigerconstructie**: Code die tijdens het ontwerpen van het programma wordt gebruikt maar geen deel uitmaakt van de uiteindelijke versie.

**wachter**: Een programmeerpatroon dat door middel van een voorwaardelijke instructie foute situaties controleert en afhandelt.

## 6.11 Oefeningen

**Oefening 6.4** Teken een stapeldiagram voor het volgende programma. Wat drukt het programma af?

def b(z):
     prod = a(z, z)
     print z, prod
     return prod
def a(x, y):
     x = x + 1
     return x \* y
def c(x, y, z):
      sum = x + y + z
      pow = b(sum)\*\*2
      return pow
x = 1
y = x + 1
print c(x, y+3, x+y)

**Oefening 6.5** De Ackermann functie, is gedefineerd als_A(m, n)_3:

-   ![formula002.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZes?action=AttachFile&do=get&target=formula002.png "formula002.png")
    

Schrijf een functie genaamd ack die Ackerman’s functie evalueert. Maak gebruik van uw functie om ack(3, 4) te evalueren, de uitkomst van deze functie is 125. Wat gebeurt er bij grotere waarden voor m en n?

**Oefening 6.6** Een palindroom is een woord dat van voor naar achteren en andersom op dezelfde manier wordt gespeld, zoals "lepel" en "legerregel”. Dus een woord is een palindroom als de eerste en laatste letters hetzelfde zijn.

De volgende functies krijgen een string mee en geven de eerste, laatste en middelste letters terug:

def eerste(woord):
      return woord\[0\]
def laatste(woord):
      return woord\[-1\]
def middelste(woord):
      return woord\[1:-1\]

In hoofdstuk 8 zullen we zien hoe deze functies werken.

1.  Typ deze functies over en zet deze in een bestand genaamd palindroom.py en test deze. Wat gebeurt er als u middelste aanroept met een string van twee letters? Of één letter? Hoe zit het met een lege string, die wordt geschreven als '', en geen letters bevat?
    
2.  Schrijf een functie genaamd is\_palindroom die een string meekrijgt als argument en True teruggeeft als het een palindroom is en anders False teruggeeft. Denk eraan dat u de ingebouwde functie len kunt gebruiken om de lengte van een string te achterhalen.
    

**Oefening 6.7** Een getal, _a_, is de macht van _b_ als het deelbaar is door _b_ en _a/b_ is de macht van _b_. Schrijf een functie genaamd is\_de\_macht die de parameters a en b meekrijgt en True terug geeft als a een macht van b is.

**Oefening 6.8** De grootste gemene deler (GGD) van _a_ en _b_ is het grootste getal waardoor je beide kunt delen zonder een rest4 .

Een manier om de GGD uit twee getallen te vinden is met behulp van Euclid’s algoritme, deze is gebaseerd op waarneming dat als _r_ de rest is bij de deling van _a_ door _b_, dan is _ggd(a, b) = ggd(b, r)_. We kunnen _ggd_(_a_, 0) = _a_ beschouwen als een basisblok.

Schrijf een functie genaamd ggd die de parameters a en b meekrijgt en hun grootste gemene deler teruggeeft.

Hebt u hulp nodig? kijk dan eens op [nl.wikipedia.org/wiki/Algoritme\_van\_Euclides](http://nl.wikipedia.org/wiki/Algoritme_van_Euclides).

* * *

1 Zie [http://nl.wikipedia.org/wiki/Rij\_van\_Fibonacci](http://nl.wikipedia.org/wiki/Rij_van_Fibonacci)  
2 Zie [http://nl.wikipedia.org/wiki/Gammafunctie](http://nl.wikipedia.org/wiki/Gammafunctie).  
3 Zie [http://nl.wikipedia.org/wiki/Ackermannfunctie](http://nl.wikipedia.org/wiki/Ackermannfunctie)  
4 Deze oefening is gebaseerd op een voorbeeld van Abelson en Sussman’s structuur en interpretatie van computer programma's.