[community/ThinkPython/HoofdstukZeven - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven)

# Hoofdstuk 7 Iteraties

## 7.1 Meervoudige toewijzing

Zoals u wellicht al hebt ontdekt, is het mogelijk om vaker een waarde toe te kennen aan dezelfde variabele. De nieuwe toekenning zal de bestaande variabele laten verwijzen naar de nieuwe waarde (en niet meer naar de oude waarde).

jan    = 5
print    jan,
jan    = 7
print    jan

De uitvoer van het programma is 5 7, omdat de eerste keer dat jan wordt weergegeven, de waarde 5 is. De tweede keer is de waarde 7. De komma aan het einde van de eerste print instructie onderdrukt een nieuwe regel, waardoor beide uitvoeren op dezelfde regel verschijnen.

Hier is een voorbeeld van **meervoudige toewijzing** in een toestandsdiagram:

-   ![boek010_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven?action=AttachFile&do=get&target=boek010_nl.png "boek010_nl.png")
    

Bij een meervoudige toewijzing is het bijzonder belangrijk om onderscheid te maken tussen een toewijzingsopdracht en een vergelijkinginstructie. Omdat Python het gelijkteken (=) gebruikt voor toewijzing kunt u gemakkelijk in de fout gaan door een instructie als  a = b  als een gelijkheidsinstructie te interpreteren. Dat is het echter niet!

Ten eerste, gelijkheid is een symmetrische relatie. Toekenning is dat niet. Bijvoorbeeld: in de wiskunde, als _a_ = 7 is 7 = _a_. Maar in Python is de instructie a = 7 toegestaan, echter 7 = a is dat niet.

Bovendien, in de wiskunde is een gelijkheidsinstructie of waar of niet waar, wanneer dan ook. Als NU _a = b_ zal _a_ altijd gelijk zijn aan _b_. In Python kan een toekenningsinstructie twee variabelen gelijk maken, maar dat hoeft niet altijd zo te blijven:

a = 5
b = a        # a en b zijn nu gelijk
a = 3        # a en b zijn niet langer gelijk

De derde regel verandert de waarde van a maar verandert de waarde van b niet. Dit betekent dat ze niet meer gelijk zijn.

Alhoewel meervoudige toekenning vaak nuttig is, moet u het met voorzichtigheid gebruiken. Als de waardes van de variabelen vaak veranderen, kan het de code moeilijk leesbaar en moeilijk te debuggen maken.

## 7.2 Variabelen bijwerken

Eén van de meest voorkomende vormen van meervoudige toekenning is **bijwerken**, waar de nieuwe waarde van een variabele afhankelijk is van de oude waarde.

x = x+1

Dit betekent "haal de huidige waarde van x op, tel er één bij op, werk x vervolgens bij met de nieuwe waarde." Als u een variabele die niet bestaat probeert bij te werken, zal dit een fout geven, omdat Python de rechterkant controleert voordat het een waarde toekent aan x.

\>>> x = x+1
NameError: name 'x' is not defined

Voordat u een variabele kunt bijwerken, dient u deze te **initialiseren**, normaal gesproken met een simpele toekenning:

\>>> x = 0
\>>> x = x+1

Een variabele bijwerken door met 1 te verhogen wordt **toename** genoemd; met 1 verminderen wordt **afname** genoemd.

## 7.3 De 'while' instructie

Computers worden vaak gebruikt voor het automatiseren van herhalende taken. Herhalen van identieke of soortgelijke taken zonder fouten is iets waar computers goed, en mensen slecht in zijn.

We hebben twee programma's gezien, aftellen en print\_n, die gebruik maken van recursie om herhalingen uit te voeren. Dit wordt ook wel **iteratie** genoemd. Omdat iteraties veel voorkomen, biedt Python verschillende functies die het gemakkelijker maken. Eén daarvan is de for instructie die we zagen in paragraaf 4.2. We komen daar later op terug.

Een andere is de while instructie. Hier is een versie van countdown die gebruik maakt van een while instructie:

