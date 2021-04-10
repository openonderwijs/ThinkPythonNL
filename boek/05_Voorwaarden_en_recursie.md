[community/ThinkPython/HoofdstukVijf - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijf)

# Hoofdstuk 5 Voorwaarden en recursie

## 5.1 Modulus operator

De **modulus operator** werkt op gehele getallen en levert de rest wanneer de eerste operand wordt gedeeld door de tweede. In Python is de modulus operator een procent teken (%). De zinsbouw is dezelfde als die voor andere operatoren:

\>>>  quotiënt = 7 / 3
\>>>  print quotiënt
2
\>>>  rest = 7 % 3
\>>>  print rest 
1

Dus 7 gedeeld door 3 is 2 met rest 1.

De modulus operator blijkt verrassend handig te zijn. Bijvoorbeeld: hiermee kunt u controleren of een getal deelbaar is door een ander getal; is x % y nul dan is x deelbaar door y.

U kunt ook het rechter cijfer(s) van een getal afscheiden. Bijvoorbeeld: x % 10 levert het rechter cijfer op van x (in grondtal 10). Insgelijks levert x % 100 de laatste twee cijfers op.

## 5.2 Booleaanse expressies

Een **booleaanse expressie** is een uitdrukking, die of waar (true) of onwaar (false) is. De onderstaande voorbeelden gebruiken de operator ==, die twee operanden vergelijkt en een True oplevert als ze gelijk zijn en anders een False:

\>>> 5 == 5
True
\>>> 5 == 6
False

True en False zijn speciale waarden van het type bool; dit zijn geen strings:

\>>> type(True)
<type 'bool'>
\>>> type(False)
<type 'bool'>

De == operator is één van de **vergelijkingsoperatoren**, de andere zijn:

          x  != y                      #  x is niet gelijk aan y
          x  > y                       #  x is groter dan y
          x  < y                       #  x is kleiner dan y
          x  >= y                      #  x is groter dan of gelijk aan y
          x  <= y                      #  x is kleiner dan of gelijk aan y

Hoewel deze operaties u waarschijnlijk bekend voorkomen, verschillen de Python symbolen van de wiskundige symbolen. Een veel gemaakte fout is het gebruik van het is-gelijk teken (=) in plaats van een dubbel is-gelijk teken (==). Onthoudt goed dat een enkele = betekent: toekennen, en een dubbele == is de vergelijkingsoperator. In Python bestaat niet zoiets als =< of =>.

## 5.3 Logische operatoren

We kennen drie **logische operatoren**: and (en), or (of) en not (niet). De semantiek (betekenis) van deze operatoren is overeenkomstig de betekenis in het Engels. Bijvoorbeeld: x > 0 and x < 10 is waar alleen als x groter is dan 0 _en_ kleiner dan 10.

n%2 == 0 or n%3 == 0 is waar als _een van beide_ condities waar is, dat wil zeggen: als het getal deelbaar is door 2 of 3.

Als laatste, de not operator inverteert een booleaanse expressie, dus not (x > y) is waar als x > y onwaar is, dat wil zeggen: als x kleiner of gelijk is aan y.

Strikt genomen moeten de operanden van de logische operatoren booleaanse expressies zijn, maar Python is niet zo strikt. Elk getal ongelijk aan nul wordt als "waar" opgevat.

\>>> 17 and True
True

Deze flexibiliteit kan handig zijn, maar er zijn enkele subtiele verschillen die verwarrend zijn. Probeer deze te vermijden (tenzij u weet waar u mee bezig bent).

## 5.4 Voorwaardelijke uitvoering

**Voorwaardelijke instructies** bieden de mogelijkheid om voorwaarden te controleren en op basis daarvan het gedrag van het programma aan te passen. Zonder deze instructies is het nagenoeg onmogelijk om tot bruikbare programma's te komen. De eenvoudigste vorm is de if instructie:

if x > 0:
      print 'x is positive'

De booleaanse expressie na de if instructie wordt de **voorwaarde** genoemd. Is deze waar, dan wordt de ingesprongen instructie uitgevoerd; zo niet, dan wordt niets uitgevoerd.

