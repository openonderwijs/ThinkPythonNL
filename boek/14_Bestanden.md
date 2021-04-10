[community/ThinkPython/HoofdstukVeertien - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVeertien)

# Hoofdstuk 14 Bestanden

## 14.1 Persistentie

Het merendeel van de programma's die we tot nu toe hebben gezien, zijn zo gezegd vluchtig op een manier dat ze een korte tijd draaien en wat uitvoer produceren. Maar zodra ze gestopt zijn, verdwijnen hun gegevens. Voert u de programma's opnieuw uit dan starten ze met een schone lei.

Andere programma's zijn **persistent**: deze draaien voor langere tijd achtereen (of voor altijd); ze bewaren tenminste iets van hun gegevens permanent in opslag (bijvoorbeeld een harde schijf) en als ze gestopt en opnieuw uitgevoerd worden, gaan ze verder met waar ze gebleven waren.

Voorbeelden van persistente programma's zijn besturingssystemen; deze draaien continue zodra een computer aan staat, of webservers die altijd draaien en wachten op een verzoek dat langs komt op het netwerk.

Eén van de eenvoudigste manieren voor programma's om hun gegevens te onderhouden, is door tekstbestanden te lezen en te schrijven.

We hebben al programma's gezien die tekstbestanden lezen; in dit hoofdstuk zullen we programma's zien die in tekstbestanden gaan schrijven.

Een alternatief is het opslaan van de status van een programma in een database. In dit hoofdstuk zal ik een eenvoudige database en een module pickle introduceren; deze maken het voor een programma gemakkelijk om gegevens op te slaan.

## 14.2 Lezen en schrijven

Een tekstbestand is een reeks karakters, opgeslagen op een permanent medium zoals een harde schijf, flash geheugen, CD-rom of DVD. We hebben gezien hoe een bestand wordt geopend en gelezen in paragraaf 9.1.

Het schrijven in een bestand werkt als u dit opent in de 'w' modus als een tweede parameter:

\>>> fout = open('uitvoer.txt', 'w')
\>>> print fout
<open file 'uitvoer.txt', mode 'w' at 0xb7eb2410>

Bestaat een bestand al, dan zal het openen in 'schrijf' modus de oude gegevens wissen en fris beginnen; let dus goed op! Bestaat het bestand nog niet, dan wordt dit nieuw aangemaakt.

De schrijf methode plaatst gegevens in een bestand.

\>>> regel1= "Dit hier in de halskwab,\\n"
\>>> fout.write(regel1)

Nogmaals, het bestandsobject houdt bij waar het gebleven is, dus roept schrijven opnieuw aan, en voegt gegevens toe aan het einde.

\>>> regel2 = "het symbool van ons land.\\n"
\>>> fout.write(regel2)

Bent u klaar met schrijven dan moet u het bestand sluiten.

\>>> fout.close()

## 14.3 Formatteer operator

Het argument van schrijf moet een string zijn, dus willen we andere waarden in een bestand plaatsen, dan moeten deze naar een string worden omgezet. De eenvoudigste manier is met een str:

\>>> x = 52
\>>> f.write(str(x))

Een alternatief is gebruik te maken van de **formatteer operator**, het "%" teken. Toegepast op gehele getallen is het % teken de modulusoperator.

Maar als de eerste operand een string is, dan is het % teken een formatteeroperator.

De eerste operand is de **formaatstring**, die één of meer **formatteerreeksen** bevat, die beschrijven hoe de tweede operand wordt geformatteerd. Het resultaat is een string.

Bijvoorbeeld, de formatteerreeks '%d' betekent dat de tweede operand geformatteerd moet worden als een geheel getal (d staat voor “decimaal”):

\>>> kamelen = 42
\>>> '%d' % kamelen
'42'

Het resultaat is de string '42', niet te verwarren met de getalwaarde 42.

Een formatteerreeks kan overal in een string voorkomen; u kunt dus een waarde in een zin opnemen:

\>>> kamelen = 42
\>>> 'Ik heb %d kamelen gezien.' % kamelen
'Ik heb 42 kamelen gezien.'

Komen er meerdere formatteerreeksen voor in een string, dan moet het tweede argument een tupel zijn. Elke formatteerreeks wordt, in volgorde, vergeleken met een element uit de tupel.