function isnumbered(obj) { return obj.childNodes.length && obj.firstChild.childNodes.length && obj.firstChild.firstChild.className == 'LineNumber'; } function nformat(num,chrs,add) { var nlen = Math.max(0,chrs-(''+num).length), res = ''; while (nlen>0) { res += ' '; nlen-- } return res+num+add; } function addnumber(did, nstart, nstep) { var c = document.getElementById(did), l = c.firstChild, n = 1; if (!isnumbered(c)) { if (typeof nstart == 'undefined') nstart = 1; if (typeof nstep == 'undefined') nstep = 1; var n = nstart; while (l != null) { if (l.tagName == 'SPAN') { var s = document.createElement('SPAN'); var a = document.createElement('A'); s.className = 'LineNumber'; a.appendChild(document.createTextNode(nformat(n,4,''))); a.href = '#' + did + '\_' + n; s.appendChild(a); s.appendChild(document.createTextNode(' ')); n += nstep; if (l.childNodes.length) { l.insertBefore(s, l.firstChild); } else { l.appendChild(s); } } l = l.nextSibling; } } return false; } function remnumber(did) { var c = document.getElementById(did), l = c.firstChild; if (isnumbered(c)) { while (l != null) { if (l.tagName == 'SPAN' && l.firstChild.className == 'LineNumber') l.removeChild(l.firstChild); l = l.nextSibling; } } return false; } function togglenumber(did, nstart, nstep) { var c = document.getElementById(did); if (isnumbered(c)) { remnumber(did); } else { addnumber(did,nstart,nstep); } return false; } document.write('<a href="#" onclick="return togglenumber(\\'CA-8c30db69827c97f151dbd3938c4ab16458b2e482\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-8c30db69827c97f151dbd3938c4ab16458b2e482_1) def aftellen(n):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-8c30db69827c97f151dbd3938c4ab16458b2e482_2)        while n > 0:
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-8c30db69827c97f151dbd3938c4ab16458b2e482_3)            print n
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-8c30db69827c97f151dbd3938c4ab16458b2e482_4)            n = n\-1
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-8c30db69827c97f151dbd3938c4ab16458b2e482_5)        print 'lancering!'

U kunt de while instructie bijna lezen alsof het Engels is. Het betekent: "Zolang n groter is dan 0, geef de waarde van n weer en verminder dan de waarde van n met 1. Wanneer 0 wordt bereikt, geef het woord lancering! weer".

Meer formeel, hier is het proces van de uitvoering van een while instructie:

1.  Evalueer de conditie, dat True of False is.
    
2.  Als de conditie false is, stop de while instructie en ga door met uitvoeren vanaf de volgende instructie.
    
3.  Als de conditie true is, voer de inhoud van de while-lus uit en ga dan terug naar stap 1.

Dit type proces heet een **lus**, omdat er na de derde stap terug wordt gegaan naar het begin.

De inhoud van de lus zou de waarde van één of meer variabelen moeten veranderen, zodat uiteindelijk de conditie false wordt en de lus eindigt. Anders zal de lus eeuwig herhaald worden. Dat heet een **oneindige lus**. Een eindeloze bron van vermaak voor informatici is de constatering dat de gebruiksaanwijzing op shampoo, "inzepen, spoelen, herhalen," een oneindige lus is.

In het geval van aftellen, kunnen we bewijzen dat de lus eindigt, omdat we weten dat de waarde van n eindig is en we kunnen zien dat de waarde van n elke keer door de lus kleiner wordt, zodat uiteindelijk de 0 bereikt zal worden. In andere gevallen is het niet zo gemakkelijk te zeggen:

document.write('<a href="#" onclick="return togglenumber(\\'CA-dca857ec3c6d28efa21a230d3e7eb2b464eb7e5b\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-dca857ec3c6d28efa21a230d3e7eb2b464eb7e5b_1) def reeks(n):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-dca857ec3c6d28efa21a230d3e7eb2b464eb7e5b_2)       while n != 1:
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-dca857ec3c6d28efa21a230d3e7eb2b464eb7e5b_3)             print n,
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-dca857ec3c6d28efa21a230d3e7eb2b464eb7e5b_4)             if n%2 == 0:                 \# n is even
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-dca857ec3c6d28efa21a230d3e7eb2b464eb7e5b_5)                  n = n/2
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-dca857ec3c6d28efa21a230d3e7eb2b464eb7e5b_6)             else:                        \# n is oneven
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-dca857ec3c6d28efa21a230d3e7eb2b464eb7e5b_7)                  n = n\*3+1

De conditie voor deze lus is n! = 1, zodat de lus zal doorgaan tot n gelijk aan 1 is, wat de conditie false maakt.