Wanneer instructies dezelfde structuur als functiedefinities hebben, dat wil zeggen, een kop gevolgd door een ingesprongen blok, dan worden deze **samengestelde instructies** genoemd.

Er bestaat geen limiet op het aantal instructies dat in een body mag voorkomen, maar het moet er tenminste één zijn. Het kan voorkomen dat het handig is om een body te maken zonder instructies (normaal gesproken als aandachtspunt voor nog te schrijven code). In dat geval kunt u de pass instructie gebruiken die niets doet.

if x < 0:
      pass                # noodzaak om negatieve waarden af te handelen!

## 5.5 Alternatieve uitvoering

Een tweede vorm van de if instructie is een **alternatieve uitvoering**, waarbij twee keuzes mogelijk zijn en de voorwaarde besluit welke wordt uitgevoerd. De zinsbouw lijkt hierop:

if x%2 == 0:
      print 'x is even'
else:
      print 'x is oneven'

Als de rest van x gedeeld door 2 gelijk aan 0 is, dan weten we dat x even is en het programma geeft een bericht weer met die boodschap. Is de voorwaarde onwaar dan zal de tweede set instructies worden uitgevoerd. Aangezien de voorwaarde of waar of onwaar is, wordt altijd tenminste één van de alternatieven uitgevoerd. De alternatieven worden takken genoemd omdat zij aftakkingen zijn in de stroom van uitvoeringen.

## 5.6 Gekoppelde voorwaarden

Soms zijn er meer dan twee mogelijkheden en hebben we meer dan twee takken nodig. Een manier om een dergelijke berekening vorm te geven is een **gekoppelde voorwaarde**:

if x < y:
      print 'x is kleiner dan y'
elif x > y:
      print 'x is groter dan y'
else:
      print 'x en y zijn gelijk'

elif is een afkorting van "else if". Ook hier wordt precies één tak uitgevoerd. Er is geen limiet op het aantal elif instructies. Staat er een else clausule, dan is dat het einde, maar deze hoeft er niet te staan.

if choice == 'a':
      teken\_a()
elif choice == 'b':
      teken\_b()
elif choice == 'c':
      teken\_c()

Elke voorwaarde wordt op volgorde gecontroleerd. Is de eerste onwaar, dan wordt de volgende gecontroleerd, enzovoorts. Is er één waar dan wordt de bijbehorende tak uitgevoerd en de instructie eindigt. Zelfs als er meer dan één voorwaarde waar zou zijn. Alleen de tak bij de eerste keer waar wordt uitgevoerd.

## 5.7 Geneste voorwaarden

Een voorwaarde kan genest worden binnen een andere voorwaarde. Een andere manier van schrijven van het driedelingsvoorbeeld hierboven is:

if x == y:
       print 'x and y zijn gelijk'
else:
       if x < y:
            print 'x is kleiner dan y'
       else:
            print 'x is groter dan y'

De buitenste voorwaarde bevat twee takken. De eerste tak bevat een eenvoudige instructie. De tweede tak bevat een nieuwe if instructie, die op zijn beurt twee takken kent. Deze twee takken zijn allebei eenvoudige instructies, hoewel deze ook weer voorwaardelijke instructies kunnen zijn.

Hoewel de inspringing van de instructies de structuur verduidelijken, worden geneste voorwaarden al snel moeilijk leesbaar. Over het algemeen is het een goed idee om deze constructie te vermijden, als het enigszins mogelijk is.

Logische operatoren leveren vaak een manier om geneste voorwaardelijke instructies te vereenvoudigen. Bijvoorbeeld: we kunnen de volgende code herschrijven met een enkele voorwaarde:

if 0 < x:
       if x < 10:
            print 'x is een positief eencijferig getal.'

De print instructie wordt alleen uitgevoerd als aan beide voorwaarden is voldaan, dus kunnen we hetzelfde effect bereiken met de and operator:

if 0 < x and x < 10:
       print 'x is a een positief eencijferig getal.'

