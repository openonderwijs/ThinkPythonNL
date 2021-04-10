[community/ThinkPython/HoofdstukEen - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukEen)

> # Hoofdstuk 1 De manier van programmeren
> 
> Het doel van dit boek is om u te leren denken als een programmeur. De manier waarop programmeurs denken, combineert de beste eigenschappen van wiskunde, technische wetenschappen en de natuurwetenschappen. Net als wiskundigen gebruiken programmeurs een formele taal om een idee weer te geven. Net als bouwkundigen bedenken ze dingen, maken de benodigde onderdelen, assembleren deze en bedenken er weer een alternatief voor. Net als natuurkundigen observeren ze het gedrag van een complex systeem en testen vervolgens de gemaakte voorspellingen.
> 
> De belangrijkste vaardigheid van een programmeur is **probleemoplossing**. Met probleemoplossing bedoelen we het vermogen om problemen te formuleren, creatief te denken over oplossingen en de oplossing duidelijk en nauwkeurig uit te kunnen leggen. Het is mooi meegenomen dat leren programmeren een uitstekende manier is om probleemoplossingen te bedenken. Dat is waarom we dit hoofdstuk “De manier van programmeren” noemen.
> 
> Op één niveau zult u leren programmeren, wat op zich een nuttige vaardigheid is. Op een ander niveau zult u programmeren als middel gebruiken om tot een doel te komen. Dit zal duidelijker worden naarmate we verder gaan.
> 
> ## 1.1 De programmeertaal Python
> 
> De programmeertaal die u gaat leren is Python. Python is een voorbeeld van een hogere programmeertaal of zoals het in het algemeen **high-level language** wordt genoemd. Andere talen op dit niveau zijn: C, C++, Perl, en Java.
> 
> Er bestaan ook programmeertalen op een lager niveau, **"low-level languages"**. Deze worden ook wel "machine taal" of "assembler taal" genoemd. Computers kunnen alleen een low-level language uitvoeren. Dit houdt in dat een high-level language eerst omgezet moet worden naar een low-level language. Dit kost extra computertijd, wat een klein nadeel is van de high-level languages.
> 
> De voordelen van de high-level languages zijn echter vele malen groter. Op de eerste plaats is het veel makkelijker om in een high-level language te programmeren. High-level languages zijn korter en makkelijker te lezen. Ook zijn deze in het algemeen correcter geschreven en bevatten dus minder fouten. Ten tweede zijn deze talen **"portable"**. Dit houdt in dat ze niet één en dezelfde pc nodig hebben, maar werken op verschillende soorten computers met weinig of geen aanpassingen. De low-level languages zijn specifiek voor één pc gemaakt en moeten herschreven worden voor een andere pc als u ze hierop wilt gebruiken.
> 
> De nadelen wegen dus niet op tegen de voordelen en dat is precies de reden dat bijna alle programma's worden geschreven in een high-level language. Low-level languages worden alleen gebruikt voor zeer gespecialiseerde programma's.
> 
> Twee verschillende programma's zetten de high-level languages om in low-level languages zodat de computer ze kan lezen. De verschillende programma's zijn **"interpreters"** en **"compilers"**. Een interpreter leest een high-level language en voert deze uit; dit houdt in dat het precies doet wat er in het programma staat. Het leest het programma lijn voor lijn en bekijkt dan wat er uitgevoerd moet worden. Een voorbeeld hiervan ziet u hieronder:
> 
> -   ![boek001_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukEen?action=AttachFile&do=get&target=boek001_nl.png "boek001_nl.png")
>     
> 
> Een compiler leest het programma en vertaalt het helemaal naar machinetaal voordat hij het programma gaat uitvoeren. In deze voorbeelden wordt de programmacode de **"source code"** genoemd, het naar machinetaal vertaalde programma wordt **"object code"** of **"executable"** genoemd. Als een programma is gecompileerd kunt u het meerdere malen uitvoeren zonder dat het programma opnieuw vertaald hoeft te worden.
> 
> -   ![boek002_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukEen?action=AttachFile&do=get&target=boek002_nl.png "boek002_nl.png")
>     
> 
> Python wordt beschouwd als een geïnterpreteerde programmeertaal. Dit omdat alle python programma's worden uitgevoerd door een interpreter. De interpreter kan op twee manieren gebruikt worden: interactieve modus en script modus. Bij interactieve modus wordt, na het typen van code, het resultaat direct getoond door de interpreter.
> 
> Een voorbeeld van de interactieve modus ziet u hieronder:
> 
> \>>> 1 + 1
> 2
> 
> De visgraat, >>> is de prompt die de interpreter gebruikt om aan te geven dat hij klaar is. Als u 1 + 1 ingeeft en op Enter drukt, komt de interpreter met de uitkomst 2.
> 
> Bij de andere optie, script modus, slaat u code op in een python bestand. De interpreter wordt gebruikt om dit bestand uit te voeren. Dit bestand wordt een **"script"** , ofwel **"module"** genoemd. Alle door python uitvoerbare scripts of bestanden eindigen hun bestandsnaam met .py of .pyw (de zg. extensie)
> 
> Om een script uit te laten voeren moet u de interpreter de naam van het bestand laten weten. In een Unix commando scherm typt u bijvoorbeeld: "python voorbeeld.py". In "python voorbeeld.py" wordt de tekst "python" gebruikt om aan te geven dat het om een python script gaat. Als u een ander besturingssysteem dan een op Unix gebaseerd systeem gebruikt, kan er verschil zitten in de manier waarop het script wordt uitgevoerd. Instructies om uw script op een ander systeem uit te voeren kunt u allemaal vinden op de website [www.python.org](http://www.python.org).
> 
> De interactieve modus kunt u het best gebruiken om kleine stukken code te testen omdat het resultaat meteen zichtbaar wordt. Als u meer dan een paar regels code hebt, kunt u ze het best in een script opslaan, zodat dit in de toekomst gewijzigd en uitgevoerd kan worden.
> 
> ## 1.2 Wat is een programma?
> 
> Een **programma** is een serie instructies (statements genoemd) waarin precies is beschreven hoe een bewerking door een computer wordt uitgevoerd. De bewerking kan rekenkundig zijn, zoals een vergelijking oplossen, of het begin van een polynomial opzoeken. Maar het kan ook een symbolische bewerking zijn, zoals het zoeken en vervangen van een tekst in een document of (vreemd genoeg) het compileren van een programma.
> 
> De details zien er in elke taal verschillend uit, maar een aantal basisinstructies komen in elke taal voor:
> 
> **invoer (input)**: Gegevens ophalen van het toetsenbord, een bestand of een ander randapparaat.
> 
> **uitvoer (output)**: Gegevens weergeven op het scherm of doorsturen naar een bestand of een ander randapparaat.
> 
> **bereken (math)**: Standaard wiskundige operatie uitvoeren, zoals optellen of vermenigvuldigen.
> 
> **voorwaardelijke uitvoering (conditional execution)**: Controleren of aan een bepaalde voorwaarde wordt voldaan en de opdrachten in de juiste volgorde uitvoeren.
> 
> **herhaling (repetition)**: Een actie meerdere keren uitvoeren, veelal met een bepaalde variatie.
> 
> Geloof het of niet, dat is het zo ongeveer. Elk programma dat u ooit hebt gebruikt, ongeacht hoe complex, is samengesteld uit instructies die lijken op deze. Als u denkt aan programmeren is dat niets anders dan het opdelen van een grote complexe taak in steeds kleinere deeltaken totdat de deeltaken eenvoudig genoeg zijn om uitgevoerd te worden door een van deze basisinstructies.
> 
> Dit zal misschien nog onduidelijk zijn, maar we zullen hierop terugkomen wanneer we het gaan hebben over **algoritmes**.
> 
> ## 1.3 Wat is debuggen?
> 
> Programmeren is foutgevoelig. Om onduidelijke redenen worden programmeerfouten **bugs** genoemd; het proces om ze op te sporen wordt **debuggen** genoemd.
> 
> Er kunnen drie soorten fouten optreden in een programma: syntaxis (zinsbouw) fouten, runtime (uitvoerings) fouten en semantische (taalkundige) fouten. Het is handig om onderscheid te maken tussen deze fouten zodat ze sneller kunnen worden opgespoord.
> 
> ### 1.3.1 Syntaxis fouten
> 
> Python kan alleen een programma uitvoeren als de zinsbouw correct is; zo niet, dan geeft de interpreter een foutbericht weer. **Syntaxis** verwijst naar de structuur van een programma en de regels over deze structuur. Bijvoorbeeld: haakjes moeten altijd in tweetallen voorkomen, dus (1 + 2) is toegestaan maar 8) levert een **syntax error**.
> 
> In het Nederlands of Engels kunnen lezers de meeste fouten in de zinsbouw wel lezen; daarom kunnen we gedichten lezen zonder iedere keer te struikelen over "fouten" in de zinsbouw. Python is niet zo vergevingsgezind. Zodra er maar één enkele zinsbouwfout ergens in het programma staat, zal Python een foutbericht weergeven en stoppen. Het programma zal dan niet uitgevoerd worden. Tijdens de eerste paar weken van een "programmeurscarrière" zult u veel tijd kwijt zijn met het achterhalen van zinsbouwfouten. Krijgt u meer ervaring, dan maakt u minder fouten en als u fouten maakt zijn deze sneller gevonden.
> 
> ### 1.3.2 Runtime fouten
> 
> De tweede soort fouten zijn runtime fouten. Die zijn zo genoemd omdat deze fouten pas aan het licht komen nadat het programma is gestart. Deze fouten worden ook wel **exceptions** (uitzonderingen) genoemd, omdat ze over het algemeen aangeven dat iets uitzonderlijks (en foutiefs) is opgetreden.
> 
> Runtime fouten zijn zeldzaam in eenvoudige programma's, zoals u zult zien in de eerste paar hoofdstukken. Het kan dus even duren voordat u een dergelijke fout gaat ontdekken.
> 
> ### 1.3.3 Semantische fouten
> 
> De derde soort fout is de **semantische fout**. Als in het programma een semantische fout zit, zal het uitstekend uitgevoerd worden in die zin dat de computer geen foutmelding zal geven. Het programma zal niet de juiste zaken uitvoeren maar iets anders. Om precies te zijn: het programma zal doen wat u het verteld hebt te doen.
> 
> Het probleem is dat het programma dat u hebt geschreven niet het programma is dat u wilde schrijven. De betekenis van het programma (de semantiek) is fout. Het identificeren van semantische fouten is een delicaat proces omdat u naar de uitvoer van het programma kijkt en dan, al terugwerkend, moet achterhalen wat het programma gedaan heeft.
> 
> ### 1.3.4 Experimenteel debuggen
> 
> Eén van de belangrijkste vaardigheden die u zult aanleren is debuggen. Hoewel het frustrerend kan zijn, is debuggen een van de meest intellectuele, uitdagende en interessante onderdelen van programmeren.
> 
> Debuggen lijkt in veel opzichten op het werk van een detective. U wordt geconfronteerd met aanwijzingen en u moet de processen en gebeurtenissen, die naar het resultaat hebben geleid, deduceren.
> 
> Debuggen lijkt ook op een experimentele wetenschap. Zodra u een idee hebt over wat er mis ging, past u het programma aan en probeert u het opnieuw. Is uw aanname correct, dan kunt u de uitkomst van de wijziging voorspellen en bent u een stap dichter bij het werkend maken van uw programma. Is uw aanname fout, dan moet u een nieuwe verzinnen. Zoals Sherlock Holmes benadrukte, “Wanneer u het onmogelijke hebt uitgesloten; wat dan nog overblijft, hoe onwaarschijnlijk ook, moet de waarheid zijn.” (A. Conan Doyle, _The Sign of Four_)
> 
> Voor bepaalde mensen is programmeren en debuggen zo ongeveer hetzelfde. Dat wil zeggen, programmeren is het proces van geleidelijk aan debuggen van een programma totdat het doet wat u wilt. Het idee is dat u gaat starten met een programma dat _iets_ doet, kleine veranderingen aanbrengen en dit blijven debuggen, zodat u uiteindelijk een werkend programma overhoudt.
> 
> Bijvoorbeeld: Linux is een besturingssysteem dat duizenden regels code bevat, maar is gestart als een eenvoudig programma dat Linus Torvalds gebruikte om de Intel 80386 chip te onderzoeken. Larry Greenfield geeft aan: “Eén van Linus’ eerste projecten was een programma dat moest omschakelen tussen het printen van AAAA en BBBB. Dit is later ontwikkeld tot Linux.” (_The Linux Users’ Guide_ Beta Version 1).
> 
> In de volgende hoofdstukken zullen we meer suggesties geven over het debuggen en andere programmeergewoonten.
> 
> ## 1.4 Formele en natuurlijke talen
> 
> **Natuurlijke talen** zijn de talen die mensen spreken, zoals Nederlands, Engels, Frans en Duits. Deze zijn niet ontworpen door mensen (hoewel mensen er enige ordening in willen brengen). Zij ontwikkelen zich op een natuurlijke wijze.
> 
> **Formele talen** zijn talen die zijn ontworpen door mensen voor een specifieke toepassing. Bijvoorbeeld: de notatie die wiskundigen gebruiken is een formele taal die in het bijzonder goed is in het omschrijven van relaties tussen getallen en symbolen. Scheikundigen gebruiken een formele taal om de chemische structuur van moleculen te beschrijven. En de meest belangrijke:
> 
> -   **Programmeertalen zijn formele talen die zijn ontworpen om de werking van een computer te beschrijven.**
>     
> 
> Formele talen zijn geneigd om strikte regels te hanteren ten aanzien van de zinsbouw. Bijvoorbeeld: 3+3 = 6 is syntactisch een correcte wiskundige formulering, maar 3+ = 3$6 is dat niet. _H_2_O_ is een syntactisch correcte scheikundige formule, maar 2_Zz_ is dat niet.
> 
> Zinsbouwregels komen in twee smaken, de één is kenmerkend voor **symbolen**, de ander voor de structuur. Symbolen zijn de basis elementen van een taal, zoals woorden, getallen en scheikundige elementen. Een probleem met 3+ = 3$6 is dat $ geen rechtmatig symbool in de wiskunde is (niet voor zover bekend). Vergelijkbaar, 2_Zz_ is niet rechtmatig omdat er geen element bestaat met de afkorting _Zz_.
> 
> De tweede soort zinsbouwfouten is kenmerkend voor de structuur van een instructie; dat wil zeggen, de manier waarop de symbolen zijn gerangschikt. De instructie 3+ = 3$6 is niet rechtmatig omdat, hoewel de "+" en de "=" rechtmatige symbolen zijn, u het ene symbool niet direct achter het andere mag plaatsen. Vergelijkbaar, in een scheikundige formule komt het onderschrift na het element en niet ervoor.
> 
> **Oefening 1.1** Schrijf een netjes gestructureerde Nederlandse zin met ongeldige symbolen op. Schrijf daarna een andere zin met alleen geldige symbolen maar met een ongeldige structuur.
> 
> Wanneer u een zin in het Nederlands leest of een instructie in een formele taal, dan moet u de structuur van de zin ontrafelen (in een natuurlijke taal doet u dit onbewust). Dit proces wordt **ontleden (parsing)** genoemd.
> 
> Bijvoorbeeld: wanneer u de zin “Het kwartje is gevallen” hoort begrijpt u dat “het kwartje” het onderwerp is en “gevallen” het gezegde. Hebt u eenmaal de zin ontleed, dan snapt u de betekenis of de zinsbouw van de zin. Aangenomen dat u weet wat een kwartje is en wat gevallen betekent, zult u de gevolgen van deze zin begrijpen.
> 
> Hoewel formele en natuurlijke talen veel overeenkomsten hebben in gemeenschappelijke symbolen, structuur en zinsbouw zijn er enkele verschillen:
> 
> **dubbelzinnigheid**: Natuurlijke talen zitten vol dubbelzinnigheid, waar mensen raad mee weten door aanwijzingen vanuit de context, de samenhang en andere informatie. Formele talen zijn ontworpen om zo goed als of compleet ondubbelzinnig te zijn. Dit betekent dat elke instructie maar één betekenis heeft, ongeacht de context.
> 
> **overtolligheid**: Om met dubbelzinnigheid om te gaan en misverstanden te voorkomen bedienen natuurlijke talen zich van veel overtolligheid. Met als resultaat, dat deze breedsprakig zijn en dus veel woorden nodig hebben. Formele talen zijn minder uitgebreid en beknopter.
> 
> **letterlijkheid**: Natuurlijke talen zitten vol met taaleigenaardigheden en beeldspraak. Als ik zeg, “Het kwartje is gevallen”, dan is er waarschijnlijk geen kwartje en is er niets gevallen1. Formele talen bedoelen precies wat ze zeggen.
> 
> Mensen die opgroeien in het spreken van een natuurlijke taal — iedereen dus — hebben het vaak moeilijk met het zich aanpassen aan een formele taal. In sommige opzichten is het verschil tussen een formele en een natuurlijke taal net als het verschil tussen poëzie en proza, maar dan zo:
> 
> **poëzie** : Woorden worden gebruikt om hun klank en hun betekenis, en het gehele gedicht tezamen schept een effect of een emotionele reactie. Dubbelzinnigheid is niet alleen gebruikelijk maar vaak met opzet gebruikt.
> 
> **Proza**: De letterlijke betekenis van woorden is belangrijker en de structuur voegt nog meer aan de betekenis toe. Proza is meer vatbaar voor analyse dan poëzie, maar nog steeds vaak dubbelzinnig.
> 
> **Programma's**: De betekenis van een computerprogramma is ondubbelzinnig en letterlijk en kan volledig worden begrepen door analyse van de symbolen en de structuur.
> 
> Hierbij een aantal suggesties voor het lezen van programma's (en andere formele talen). Als eerste, onthoudt dat formele talen compacter zijn dan natuurlijke talen, het duurt dus langer om ze te lezen. Ook is de structuur van groot belang; het is normaal gesproken geen goed idee om van boven naar beneden en van links naar rechts te lezen. Leer in plaats daarvan het programma in uw hoofd te ontleden. Stel de identiteit vast van de symbolen en verklaar de structuur. Tenslotte, de details maken veel verschil. Kleine fouten in de spelling en de interpunctie, waarmee u wel weg komt in natuurlijke talen, kunnen een groot verschil maken in een formele taal.
> 
> ## 1.5 Het eerste programma
> 
> Traditioneel heet het eerste programma dat u schrijft in een nieuwe taal "Hello, World!" omdat het alleen de woorden "Hello, World!" weergeeft. In Python ziet het er zo uit:
> 
> print 'Hello, World!'
> 
> Dit is een voorbeeld van een **print instructie**2 , die eigenlijk niet iets afdrukt op papier. Het geeft een waarde weer op het scherm. In dit geval is het resultaat
> 
> Hello, World!
> 
> De aanhalingstekens in het programma markeren het begin en einde van de tekst die wordt weergegeven, ze worden niet weergegeven in het resultaat.
> 
> Sommige mensen beoordelen de kwaliteit van een programmeertaal door de eenvoud van het "Hello, world!" programma. Met deze norm doet Python het zo goed mogelijk.
> 
> ## 1.6 Debuggen
> 
> Het is een goed idee om dit boek te lezen naast een computer zodat u de voorbeelden kunt uitproberen tijdens het lezen. U kunt de meeste voorbeelden uitvoeren in de interactieve modus, maar als u de code in een script opslaat is het eenvoudiger om verschillende varianten uit te proberen.
> 
> Telkens als u experimenteert met een nieuw element zou u fouten moeten maken. Bijvoorbeeld in het “Hello, world!” programma, wat gebeurt er als u een aanhalingsteken weglaat? Wat als beide worden weggelaten? Wat als u print verkeerd spelt?
> 
> Deze manier van experimenteren helpt u te onthouden wat u leest; het helpt u ook bij het debuggen omdat u weet wat de foutberichten betekenen. Het is handiger om nu en expres fouten te maken dan later en per ongeluk.
> 
> Programmeren en in het bijzonder debuggen brengen soms heftige emoties te weeg. Als u worstelt met een moeilijke bug (fout), kunt u zich boos, wanhopig of uit het veld geslagen voelen.
> 
> Er is bewijs dat mensen van nature reageren naar computers toe alsof het mensen zijn3. Als ze correct werken, behandelen we ze als teamleden maar als ze koppig of grof zijn, dan reageren we op computers op dezelfde manier als op koppige en grove mensen.
> 
> Voorbereid zijn op dergelijke reacties helpt u om hier goed mee om te gaan. Een manier van benaderen is te denken aan de computer als een werknemer met bepaalde sterke kanten, zoals snelheid en precisie, en specifieke zwakheden, zoals gebrek aan inlevingsvermogen en het grote plaatje niet kunnen overzien.
> 
> Uw opdracht is om een goede manager te zijn: zoek naar wegen om voordeel te halen uit de sterke kanten en de zwakke kanten te verzachten. En zoek wegen om uw emotie te gebruiken bij het vastbijten in het probleem, zonder dat uw reacties uw effectiviteit negatief beïnvloeden.
> 
> Leren hoe te debuggen kan frustratie te weeg brengen, maar het is een waardevolle vaardigheid die nuttig is bij veel activiteiten buiten het programmeren. Aan het einde van elk hoofdstuk is er een debug onderdeel, zoals dit, met mijn oordeel over het debuggen. Ik hoop dat het helpt!
> 
> ## 1.7 Woordenlijst
> 
> **probleemoplossing**: Het proces van het formuleren van fouten, het zoeken naar een oplossing en de oplossing duidelijk maken.
> 
> **high-level language**: Een programmeertaal zoals Python die ontworpen is om gemakkelijk door mensen te worden gelezen en geschreven.
> 
> **low-level language**: Een programmeertaal die ontworpen is om gemakkelijk door een computer te worden uitgevoerd; ook wel “machine taal”. Om gemakkelijker tot machinetaal te komen wordt een "assembleertaal" gebruikt.
> 
> **overdraagbaarheid**: Een eigenschap van een programma zodat het op verschillende soorten computers kan worden uitgevoerd.
> 
> **interpreteren**: Een programma uitvoeren in een high-level language door het regel voor regel te vertalen.
> 
> **compileren**: Een programma geschreven in een high-level language in één keer vertalen naar een low-level language, ter voorbereiding om het later uit te voeren.
> 
> **source code**: Een programma in een high-level language voordat het wordt gecompileerd, ook broncode genoemd.
> 
> **object code**: De uitvoer van een compiler nadat het programma is vertaald.
> 
> **executable**: Een andere naam voor object code die klaar is om uitgevoerd te worden.
> 
> **prompt**: Karakter(s) weergegeven door de interpreter om aan te geven dat deze klaar is voor invoer van de gebruiker, ook wel oproepteken genoemd.
> 
> **script** **module**: Een programma opgeslagen in een bestand, normaal gesproken een bestand dat wordt geïnterpreteerd; beschouw een script (module) als een draaiboek met acties voor de computer.
> 
> **interactieve modus**: Een manier van werken met de Python interpreter door het typen van opdrachten en uitdrukkingen achter de prompt.
> 
> **script modus**: Een manier van werken met de Python interpreter om instructies te lezen en uit te voeren in een script (module).
> 
> **programma**: Een verzameling instructies die de bewerking door de computer beschrijven.
> 
> **algoritme**: Een algemeen proces voor het oplossen van een bepaalde categorie van problemen.
> 
> **bug**: Een fout in een programma.
> 
> **debuggen**: Het proces voor het vinden en verwijderen van elk van de drie soorten programmeerfouten.
> 
> **syntaxis**: De structuur van een programma, ook zinsbouw.
> 
> **syntax error**: Een fout in een programma die het ontleden onmogelijk maakt (en daardoor onmogelijk te interpreteren is).
> 
> **uitzondering**: Een fout die geconstateerd is tijdens de uitvoering van het programma, ook exception of runtime error.
> 
> **semantiek**: De betekenis van een programma.
> 
> **semantische fout**: Een fout in een programma die tot gevolg heeft dat het programma iets anders uitvoert dan de programmeur bedoelde.
> 
> **natuurlijke taal**: Een willekeurige taal die mensen spreken en zich natuurlijk ontwikkelt.
> 
> **formele taal**: Een willekeurige taal die mensen hebben ontworpen voor specifieke doeleinden, zoals het weergeven van wiskundige ideeën of computer programma's; alle programmeertalen zijn formele talen.
> 
> **token**: Een van de basiselementen van de syntactische structuur van een programma, overeenkomstig met een woord in een natuurlijke taal.
> 
> **ontleden**: Een programma onderzoeken en de syntactische structuur daarvan analyseren.
> 
> **print instructie**: Een instructie die zorgt dat de Python interpreter een waarde op het scherm weergeeft.
> 
> ## 1.8 Oefeningen
> 
> **Oefening 1.2** Gebruik een web browser en ga naar de Python Website [python.org](http://www.python.org). Deze pagina bevat informatie over Python en links naar aan Python gerelateerde pagina's en geeft de mogelijkheid om in de Python documentatie te zoeken.
> 
> Bijvoorbeeld: geef 'print' op in het zoekvak, de eerste link die verschijnt is het artikel in de documentatie over de print instructie. Op dit moment zal niet alles begrijpelijk zijn, maar het is goed om te weten waar u documentatie kunt vinden.
> 
> **Oefening 1.3** Start de Python interpreter en typ help(), hiermee start de online help functie. Of type help('print') waarmee informatie over de print instructie wordt verkregen.
> 
> Als dit voorbeeld niet werkt moet u waarschijnlijk extra Python documentatie installeren of een omgevingsvariabele instellen; de details hangen af van uw besturingssysteem en de versie van Python.
> 
> **Oefening 1.4** Start de Python interpreter en gebruik deze als een rekenmachine. De zinsbouw van Python voor rekenfuncties is nagenoeg dezelfde als bij een gewone rekensom. Bijvoorbeeld: de symbolen +, - en / verwijzen naar optellen, aftrekken en delen, zoals u zou verwachten. Het symbool voor vermenigvuldigen is "\*".
> 
> Als u 10 kilometer loopt in 43 minuten en 30 seconden, wat is dan uw gemiddelde tijd per mijl? Wat is uw gemiddelde snelheid in mijl per uur? (Hint: één mijl is 1.61 kilometer).
> 
> * * *
> 
> 1 Dit spreekwoord betekent dat iemand zich iets realiseert na even in verwarring te zijn geweest.  
> 2 In Python 3.0, is print een functie en geen instructie, dus de zinsbouw is print(’Hello, World!’). Op functies gaan we binnenkort in!  
> 3 Zie Reeves en Nass, _The Media Equation: How People Treat Computers, Television, and New Media Like Real People and Places._