Elke keer door de lus gaand, geeft het programma de uitvoer weer van de waarde van n en controleert dan of het even of oneven is. Als het even is, wordt n gedeeld door 2. Als het oneven is, wordt de waarde van n vervangen door n \* 3 +1. Bijvoorbeeld: als het argument 3 wordt doorgegeven aan reeks, is de resulterende reeks 3, 10, 5, 16, 8, 4, 2, 1.

Daar n soms toeneemt en soms afneemt, is er geen duidelijk bewijs dat n ooit zal oplopen tot 1, of dat het programma eindigt. Voor een aantal specifieke waarden van n, kunnen we beëindiging bewijzen. Bijvoorbeeld, als de startwaarde een macht van twee is, dan is de waarde van n elke keer door de lus gaand gelijk totdat 1 wordt bereikt. Het vorige voorbeeld eindigt met een dergelijke volgorde, beginnend met 16.

Een moeilijke vraag is of we kunnen bewijzen dat dit programma eindigt voor _alle positieve waarden_ van n. Tot zover1, is niemand in staat geweest om het te bewijzen _of_ te weerleggen!

**Oefening 7.1** Herschrijf de functie print\_n van paragraaf 5.8 met behulp van iteratie in plaats van recursie.

## 7.4 break

Soms weet u niet dat het tijd is om een lus te beëindigen totdat u halverwege de code bent. In dat geval kunt u de break instructie gebruiken om de lus te beëindigen.

Bijvoorbeeld: u wilt de invoer van de gebruiker opnemen, totdat ze klaar typen. U zou dan het volgende kunnen schrijven:

document.write('<a href="#" onclick="return togglenumber(\\'CA-88c5b609ab858bebc23f546872f8790849eabecb\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-88c5b609ab858bebc23f546872f8790849eabecb_1) while True:
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-88c5b609ab858bebc23f546872f8790849eabecb_2)      regel = raw\_input('\> ')
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-88c5b609ab858bebc23f546872f8790849eabecb_3)      if regel == 'klaar':
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-88c5b609ab858bebc23f546872f8790849eabecb_4)            break
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-88c5b609ab858bebc23f546872f8790849eabecb_5)      print regel 
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-88c5b609ab858bebc23f546872f8790849eabecb_6) 
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven#CA-88c5b609ab858bebc23f546872f8790849eabecb_7) print 'Klaar!'

De lus conditie is True, wat altijd waar is, dus zal de lus doorgaan totdat de break instructie wordt bereikt.

Elke keer in de lus zal de gebruiker om een reactie gevraagd worden met een > (groter-dan teken). Als de gebruiker klaar typt, beëindigt de break instructie de lus. Anders zal het programma weergeven wat de gebruiker heeft geschreven en de lus opnieuw uitvoeren. Hier is een voorbeeld uitvoering:

\> niet klaar
niet klaar
\> klaar
Klaar!

Deze manier van while lussen schrijven komt vaak voor, omdat u de conditie waar u maar wilt, kunt controleren, en dus niet alleen aan het begin van de lus. Daarnaast kunt u de stopconditie bevestigend ("Stop wanneer dit gebeurt") in plaats van negatief ("Ga door totdat dit gebeurt") implementeren.

## 7.5 vierkantswortel

Lussen worden vaak gebruikt in programma's die numerieke resultaten berekenen door te beginnen met een geschat antwoord en deze iteratief te verbeteren.

Als voorbeeld, een manier om de vierkantswortels te berekenen is Newton's methode. Veronderstel dat u de vierkantswortel van _a_ wilt weten. Als u begint met om het even welke schatting voor _x_, kunt u een nauwkeurige schatting berekenen met de volgende formule:

-   ![formula001.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven?action=AttachFile&do=get&target=formula001.png "formula001.png")
    

Bijvoorbeeld, als _a_ is 4 en _x_ is 3:

\>>> a = 4.0
\>>> x = 3.0
\>>> y = (x + a/x) / 2
\>>> print y
2.16666666667

Dit ligt dichter bij het juiste antwoord (√4 = 2). Als we het proces met de nieuwe schatting herhalen zal het resultaat nog dichter bij het antwoord komen te liggen:

\>>> x = y
\>>> y = (x + a/x) / 2
\>>> print y
2.00641025641

Na een aantal herzieningen is de schatting bijna gelijk:

\>>> x = y
\>>> y = (x + a/x) / 2
\>>> print y
2.00001024003
\>>> x = y
\>>> y = (x + a/x) / 2
\>>> print y
2.00000000003