## 5.8 Recursie

Het is een functie toegestaan om een andere functie aan te roepen; het is ook toegestaan dat een functie zichzelf aanroept. Het ligt niet voor de hand om te veronderstellen dat dit een goede zaak is, maar het blijkt dat dit één van de meest wonderbaarlijke zaken is die een programma kan doen. Bijvoorbeeld: kijk eens naar de volgende functie:

def aftellen(n):
       if n <= 0:
            print 'Lanceer!'
       else:
            print n
            aftellen(n-1)

Is n gelijk aan 0 of negatief, dan wordt het woord "Lanceer!" weergegeven; zo niet, dan wordt n weergegeven en vervolgens roept het een functie genaamd aftellen aan —zichzelf dus— en geeft n-1 als een argument mee.

Wat gebeurt er als we de functie op deze manier aanroepen?

\>>> aftellen(3)

De uitvoering van aftellen start met n=3 en omdat n groter is dan 0, geeft het de waarde 3 weer en roept zichzelf aan...

-   De uitvoering van aftellen start met n=2, en omdat n groter is dan 0, geeft het de waarde 2 weer en roept zichzelf aan...
    
    -   De uitvoering van aftellen start met n=1 en omdat n groter is dan 0, geeft het de waarde 1 weer en roept zichzelf aan...
        
        -   De uitvoering van aftellen start met n=0 en omdat n niet groter is dan 0 wordt het woord "Lanceer!" geprint en keert terug.
            
        
        Het aftellen, aangekomen bij n=1, keert terug.
        
    
    Het aftellen, aangekomen bij n=2, keert terug.
    

Het aftellen, aangekomen bij n=3, keert terug.

En u bent terug in \_\_main\_\_. Dus, de volledige uitvoer lijkt hierop:

3
2
1
Lanceer!

Een functie die zichzelf aanroept, is **recursief** (terugkerend); het proces heet **recursie**.

Een ander voorbeeld; we schrijven een functie die een string n keer afdrukt.

def print\_n(s, n):
      if n <= 0:
            return
      print s
      print\_n(s, n-1)

Zodra n <= 0 waar is, beëindigt de return instructie deze functie. De uitvoering wordt direct aan de aanroeper overgedragen en de resterende regels van de functie worden niet uitgevoerd.

De rest van de functie is gelijk aan aftellen: is n groter dan 0, dan wordt s weergegeven en wordt de functie zelf aangeroepen om s ''n''-1 keer weer te geven. Dus het aantal regels in de uitvoer is 1 + (n - 1), wat opgeteld n is.

Voor eenvoudige voorbeelden zoals dit is het waarschijnlijk gemakkelijker om een for lus te gebruiken. Later zullen we voorbeelden zien, die moeilijk met behulp van een for lus te schrijven zijn, maar eenvoudig met recursie. Dus is het goed hier vroeg mee te beginnen.

## 5.9 Stapeldiagrammen voor recursieve functies

In paragraaf 3.10 gebruikten we een stapeldiagram om de status van een programma weer te geven gedurende de aanroep. Dezelfde soort diagrammen kunnen helpen om een recursieve functie te verklaren.

Iedere keer als een functie wordt aangeroepen maakt Python een nieuw functiekader aan. Deze bevat de lokale variabelen en parameters van de functie. Voor een recursieve functie kunnen er meerdere kaders op hetzelfde moment op de stapel staan.

Onderstaande tekening laat een stapeldiagram zien voor aftellen aangeroepen met n = 3:

-   ![boek007_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijf?action=AttachFile&do=get&target=boek007_nl.png "boek007_nl.png")
    

Zoals gewoonlijk, staat boven aan de stapel het kader voor \_\_main\_\_. Deze is leeg omdat we geen enkele variabele hebben gemaakt in \_\_main\_\_ en daaraan ook geen argumenten hebben doorgegeven.

De vier kaders voor aftellen hebben verschillende waarden voor de parameter n. Onderaan de stapel, waarbij n=0, wordt het **basisblok** genoemd. Het basisblok maakt geen recursieve aanroep, dus is dit het laatste kader.

