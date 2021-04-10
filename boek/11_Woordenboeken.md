[community/ThinkPython/HoofdstukElf - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukElf)

# Hoofdstuk 11 Woordenboeken

Een **woordenboek** is net zoiets als een lijst, maar dan meer generiek. In een lijst moeten de indices gehele getallen zijn. In een woordenboek kunnen indices zo ongeveer elk type zijn.

U moet een woordenboek zien als een set indices, sleutels genaamd, die passen op een set waarden. Elke sleutel past op een waarde. Het verband tussen een sleutel en een waarde wordt een **sleutel-waarde paar** genoemd of soms een **item**.

Als voorbeeld gaan we een Nederlands-Spaans woordenboek maken, dus de sleutels en de waarden zijn allemaal strings.

De functie dict maakt een nieuw woordenboek aan zonder inhoud. Omdat dict de naam is van een ingebouwde functie, moet u deze naam niet als naam voor een variabele gebruiken.

\>>> nl2sp = dict()
\>>> print nl2sp
{}

De accolades "{}" vertegenwoordigen een leeg woordenboek. Voor het toevoegen van items aan het woordenboek kunt u vierkante haken gebruiken:

\>>> nl2sp\['één'\] = 'uno'

Deze regel maakt een item aan waarbij de sleutel ’één’ past op de waarde 'uno'. Printen we het woordenboek opnieuw dan zien we een sleutel-waarde paar met een dubbelepunt tussen de sleutel en de waarde:

\>>> print nl2sp
{'één': 'uno'}

Dit formaat bij uitvoer is ook het formaat bij invoer. Bijvoorbeeld: u kunt een nieuw woordenboek aanmaken met drie items:

\>>> nl2sp = {'één': 'uno', 'twee': 'dos', 'drie': 'tres'}

Het uitprinten van nl2sp levert waarschijnlijk een verrassing op:

\>>> print nl2sp
{'één': 'uno', 'drie': 'tres', 'twee': 'dos'}

De volgorde van de sleutel-waarde paren is niet hetzelfde. Als u dit voorbeeld op uw computer uitvoert, kan het zijn dat u nog een ander resultaat krijgt. Over het algemeen is de volgorde van de items onvoorspelbaar.

Maar dit is niet echt een probleem omdat de elementen van een woordenboek nooit geïndexeerd worden met behulp van gehele getallen. In plaats daarvan gebruikt u sleutels om de bijbehorende waarden te vinden:

\>>> print nl2sp\['twee'\]
'dos'

De sleutel ’twee’ past altijd op de waarde 'dos' dus de volgorde van items doet er niet toe.

Bevindt de sleutel zich niet in het woordenboek dan krijgt u een foutmelding betreffende de sleutel:

\>>> print nl2sp\['four'\]
KeyError: 'vier'

De len functie werkt ook op woordenboeken; deze geeft het aantal sleutel-waarde paren terug:

\>>> len(nl2sp)
3

De in operator werkt op woordenboeken; deze meldt of iets als _sleutel_ bestaat in een woordenboek; komt iets als waarde voor dan werkt deze operator niet.

\>>> 'één' in nl2sp
True
\>>> 'uno' in nl2sp
False

U kunt de methode values gebruiken om te zien of iets als waarde tevoorschijn komt in een woordenboek; deze geeft de waarden als een lijst terug en gebruikt vervolgens de in operator:

\>>> waarden= nl2sp.values()
\>>> 'uno' in waarden
True