In het algemeen weten we niet van te voren hoeveel stappen er nodig zijn om het juiste antwoord te krijgen, maar we weten wel wanneer we er zijn omdat de schatting niet meer verandert:

\>>>   x = y
\>>>   y = (x + a/x) / 2
\>>>   print y
2.0
\>>>   x = y
\>>>   y = (x + a/x) / 2
\>>>   print y
2.0

Wanneer y == x, kunnen we stoppen. Dit is een lus die begint met een initiële schatting van x; die wordt verbeterd totdat de uitkomst ophoudt te veranderen:

while True:
      print x
      y = (x + a/x) / 2
      if y == x:
            break
      x = y

Voor de meeste waarden van a werkt dit prima, maar over het algemeen is het gevaarlijk om float waarden te vergelijken. Floating-point waarden zijn alleen bij benadering correct: de meeste rationele getallen, zoals 1/3, en irrationele getallen, zoals √2, kunnen niet exact worden weergegeven met een float.

In plaats van te controleren of x en y exact gelijk zijn, is het veiliger om de ingebouwde functie abs te gebruiken om de absolute waarde of grootheid of het verschil ertussen te berekenen:

if abs(y-x) < epsilon:
     break

Hierbij heeft epsilon een waarde als 0.0000001 die bepaalt hoe dichtbij dichtbij genoeg is.

**Oefening 7.2** kapsel deze lus in, in een functie genaamd vierkantswortel die de parameter a meekrijgt, een redelijke waarde voor x kiest en een schatting van de vierkantswortel van a teruggeeft.

## 7.6 Algoritmes

Newton’s methode is een voorbeeld van een **algoritme**: het is een mechanisch proces voor het oplossen van een categorie problemen (in dit geval, het berekenen van de vierkantswortel).

Het is niet gemakkelijk om het algoritme te definiëren. Wat helpt, is te beginnen met iets dat geen algoritme is. Toen u leerde ééncijferige getallen te vermenigvuldigen, hebt u waarschijnlijk de tafels uit uw hoofd geleerd. Het resultaat: u hebt 100 specifieke oplossingen onthouden. Dat soort kennis is niet algoritmisch.

Maar als u "lui" was, speelde u waarschijnlijk vals door een paar trucjes te leren. Bijvoorbeeld, om het product van _n_ en 9 te vinden, kunt u _n_ − 1 opschrijven als het eerste getal en 10 − _n_ als het tweede getal. Deze truc is een algemene oplossing voor het vermenigvuldigen van getallen van één cijfer met 9. Dat is een algoritme!

Overeenkomstig zijn de technieken die u leerde voor het optellen met het overdragen, aftrekken met lenen en staartdelingen; dat zijn allemaal algoritmes. Eén van de kenmerken van een algoritme is dat deze geen enkele intelligentie nodig heeft om hem uit te voeren. Het zijn mechanische processen waarbij elke stap de vorige volgt, overeenkomstig een serie eenvoudige regels.

In mijn ogen is het beschamend dat mensen zoveel tijd op school kwijt zijn aan het leren hoe algoritmes uit te voeren, die letterlijk geen intelligentie vereisen.

Aan de andere kant is het proces van het ontwerpen van een algoritme interessant, een intellectuele uitdaging en een centraal onderdeel van wat wij programmeren noemen.

Een aantal van de zaken die mensen van nature doen, zonder moeite of bewuste gedachte, zijn de allermoeilijkste om uit te drukken in een algoritme. Begrijpen van een natuurlijke taal is een goed voorbeeld. We doen het allemaal maar tot nu toe is nog niemand in staat geweest het _hoe_ we het doen uit te leggen, tenminste niet in de vorm van een algoritme.

## 7.7 Debuggen

Als u begint met het schrijven van grotere programma's, besteedt u meer tijd aan het debuggen. Meer code betekent meer kans op het maken van een fout en meer plaatsen waar de fout verstopt zit.

Eén manier om de debugtijd terug te dringen is “debuggen door splitsing”. Bijvoorbeeld: u hebt 100 regels code in uw programma en u controleert één voor één; dan kost dat 100 stappen.

Splits, in plaats daarvan, het probleem in twee delen. Kijk in het midden van het programma, of daar in de buurt, naar een tussenliggende waarde die u kunt controleren. Voeg een print statement toe (of iets anders met een controleerbaar effect) en voer het programma uit.