-   Teken een stapeldiagram voor print\_n aangeroepen met s = 'Hallo' en n=2.
    
    Schrijf een functie genaamd doe\_n die een functieobject en een getal n als argumenten krijgt en die de gegeven functie n keer aanroept.
    

## 5.10 Oneindige recursie

Bereikt een recursie (herhaling) nooit het basis blok, dan gaat deze altijd maar door met maken van recursieve aanroepen en het programma stopt nooit. Dit staat bekend als een oneindige recursie en dat is over het algemeen geen goed idee. Hierbij een miniem programmaatje met een oneindige recursie:

def recursie():
      recursie()

In de meeste omgevingen draait een programma met een oneindige recursie niet voor altijd. Python rapporteert een foutboodschap zodra het maximum aantal recursies is bereikt:

   File "<stdin>", line 2, in recurse
   File "<stdin>", line 2, in recurse
   File "<stdin>", line 2, in recurse
                         .
                         .
                         .
   File "<stdin>", line 2, in recurse
RuntimeError: Maximum recursion depth exceeded

Dit spoor terug is ietsje groter dan dat wat we in het vorige hoofdstuk zagen. Op het moment dat de fout optreedt staan er al 1000 blokken op de stapel!

## 5.11 Toetsenbord invoer

De programma's die we tot nu toe hebben geschreven zijn een beetje ongemanierd in die zin dat ze geen invoer van de gebruiker accepteren. Ze doen gewoon iedere keer hetzelfde.

Python levert een ingebouwde functie genaamd raw\_input (kale invoer) die zijn gegevens via het toetsenbord ontvangt1. Zodra deze functie wordt aangeroepen stopt het programma en wacht totdat de gebruiker iets typt. Typt de gebruiker een Return of een Enter, dan gaat het programma verder en raw\_input geeft terug wat de gebruiker heeft getypt als string.

\>>> invoer = raw\_input()
Waar wacht u op?
\>>> print invoer 
Waar wacht u op?

Voordat we invoer van de gebruiker vragen is het een goed idee om een boodschap weer te geven waarin wordt aangegeven wat we verwachten. raw\_input kan een boodschap als argument mee krijgen:

\>>> name = raw\_input('Wat...is uw naam?\\n')
Wat...is uw naam?
Willem van Oranje, Prins der Nederlanden!
\>>> print name
Willem van Oranje, Prins der Nederlanden!

Het onderdeel \\n aan het einde van de prompt vertegenwoordigt een **newline** (nieuwe regel); dit is een speciaal karakter, dat een nieuwe regel geeft. Daarom verschijnt de invoer van de gebruiker onder de boodschap.

Verwacht u van de gebruiker een geheel getal, dan kunt u proberen dit om te zetten naar een int:

\>>> boodschap = 'Wat...is de lucht snelheid van een lege zwaluw?\\n'
\>>> snelheid = raw\_input(boodschap)
Wat...is de lucht snelheid van een lege zwaluw?
17
\>>> int(snelheid)
17

Maar als de gebruiker iets anders typt dan een rij getallen krijgt u een foutboodschap:

\>>> snelheid = raw\_input(boodschap)
Wat...is de lucht snelheid van een lege zwaluw?
Welke bedoelt u, een boeren- of een gierzwaluw?
\>>> int(snelheid )
ValueError: invalid literal for int()

We zullen later bekijken hoe we met dergelijke fouten omgaan.

## 5.12 Debuggen

Het spoor terug dat Python weergeeft zodra een fout optreedt bevat een heleboel informatie, maar het kan overstelpend zijn; in het bijzonder als er veel blokken op de stapel staan. De meest bruikbare onderdelen zijn normaal gesproken:

-   • Wat voor een soort fout is het, en  
    • Waar treedt deze op.
    

Fouten in de zinsbouw zijn over het algemeen makkelijk te vinden maar er zijn enkele gotchas. Witte vlek fouten zijn een valkuil, omdat spaties en tabstops onzichtbaar zijn en we gewoon zijn deze te negeren.