Het volgende voorbeeld gebruikt '%d' om een geheel getal '%g' te formatteren; voor het formatteren van een drijvende komma getal wordt '%s' gebruikt, vraag me niet waarom:

\>>> 'In %d jaren heb ik %g %s gezien.' % (3, 0.1, 'kamelen')
'In 3 jaren heb ik 0.1 kamelen gezien.'

Het aantal elementen in een tupel moet overeenkomen met het aantal formatteerreeksen in de string.

Ook de soorten elementen moeten overeenkomen met de formatteerreeksen:

\>>> '%d %d      %d' % (1, 2)
TypeError:      not enough arguments for format string
\>>> '%d' %       'euro's'
TypeError:      illegal argument type for built-in operation

In het eerste voorbeeld zijn er te weinig elementen; in het tweede voorbeeld is het element van het verkeerde soort.

De formatteeroperator is krachtig maar kan moeilijk zijn in het gebruik. Lees er meer over bij [docs.python.org/lib/typesseq-strings.html](https://wiki.ubuntu-nl.org/docs.python.org/lib/typesseq-strings.html).

## 14.4 Bestandsnamen en paden

Bestanden zijn georganiseerd in **directory's**, ook wel mappen genoemd. Elk programma dat draait heeft een "huidige directory", dat is de standaard directory voor de meeste bewerkingen. Bijvoorbeeld: opent u een bestand om te lezen dan kijkt Python in de huidige directory.

De os module levert functies om te werken met bestanden en directory's (“os” staat voor “operating system” of ook "besturingssysteem"). os.getcwd geeft de naam terug van de huidige directory:

\>>> import os
\>>> cwd = os.getcwd()
\>>> print cwd
/home/jan

cwd staat voor “current working directory”, de huidige werk directory. Het resultaat in dit voorbeeld is /home/jan, dit is de home directory van een gebruiker genaamd jan.

Een string zoals cwd die een bestand identificeert wordt een **pad** genoemd. Een **relatief pad** begint vanaf de huidige directory; een absoluut pad begint vanaf de hoogste directory in het bestandssysteem.

De paden die we tot nu toe hebben gezien, zijn eenvoudige bestandsnamen; deze zijn dus relatief vanaf de huidige directory. U kunt os.path.abspath gebruiken om het absolute pad te vinden:

\>>> os.path.abspath('memo.txt')
'/home/jan/memo.txt'

os.path.exists controleert het bestaan van een bestand of een directory:

\>>> os.path.exists('memo.txt')
True

Bestaat deze, dan controleert os.path.isdir of het een directory is:

\>>> os.path.isdir('memo.txt')
False
\>>> os.path.isdir('muziek')
True

Op dezelfde manier controleert os.path.isfile of het een bestand is.

os.listdir geeft een lijst met bestanden (en andere directory's) in de gegeven directory terug:

\>>> os.listdir(cwd)
\['muziek', 'fotos', 'memo.txt'\]

Het volgende voorbeeld "wandelt" door een directory, drukt de namen af van alle bestanden en roept zichzelf steeds aan in iedere directory, en laat zo de werking zien van deze functies.

def lopen(dir):
       for naam in os.listdir(dir):
            pad = os.path.join(dir, naam)
            if os.path.isfile(pad):
                  print pad
            else:
                  lopen(pad)

os.path.join pakt een directory en een bestandsnaam en combineert deze tot een volledig pad.

**Oefening 14.1** Pas lopen zodanig aan dat in plaats van de bestandsnamen af te drukken een lijst met namen wordt teruggegeven.

**Oefening 14.2** De os module levert een functie genaamd walk die lijkt op de functie lopen maar is ruimer toe te passen. Lees de documentatie en gebruik deze functie om de bestandsnamen af te drukken in een gegeven directory en de onderliggende directory's.

## 14.5 Uitzonderingen afvangen

Bij het lezen en schrijven van bestanden kunnen nogal wat zaken misgaan. Probeert u een bestand te openen dat niet bestaat dan krijgt u een IOError:

\>>> vin = open('fout\_bestand')
IOError: \[Errno 2\] No such file or directory: 'fout\_bestand'

Hebt u geen toegangsrechten voor een bestand:

\>>> fout = open('/etc/passwd', 'w')
IOError: \[Errno 13\] Permission denied: '/etc/passwd'

En probeert u een directory te openen om te kunnen lezen, dan krijgt u:

\>>> vin = open('/home')
IOError: \[Errno 21\] Is a directory

Het voorkomen van deze fouten kan met behulp van functies zoals os.path.exists en os.path.isfile, maar dit kost veel tijd en extra code om alle mogelijke gevallen te controleren (als “Error 21” een indicatie is, dan kunnen tenminste 21 zaken fout gaan).

Het is verstandiger om door te gaan en proefondervindelijk de problemen aan te pakken als deze zich voordoen. En dat is nu precies wat de try instructie doet. De zinsbouw komt overeen met een if instructie:

try:
       vin = open('fout\_bestand')
       for regel in vin:
            print regel 
       vin.close()
except:
       print 'Iets ging fout.'

Python begint met het uitvoeren van de try clausule. Gaat alles goed dan wordt de except clausule overgeslagen en gaat het proces verder. Treedt een uitzondering op dan wordt de try clausule verlaten en en de except clausule uitgevoerd.

Het afhandelen van een uitzondering met een try instructie wordt het **afvangen** van een uitzondering genoemd. In dit voorbeeld drukt de except clausule een foutboodschap af die niet erg betekenisvol is. Over het algemeen geeft het afvangen van uitzonderingen u de mogelijkheid het probleem op te lossen, of opnieuw te proberen en op z'n minst het programma netjes te stoppen.

## 14.6 Databases

Een **database** is een bestand dat ingericht is voor het opslaan van gegevens. De meeste databases zijn net zo ingericht als een woordenboek in die zin dat ze sleutels aan waarden koppelen. Het grootste verschil is dat de database op schijf staat (of een ander opslag medium), dus blijft bestaan nadat het programma stopt.

De module anydbm levert een interface voor het aanmaken en bijhouden van database bestanden. Hierbij een voorbeeld waarbij een database wordt aangemaakt die onderschriften bevat voor bestanden met afbeeldingen.

Een database openen gaat op dezelfde manier als het openen van andere bestanden:

\>>> import anydbm
\>>> db = anydbm.open('onderschrift.db', 'c')

De modus 'c' betekent dat de database moet worden aangemaakt als deze nog niet bestaat. Het resultaat is een databaseobject dat gebruikt kan worden (voor de meeste bewerkingen) zoals een woordenboek. Maakt u een nieuw item dan zal anydbm het databasebestand bijwerken.

\>>> db\['mug.png'\] = 'Foto van een mug.'

Benadert u een van de items dan leest anydbm het bestand:

\>>> print db\['mug.png'\]
Foto van een mug.

Maakt u een andere toewijzing naar een bestaande sleutel dan vervangt anydbm de oude waarde:

\>>> db\['mug.png'\] = 'Foto van een mug die prikt.'
\>>> print db\['mug.png'\]
Foto van een mug die prikt.

Veel van de woordenboekmethoden, zoals keys en items, werken ook op databaseobjecten. Dus ook herhaling met behulp van een for instructie.

for sleutel in db:
        print sleutel

Net als met andere bestanden moet u de database sluiten als u klaar bent:

\>>> db.close()

## 14.7 Inmaken?

Een beperking van anydbm is dat de sleutels en waarden strings moeten zijn. Probeert u een ander soort te gebruiken dan krijgt u een foutboodschap.

De pickle module biedt uitkomst. Deze vertaalt zo ongeveer elk soort object naar een string die kan worden opgeslagen in een database en vertaalt vervolgens strings terug naar objecten.

pickle.dumps krijgt een object mee als parameter en geeft een stringrepresentatie terug. (dumps is een afkorting voor “dump string”):

\>>> import pickle
\>>> t = \[1, 2, 3\]
\>>> pickle.dumps(t)
'(lp0\\nI1\\naI2\\naI3\\na.'

Het formaat is niet erg handig te lezen door mensen; het is bedoeld om makkelijk door pickle te kunnen laten interpreteren. pickle.loads (“load string”) reconstrueert het object:

\>>>   t1 = \[1, 2, 3\]
\>>>   s = pickle.dumps(t1)
\>>>   t2 = pickle.loads(s)
\>>>   print t2
\[1, 2, 3\]

Hoewel het nieuwe object dezelfde waarde heeft als het oude object, is het toch in het algemeen niet hetzelfde object:

\>>> t == t2
True
\>>> t is t2
False

Met andere woorden, pickling en daarna unpickling heeft hetzelfde effect als het kopiëren van het object.

U kunt pickle gebruiken voor het opslaan van niet-strings in een database. In feite is deze combinatie zo gewoon dat deze is opgenomen in een module genaamd shelve.

**Oefening 14.3** Hebt u Oefening 12.4 uitgevoerd, wijzig dan uw oplossing zodanig dat deze een database aanmaakt die elk woord in de lijst koppelt aan een lijst met woorden die dezelfde set met letters gebruikt.

Schrijf een ander programma dat een database opent en de inhoud afdrukt in voor mensen leesbaar formaat.

## 14.8 Pijpen

De meeste besturingssystemen leveren een interface met een opdrachtregel, deze wordt ook wel **shell** genoemd. Shells leveren normaal gesproken opdrachten om door het bestandssysteem te navigeren en applicaties te starten. Bijvoorbeeld: in Unix kunt u van directory veranderen via cd, de inhoud van een directory laten zien via ls en een web browser starten door firefox te typen.

Elk programma dat u via de shell kunt starten, kan ook via Python gestart worden met behulp van een **pijp (pipe)**. Een pijp is een object dat een lopend proces vertegenwoordigt.

Bijvoorbeeld: de Unix opdracht ls -l geeft normaal de inhoud van de huidige directory weer (in uitgebreide vorm). U kunt dit starten met os.popen:

\>>> opdracht = 'ls -l'
\>>> ba = os.popen(opdracht)

Het argument is een string die een shellopdracht bevat. De antwoordwaarde is een bestandsaanwijzer die zich net zo gedraagt als een geopend bestand. U kunt de uitvoer van ls regel voor regel lezen met readline of het geheel in één keer met read:

\>>> resultaat = ba.read()

Bent u klaar dan sluit u de pijp net als een bestand:

\>>> status = ba.close()
\>>> print status
None

De antwoordwaarde is de eindstatus van het ls proces, None betekent dat dit normaal is geëindigd zonder fouten.

Een gebruikelijke manier om pijpen te gebruiken, is voor het incrementeel lezen van gecomprimeerde bestanden, dat wil zeggen zonder decompressie het hele bestand in één keer. De volgende functie krijgt de naam van een gecomprimeerd bestand als parameter mee, en geeft een pijp terug die gunzip gebruikt om de inhoud te decomprimeren:

def open\_gunzip(bestandsnaam):
      opdracht = 'gunzip -c ' + bestandsnaam
      ba = os.popen(opdracht)
      return ba

Leest u de regels uit ba één voor één dan hoeft u het gedecomprimeerde bestand nooit in het geheugen of op schijf op te slaan.

## 14.9 Modules schrijven

Elk bestand dat Python code bevat, kan geïmporteerd worden als een module. Bijvoorbeeld: stel dat u een bestand hebt, genaamd wt.py met de volgende:

def regelteller(bestandsnaam):
      teller = 0
      for regel in open(bestandsnaam):
           teller += 1
      return teller
print regelteller('wt.py')

Als u dit programma uitvoert, dan leest dit zichzelf in en drukt het het aantal regels van dit bestand af, dit is 7. U kunt het ook als volgt importeren:

\>>> import wt
7

Nu hebt u een moduleobject wt:

\>>> print wt
<module 'wt' from 'wt.py'>

Deze levert een functie genaamd regelteller:

\>>> wt.regelteller('wt.py')
7

Dus dat is de manier om modules te schrijven in Python.

Het enige probleem met dit voorbeeld is dat als u de module importeert, dit als eerste de testcode aan het einde uitvoert. Het is gebruikelijk dat als u een module importeert, dat dit wel gedefinieerd, maar niet uitgevoerd wordt.

Programma's die geïmporteerd moeten worden, gebruiken vaak het volgende jargon:

if \_\_name\_\_ == '\_\_main\_\_':
      print regelteller('wt.py')

\_\_name\_\_ is een ingebouwde variabele die wordt gezet zodra het programma start. Draait het programma als een script, dan heeft \_\_name\_\_ de waarde \_\_name\_\_; in dat geval wordt de testcode uitgevoerd. Anders, als de module wordt geïmporteerd, wordt de testcode overgeslagen.

**Oefening 14.4** Typ dit voorbeeld over in een bestand genaamd wt.py en voer deze uit als een script. Start daarna de Python interpreter en importeer wt. Wat is de waarde van \_\_name\_\_ als de module is geïmporteerd?

Waarschuwing: Importeert u een module die al een keer is geïmporteerd dan doet Python niets. Het bestand wordt ook niet opnieuw ingelezen, zelfs niet als dit gewijzigd is.

Wilt u een module opnieuw laden dan kunt u gebruikmaken van de ingebouwde functie reload. Maar dit kan lastig zijn, dus de veiligste optie is om de interpreter opnieuw te starten en de module opnieuw te importeren.

## 14.10 Debuggen

Bij het lezen en schrijven van bestanden kunt u in de problemen komen met witregels. Deze fouten zijn moeilijk op te sporen omdat spaties, tabstops en regeleinden normaal gesproken onzichtbaar zijn:

\>>> s = '1 2\\t 3\\n 4'
\>>> print s
1 2 3
  4

De ingebouwde functie repr kan helpen. Deze krijgt een willekeurig object als een argument en geeft een string terug die het object weergeeft. Voor strings laat het onzichtbare karakters voorafgaan door een backslash:

\>>> print repr(s)
'1 2\\t 3\\n 4'

Dit is handig bij het debuggen.

Een ander probleem waar u tegen aan kunt lopen, is dat verschillende systemen andere karakters gebruiken voor de markering van het einde van een regel. Sommige systemen gebruiken een "nieuwe regel" weergegeven door een \\n. Andere gebruiken het karakter "terug" weergegeven door een \\r. Weer andere gebruiken beide. Verplaatst u bestanden tussen verschillende systemen dan kunnen deze inconsequenties problemen veroorzaken.

Voor de meeste systemen bestaan applicaties die van het ene naar het andere formaat kunnen converteren. U kunt deze vinden en daarover meer lezen op [wikipedia.org/wiki/Newline](https://wiki.ubuntu-nl.org/wikipedia.org/wiki/Newline). Of u kunt er zelf één schrijven.

## 14.11 Woordenlijst

**persistent**: Maakt deel uit van een programma dat voor onbepaalde tijd draait en op z'n minst iets van zijn gegevens in een permanente opslag bewaart.

**formatteeroperator**: Een operator, %, die een formaatstring en een tupel meekrijgt en een string maakt waarbij de elementen uit de tupel geformatteerd zijn overeenkomstig het formaat string.

**formaatstring**: Een string, gebruikt door de formatteeroperator, die formatteerreeksen bevat.

**formatteerreeks**: Een reeks van karakters in een formaatstring, zoals %d, die aangeeft hoe een waarde geformatteerd moet worden.

**tekstbestand**: Een reeks karakters opgeslagen op een permanente opslag zoals een harde schijf.

**directory**: Een verzameling van bestanden voorzien van een naam, ook wel een map genoemd.

**pad**: Een string die een bestand identificeert.

**relatief pad**: Een pad dat begint vanaf de huidige directory.

**absolute pad**: Een pad dat begint vanaf de hoogste directory in een bestandssysteem.

**afvangen**: voorkomt dat een uitzondering het programma vroegtijdig beëindigt; hier wordt gebruik gemaakt van de try en except instructies.

**database**: Een bestand waarvan de inhoud is georganiseerd als een woordenboek met sleutels die overeenkomen met waarden.

## 14.12 Oefeningen

**Oefening 14.5** De urllib module levert methoden voor het aanpassen van URL's en het downloaden van het web. Het volgende voorbeeld downloadt een geheim bericht thinkpython.com en drukt dit af:

import urllib
connectie = urllib.urlopen('http://thinkpython.com/secret.html')
for regel in connectie.fp:
     print regel.strip()

Voer deze code uit en volg de instructies die u daarin ziet.

**Oefening 14.6** In een grote verzameling van MP3 bestanden kan het gebeuren dat meerdere kopieën van hetzelfde liedje voorkomen, in verschillende directory's of onder een ander bestandsnaam. Het doel van deze oefening is het zoeken naar deze duplicaten.

1.  Schrijf een programma die een directory en al zijn onderliggende directory's herhaaldelijk doorzoekt en een lijst teruggeeft met de complete paden voor alle bestanden met een gegeven achtervoegsel (zoals .mp3). Tip: os.path levert verschillende handige functies voor het bewerken van bestanden en namen van paden.
    
2.  Voor het herkennen van duplicaten kunt u hashfuncties gebruiken die een bestand lezen en een korte samenvatting maken van de inhoud. Bijvoorbeeld: MD5 (Message-Digest algoritme 5) kan een bericht van willekeurige lengte oppakken en een 128-bit "controlegetal" teruggeven. De kans is onwaarschijnlijk klein dat twee bestanden, met een verschillende inhoud, hetzelfde controlegetal teruggeven. U kunt meer lezen over MD5 bij [wikipedia.org/wiki/Md5](https://wiki.ubuntu-nl.org/wikipedia.org/wiki/Md5). Op een Unix systeem kunt u het programma md5sum gebruiken en een pijp om de controlegetallen vanuit Python te berekenen.
    

**Oefening 14.7** De Internet Speelfilm Database (IMDb) is een online verzameling van informatie over speelfilms. Deze database is beschikbaar in tekstformaat, dus is deze redelijk eenvoudig in te lezen door Python.

Voor deze Oefening hebt u de volgende bestanden nodig: actors.list.gz en actresses.list.gz, u kunt deze downloaden bij [www.imdb.com/interfaces#plain](https://wiki.ubuntu-nl.org/www.imdb.com/interfaces#plain).

Ik heb een programma geschreven die deze bestanden ontleedt en ze opsplitst in namen van acteurs, titels van speelflims, enz. U kunt dit downloaden bij [thinkpython.com/code/imdb.py](https://wiki.ubuntu-nl.org/thinkpython.com/code/imdb.py).

Voert u imdb.py uit als een script, dan wordt actors.list.gz gelezen en wordt één acteur-speelfilm combinatie per regel afgedrukt. Of, als u import imdb downloadt, dan kunt u de functie process\_file ook gebruiken om het bestand te verwerken. De argumenten zijn een bestandsnaam, een functieobject en, optioneel, het aantal te verwerken regels. Hierbij een voorbeeld:

import imdb
def print\_info(actor, date, title, role):
      print actor, date, title, role
imdb.process\_file('actors.list.gz', print\_info)

Zodra u process\_file aanroept, opent deze bestandsnaam, leest de inhoud en roept print\_info eenmaal aan voor iedere regel in het bestand. print\_info krijgt een acteur, datum, speelfilmtitel en rol als argumenten mee en drukt deze af.

1.  Schrijf een programma dat actors.list.gz en actresses.list.gz leest en die "shelve" gebruikt om een database te bouwen die elke acteur koppelt aan zijn of haar films.
    
2.  Twee acteurs zijn "medeacteur" als ze minstens in één speelfilm samen hebben geacteerd. Verwerk de database uit de voorgaande stap en bouw een tweede database die elke acteur koppelt aan een lijst met zijn of haar medeacteurs.
3.  Schrijf een programma die de "Six Degrees of Kevin Bacon" kan afspelen; hierover kunt u meer lezen bij [wikipedia.org/wiki/Six\_Degrees\_of\_Kevin\_Bacon](https://wiki.ubuntu-nl.org/wikipedia.org/wiki/Six_Degrees_of_Kevin_Bacon). Deze oefening is een uitdaging omdat het programma vereist dat het kortste pad in een grafiek moet worden gevonden. Meer over "het kortste pad" algoritmes bij [wikipedia.org/wiki/Shortest\_path\_problem](https://wiki.ubuntu-nl.org/wikipedia.org/wiki/Shortest_path_problem).