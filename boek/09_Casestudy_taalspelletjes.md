[community/ThinkPython/HoofdstukNegen - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegen)

> # Hoofdstuk 9 Casestudy: taalspelletjes
> 
> ## 9.1 Woordenlijsten lezen
> 
> Voor de oefeningen in dit hoofdstuk hebben we een lijst met Nederlandse woorden nodig. Op het internet zijn veel woordenlijsten beschikbaar en een vrij te gebruiken woordenlijst is die van de NTG Werkgroep Spelling1. Deze lijst bevat bijna 223.000 woorden waaronder die uit het groene boekje. Deze woordenlijst mag door iedereen gebruikt worden, binnen de voorwaarden die in de licentie (de [GNU Lesser General Public License](http://www.gnu.org/copyleft/lesser.html)) zijn vastgelegd. De bestandsnaam is: woorden.max; zie ... voor een kopie van de lijst.
> 
> Dit bestand is een tekstbestand en is dus te openen met een willekeurige tekstverwerker maar ook leesbaar voor Python. De ingebouwde functie open krijgt de naam van een bestand mee als parameter en geeft een **bestandsobject** terug, die te gebruiken is om het bestand te lezen.
> 
> \>>> fin = open('woorden.max')
> \>>> print fin
> <open file 'woorden.max', mode 'r' at 0xb7f4b380>
> 
> fin is een algemene naam voor een bestandsobject dat gebruikt wordt bij invoer. Mode 'r' geeft aan dat dit bestand wordt geopend om het te lezen (in tegenstelling tot 'w' voor wegschrijven).
> 
> Het bestandsobject levert verschillende manieren voor het lezen, waaronder readline; deze leest de karakters uit een bestand totdat het een nieuwe regel tegenkomt en geeft het resultaat terug als een string:
> 
> \>>> fin.readline()
> 'A4\\r\\n'
> 
> Het eerste woord in deze specifieke lijst is "A4". Dit is de maat van een stuk papier. De reeks \\r\\n vertegenwoordigt twee whitespace karakters, een regel omhaal en een nieuwe regel, die dit woord afscheiden van het volgende woord.
> 
> Het bestandsobject houdt bij op welke plaats het zich in het bestand bevindt, dus als u readline opnieuw aanroept krijgt u het volgende woord:
> 
> \>>> fin.readline()
> 'Aagje\\r\\n'
> 
> Het volgende woord is "Aagje", ook weer met (whitespace) karakters; daar kunnen we vanaf komen met de string methode "strip":
> 
> \>>> line = fin.readline()
> \>>> woord = line.strip()
> \>>> print woord
> aahed
> 
> U kunt ook het bestandsobject als onderdeel van een for lus gebruiken. Dit programma leest woorden.max en print elk woord op een nieuwe regel:
> 
> fin = open('woorden.max')
> for line in fin:
>        woord = line.strip()
>        print woord
> 
> **Oefening 9.1:** Schrijf een programma dat woorden.max leest en alleen die woorden afdrukt die meer dan 20 karakters bevatten (uitgezonderd de spaties).
> 
> ## 9.2 Oefeningen
> 
> In de volgende paragraaf staan oplossingen voor deze oefeningen. Probeer eerst zelf met een oplossing te komen voordat u naar onderstaande oplossingen kijkt.
> 
> **Oefening 9.2:** In 1939 publiceerde Ernest Vincent Wright een novelle van 50,000 woorden genaamd _Gadsby_. Deze novelle bevat niet de letter "e". Wetende dat de "e" de meest voorkomende letter is in het Engels, is dat niet gemakkelijk. In feite is het moeilijk om één enkele gedachte te formuleren zonder dit meest gebruikte symbool. Dit gaat langzaam van start maar voorzichtig aan lukt dit; door training wordt u daar handig in.
> 
> Dit soort teksten wordt een lipogram genoemd.
> 
> Schrijf een functie genaamd heeft\_geen\_e die de waarde True teruggeeft als een gegeven woord geen "e" bevat.
> 
> Wijzig het programma uit de vorige paragraaf om alleen die woorden te printen die geen "e" bevatten en bereken het percentage van de woorden die geen "e" bevatten in de lijst.
> 
> **Oefening 9.3:** Schrijf een functie genaamd vermijdt die een woord en een lijst met verboden letters krijgt en vervolgens True teruggeeft als het woord geen van de verboden letters bevat.
> 
> Wijzig het programma zodanig dat het aan de gebruiker vraagt om een serie verboden letters en print het aantal van de woorden die geen enkele van de verboden letters bevat. Kunt u een combinatie van 5 verboden letters vinden die het minste aantal woorden terug geeft?
> 
> **Oefening 9.4:** Schrijf een functie genaamd gebruik\_alleen die een woord en een lijst met letters krijgt en vervolgens True teruggeeft als het woord alleen de letters uit de lijst bevat. Kunt u een zin maken waarin alleen de letters acefhlo worden gebruikt? Anders dan “Hoe alfalfa?”
> 
> **Oefening 9.5:** Schrijf een functie genaamd gebruik\_alles die een woord en een lijst met verplichte letters krijgt en vervolgens True teruggeeft als het woord alle verplichte letters tenminste één keer bevat. Hoeveel woorden bevatten de klinkers aeiou? Hoe zit dat met aeiouy?
> 
> **Oefening 9.6:** Schrijf een functie genaamd is\_alfabetisch die True teruggeeft als de letters in een woord op alfabetische volgorde staan (dubbele letters zijn toegestaan). Hoeveel alfabetische woorden bestaan in het Nederlands?
> 
> ## 9.3 Zoek
> 
> Alle oefeningen in de voorgaande paragraaf hebben iets gemeenschappelijk: ze kunnen opgelost worden met het zoekpatroon uit paragraaf 8.6. Het eenvoudigste voorbeeld is:
> 
> def heeft\_geen\_e(woord):
>     for letter in woord:
>         if letter == 'e':
>             return False
>     return True
> 
> De for lus doorloopt de karakters in woord. Vinden we de letter "e" dan geven we direct een False terug, zo niet, gaan we naar de volgende letter. Komen we de lus normaal door, dat betekent dat we geen "e" hebben gevonden, dus geven we True terug.
> 
> Deze functie is beknopter te schrijven door gebruik te maken van de in operator maar door te starten met deze versie wordt de logica van het zoekpatroon aangetoond.
> 
> Vermijden is de meer generieke versie van heeft\_geen\_e maar heeft dezelfde structuur:
> 
> def vermijden(woord, verboden):
>     for letter in woord:
>         if letter in verboden:
>             return False
>     return True
> 
> We kunnen False teruggeven zodra we een verboden letter vinden; komen we bij het einde van de lus dan geven we True terug.
> 
> gebruik\_alleen is vergelijkbaar behalve dat de betekenis van de conditie is omgedraaid:
> 
> def gebruik\_alleen(woord, beschikbaar):
>     for letter in woord:
>         if letter not in beschikbaar:
>             return False
>     return True
> 
> In plaats van een lijst met verboden letters hebben we een lijst met beschikbare letters. Zodra we een letter in een woord vinden, die beschikbaar is, geven we False terug.
> 
> gebruik\_alles is vergelijkbaar behalve dat we de rol van het woord en de reeks met letters omdraaien:
> 
> def gebruik\_alles(woord, verplicht):
>     for letter in verplicht:
>         if letter not in woord:
>             return False
>     return True
> 
> In plaats van de letter door woord te laten lopen, doorloopt de lus de verplichte letters. Zodra één van de verplichte letters niet in het woord voorkomen geven we False terug. Als u echt denkt zoals een computerwetenschapper, dan zou u gebruik\_alles hebben herkend als een vorm van een eerder opgelost probleem en zou u het volgende hebben geschreven:
> 
> def gebruik\_alles(woord, verplicht):
>     return gebruik\_alleen(verplicht, woord)
> 
> Dit is een voorbeeld van een programma-ontwikkel-methode genaamd **probleemherkenning**. Dit houdt in dat u een probleem, waaraan u werkt, herkent als iets wat u eerder hebt opgelost en past de eerder ontwikkelde oplossing toe.
> 
> ## 9.4 Lussen met indices
> 
> De functies uit de voorgaande paragraaf zijn met een for lus geschreven, omdat alleen de karakters uit de reeks gebruikt worden. Voor is\_alfabetisch moeten we aanliggende letters vergelijken; dat is een beetje lastig met een for lus:
> 
> def is\_alfabetisch (woord):
>     vorige = woord\[0\]
>     for c in woord:
>         if c < vorige:
>             return False
>         vorige = c
>     return True
> 
> Een alternatief is om "terugkeer" te gebruiken:
> 
> def is\_alfabetisch (woord):
>     if len(woord) <= 1:
>         return True
>     if woord\[0\] > woord\[1\]:
>         return False
>     return is\_alfabetisch (woord\[1:\])
> 
> Een andere optie is om de while lus te gebruiken:
> 
> def is\_alfabetisch (woord):
>     i = 0
>     while i < len(woord)-1:
>         if woord\[i+1\] < woord\[i\]:
>             return False
>         i = i+1
>     return True
> 
> De lus begint met i=0 en eindigt zodra i=len(woord)-1. Iedere passage door de lus wordt het 'i'ste karakter (denk aan het huidige karakter) vergeleken met de "i"+1-ste karakter (denk aan het volgende karakter).
> 
> Zodra het volgende karakter kleiner is (alfabetisch voor) dan het huidige karakter hebben we een breuk in de alfabetische lijn ontdekt en geven we False terug.
> 
> Komen we aan het einde van de lus zonder een False melding dan is het woord voor de test geslaagd. Om uzelf te overtuigen dat de lus correct eindigt, overweeg een voorbeeld zoals 'flossy'. De lengte van het woord is 6, dus de laatste keer dat de lus doorlopen wordt is als i de waarde 4 heeft; dit is de index van het op één na laatste karakter. Bij de laatste passage wordt het op één na laatste karakter vergeleken met het laatste en dat is wat we willen.
> 
> Hierbij een versie van is\_palindroom (zie oefening 6.6); deze gebruikt twee indices, een start aan het begin loopt op en de andere start aan het einde loopt af.
> 
> def is\_palindroom(woord):
>     i = 0
>     j = len(woord)-1
>     while i<j:
>         if woord\[i\] != woord\[j\]:
>             return False
>         i = i+1
>         j = j-1
>     return True
> 
> Of, als u hebt opgemerkt dat dit een vorm is van een eerder opgelost probleem, zou u het als volgt hebben geschreven:
> 
> def is\_palindroom(woord):
> return is\_omgekeerd(woord, woord)
> 
> Vooropgesteld dat u oefening 8.8 hebt uitgevoerd.
> 
> ## 9.5 Debuggen
> 
> Programma's testen is moeizaam. De functies in dit hoofdstuk zijn relatief gemakkelijk te testen omdat u de uitkomst meteen kunt controleren. Zo is het ergens tussen moeilijk en onmogelijk om een verzameling woorden te kiezen die op alle mogelijke fouten test.
> 
> Neem heeft\_geen\_e als voorbeeld; we kunnen twee voor de hand liggende gevallen controleren: woorden met een 'e' moeten False teruggeven en woorden zonder moeten True teruggeven. Het is niet moeilijk om met een voorbeeld van elk te komen.
> 
> Binnen elk geval zijn een aantal minder voor de hand liggende gevallen. Onder de woorden met een "e" moet u woorden testen met een "e" aan het begin, aan het einde en ergens in het midden. U moet lange en korte en heel korte woorden, zoals een lege string, testen. De lege string is een voorbeeld van een **speciaal geval**; dit is één van de niet voor de hand liggende gevallen waarbij een fout op de loer ligt.
> 
> In aanvulling op de gemaakte testgevallen, kunt u het programma ook testen met een woordenlijst zoals woorden.tct. Bij het doorlopen van de uitvoer kunt u een fout opmerken maar let op: u kunt een soort fout opmerken (woorden die niet behoren voor te komen en dat wel doen) en niet de andere (woorden die moeten voorkomen en dat niet doen).
> 
> In het algemeen kan testen helpen bij het vinden van bugs maar het is niet gemakkelijk om een goede set met testgevallen te maken en stel dat dit wel lukt, dan bent u er toch nooit zeker van dat uw programma correct werkt.
> 
> Aldus volgens een legendarische computerwetenschapper:
> 
> Programma's testen kan worden gebruikt om het optreden van fouten aan te tonen maar het kan nooit de afwezigheid aantonen! — Edsger W. Dijkstra
> 
> ## 9.6 Woordenlijst
> 
> **bestandsobject:** Een waarde die een open bestand vertegenwoordigt.
> 
> **probleemherkenning:** Een manier van oplossen van een probleem door dit uit te drukken als een vorm of voorbeeld van een eerder opgelost probleem.
> 
> **speciaal geval:** Een testgeval dat afwijkend of niet voor de hand liggend is (en waarschijnlijk niet correct wordt afgehandeld).
> 
> ## 9.7 Oefeningen
> 
> **Oefening 9.7** Deze vraag is gebaseerd op een raadsel genoemd tijdens een uitzending van het radioprogramma Car Talk2:
> 
> Geef een woord met drie opeenvolgende dubbele letters. Hierbij een aantal woorden die daar bijna aan voldoen maar net niet. Bijvoorbeeld: het woord committee, c-o-m-m-i-t-t-e-e. Het is fraai behalve dat de "i" ertussen staat. Of Mississippi: M-i-s-s-i-s-s-ip-p-i. Als u de "i"'s ertussenuit kunt halen werkt het. Maar er bestaat een woord dat drie achtereenvolgende paren van letters heeft en volgens mijn beste weten is dit het enige woord. Waarschijnlijk bestaan er 500 andere maar ik kan er maar één bedenken. Welk woord is dat?
> 
> Schrijf een programma om dit woord te vinden. De oplossing is te vinden op [thinkpython.com/code/cartalk.py](http://www.thinkpython.com/code/cartalk.py).
> 
> **Oefening 9.8** Hierbij een ander _Car Talk_ raadsel3:
> 
> Ik reed een keer op de snelweg en lette op de kilometerteller. Zoals de meeste kilometertellers heeft deze 6 cijfers met alleen de hele kilometers. Dus als mijn auto, bijvoorbeeld, op 300.000 kilometer staat, zie ik 3-0-0-0-0-0.
> 
> Wat ik die dag zag was interessant. Ik merkte op dat de laatste 4 cijfers een palindroom waren, dat wil zeggen hetzelfde van voor naar achter als omgekeerd. Bijvoorbeeld 5-4-4-5 is een palindroom dus mijn kilometerteller staat, laten we zeggen op 3-1-5-4-4-5.
> 
> Eén kilometer later zijn de laatste 5 cijfers een palindroom. Bijvoorbeeld: het zou 3-6-5-4-5-6 kunnen zijn. Eén kilometer hierna zijn de middelste 4 cijfers van de 6 een palindroom. En na nog één kilometer zijn alle 6 de cijfers een palindroom! “De vraag is: wat was de stand van de kilometerteller op het moment dat ik de eerste keer keek?"
> 
> Schrijf een Python programma die alle 6 cijferige nummers test en print alle nummers die aan deze eisen voldoen. De oplossing is te vinden op [thinkpython.com/code/cartalk.py](http://www.thinkpython.com/code/cartalk.py).
> 
> **Oefening 9.9** Hierbij nog een Car Talk raadsel dat op te lossen is met zoeken4:
> 
> Kort geleden bracht ik een bezoek aan mijn moeder en toen realiseerden we ons dat de twee cijfers die mijn leeftijd vormen, omgedraaid haar leeftijd vormen. Bijvoorbeeld: als zij 73 is, ben ik 37. We vroegen ons af hoe vaak dit de afgelopen jaren is voorgekomen maar we werden afgeleid door andere zaken en hebben nooit het antwoord berekend.
> 
> Thuis gekomen berekende ik dat cijfers van onze leeftijden tot nu toe zes keer hebben kunnen verwisselen. Ik berekende ook dat als we geluk hebben het nog eens zal voorkomen in de toekomst over een paar jaar en als we veel geluk hebben het zelfs nog een keer zal voorkomen, dus acht keer in totaal. "Dus de vraag is: hoe oud ben ik nu?"
> 
> Schrijf een Python programma dat zoekt naar de oplossingen voor dit raadsel. Tip: De string methode zfill kan handig zijn.
> 
> Bekijk de oplossing op [thinkpython.com/code/cartalk.py](http://www.thinkpython.com/code/cartalk.py).
> 
> * * *
> 
> 1 [www.ntg.nl/spelling/](http://www.ntg.nl/spelling/)  
> 2 [www.cartalk.com/content/puzzler/transcripts/200725](http://www.cartalk.com/content/puzzler/transcripts/200725)  
> 3 [www.cartalk.com/content/puzzler/transcripts/200725](http://www.cartalk.com/content/puzzler/transcripts/200803)  
> 4 [www.cartalk.com/content/puzzler/transcripts/200725](http://www.cartalk.com/content/puzzler/transcripts/200813)