De in operator gebruikt verschillende algoritmes voor lijsten en woordenboeken. Voor lijsten gebruikt het een zoekalgoritme, zoals in paragraaf 8.6. Wordt de lijst langer dan duurt de zoekopdracht ook langer. Voor woordenboeken gebruikt Python een algoritme genaamd **hashtable** (hashtabel) die een opmerkelijke eigenschap heeft: de in operator doet er altijd even lang over en het maakt niet uit hoeveel items zich in het woordenboek bevinden. Ik zal niet uitleggen hoe dat mogelijk is maar u kunt er meer over lezen op [nl.wikipedia.org/wiki/Hashtabel](http://nl.wikipedia.org/wiki/Hashtabel).

**Oefening 11.1** Schrijf een functie die woorden uit woorden.txt leest en deze opslaat als sleutels in een woordenboek. Het doet er niet toe wat de waarden zijn. Gebruik dan de in operator als een snelle manier om te controleren of een string in het woordenboek voorkomt.

Hebt u ook oefening 10.8 uitgevoerd, dan kunt u de snelheid vergelijken van de lijst in operator en de bisectiemethode.

## 11.1 Woordenboek als een verzameling tellers

Stel u hebt een reeks woorden en u wilt weten hoe vaak elke letter voorkomt. Dit is op verschillende manieren aan te pakken:

1.  U kunt 26 variabelen aanmaken, één voor iedere letter van het alfabet. Vervolgens kunt u door de reeks heen lopen en voor ieder karakter de bijbehorende teller ophogen, hierbij gebruikmakend van een gekoppelde voorwaarde.
2.  U kunt een lijst met 26 elementen aanmaken. Vervolgens kunt u elk karakter omzetten in een getal (door gebruik te maken van de ingebouwde functie ord); het getal als een index te gebruiken naar de lijst toe en de juiste teller op te hogen.
    
3.  U kunt een woordenboek maken met de karakters als sleutels en de tellers als bijbehorende waarden. De eerste keer dat u een karakter ziet voegt u een item toe aan het woordenboek. Hierna verhoogt u de waarde van een bestaand item.

Elk van deze opties voert dezelfde berekening uit maar de uitwerking van die berekening is steeds anders.

Een **uitwerking** is een manier van uitvoeren van een berekening; bepaalde uitwerkingen zijn beter dan andere. Bijvoorbeeld: een voordeel van het woordenboek is dat het niet nodig is van te voren te weten welke letters voorkomen in de reeks. We maken alleen ruimte voor die letters die voorkomen.

Zie onder hoe de code eruit kan zien:

def histogram(s):
      d = woordenb()
      for c in s:
            if c not in d:
                 d\[c\] = 1
            else:
                 d\[c\] += 1
      return d

De naam van de functie is **histogram**; dit is een statistische term voor een serie tellers (of frequenties).

De eerste regel van de functie maakt een leeg woordenboek aan. De for lus doorloopt de string. Elke keer als we de lus doorlopen, maken we een nieuw item aan met de sleutel c en start waarde 1 (we hebben de letter één keer gezien), mits die nog niet in het woordenboek voorkomt. Komt c al voor in het woordenboek dan hogen we d\[c\] op.

Kijk hieronder hoe dat werkt:

\>>> h = histogram('brontosaurus')
\>>> print h
{'a': 1, 'b': 1, 'o': 2, 'n': 1, 's': 2, 'r': 2, 'u': 2, 't': 1}

Het histogram geeft aan dat de letters ’a’ en 'b' één keer voorkomen, 'o' komt twee keer voor, enzovoorts.

**Oefening 11.2** Woordenboeken hebben een methode genaamd get die als sleutel een standaard waarde meekrijgt. Komt de sleutel voor in het woordenboek dan geeft get de bijbehorende waarde terug, zo niet dan geeft het de standaard waarde terug.

Bijvoorbeeld:

\>>> h = histogram('a')
\>>> print h
{'a': 1}
\>>> h.get('a', 0)
1
\>>> h.get('b', 0)
0

Gebruik get om histogram compacter te herschrijven. Het is mogelijk om de if instructie te schrappen.

## 11.2 Lussen en woordenboeken

Gebruikt u een woordenboek in een for instructie, dan doorloopt deze de sleutels van het woordenboek. Bijvoorbeeld: print\_hist drukt elke sleutel met de bijbehorende waarde af:

def print\_hist(h):
      for c in h:
           print c, h\[c\]

Zie onder hoe de uitvoer eruit ziet:

\>>> h = histogram('papegaaien')
\>>> print\_hist(h)
g 1
i 1
e 2
a 3
p 2
n 1

Zoals eerder gemeld staan de sleutels in willekeurige volgorde.

**Oefening 11.3** Woordenboeken hebben een methode genaamd keys die de sleutels van een woordenboek teruggeven in willekeurige volgorde als een lijst.

Wijzig print\_hist zodat deze de sleutels en hun waarde in alfabetische volgorde afdrukt.

## 11.3 Omgekeerd opzoeken

Gegeven een woordenboek d en een sleutel k, dan is het gemakkelijk om de bijbehorende waarde te vinden v = d\[k\]. Deze operatie wordt **opzoeken** (lookup) genoemd.

Maar wat als u v hebt en u wilt k vinden? U hebt twee problemen: het eerste, er bestaan wellicht meerdere sleutels die bij deze waarde v passen. Afhankelijk van de applicatie zou u er één kunnen kiezen of u moet een lijst maken met alle bijpassende sleutels. Het tweede, er bestaat geen eenvoudige zinsbouw voor **omgekeerd opzoeken**, u zult moeten zoeken.

Hierbij een functie die een waarde meekrijgt en de eerste sleutel teruggeeft die overeenkomt met die waarde:

def omgekeerd\_opzoeken(d, v):
      for k in d:
           if d\[k\] == v:
                return k
      raise ValueError

Deze functie is alweer een ander voorbeeld van een zoekpatroon maar deze gebruikt een kenmerk dat we nog niet eerder hebben gezien: raise. De raise instructie veroorzaakt een uitzondering (exception), in dit geval een ValueError, die aangeeft dat er iets mis is met de waarde van een parameter.

Komen we aan het einde van de lus, dan betekent dat, dat v niet in het woordenboek voorkomt als waarde, dus we veroorzaken een uitzondering.

Hierbij een voorbeeld van een succesvolle omgekeerde opzoekinstructie:

\>>> h = histogram('papagaai')
\>>> k = omgekeerd\_opzoeken(h, 2)
\>>> print k
p

En een niet succesvolle:

\>>> k = omgekeerd\_opzoeken(h, 4)
Traceback (most recent call last):
   File "<stdin>", line 1, in ?
   File "<stdin>", line 5, in omgekeerd\_opzoeken
ValueError

Het resultaat van een uitzondering is hetzelfde als wanneer Python er zelf één veroorzaakt: het drukt een afgelopen spoor en een foutboodschap af.

De raise instructie krijgt een gedetailleerde foutboodschap mee als optioneel argument. Bijvoorbeeld:

\>>> raise ValueError, 'waarde komt niet voor in het woordenboek'
Traceback (most recent call last):
   File "<stdin>", line 1, in ?
ValueError: waarde komt niet voor in het woordenboek

Omgekeerd opzoeken is veel langzamer dan voorwaarts opzoeken; moet u dit vaak doen of als het woordenboek omvangrijk wordt dan zal de performance van uw programma er onder lijden.

**Oefening 11.4** Wijzig omgekeerd\_opzoeken zodanig dat het een lijst aanmaakt, en teruggeeft, met _alle_ sleutels die overeenkomen met v of een lege lijst als er geen één overeenkomt.

## 11.4 Woordenboeken en lijsten

Lijsten kunnen als waarden voorkomen in een woordenboek. Bijvoorbeeld: Stel u hebt een woordenboek met daarin letters en hun frequenties, dan is het aardig om deze te kunnen draaien. Dus een woordenboek maken met daarin frequenties en letters die daarbij horen. Omdat haast wel zeker verschillende letters eenzelfde frequentie delen moet elke waarde in het omgekeerde woordenboek een lijst met letters zijn.

Hierbij een functie die het woordenboek omdraait:

def draai\_woordenb(d):
     omkeer = woordenb()
     for key in d:
           waarde = d\[key\]
           if waarde not in inv:
                inv\[waarde\] = \[key\]
           else:
                inv\[waarde\].append(key)
     return omkeer 

Bij iedere passage van de lus krijgt key een sleutel van d en waarde krijgt de bijbehorende waarde. Als waarde niet gelijk is aan omkeer, dan betekent dat we deze nog niet eerder zijn tegengekomen;dan maken we een nieuw item aan en initialiseren dit met een **eenling** (een lijst die uit één enkel element bestaat). Zo niet dan zijn we de waarde eerder tegengekomen en voegen de overeenkomstige sleutel toe aan de lijst.

Hierbij een voorbeeld:

\>>> hist = histogram('papagaai')
\>>> print hist
{'a': 4, 'p': 2, 'g': 1, 'i': 1}
\>>> omkeer = invert\_dict(hist)
\>>> print omkeer 
{1: \['g', 'i'\], 2: \['p'\], 4: \['a'\]}

En hieronder staat een diagram met hist en omkeer:

-   ![boek018_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukElf?action=AttachFile&do=get&target=boek018_nl.png "boek018_nl.png")
    

Een woordenboek is weergegeven als een doos van het type dict erboven en de paar sleutelwaarden erin. Zijn de waarden gehele getallen, drijvende komma of strings dan teken ik ze in de doos. Maar lijsten teken ik meestal buiten de doos om de tekening eenvoudig te houden.

Lijsten kunnen waarden zijn in een woordenboek, zoals het voorbeeld laat zien, maar ze kunnen nooit als sleutel fungeren. Kijk maar eens wat er dan gebeurt:

\>>> t = \[1, 2, 3\]
\>>> d = woordenb()
\>>> d\[t\] = 'Foutje'
Traceback (most recent call last):
   File "<stdin>", line 1, in ?
TypeError: list objects are unhashable

Ik noemde al eerder dat een woordenboek wordt geïmplementeerd met behulp van een hashtabel en dat betekent dat de sleutels **ingehasht** moeten worden.

Een **hash** is een functie die een waarde (elke soort) meekrijgt en een geheel getal terug geeft. Woordenboeken gebruiken deze gehele getallen, hashwaarden genaamd, om de paren met sleutelwaarden op te slaan en terug te vinden.

Dit systeem werkt prima als de sleutels onveranderbaar zijn. Zodra de sleutels veranderlijk zijn, zoals in lijsten, gebeuren er vervelende zaken. Bijvoorbeeld: als u een sleutelpaar maakt hasht Python de sleutel en bewaart deze in de overeenkomstige locatie. Wijzigt u de sleutel en hasht deze opnieuw, dan gaat deze naar een andere locatie. In dat geval hebt u twee entries voor dezelfde sleutel of u bent niet in staat de sleutel te vinden. In beide gevallen werkt het woordenboek niet goed.

Daarom moeten sleutels te hashen zijn en lijsten zijn dat niet. De eenvoudigste manier om deze beperking te omzeilen is om tupels te gebruiken; we zullen deze in het volgende hoofdstuk behandelen.

Omdat woordenboeken te veranderen zijn, kunnen zij ook niet als sleutels optreden maar ze kunnen wel als waarde optreden..

**Oefening 11.5** Lees de documentatie over de woordenboekmethode setdefault en gebruik deze om een beperkte versie van draai\_woordenb te schrijven.

## 11.5 Memo's

Hebt u gespeeld met de fibonacci functie uit paragraaf 6.7? Dan hebt u wellicht ontdekt dat hoe groter het argument, dat u invoerde, hoe langer de functie erover doet. Bovendien loopt de tijd van de uitvoering zeer snel op.

Om dit te begrijpen, beschouw de **aanroepgrafiek** voor fibonacci met n=4:

-   ![book019.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukElf?action=AttachFile&do=get&target=book019.png "book019.png")
    

Een aanroepgrafiek geeft een serie functiekaders weer, met lijnen die elk kader verbinden met de functie die wordt aangeroepen. Aan de bovenkant van de de grafiek staat fibonacci met n=4 die fibonacci aanroept met n=3 en n=2. Op zijn beurt roept fibonacci met n=3, fibonacci aan met n=2 en n=1. Enzovoorts.

Tel maar hoe vaak fibonacci(0) en fibonacci(1) worden aangeroepen. Dit is een niet zo efficiënte oplossing voor het probleem en het wordt nog erger als de argumenten groter worden..

Een oplossing is om bij te houden welke waarden al zijn berekend en deze dan op te slaan in een woordenboek. Een eerder berekende waarde, die is opgeslagen voor later gebruik, wordt een **memo**1 genoemd. Hierbij een implementatie van fibonacci waarbij van memo's gebruik wordt gemaakt:

bekend = {0:0, 1:1}
def fibonacci(n):
      if n in bekend:
           return bekend\[n\]
      resultaat = fibonacci(n-1) + fibonacci(n-2)
       bekend\[n\] = resultaat
       return resultaat

bekend is een woordenboek dat bijhoudt welke Fibonacci getallen we al kennen. Het begint met twee items: 0 komt overeen met 0 en 1 komt overeen met 1.

Zodra fibonacci wordt aangeroepen, controleert deze bekend. Is het resultaat daarin dan wordt dit direct teruggegeven. En anders moet het de nieuwe waarde berekenen en deze weer toevoegen aan het woordenboek en teruggeven.

**Oefening 11.6** Voer deze versie van fibonacci uit en de originele met een reeks van parameters en vergelijk de looptijd.

## 11.6 Globale variabelen

In het voorgaande voorbeeld is bekend aangemaakt buiten de functie, dus behoort het toe aan een speciaal kader genaamd \_\_main\_\_. V in \_\_main\_\_ wordt soms ook **globaal** genoemd omdat deze vanuit elke functie benaderd kan worden. In tegenstelling tot lokale variabelen die verdwijnen als hun functie stopt, blijven globale variabelen bestaan van de ene functieaanroep naar de volgende.

Het is gebruikelijk om globale variabelen te gebruiken voor **vlaggen**. Dat zijn booleaanse variabelen die aangeven ("vlag") of een conditie al of niet waar is. Bijvoorbeeld: sommige programma's gebruiken een vlag genaamd breedsprakig (verbose) om het niveau van details in de uitvoer te controleren:

breedsprakig = True
def voorbeeld1():
       if breedsprakig:
            print 'Running voorbeeld1'

Probeert u een globale variabele opnieuw toe te kennen, dan zult u mogelijk verbaasd staan te kijken. Het volgende voorbeeld is bedoeld om bij te houden of een functie is aangeroepen:

al\_aangeroepen = False
def voorbeeld2():
       al\_aangeroepen = True                 # WRONG

Maar zodra u deze uitvoert zult u zien dat de waarde van al\_aangeroepen niet verandert. Het probleem is dat voorbeeld2 een nieuwe lokale variabele aanmaakt, genaamd al\_aangeroepen. De lokale variabele verdwijnt zodra de functie beëindigd is en heeft dus geen effect op de globale variabele.

Om een globale variabele binnenin een functie opnieuw toe te kennen, moet u de globale variabele declareren voordat u deze gebruikt:

al\_aangeroepen = False
def voorbeeld2():
       global al\_aangeroepen
       al\_aangeroepen = True

De globale instructie vertelt de interpreter zoiets als: "In deze functie, wanneer ik zeg al\_aangeroepen, bedoel ik de globale variabele, maak geen lokale aan".

Hierbij een voorbeeld dat probeert een globale variabele bij te werken:

tel = 0
def voorbeeld3():
      tel = tel + 1                  # WRONG

Voert u deze uit dan krijgt u:

UnboundLocalError: local variable 'count' referenced before assignment

Python neemt aan dat tel lokaal is; dat betekent dat u deze leest nog voordat deze geschreven is. De oplossing, zoals eerder gezegd, is om tel globaal te declareren.

def voorbeeld3():
      global tel
      tel += 1

Is de globale waarde aan te passen, dan kunt u deze wijzigen zonder deze te declareren:

bekend = {0:0, 1:1}
def voorbeeld4():
      bekend\[2\] = 1

Dus u kunt elementen toevoegen, verwijderen en vervangen van een globale lijst of woordenboek maar wilt u een variabele opnieuw toekennen dan moet u deze declareren:

def voorbeeld5():
      global bekend
      bekend = woordenboek()

## 11.7 Lange gehele getallen

Berekent u fibonacci(50), dan krijgt u:

\>>> fibonacci(50)
12586269025L

De "L" aan het einde geeft aan dat het resultaat een lang geheel getal2 is van het type long.

Waarden van het type int hebben een beperkt bereik. Lange gehele getallen kunnen bijzonder groot worden maar als ze groter worden, nemen ze ook meer ruimte en tijd in.

De wiskundige operatoren werken op lange gehele getallen, en functies in de math module ook. In het algemeen geldt dat code die met een int werkt, ook werkt met een long.

Iedere keer als het resultaat van een berekening te groot is om als geheel getal (integer) weer te geven, zal Python het resultaat weergeven als een lang geheel getal (long integer):

\>>> 1000 \* 1000
1000000
\>>> 100000 \* 100000
10000000000L

In het eerste geval heeft het resultaat het type int, in het tweede geval is dit een long.

**Oefening 11.7** Kwadrateren van grote gehele getallen is de basis voor gebruikelijke algoritmes voor de versleuteling van publieke-sleutels. Lees de Wikipedia pagina over het RSA algoritme3 en schrijf functies die berichten coderen en decoderen.

## 11.8 Debuggen

Zodra u met grotere verzamelingen gegevens werkt, kan het onpraktisch worden om te gaan debuggen door het printen en controleren van gegevens met de hand. Hierbij enkele suggesties voor het debuggen van grote verzamelingen van gegevens:

**Minder invoer**: Als het enigszins kan, beperk de omvang van de gegevensverzameling. Bijvoorbeeld: als het programma een tekstbestand leest, start dan met de eerste 10 regels of met het kleinste voorbeeld dat u kunt vinden. U kunt de bestanden zelf aanpassen of nog beter het programma dusdanig aanpassen dat het alleen de eerste n regels leest. Treedt nu een fout op dan kunt u n terugbrengen tot de kleinst mogelijke waarde waarbij de fout nog optreedt en vervolgens de waarde geleidelijk aan omhoog brengen als u fouten hebt gecorrigeerd en weer nieuwe fouten vindt.

**Controleer samenvattingen types**: In plaats van het printen en controleren van een complete gegevensverzameling, overweeg het printen van een samenvatting van de gegevens. Bijvoorbeeld: het aantal items in een woordenboek of het totaal van een lijst met getallen.  
  
Een gebruikelijke oorzaak van uitvoeringsfouten is dat een waarde niet het juiste type heeft. Voor het debuggen van dit soort fouten is het vaak voldoende om het type van de waarden te printen.

**Schrijf ingebouwde controles**: Soms kunt u code schrijven die automatisch controleert op fouten. Bijvoorbeeld: als u het gemiddelde berekent van een lijst met getallen, dan kunt u controleren of het resultaat niet groter is dan het grootste getal of kleiner dan het kleinste getal. Dit wordt een "gezondheids-controle" genoemd omdat het "gekke" resultaten ontdekt.  
  
Een ander soort controle vergelijkt de resultaten van twee verschillende berekeningen om te zien of deze consistent zijn. Dit wordt een consistentie-controle genoemd.

**Uitvoer netjes printen**: Uitvoer van het debug proces formatteren maakt het eenvoudiger om een fout op te sporen. Bekijk het voorbeeld uit paragraaf 6.9. De pprint module levert een pprint functie die de ingebouwde types weergeeft in een leesbaar formaat.

Zoals eerder gezegd, tijd besteed aan het bouwen van steigers vermindert de tijd die anders besteed moet worden aan debuggen.

## 11.9 Woordenlijst

**woordenboek**: De overeenkomst van een verzameling met sleutels en hun overeenkomstige waarden.

**sleutel-waarden paar**: De vertegenwoordiging van de overeenkomst tussen een sleutel en een waarde.

**item**: Een andere naam voor een sleutel-waarden paar.

**sleutel**: Een object dat voorkomt in een woordenboek als het eerste deel van een sleutel-waarden paar.

**waarde**: Een object dat voorkomt in een woordenboek als het tweede deel van een sleutel-waarden paar. Dit is specifieker dan het voorgaande gebruik van het woord "waarde".

**implementatie**: Een manier van uitvoeren van een berekening.

**hash tabel**: Het algoritme dat wordt gebruikt om Python woordenboeken te implementeren.

**hash functie**: Een functie gebruikt bij hash tabellen om de locatie van een sleutel te berekenen.

**hashbaar**: Een type dat een hash functie heeft. Niet wijzigbare types zoals integers, floats en strings zijn hashbaar, wijzigbare types zoals lijsten en woordenboeken niet.

**Opzoeken**: Een actie op een woordenboek die een sleutel gebruikt en de bijbehorende waarde vindt.

**Omgekeerd zoeken**: Een actie op een woordenboek die een waarde gebruikt en één of meer bijbehorende sleutels vindt.

**singleton**: Een lijst (of een andere reeks) met één enkel element.

**aanroepgrafiek**: Een diagram dat elk kader, aangemaakt gedurende de uitvoering van programma, weergeeft met een pijl van de aanroeper naar de aangeroepene.

**histogram**: Een verzameling tellers.

**memo**: Een berekende waarde die wordt opgeslagen om onnodige berekeningen in de toekomst te voorkomen.

**globale variabele**: Een variabele gedefinieerd buiten een functie. Globale variabelen zijn te benaderen vanuit elke functie.

**vlag**: Een booleaanse variabele gebruikt om aan te geven of een voorwaarde waar is.

**declaratie**: Een instructie zoals global die de interpreter iets vertelt over een variabele.

## 11.10 Oefeningen

**Oefening 11.8** Hebt u oefening 10.5 uitgevoerd, dan hebt u een functie genaamd heeft\_dubbelen die een lijst meekrijgt als een parameter en Waar terug geeft als er enig object meer dan twee keer in de lijst voorkomt.

Gebruik een woordenboek om een snellere en eenvoudiger versie van heeft\_dubbelen te schrijven.

**Oefening 11.9** Twee woorden zijn "roterende paren” als u een woord kunt omdraaien en dan een ander woord terug krijgt (zie **roteer\_woord** in oefening 8.12).

Schrijf een programma dat een woordenlijst inleest en alle roterende paren vindt.

**Oefening 11.10** Hierbij een andere puzzel uit Car Talk4:

-   Deze is ingezonden door een man genaamd Dan O’Leary. Hij kwam, kort geleden, op een normaal éénlettergrepig woord van vijf letters dat de volgende unieke eigenschap bezit. Verwijdert u de eerste letter dan vormen de resterende letters een homofoon (gelijkklinkend) van het oorspronkelijke woord. Vervang de eerste letter, dat wil zeggen, plaats de eerste terug en verwijder de tweede letter en het resultaat is opnieuw een homofoon van het oorspronkelijke woord. De vraag is over welk woord hebben wij het?
    
      
    Ik geef nu een voorbeeld dat niet opgaat. Neem het woord van vijf letters 'wrack'. W-R-A-C-K, zoals in ‘wrack with pain.’ Verwijder de eerste letter en een woord van vier letters ’R-A-C-K’ blijft over. Als in, ‘Holy cow, did you see the rack on that buck! It must have been a nine-pointer!’ Dit is een perfecte homofoon. Plaatst u de ‘w’ terug en verwijderd u de ‘r’ dan blijft over het woord ‘wack’, dit is een echt woord maar geen homofoon van de andere twee woorden.  
      
    Maar er is tenminste één woord, voor zover Dan en wij weten, die twee homofoons bevat als we de bovenstaande regels in acht nemen. De vraag is: wat is dat woord?
    

U kunt het woordenboek uit oefening 11.1 gebruiken om te controleren of een string in de woordenlijst voorkomt.

Deze controle of twee woorden homofoon zijn kan worden uitgevoerd met het CMU Pronouncing Dictionary. Dit is te downloaden bij [www.speech.cs.cmu.edu/cgi-bin/cmudict](https://wiki.ubuntu-nl.org/www.speech.cs.cmu.edu/cgi-bin/cmudict) of bij [thinkpython.com/code/c06d](http://www.thinkpython.com/code/c06d) en u kunt ook [thinkpython.com/code/pronounce.py](http://www.thinkpython.com/code/pronounce.py) downloaden; dit bevat een functie genaamd read\_dictionary die de pronouncing dictionary leest en een Python woordenboek teruggeeft waarbij ieder woord overeenkomt met een string die zijn primaire uitspraak beschrijft.

Schrijf een programma die alle woorden opsomt die de puzzel oplossen. U kunt mijn oplossing vinden op [thinkpython.com/code/homophone.py](http://thinkpython.com/code/homophone.py).

* * *

1 See [http://wikipedia.org/wiki/Memoization](http://wikipedia.org/wiki/Memoization) 2 In Python 3.0, is het type long verdwenen, alle gehele getallen (integers), ook de hele grote zijn van het type int. 3 [http://nl.wikipedia.org/wiki/RSA\_%28cryptografie%29](http://nl.wikipedia.org/wiki/RSA_%28cryptografie%29) 4 [http://www.cartalk.com/content/puzzler/transcripts/200717](http://www.cartalk.com/content/puzzler/transcripts/200717)