\>>> x = 5
\>>>  y = 6
   File "<stdin>", line 1
      y = 6
      ˆ
SyntaxError: invalid syntax

In dit voorbeeld is het probleem dat de tweede regel één spatie is ingesprongen. Maar de foutboodschap wijst naar y; dit is misleidend. In het algemeen geeft de foutboodschap aan waar het probleem is ontdekt, maar de eigenlijke fout kan verder terug liggen, soms zelfs in de vorige regel.

Dit zelfde geldt voor uitvoeringsfouten (runtime errors). Stel dat u de signaal/ruis verhouding in decibels wilt berekenen. De formule luidt SNRdb = 10 log10 (Psignaal /Pruis ). In Python zou u dat als volgt kunnen opschrijven:

import math
signaal\_sterkte = 9
ruis\_sterkte = 10
ratio = signaal\_sterkte / ruis\_sterkte 
decibels = 10 \* math.log10(ratio)
print decibels

Maar zodra u dit uitvoert krijgt u een foutboodschap2:

Traceback (most recent call last):
   File "snr.py", line 5, in ?
      decibels = 10 \* math.log10(ratio)
OverflowError: math range error

De foutboodschap wijst naar regel 5 maar er is niets mis met die regel. Om de eigenlijke fout te vinden is het raadzaam om de waarde van ratio weer te geven; deze blijkt 0 te zijn. Het probleem zit in regel 4 omdat twee gehele getallen delen een floor deling oplevert. De oplossing is om signaalsterkte en ruissterkte als floating-point waarden op te nemen.

In het algemeen vertellen foutboodschappen u waar het probleem is ontdekt, maar dat is meestal niet de plaats waar de fout wordt veroorzaakt.

## 5.13 Woordenlijst

**modulus operator**: Een operator, aangeduid met een procent teken (%), die met gehele getallen werkt en die de rest bevat als een getal wordt gedeeld door een ander getal.

**booleaanse expressie**: Een expressie die of de waarde waar (True) of onwaar (False) heeft.

**vergelijkingsoperator**: Een van de operatoren waarmee operanden worden vergeleken: \==, !=, >, <, >=, en <=.

**logische operator**: Een van de operatoren waarmee booleaanse expressies worden opgebouwd: and, or, en not.

**voorwaardelijke instructie**: Een instructie die de volgorde van uitvoering stuurt, afhankelijk van een bepaalde voorwaarde.

**voorwaarde**: De booleaanse expressie in een voorwaardelijke instructie die bepaalt welke tak wordt uitgevoerd.

**samengestelde instructie**: Een instructie die bestaat uit een kop en een body. De kop eindigt met een dubbelepunt (:). De body is relatief ten opzichte van de kop ingesprongen.

**body**: De reeks instructies in een sequentieel samengestelde instructie.

**tak**: Een van de alternatieve instructies in een voorwaardelijke instructie.

**gekoppelde voorwaarde**: Een voorwaardelijke instructie met een reeks alternatieve takken.

**geneste voorwaarde**: Een voorwaardelijke instructie, die voorkomt in één van de takken van een andere voorwaardelijke instructie.

**recursie**: Het proces van het aanroepen van de functie, die op dat moment wordt uitgevoerd.

**basisblok**: Een voorwaardelijke tak in een recursieve functie, die geen recursieve aanroep meer doet.

**oneindige recursie**: Een functie die zichzelf aanroept zonder dat deze ooit het basisblok bereikt. Uiteindelijk veroorzaakt een oneindige recursie een uitvoeringsfout (runtime error).

## 5.14 Oefeningen

**Oefening 5.1** Fermat’s laatste stelling geeft aan dat er geen gehele getallen _a_, _b_, and _c_ bestaan zodanig dat

-   _a_n + _b_n = _c_n
    

voor iedere waarde van _n_ groter dan 2.