Als de uitkomst in het midden foutief is, moet het probleem zich in de eerste helft van het programma bevinden. Is de uitkomst correct dan bevindt het probleem zich in de tweede helft.

Ieder keer als u een controle zoals deze uitvoert, halveert u het aantal regels dat u moet doorzoeken. Na zes stappen (duidelijk minder dan 100), bent u bij één of twee regels aanbeland, in theorie althans.

In de praktijk is het niet altijd even helder wat het "midden van een programma" is en is het niet altijd mogelijk dat te controleren. Het heeft geen zin om het aantal regels te tellen en daarmee het exacte midden te bepalen. Denk, in plaats daarvan, aan die plaatsen in het programma waar fouten kunnen optreden en waarbij u gemakkelijk een controle kunt inbouwen. Kies dan een positie waar u denkt dat de kansen gelijk zijn voor het optreden van een fout ervoor of erna.

## 7.8 Woordenboek

**meervoudige toewijzing**: Het vaker toewijzen van een waarde aan een variabele tijdens de werking van een programma.

**update**: Een toekenning waar de nieuwe waarde van een variabele afhankelijk is van de oude waarde.

**initialiseren**: Een toekenning die een initiële waarde aan een variabele geeft die zal worden bijgewerkt.

**toename**: Een bewerking die de waarde van een variabele verhoogt (meestal met één).

**afname**: Een bewerking die de waarde van een variabele verlaagt.

**iteratie**: Herhaalde uitvoering van een reeks instructies door ofwel gebruik te maken van een recursieve functie aanroep, of door een lus.

**oneindige lus**: Een lus waarin de conditie nooit "niet waar" zal zijn.

## 7.9 Oefeningen

**Oefening 7.3** Om het vierkantswortel-algoritme uit dit hoofdstuk te testen, zou u het kunnen vergelijken met math.sqrt. Schrijf een functie genaamd test\_vierkantswortel die een tabel weergeeft zoals deze:

1.0   1.0               1.0                0.0
2.0   1.41421356237     1.41421356237      2.22044604925e-16
3.0   1.73205080757     1.73205080757      0.0
4.0   2.0               2.0                0.0
5.0   2.2360679775      2.2360679775       0.0
6.0   2.44948974278     2.44948974278      0.0
7.0   2.64575131106     2.64575131106      0.0
8.0   2.82842712475     2.82842712475      4.4408920985e-16
9.0   3.0               3.0                0.0

De eerste kolom is een getal, _a_; de tweede kolom is de vierkantswortel van a berekend met de functie van Oefening 7.2; de derde kolom is de vierkantswortel berekend door math.sqrt; de vierde kolom is de absolute waarde van het verschil tussen de twee schattingen.

**Oefening 7.4** De ingebouwde functie eval neemt een string en evalueert die middels de Python-interpreter.

Als voorbeeld:

\>>> eval('1 + 2 \* 3')
7
\>>> import math
\>>> eval('math.sqrt(5)')
2.2360679774997898
\>>> eval('type(math.pi)')
<type 'float'>

Schrijf een functie genaamd eval\_loop die iteratief om invoer vraagt van de gebruiker, de resulterende invoer evalueert middels eval, en het resultaat weergeeft.

De functie dient door te gaan totdat de gebruiker 'done' typt, en vervolgens de waarde van de laatste expressie die geëvalueerd is, teruggeeft.

**Oefening 7.5** De briljante wiskundige Srinivasa Ramanujan vond een oneindige serie2 uit die kan worden gebruikt om een numerieke benadering van π te genereren:

-   ![formula002.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeven?action=AttachFile&do=get&target=formula002.png "formula002.png")
    

Schrijf een functie genaamd schat\_pi die gebruik maakt van deze formule om een schatting van π te berekenen en terug te geven. Deze moet gebruik maken van een while lus om de termen van de sommering te berekenen tot de laatste term kleiner is dan 1e-15 (dat is Python notatie voor 10\-15). U kunt het resultaat controleren door het te vergelijken met math.pi.

U kunt een uitwerking vinden op [thinkpython.com/code/pi.py](http://www.greenteapress.com/thinkpython/code/pi.py).

* * *

1 Zie [nl.wikipedia.org/wiki/Vermoeden\_van\_Collatz](http://nl.wikipedia.org/wiki/Vermoeden_van_Collatz).  
2 Zie [nl.wikipedia.org/wiki/Pi\_(wiskunde)](http://nl.wikipedia.org/wiki/Pi_(wiskunde)).