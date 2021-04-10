[community/ThinkPython/HoofdstukDertien - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukDertien)

> # Hoofdstuk 13 Casestudy: gegevensstructuur selectie
> 
> ## 13.1 Woord frequentie analyse
> 
> Zoals gebruikelijk behoort u eerst op z'n minst een poging te wagen om onderstaande oefeningen op te lossen, voordat u mijn oplossingen raadpleegt.
> 
> **Oefening 13.1** Schrijf een programma dat een bestaand boek leest, vervolgens elke regel in losse woorden omzet, daarna de spaties en leestekens verwijdert en tenslotte alles omzet naar kleine letters. Tip: De string module levert strings genaamd whitespace, die bevat een spatie, tab, nieuwe regel, enz., en punctuation die de leestekens bevat. Eens zien of we Python kunnen laten zweten:
> 
> \>>> import string
> \>>> print string.punctuation
> !"#$%&'()\*+,-./:;<=>?@\[\\\]ˆ\_\`{|} ̃
> 
> U kunt ook de string methodes strip, replace entranslate proberen.
> 
> **Oefening 13.2** Ga naar het project Gutenberg ([http://gutenberg.net](http://gutenberg.net)) en download uw favoriete boek zonder copyright in platte tekst formaat.
> 
> Pas uw programma uit de vorige oefening aan, zodanig dat deze het gedownloade boek inleest, de titelinformatie in het begin overslaat en de rest van de woorden verwerkt zoals hiervoor beschreven. Pas het programma verder aan zodat het totaal aantal woorden in het boek wordt geteld en het aantal keren dat het woord wordt gebruikt.
> 
> Print het aantal verschillende woorden dat in het boek wordt gebruikt. Vergelijk verschillende boeken van verschillende auteurs en verschillende gebieden. Welke auteurs gebruiken een uitgebreide vocabulaire?
> 
> **Oefening 13.3** Pas het programma uit de vorige oefening aan om de 20 meest gebruikte woorden in een boek te printen.
> 
> **Oefening 13.4** Pas het vorige programma aan om een woordenlijst in te lezen (zie paragraaf 9.1) en print dan alle woorden uit het boek die niet in de woordenlijst voorkomen. Hoeveel van deze woorden zijn tikfouten? Hoeveel zijn gebruikelijke woorden die in een woordenlijst thuis horen en hoeveel zijn werkelijk vreemde woorden?
> 
> ## 13.2 willekeurige getallen
> 
> Geeft u een computerprogramma steeds dezelfde invoer dan produceert dit iedere keer dezelfde uitvoer, dus computerprogramma's zijn **voorspelbaar**. Voorspelbaarheid is normaal gesproken een goede zaak, omdat we verwachten dat eenzelfde berekening altijd hetzelfde resultaat oplevert. Niettemin, voor bepaalde applicaties willen we dat de computer onvoorspelbaar is.
> 
> Spelletjes zijn een voor de hand liggend voorbeeld, maar er zijn er meer.
> 
> Een programma volledig onvoorspelbaar maken blijkt niet zo gemakkelijk te zijn maar er bestaan manieren om ze onvoorspelbaar te laten lijken. Eén van deze manieren is het gebruik van algoritmes die zogenaamd willekeurige (random) getallen aanmaken. Zogenaamd willekeurige getallen zijn niet echt willekeurig, omdat ze aangemaakt worden met een voorspelbare berekening, maar door gewoon naar de getallen te kijken is het zo goed als onmogelijk om ze te onderscheiden van echte willekeurige getallen.
> 
> De random module levert functies die **zogenaamd willekeurige** getallen aanmaken (we zullen ze gewoon "willekeurig" (random) noemen.)
> 
> De functie random geeft een willekeurig getal tussen de 0,0 en 1,0 terug (inclusief 0,0 maar zonder 1,0). Iedere keer als u random aanroept krijgt u het volgende nummer uit een lange reeks. Draai deze lus en u ziet een tiental getallen:
> 
> import random
> for i in range(10):
>       x = random.random()
>       print x
> 
> De functie randint krijgt de parameters low en high mee en geeft een geheel getal terug tussen low en high (inclusief beide).
> 
> \>>> random.randint(5, 10)
> 5
> \>>> random.randint(5, 10)
> 9
> 
> Voor het willekeurig kiezen van een element uit een reeks kunt u choice gebruiken:
> 
> \>>> t = \[1, 2, 3\]
> \>>> random.choice(t)
> 2
> \>>> random.choice(t)
> 3
> 
> De random module levert ook functies voor het genereren van willekeurige waarden uit doorlopende verdelingen inclusief Gaussische, exponentiële, gamma en nog enkele.
> 
> Oefening 13.5 Schrijf een functie genaamd kies\_uit\_histogram die een histogram meekrijgt, zoals gedefinieerd in paragraaf 11.1 en een willekeurige waarde uit het histogram teruggeeft; houdt hierbij rekening met de kansberekening in relatie tot de frequentie. Bijvoorbeeld voor dit histogram:
> 
> \>>> t = \['a', 'a', 'b'\]
> \>>> h = histogram(t)
> \>>> print h
> {'a': 2, 'b': 1}
> 
> Uw functie moet ’a’ een 2/3 kans geven en 'b' 1/3 kans.
> 
> ## 13.3 Woord histogram
> 
> Hierbij een programma dat een bestand inleest en een histogram opbouwt met de woorden uit het bestand:
> 
> import string
> def verwerk\_bestand(bestandsnaam):
>      h = wb()
>      fp = open(bestandsnaam)
>      for regel in fp:
>            verwerk\_regel(regel, h)
>      return h
> def verwerk\_regel(regel, h):
>      regel = line.replace('-', ' ')
>      for woord in line.split():
>            woord = word.strip(string.punctuation + string.whitespace)
>            woord = word.lower()
>            h\[woord\] = h.get(woord, 0) + 1
> hist = verwerk\_bestand('emma.txt')
> 
> Dit programma leest emma.txt, die de tekst van _Emma_ door Jane Austen bevat.
> 
> verwerk\_bestand doorloopt de regels van het bestand en geeft deze één voor één door aan verwerk\_regel. Het histogram h wordt gebruikt als een soort verzamelaar.
> 
> verwerk\_regel gebruikt de string methode replace om de afbreekstreepjes te vervangen door spaties voordat split wordt gebruikt om de regel op te delen in een lijst met strings. Het doorloopt de lijst met woorden en gebruikt strip en lower om de interpunctie te verwijderen en de hoofdletters naar kleine letters om te zetten. (Het is kort door de bocht om te zeggen dat strings worden "omgezet", denk eraan dat strings onveranderbaar zijn dus methoden zoals strip en lower zullen nieuwe strings teruggeven.)
> 
> Uiteindelijk werkt verwerk\_regel het histogram bij door een nieuw item aan te maken of een bestaand item op te hogen.
> 
> Om het totaal aantal woorden in het bestand te tellen kunnen we alle frequenties uit het histogram bij elkaar optellen :
> 
> def totaal\_woorden(h):
>      return sum(h.values())
> 
> Het aantal verschillende woorden is gewoon het aantal items in het woordenboek:
> 
> def verschillende\_woorden(h):
>      return len(h)
> 
> Hierbij een deel van de code om de resultaten te printen:
> 
> print 'Totaal aantal woorden:', totaal\_woorden(hist)
> print 'Aantal verschillende woorden:', verschillende\_woorden(hist)
> 
> En de resultaten:
> 
> Totaal aantal woorden: 161073
> Aantal verschillende woorden: 7212
> 
> ## 13.4 Meest voorkomende woorden
> 
> Voor het vinden van de meest voorkomende woorden kunnen we het DSU patroon toepassen; meest\_voorkomende krijgt een histogram mee en geeft een lijst met woordfrequentie tupels terug, gesorteerd in omgekeerde volgorde qua frequentie:
> 
> def meest\_voorkomende(h):
>      t = \[\]
>      for sleutel, waarde in h.items():
>            t.append((waarde, sleutel))
>      t.sort(reverse=True)
>      return t
> 
> Hierbij een lus die de meest voorkomende woorden print:
> 
> t = meest\_voorkomende(hist)
> print 'De meest voorkomende woorden zijn:'
> for freq, woord in t\[0:10\]:
>      print woord, '\\t', freq
> 
> En hierbij de resultaten uit _Emma_:
> 
> De meest voorkomende woorden zijn:
> to         5242
> the        5204
> and        4897
> of         4293
> i          3191
> a          3130
> it         2529
> her        2483
> was        2400
> she        2364
> 
> ## 13.5 Optionele parameters
> 
> We hebben de ingebouwde functies en methoden gezien, die een variabel aantal argumenten meekrijgen. Het is ook mogelijk om een zelfgebouwde functie te schrijven met optionele argumenten. Bijvoorbeeld: dit is een functie die de meest voorkomende woorden in een histogram print:
> 
> def print\_meest\_voorkomende(hist, num=10)
>      t = meest\_voorkomende(hist)
>      print 'De meest voorkomende woorden zijn:'
>      for freq, woord in t\[0:num\]:
>            print woord, '\\t', freq
> 
> De eerste parameter is verplicht, de tweede optioneel. De **standaardwaarde** van num is 10.
> 
> Geeft u maar één argument mee:
> 
> print\_meest\_voorkomende(hist)
> 
> dan krijgt num de standaardwaarde. Geeft u twee argumenten mee:
> 
> print\_meest\_voorkomende(hist, 20)
> 
> dan krijgt num de waarde van het argument. Met andere woorden het optionele argument **overschrijft** de standaardwaarde.
> 
> Heeft een functie zowel verplichte als optionele parameters, dan moeten alle verplichte parameters als eerste worden opgegeven en daarna de optionele.
> 
> ## 13.6 Woordenboek aftrekken
> 
> Woorden in een boek vinden, die niet in de woordenlijst staan words.txt is een probleem dat u wellicht herkent als het aftrekken van een set; dat wil zeggen, we willen alle woorden vinden uit een set (de woorden uit een boek) die niet voorkomen in een andere set (de woorden uit de lijst).
> 
> aftrekken krijgt de woordenboeken d1 en d2 en geeft een nieuw woordenboek terug die alle sleutels uit d1 bevat die niet voorkomen in d2. Omdat we niet geïnteresseerd zijn in de waarden zetten we deze op Geen.
> 
> def aftrekken(d1, d2):
>       resultaat = wb()
>       for sleutel in d1:
>            if sleutel not in d2:
>                 resultaat\[sleutel\] = None
>       return resultaat
> 
> Voor het vinden van woorden in het boek die niet in words.txt staan, gebruiken we verwerk\_regel om een histogram te maken voor words.txt en af te trekken:
> 
> woorden = verwerk\_regel('words.txt')
> diff = aftrekken(hist, words)
> print "De woorden in het boek die niet in de woordenlijst voorkomen zijn:"
> for woord in diff.keys():
>       print woord,
> 
> Hierbij enkele resultaten uit _Emma_:
> 
> De woorden in het boek die niet in de woordenlijst voorkomen zijn:
>   rencontre jane's blanche woodhouses disingenuousness
> friend's venice apartment ...
> 
> Een aantal van deze woorden zijn namen en bezittingen. Andere, zoals "rencontre" zijn niet meer zo gebruikelijk. Maar een paar zijn toch gebruikelijke woorden die in de woordenlijst thuis horen!
> 
> **Oefening 13.6** Python levert een gegevensstructuur genaamd 'set' die een veel voorkomende set operaties levert. Lees de documentatie op \[docs.python.org/lib/types-set.html|docs.python.org/lib/types-set.html\]\] en schrijf een programma die de set aftrekken gebruikt om de woorden te vinden in het boek die niet in de woordenlijst voorkomen.
> 
> ## 13.7 Willekeurige woorden
> 
> Het meest eenvoudige algoritme om een willekeurig woord uit het histogram te kiezen is het opbouwen van een lijst met meerdere kopieën van elk woord, overeenkomstig de waargenomen frequentie en kies dan uit de lijst:
> 
> def willekeurig\_woord(h):
>       t = \[\]
>       for woord, freq in h.items():
>             t.extend(\[woord\] \* freq)
>       return willekeurige.keuze(t)
> 
> De uitdrukking \[woord\] \* freq bouwt een lijst op met freq kopieën van de string woord. De extend methode komt overeen met append behalve dat het argument een reeks is.
> 
> **Oefening 13.7** Dit algoritme werkt maar is niet erg efficiënt; iedere keer als u een willekeurig woord kiest, wordt de lijst opnieuw opgebouwd; deze is zo groot als het originele boek. Een voor de hand liggende verbetering is deze lijst eenmalig op te bouwen en dan meerdere selecties te maken, maar de lijst blijft nog steeds groot.
> 
> Een alternatief is:
> 
> 1.  Gebruik sleutels om een lijst met woorden uit het boek te verkrijgen.
>     
> 2.  Bouw een lijst op die de cumulatieve som bevat van de woordfrequenties (zie oefening 10.1). Het laatste item uit deze lijst is het totaal aantal woorden uit het boek, _n_.
>     
> 3.  Kies een willekeurig getal van 1 tot n. Gebruikt een bi-sectionele zoekopdracht (zie oefening 10.8) om de index te vinden waarbij het willekeurige getal past in de cumulatieve som.
> 4.  Gebruik de index om het overeenkomstige woord in de woordenlijst te vinden.
> 
> Schrijf een programma die dit algoritme gebruikt om een willekeurig woord uit het boek te kiezen.
> 
> ## 13.8 Markov analyse
> 
> Kiest u willekeurig woorden uit een boek, dan krijgt u een idee van de woordenschat maar u krijgt waarschijnlijk geen complete zin:
> 
> this the small regard harriet which knightley's it most things
> 
> Een serie willekeurige woorden vormt zelden een zin omdat er geen relatie is tussen de opeenvolgende woorden. Bijvoorbeeld: in een echte zin verwacht u een lidwoord zoals "de", gevolgd door een bijvoeglijk naamwoord of een zelfstandig naamwoord maar waarschijnlijk geen werkwoord of een bijwoord.
> 
> Een manier om dit soort verhoudingen te meten is de Markov analyse1; deze karakteriseert voor een gegeven reeks woorden de waarschijnlijkheid van het volgende woord. Bijvoorbeeld het liedje _Eric, the Half a Bee_ begint met:
> 
> -   Half a bee, philosophically,
>     Must, ipso facto, half not be.
>     But half the bee has got to be
>     Vis a vis, its entity. D’you see?
>     But can a bee be said to be
>     Or not to be an entire bee
>     When half the bee is not a bee
>     Due to some ancient injury?
>     
> 
> In deze tekst wordt het zinsdeel "half the" altijd gevolgd door het woord "bee", maar het zinsdeel "the bee" kan gevolgd worden door "has" of "is".
> 
> Het resultaat van de Markov analyse is een koppeling tussen een voorvoegsel (zoals "half the" en "the bee") met alle mogelijke achtervoegsels (zoals "has" en "is").
> 
> Gegeven deze relatie kunt u willekeurige tekst opbouwen door te starten met ieder voorvoegsel en willekeurig een passend achtervoegsel te kiezen. Vervolgens kunt u het einde van een voorvoegsel combineren met een nieuw achtervoegsel en daarmee dus een nieuw voorvoegsel bouwen en het proces herhalen.
> 
> Bijvoorbeeld: u start met het voorvoegsel "Half a"; het volgende woord moet dan "bee" zijn omdat het voorvoegsel maar één keer voorkomt in de tekst. Het volgende voorvoegsel is "a bee" dus het volgende achtervoegsel kan "philosophically", "be" of "due" zijn.
> 
> In dit voorbeeld is de lengte van het voorvoegsel altijd twee maar u kunt een Markov analyse uitvoeren met verschillende lengtes. De lengte van het voorvoegsel wordt de "orde" van de analyse genoemd.
> 
> **Oefening 13.8** Markov analyse:
> 
> 1.  Schrijf een programma dat de tekst uit een bestand leest en voer een Markov analyse uit. Het resultaat moet een woordenboek zijn dat voorvoegsels relateert aan een verzameling mogelijke achtervoegsels. De verzameling mag een lijst, tupel of een woordenboek zijn; u mag zelf een geschikte keuze maken. U kunt uw programma testen met een lengte twee voor voorvoegsels maar het programma moet zo geschreven zijn dat het eenvoudig is om met andere lengtes te werken.
> 2.  Voeg een functie aan het voorgaande programma toe die een willekeurige tekst opbouwt, gebaseerd op de Markov analyse. Hierbij een voorbeeld uit _Emma_ met lengte twee voor voorvoegsels:
>     
>     -   He was very clever, be it sweetness or be angry, ashamed or only amused, at such a stroke.
>         She had never thought of Hannah till you were never meant for me?”
>         ”I cannot make speeches, Emma:” he soon cut it all himself.
>         
>         Voor dit voorbeeld heb ik de interpunctie bij de woorden laten staan. Het resultaat is qua zinsbouw bijna correct maar niet helemaal. Semantisch lijkt het bijna zinvol, maar ook niet helemaal. Wat gebeurt er als u de lengte van het voorvoegsel vergroot? Heeft de willekeurige tekst dan meer betekenis?
> 3.  Werkt uw programma eenmaal dan wilt u wellicht een potpourri maken: bij het analyseren van de tekst uit twee of meer boeken zal de willekeurige tekst een interessante vermenging laten zien van de woordenschat en de uitdrukkingen.
> 
> ## 13.9 Gegevensstructuren
> 
> De Markov analyse gebruiken is leuk maar deze oefening heeft ook nut, namelijk: gegevensstructuur selectie. In uw oplossing voor de voorgaande oefening moesten de volgende keuzes worden gemaakt:
> 
> -   • Hoe de voorvoegsels weer te geven.  
>     • Hoe de verzameling van mogelijke achtervoegsels weer te geven.  
>     • Hoe de relatie tussen elk voorvoegsel en de verzameling van mogelijke achtervoegsels weer te geven.  
>     
> 
> Ok, de laatste is gemakkelijk; de enige soort relatie die we hebben gezien is een woordenboek dus dat is de voor de hand liggende keus.
> 
> Voor de voorvoegsels is de voor de hand liggende optie strings, een lijst van strings of een tupel van strings. Voor de achtervoegsels is één optie een lijst, een andere is een histogram (woordenboek).
> 
> Hoe moet je kiezen? De eerste stap is te denken aan de operaties die u op elk van de gegevensstructuren wilt loslaten. Voor de voorvoegsels moet het mogelijk zijn om woorden te verwijderen aan het begin en toe te voegen aan het einde. Bijvoorbeeld: is het huidige voorvoegsel "Half a" en het volgende woord is "bee" dan moet het mogelijk zijn om het volgende voorvoegsel, "a bee" te formeren.
> 
> De eerste keus kan een lijst zijn omdat dit het gemakkelijk maakt elementen te verwijderen en toe te voegen maar de mogelijkheid om voorvoegsels als sleutels in een woordenboek te gebruiken, sluit het gebruik van lijsten uit. Met tupels kunt u geen zaken toevoegen of verwijderen maar u kunt een "addition" operator gebruiken om een nieuwe tupel aan te maken:
> 
> def verschuif(voorvoegsel, woord):
>       return voorvoegsel\[1:\] + (woord,)
> 
> verschuif krijgt een tupel van woorden voorvoegsel en een string woord, en formeert een nieuwe tupel die alle woorden heeft uit voorvoegsel behalve de eerste en woord aan het einde toevoegt.
> 
> Voor de verzameling voorvoegsels is het nodig om nieuwe voorvoegsels toe te voegen (of de frequentie van een bestaande te verhogen) en een willekeurig voorvoegsel te kiezen.
> 
> Het toevoegen van een nieuw voorvoegsel is net zo gemakkelijk bij een lijst als bij een histogram. Het kiezen van een willekeurig element uit een lijst is gemakkelijk, het kiezen uit een histogram is moeilijk efficiënt uit te voeren (zie oefening 13.7).
> 
> Tot nu toe hebben we voornamelijk gesproken over het gemak van uitvoeren maar andere factoren spelen ook een rol bij de keuze voor een gegevensstructuur. Eén zo'n factor is performance. Op theoretische gronden is het aannemelijk dat de ene gegevensstructuur sneller is dan de andere. Bijvoorbeeld: de in operator is sneller voor woordenboeken dan voor lijsten, tenminste als het aantal elementen groot is.
> 
> Maar vaak weet u niet welke uitvoering sneller zal zijn. Een optie is het uitvoeren van beide en proefondervindelijk de snelheid vaststellen. Deze aanpak wordt bench-mark genoemd. Een praktisch alternatief is het kiezen van een gegevensstructuur die het eenvoudigst uit te voeren is en dan te beoordelen of deze snel genoeg is voor de uiteindelijke applicatie. Zo ja, dan hoeft u niet verder te gaan. Zo nee, dan zijn er hulpmiddelen, zoals het profile module, dat aan kan geven welke delen van het programma de meeste tijd kosten.
> 
> De andere factor die moet worden overwogen is opslagruimte. Bijvoorbeeld: het gebruik van een histogram voor een verzameling voorvoegsels kan minder ruimte innemen, omdat u elk woord maar één keer hoeft op te slaan, ongeacht hoe vaak het woord voorkomt in de tekst. In bepaalde gevallen kan het besparen van ruimte de snelheid ten goede komen en in uitzonderlijke gevallen werkt het programma helemaal niet als er geen geheugen meer beschikbaar is. Maar voor veel applicaties is ruimte een tweede overweging na performance.
> 
> Een afsluitende gedachte: in deze discussie heb ik aangenomen dat we één gegevensstructuur voor zowel de analyse en bouw gebruiken. Maar omdat dit verschillende fases zijn, is het ook mogelijk om de ene structuur voor de analyse en een andere voor de bouw te gebruiken. Dit levert een nettowinst op als de tijd die we besparen tijdens de bouw, opweegt tegen de tijd nodig voor de omzetting.
> 
> ## 13.10 Debuggen
> 
> Bij het debuggen van een programma, in het bijzonder als u werkt aan een taaie fout, zijn er vier zaken die u kunt proberen:
> 
> **lezen**: Onderzoek uw code, lees het hardop voor uzelf en controleer of het doet wat het moet doen.
> 
> **uitvoeren**: Experimenteer door aanpassingen te maken en voer verschillende versies uit. Vaak helpt het als u de juiste zaken op de juiste plaats in het programma weergeeft op het scherm; de oplossing van het probleem ligt opeens voor de hand. Maar het duurt soms even om één en ander in de steigers te zetten..
> 
> **nadenken**: Neem de tijd om rustig na te denken! Wat voor soort fout treedt op: zinsbouw, uitvoering of semantisch? Welke informatie krijgt u uit de foutmeldingen of uit de uitvoer van het programma? Wat voor soort fout veroorzaakt het probleem dat u nu ziet? Wat hebt u als laatste gewijzigd, voordat het probleem optrad?
> 
> **terugvallen**: Op enig moment is het beste wat u kunt doen: terugvallen op vorige versies. Draai alle recente veranderingen terug tot het moment dat het programma wel werkte en dat u begrijpt waarom het werkt. Bouw vanaf dat punt verder.
> 
> Beginnende programmeurs lopen soms vast op één van deze activiteiten en vergeten de andere. Elke activiteit heeft zijn eigen kans op mislukken.
> 
> Bijvoorbeeld: het lezen van uw code kan helpen als het probleem een tikfout betreft maar dit helpt niet als het probleem een misverstand is over het concept. Als u niet begrijpt wat uw programma doet, dan kunt u het wel honderd keer doorlezen en nooit de fout ontdekken, omdat deze in uw hoofd zit.
> 
> Experimenten uitvoeren kan helpen, in het bijzonder als u kleine, eenvoudige testjes uitvoert. Maar als u experimenten uitvoert zonder na te denken of uw code door te lezen, dan kunt u in een patroon terecht komen dat ik "in het wilde weg programmeren" zou willen noemen; dat wil zeggen: willekeurig het programma aanpassen totdat het de juiste dingen doet. Onnodig te zeggen dat "in het wilde weg programmeren" erg lang duurt.
> 
> U moet de tijd nemen om na te denken. Debuggen is net zoiets als experimentele wetenschap. U moet tenminste één hypothese, veronderstelling, hebben over wat het probleem is. Bestaan er twee of meer oplossingen bedenk dan een test die één oplossing uitsluit.
> 
> Een rustpauze helpt bij het nadenken. Er over praten helpt ook. Leg het probleem uit aan een ander (of jezelf) en vaak vindt u het antwoord nog voor u klaar bent met het stellen van de vraag.
> 
> Helaas mislukken de beste debugtechnieken als er te veel fouten in het programma zitten of als de code die u probeert te verbeteren te omvangrijk of te complex is. De beste optie is dan terugvallen en het programma vereenvoudigen zodanig dat u iets overhoudt dat werkt en dat door u wordt begrepen.
> 
> Beginnende programmeurs hebben vaak geen zin om terug te vallen op eerdere versies omdat ze het moeilijk vinden om regels met code (zelfs als ze fout zijn) te verwijderen. U kunt ook een kopie van uw programma maken, voordat u dit uitkleedt, als u zich hierdoor beter voelt. Vervolgens kunt u delen terug plaatsen, stukje bij beetje.
> 
> Een taaie fout vinden vereist doorlezen, uitvoeren, nadenken en soms terugvallen op oude versies. Loopt u vast bij één van deze activiteiten probeer dan een andere.
> 
> ## 13.11 Woordenboek
> 
> **deterministic**: Heeft betrekking op een programma dat, iedere keer als het wordt uitgevoerd, hetzelfde resultaat oplevert bij dezelfde invoer.
> 
> **zogenaamd willekeurig**: Behorend tot een reeks getallen die willekeurig lijkt, maar die opgebouwd is door een deterministic programma.
> 
> **standaardwaarde**: De waarde die een optionele parameter meekrijgt als geen argument wordt geleverd.
> 
> **overschrijven**: Een standaardwaarde vervangen door een argument.
> 
> **benchmarking**: Het proces van het kiezen tussen gegevensstructuren door alternatieven toe te passen en deze te testen met een steekproef uit de mogelijke invoer.
> 
> ## 13.12 Oefeningen
> 
> **Oefening 13.9** De "rang" van een woord is zijn positie in een lijst van woorden gesorteerd op frequentie: Het meest voorkomende woord heeft de eerste rang, het op één na meest voorkomende de tweede rang, enzovoorts. Zipf’s wet beschrijft de relatie tussen de rangen en de frequentie van woorden in natuurlijke talen2 .
> 
> In het bijzonder voorspelt de wet dat de frequentie, _f_ , van het woord met rang _r_ is:
> 
> -   f = cr−s
>     
> 
> Hierbij zijn _s_ en _c_ parameters die taal en tekst afhankelijk zijn. Neemt u de logaritme van beide kanten van deze vergelijking, dan krijgt u:
> 
> -   log f = log c − s log r
>     
> 
> Dus als u log _f_ op papier afzet tegen log _r_ moet u een rechte lijn krijgen onder een hoek van −_s_ en een afgesneden stuk log _c_.
> 
> Schrijf een programma dat een tekst uit een bestand leest, de woordfrequentie telt en één lijn voor elk woord print, in aflopende volgorde van frequentie met log _f_ en log _r_. Gebruik uw tekenprogramma om de resultaten te tekenen en controleer of ze een rechte lijn vormen. Kunt u de waarde van _s_ schatten?
> 
> * * *
> 
> 1 Deze casestudy is gebaseerd op een voorbeeld van Kernighan en Pike, "The Practice of Programming, 1999".  
> 2 See [http://nl.wikipedia.org/wiki/Zipfdistributie](http://nl.wikipedia.org/wiki/Zipfdistributie)