1.  Schrijf een functie genaamd controleer\_fermat die vier parameters — a, b, c en n— mee krijgt en die controleert of Fermat’s stelling overeind blijft. Is _n_ groter dan 2 en het blijkt waar dat
    
    _a_n + _b_n = _c_n
    
      
    dan moet het programma printen: "onvoorstelbaar, Fermat zat er naast!" Zo niet, dan moet het programma printen: "Nee, de stelling is waar".
    
2.  Schrijf een functie die aan de gebruiker vraagt om de waarden voor a, b, c en n, deze omzet in gehele getallen en met behulp van controleer\_fermat controleert of deze getallen de stelling van Fermat overtreden.
    

**Oefening 5.2** U krijgt drie stokken en daarmee kunt u al of niet een driehoek vormen.

Bijvoorbeeld: is een van de stokken 12 cm lang en de andere twee zijn 1 cm lang, dan is het helder dat de korte stokken elkaar nooit zullen raken. Er bestaat een eenvoudige test om te bepalen of met drie gegeven lengtes het mogelijk is om een driehoek te vormen:

"is één van de lengtes groter dan de som van de andere twee, dan is het onmogelijk een driehoek te vormen. In alle andere gevallen is het wel mogelijk"3.

1.  Schrijf een functie genaamd is\_driehoek, die drie gehele getallen als argumenten mee krijgt en die of "Ja" of "Nee" afdrukt, afhankelijk van het feit of een driehoek is te vormen met de gegeven lengtes.
    
2.  Schrijf een functie die de gebruiker vraagt om drie lengtes op te geven; deze vertaalt naar gehele getallen en gebruik maakt van is\_driehoek om te controleren of de gegeven lengtes een driehoek kunnen vormen.
    

De volgende oefening maakt gebruik van TurtleWorld uit hoofdstuk 4:

**Oefening 5.3** Bestudeer de volgende functie en zoek uit wat deze doet. Voer daarna de functie uit (zie de voorbeelden in hoofdstuk 4).

def teken(t, lengte, n):
      if n == 0:
           return
      hoek = 50
      fd(t, lengte\*n)
      lt(t, hoek)
      teken(t, lengte, n-1)
      rt(t, 2\*hoek)
      teken(t, lengte, n-1)
      lt(t, hoek)
      bk(t, lengte\*n)

**Oefening 5.4** De kromme van Koch is een fractal die lijkt op het onderstaande:

-   ![book008.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijf?action=AttachFile&do=get&target=book008.png "book008.png")
    

Voor het tekenen van de kromme van Koch met lengte x hoeft u alleen het volgende te doen

1.  Teken een kromme van Koch met lengte x/3.
2.  Draai naar links 60 graden.
3.  Teken een kromme van Koch met lengte x/3.
4.  Draai naar rechts 120 graden.
5.  Teken een kromme van Koch met lengte x/3.
6.  Draai naar links 60 graden.
7.  Teken een kromme van Koch met lengte x/3.

De enige uitzondering is wanneer x kleiner is dan 3. In dat geval zal een rechte lijn worden getekend met lengte x.

1\. Schrijf een functie genaamd koch die een turtle en een lengte als parameters meekrijgt en gebruik de turtle voor het tekenen van de kromme van Koch met de gegeven lengte.

2\. Schrijf een functie genaamd sneeuwvlok die drie krommes van Koch tekent en zo de omtrek van een sneeuwvlok vormt. Een oplossing is te vinden op [thinkpython.com/code/koch.py](http://www.thinkpython.com/code/koch.py).

3\. De kromme van Koch kan op verschillende manieren algemeen toepasbaar worden gemaakt. Zie [wikipedia.org/wiki/Koch\_snowflake](http://www.wikipedia.org/wiki/Koch_snowflake) voor voorbeelden en gebruik degene die u aanstaat.

* * *

1 In Python 3.0, wordt deze functie input genoemd.  
2 In Python 3.0, krijgt u geen foutboodschap meer, de delingsoperator voert een floating-point deling uit, zelfs met gehele getallen.  
3 is de optelsom van twee lengtes gelijk aan de derde dan vormen deze een zogenaamde "gedegenereerde" driehoek.