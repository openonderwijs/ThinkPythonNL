[community/ThinkPython/HoofdstukTwintig - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig)

# Appendix A Debuggen

In een programma kunnen verschillende soorten fouten optreden. Het is handig om deze soorten te onderscheiden om ze gemakkelijker te achterhalen:

-   Foutmeldingen in de zinsbouw worden door Python geproduceerd op het moment dat de broncode vertaald wordt naar binaire code. Ze geven meestal aan dat er iets mis is met de zinsbouw van het programma. Bijvoorbeeld: een dubbelepunt weglaten aan het einde van een def instructie geeft een wat overbodige melding SyntaxError: invalid syntax.
    
-   Foutmeldingen tijdens de uitvoering worden door de interpreter geproduceerd als er iets fout gaat terwijl het programma uitgevoerd wordt. De meeste meldingen over fouten in de uitvoering bevatten informatie over de plaats waar de fout optreedt en welke functie werd uitgevoerd. Bijvoorbeeld: een oneindige herhaling veroorzaakt een fout in de uitvoering "maximum recursion depth exceeded".
-   Fouten in de semantiek zijn problemen met een programma dat draait zonder dat er foutmeldingen uit komen maar toch niet de juiste dingen doet. Bijvoorbeeld: een berekening wordt niet in de volgorde uitgevoerd zoals u verwachtte en levert een niet correct resultaat.

De eerste stap bij het debuggen is uit te zoeken met welke soort fout u te maken hebt. Hoewel de volgende paragrafen naar het soort fout zijn onderverdeeld, zijn bepaalde technieken toepasbaar in meerdere situaties.

## A.1 Fouten in de zinsbouw

Fouten in de zinsbouw zijn over het algemeen gemakkelijk op te lossen, zodra u hebt uitgezocht wat deze zijn. Helaas zijn de foutmeldingen meestal niet zo behulpzaam. De meest voorkomende meldingen zijn SyntaxError: invalid syntax en SyntaxError: invalid token, maar geen van tweeën levert zinnige informatie.

Aan de andere kant vertelt de melding wel waar in het programma het probleem optreedt. Om precies te zijn: Python meldt waar deze het probleem ontdekte en dat is niet noodzakelijkerwijs daar waar de fout zit. Soms zit de fout voor de plaats van de foutmelding maar vaker nog in de voorafgaande regel.

Bouwt u het programma stapje voor stapje op dan moet u snel in staat zijn de fout op te sporen. Zo goed als zeker in de laatste regel die is toegevoegd.

Kopieert u code uit een boek begin dan als eerste met het zorgvuldig controleren of dit correct is gebeurd. Controleer elk karakter. Bedenk eveneens dat het boek ook een drukfout kan bevatten. Dus ziet u iets dat lijkt op een fout in de zinsbouw dan kan dat zomaar.

Hierbij een aantal handvatten om de meest voorkomende fouten in de zinsbouw te voorkomen:

1.  Wees er zeker van dat u geen sleutelwoorden uit Python gebruikt als naam voor een variabele.
2.  Controleer of een dubbelepunt aan het einde van de header van elke samengestelde instructie staat, inclusief de for, while, if, en def instructies.
    
3.  Wees er zeker van dat elke string in de code zowel een aanhalingsteken openen, als één voor sluiten heeft.
4.  Gebruikt u strings over meerder regels met drievoudige aanhalingstekens (enkel of dubbel) verzeker u ervan dat deze correct zijn afgesloten. Een string die niet goed is afgesloten, kan een invalid token fout opleveren aan het einde van uw programma of het volgende deel van uw programma wordt als string gezien tot aan de volgende string. In dat geval zou er helemaal geen foutmelding kunnen verschijnen!
    
5.  Een niet afgesloten openingsoperator —(, {, of \[— zorgt ervoor dat Python doorgaat met de volgende regel alsof die onderdeel uitmaakt van de instructie. Over het algemeen treedt onmiddellijk een fout op in de volgende regel.
6.  Controleer op de klassieker: = in plaats van == in een voorwaarde.
7.  Controleer de inspringing om er zeker van te zijn dat de regels netjes uitgelijnd zijn op de manier zoals bedoeld. Python kan overweg met spaties en tabstops, maar deze door elkaar heen gebruiken, is om problemen vragen. De beste manier om dit probleem te voorkomen, is een tekstverwerker gebruiken die de gebruiken van Python kent en het inspringen consequent verzorgt.

Als dit allemaal niets uitricht, ga dan door met de volgende paragraaf...

### A.1.1 Mijn wijzigingen halen niets uit

Zegt de interpreter dat er een fout is en u ziet deze niet, dan kan het zijn dat u en de interpreter niet naar dezelfde code kijken. Controleer uw programmeeromgeving om er zeker van te zijn dat het programma, dat u onder handen hebt, hetzelfde is als wat Python probeert uit te voeren.

Ben u hiervan niet zeker, plaats dan een voor de hand liggende fout in zinsbouw aan het begin van het programma.

Draai het programma opnieuw. Vindt de interpreter geen nieuwe fout dan wordt de nieuwe code niet uitgevoerd.

De volgende schuldigen maken een grote kans:

-   U bewerkte het bestand maar bent vergeten dit op te slaan voordat u het programma opnieuw draaide. Sommige programmeeromgevingen doen dit voor u maar anderen niet.
-   U veranderde de naam van het bestand maar voert nog steeds het bestand met de oude naam uit.
-   Iets in de ontwikkelomgeving is niet goed geconfigureerd.
-   Schrijft u een module en gebruikt u import wees er dan zeker van dat u de module niet dezelfde naam geeft als één van de Python modules.
    
-   Gebruikt u import om een module in te lezen, onthoudt dan dat u de interpreter opnieuw moet starten of gebruik reload om het gewijzigde bestand te lezen. Importeert u de module opnieuw dan doet deze nog niets.
    

Loopt u vast en u hebt geen idee wat er gebeurt, dan is deze aanpak te overwegen: begin met een nieuw programma zoals "Hello, World!" en wees er zeker van dat dit programma uit te voeren is. Voeg vervolgens stukje bij beetje de onderdelen van uw originele programma toe aan het nieuwe programma en controleer de werking na iedere toevoeging.

## A.2 Fouten tijdens de uitvoering

Is uw programma qua zinsbouw correct dan kan Python dit compileren en ten minste draaien. Wat kan er nu nog verkeerd gaan?

### A.2.1 Mijn programma doet helemaal niets

Dit probleem is zeer gebruikelijk als uw bestand bestaat uit functies en klassen maar niet echt iets aanroept om de uitvoering te starten. Dit kan de bedoeling zijn als u alleen van plan bent deze module te importeren om zo klassen en functies te leveren.

Is dit niet de bedoeling, wees er dan zeker van dat u een functie aanroept om de uitvoering te starten of voer iets uit vanaf de "prompt". Zie ook de paragraaf "Volgorde van uitvoering" hieronder.

### A.2.2 Mijn programma hangt

Stopt een programma en lijkt het alsof het niets meer doet, dan "hangt" het programma. Dit betekent vaak dat het vast zit in een oneindige lus of een oneindige herhaling.

-   Is er een bepaalde lus die u verdenkt van het probleem, voeg een print instructie toe direct aan het begin van de lus, met de tekst "begint aan de lus", en nog één direct na afloop, met de tekst "Uit de lus gestapt". Voer het programma uit. Krijgt u het eerste bericht wel te zien maar het tweede niet, dan weet u dat dit een oneindige lus is. Ga naar de paragraaf "Oneindige lus" hieronder.
    
-   In het merendeel van de gevallen zal een oneindige herhaling het programma een tijdje laten draaien om daarna de foutmelding "RuntimeError: Maximum recursion depth exceeded" te geven. Gebeurt dit, ga dan naar de paragraaf "Oneindige herhaling" hieronder. Krijgt u deze foutmelding niet, maar verdenkt u een methode of functie, dan kunt u zeker de technieken in de paragraaf "Oneindige herhaling" gaan gebruiken.
    
-   Werkt geen van deze stappen, begin dan met het testen van andere lussen en recursieve functies en methodes.
-   Haalt dat ook niets uit, dan kan het zijn dat u de volgorde van uitvoering van uw programma niet begrijpt. Ga naar de paragraaf "Volgorde van uitvoering" hieronder.

**Oneindige lus**

Denkt u te weten dat er een oneindige lus optreedt en u vermoedt welke lus dit is, voeg een print instructie aan het einde van de lus toe die de waarde van de variabelen in de voorwaarde, en de waarde van de voorwaarde print.

Bijvoorbeeld:

function isnumbered(obj) { return obj.childNodes.length && obj.firstChild.childNodes.length && obj.firstChild.firstChild.className == 'LineNumber'; } function nformat(num,chrs,add) { var nlen = Math.max(0,chrs-(''+num).length), res = ''; while (nlen>0) { res += ' '; nlen-- } return res+num+add; } function addnumber(did, nstart, nstep) { var c = document.getElementById(did), l = c.firstChild, n = 1; if (!isnumbered(c)) { if (typeof nstart == 'undefined') nstart = 1; if (typeof nstep == 'undefined') nstep = 1; var n = nstart; while (l != null) { if (l.tagName == 'SPAN') { var s = document.createElement('SPAN'); var a = document.createElement('A'); s.className = 'LineNumber'; a.appendChild(document.createTextNode(nformat(n,4,''))); a.href = '#' + did + '\_' + n; s.appendChild(a); s.appendChild(document.createTextNode(' ')); n += nstep; if (l.childNodes.length) { l.insertBefore(s, l.firstChild); } else { l.appendChild(s); } } l = l.nextSibling; } } return false; } function remnumber(did) { var c = document.getElementById(did), l = c.firstChild; if (isnumbered(c)) { while (l != null) { if (l.tagName == 'SPAN' && l.firstChild.className == 'LineNumber') l.removeChild(l.firstChild); l = l.nextSibling; } } return false; } function togglenumber(did, nstart, nstep) { var c = document.getElementById(did); if (isnumbered(c)) { remnumber(did); } else { addnumber(did,nstart,nstep); } return false; } document.write('<a href="#" onclick="return togglenumber(\\'CA-9e3cf7443481ee0b0915026c54c05fc1c3e270c8\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-9e3cf7443481ee0b0915026c54c05fc1c3e270c8_1) while x > 0 and y < 0 :
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-9e3cf7443481ee0b0915026c54c05fc1c3e270c8_2)        \# doe iets met x
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-9e3cf7443481ee0b0915026c54c05fc1c3e270c8_3)        \# doe iets met y
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-9e3cf7443481ee0b0915026c54c05fc1c3e270c8_4)        print     "x: ", x
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-9e3cf7443481ee0b0915026c54c05fc1c3e270c8_5)        print     "y: ", y
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-9e3cf7443481ee0b0915026c54c05fc1c3e270c8_6)        print     "voorwaarde: ", (x > 0 and y < 0)

Als u nu het programma uitvoert ziet u drie regels met uitvoer voor iedere passage van de lus.

De laatste ronde door de lus moet de voorwaarde false onwaar zijn. Blijft de lus doorlopen dan ziet u de waarden voor x en y; daarmee kunt u wellicht achterhalen waarom deze niet correct worden bijgewerkt.

**Oneindige herhaling**

In het merendeel van de gevallen zal een oneindige herhaling het programma een tijdje laten draaien en daarna volgt een foutmelding dat het maximaal aantal herhalingen is bereikt: recursion depth exceeded.

Denkt u dat een functie de oorzaak is van een oneindige herhaling, controleer als eerste of er een basisblok is (zie hoofdstuk 5.9). Met andere woorden, er moet een conditie voorkomen die zorgt dat de functie of methode wordt verlaten zonder in herhaling te treden. Zo niet, dan moet een nieuw algoritme worden bedacht en een nieuw basisblok worden gevonden.

Bestaat een basisblok maar het programma lijkt daar niet aan toe te komen, voeg een print instructie toe aan het begin van de functie of methode die de parameters afdrukt. Als u nu het programma uitvoert ziet u een paar regels met uitvoer van de parameters, iedere keer dat de functie of methode wordt aangeroepen. Bewegen de parameters niet naar het basis blok toe dan krijgt u mogelijk een idee waarom niet.

**Volgorde van uitvoering**

Hebt u er geen idee van hoe de volgorde van uitvoering verloopt in uw programma, voeg dan print instructies toe aan het begin van iedere functie met een melding "Start van functie fn"; fn staat voor de naam van de functie.

Voert u het programma nu uit, dan zal het een spoor uitzetten naar elke functie die wordt aangeroepen.

### A.2.3 Wanneer het programma draait krijg ik een foutmelding

Gaat er iets mis bij het uitvoeren, dan drukt Python een melding af waarin de naam van de uitzondering, de regel in het programma waar het probleem optreedt en iets van een spoor.

Het spoor identificeert de functie die op dat moment uitgevoerd wordt en de functie die deze heeft aangeroepen en de functie die _deze_ weer heeft aangeroepen, enzovoorts. Met andere woorden, het legt een spoor aan van de volgorde van functieaanroepen tot aan de huidige plaats. Ook de regelnummers van waaruit de aanroepen zijn gepleegd, worden getoond.

De eerste stap is het onderzoeken van de plaats in het programma waar de fout optreedt en te bekijken wat er kan zijn gebeurd. Hierbij enkele veel voorkomende fouten tijdens de uitvoering:

**NameError**: U probeert een variabele te gebruiken die niet in de huidige omgeving bestaat. Denk aan het onderscheid tussen lokale en globale variabelen. U kunt niet naar lokale variabelen verwijzen buiten de functie, waarin ze zijn gedefinieerd. **TypeError**: Meerdere oorzaken zijn mogelijk:

-   U probeert een waarde op een onjuiste manier te gebruiken; bijvoorbeeld: een string, lijst of tupel te indexeren met iets anders dan een geheel getal.
-   De items in een formaatstring en de items doorgegeven voor conversie komen niet overeen. Dit kan gebeuren als het aantal items niet overeenkomt of een ongeldige conversie wordt aangeroepen.
-   U geeft een verkeerd aantal argumenten door aan een functie of een methode. Kijk bij methodes naar de definitie en controleer of de eerste parameter self is. Kijk vervolgens naar de aanroep van de methode; wees er zeker van dat u de methode aanroept op een object van het juiste type, vooropgesteld dat de overige argumenten correct zijn.
    

**KeyError**: U probeert een element uit een woordenboek te benaderen met een sleutel die niet in het woordenboek voorkomt.  

**AttributeError**: U probeert een attribuut of een methode te benaderen die niet bestaat. Controleer de spelling! U kunt dir gebruiken om de bestaande attributen te laten zien. Geeft een AttributeError aan dat een object een NoneType heeft, dan betekent dat dat het None is. Een gemeenschappelijke oorzaak is, dat wordt vergeten een waarde terug te geven vanuit een functie; komt een functie tot een einde zonder een return instructie dan wordt None terug gegeven. Een andere gemeenschappelijke oorzaak is gebruik maken van het resultaat van een lijst methode, zoals sort, die None terug geeft.  

**IndexError**: De index die u gebruikt voor het benaderen van een lijst, string of een tupel is groter dan de lengte min 1. Voeg direct voor de plaats van de fout een print instructie toe om daarmee de waarde van de index weer te geven. Heeft het array de juiste omvang? Heeft de index de juiste waarde?

De Python debugger (pdb) is handig voor het opsporen van uitzonderingen omdat het daarmee mogelijk is de status van het programma te onderzoeken, voorafgaand aan de fout. U kunt meer lezen over de pdb op [docs.python.org/lib/module-pdb.html](http://docs.python.org/lib/module-pdb.html).

### A.2.4 Er zijn zoveel print instructies toegevoegd dat het regent aan uitvoer

Een van de problemen met het gebruik van de print instructies voor het debuggen is dat u bedolven raakt onder de uitvoer. U kunt op twee manieren doorgaan: of de uitvoer vereenvoudigen, of het programma vereenvoudigen.

De uitvoer vereenvoudigen kan door commentaar, dat geen toegevoegde waarde heeft, uit de print instructies te verwijderen, of te combineren of de uitvoer zodanig te formatteren dat deze eenvoudig te begrijpen is.

Het programma vereenvoudigen kan op verschillende manieren. Als eerste, verklein het probleem waarvoor het programma aan de slag moet gaan. Bijvoorbeeld: doorzoekt u een lijst, doorzoek eerst een "kleine" lijst. Heeft het programma invoer van de gebruiker nodig, geef het dan de meest eenvoudige invoer waarmee het probleem optreedt.

Ten tweede, schoon het programma op. Verwijder niet gebruikte code en reorganiseer het programma zodat het gemakkelijk te lezen is. Bijvoorbeeld: verwacht u dat het probleem in een deel van het programma zit dat nogal verweven is, probeer dat deel in een eenvoudiger structuur te herschrijven. Verdenkt u een grote functie, probeer deze op te delen in kleinere functies en test deze afzonderlijk.

Vaak leidt het zoeken naar het minimale testgeval naar de fout. Ontdekt u dat het programma in de ene situatie werkt, maar in een andere situatie niet, dan geeft dat houvast bij het zoeken naar wat er gaande is.

Op dezelfde manier kan het herschrijven helpen bij het vinden van subtiele foutjes. Brengt u een verandering aan die de werking niet mag beïnvloeden maar het wel doet, dan levert dat een mooie aanwijzing.

## A.3 Fouten in de semantiek

Om de één of andere reden zijn fouten in de semantiek het moeilijkst op te sporen omdat de interpreter geen informatie levert over wat er mis gaat. Alleen u weet wat het programma zou moeten doen.

De eerste stap is het maken van een verbinding tussen de tekst van het programma en het gedrag dat u ziet.

U hebt een hypothese, een veronderstelling, nodig over wat het programma nu eigenlijk aan het doen is. Een van de zaken die het er niet eenvoudiger op maken is dat computers zo snel zijn.

Het zou mooi zijn als u het programma kunt afremmen naar een meer hanteerbare snelheid en met sommige debuggers kan dat ook. Maar de tijd nodig voor een paar wel geplaatste print instructies is vaak korter dan het opzetten van de debugger, het invoegen en verwijderen van controle punten en door het programma heen lopen tot aan waar de fout optreedt.

### A.3.1 Mijn programma werkt niet

Stel uzelf de volgende vragen:

-   Is er iets dat het programma zou moeten doen maar dat niet lijkt te gebeuren? Zoek de sectie op met de code die deze functie uitvoert en verzeker u ervan dat deze wordt uitgevoerd op het moment dat u denkt dat het moet.
-   Gebeurt er iets dat niet zou moeten? Zoek de code op in uw programma die deze functie uitvoert; bekijk of deze wordt uitgevoerd terwijl deze het niet zou moeten doen.
-   Produceert een sectie van de code een effect dat u niet verwachtte? Wees er zeker van dat u de betreffende code begrijpt, in het bijzonder als aanroepen naar functies en methoden in andere Python modules worden gedaan. Lees de documentatie over de functie die u aanroept. Probeer ze uit door eenvoudige testgevallen te schrijven en de resultaten te controleren.

Programmeren vereist dat u een model van het programma "in uw hoofd" hebt zitten. Hebt u een programma geschreven dat niet doet wat u ervan verwacht, dan zit het probleem vaak niet in het programma, maar in het model in uw hoofd.

De beste manier om het model in uw hoofd te corrigeren, is het programma op te delen in componenten (over het algemeen de functies en methodes) en elke component afzonderlijk te testen. Zodra u een tegenstrijdigheid vindt tussen uw model en de werkelijkheid kunt u het probleem oplossen.

Natuurlijk moet u de componenten bouwen en testen tijdens de ontwikkeling van het programma. Komt u een probleem tegen, dan behoort er maar een klein deel van de nieuwe code te zijn, waarover onzekerheid is ten aanzien van de werking.

### A.3.2 Ik heb een omvangrijke en gewaagde expressie en die doet niet wat ik ervan verwacht

Het schrijven van complexe expressies is mooi, zo lang ze leesbaar blijven maar ze zijn moeilijk te ontdoen van fouten. Het is meestal een goed idee om een complexe expressie op te delen en daarbij de tussenresultaten aan tijdelijke variabelen toe te wijzen.

Bijvoorbeeld:

self.hands\[i\].addCard(self.hands\[self.findNeighbor(i)\].popCard())

Kan worden herschreven als:

document.write('<a href="#" onclick="return togglenumber(\\'CA-da98b93b34b1aaea4975a59b91a244e4dbb90c22\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-da98b93b34b1aaea4975a59b91a244e4dbb90c22_1) neighbor = self.findNeighbor(i)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-da98b93b34b1aaea4975a59b91a244e4dbb90c22_2) pickedCard = self.hands\[neighbor\].popCard()
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-da98b93b34b1aaea4975a59b91a244e4dbb90c22_3) self.hands\[i\].addCard(pickedCard)

De uitgebreide versie is gemakkelijker te lezen omdat de namen van de variabelen extra informatie opleveren en het is gemakkelijker om zo fouten op te sporen omdat u het type van de tijdelijke variabelen kunt controleren en hun waarde weergeven.

Een ander probleem dat op kan treden met omvangrijke expressies is, dat de volgorde van uitvoering niet overeenkomt met uw verwachting. Bijvoorbeeld: vertaalt u de expressie x/2π naar Python, dan zou u het zo kunnen opschrijven:

y = x / 2 \* math.pi

Dat is niet juist omdat vermenigvuldigen en delen dezelfde voorrang hebben en van links naar rechts worden geëvalueerd. Dus deze expressie berekent xπ/2.

Een goede manier om expressies te debuggen is het toevoegen van haakjes (openen en sluiten) en zo de volgorde van evalueren te verduidelijken:

y = x / (2 \* math.pi)

Zodra u niet zeker bent van de volgorde van evalueren: gebruik haakjes. Het programma zal niet alleen correct zijn (volgens de manier die u bedoeld hebt); het wordt ook beter leesbaar voor anderen die even niet meer de voorrangsregel paraat hebben.

### A.3.3 Ik heb een functie of methode die niet teruggeeft wat ik verwacht

Hebt u een return instructie met een complexe expressie, dan hebt u niet de kans de return waarde af te drukken voordat deze wordt teruggegeven. Zoals al gezegd, gebruik een tijdelijke variabele. Bijvoorbeeld in plaats van:

return self.hands\[i\].removeMatches()

kunt u ook schrijven:

document.write('<a href="#" onclick="return togglenumber(\\'CA-330db5791765533a56cdf287730914e0811b93f1\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-330db5791765533a56cdf287730914e0811b93f1_1) teller = self.hands\[i\].removeMatches()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukTwintig#CA-330db5791765533a56cdf287730914e0811b93f1_2) return teller 

U hebt nu de gelegenheid om de waarde weer te geven van teller voordat deze teruggegeven wordt.

### A.3.4 Ik zit echt vast en heb hulp nodig

Ga, als eerste, een paar minuten bij de computer weg. Computers stralen golven uit die invloed hebben op de hersens en de volgende symptomen veroorzaken:

-   Frustratie en woede.
-   Bijgeloof ("de computer haat mij") en magische gedachten ('"Het programma werkt alleen als ik mijn pet achterstevoren draag").
-   In het wilde weg programmeren (de poging tot het programmeren door het schrijven van alle mogelijke programma's en uiteindelijk diegene kiezen die werkt).

Herkent u één van deze symptomen, sta dan op en loop een rondje. Zodra u kalm bent, overdenk het programma. Wat doet het? Wat zijn een aantal mogelijke oorzaken voor dat gedrag?

Wanneer werkte het programma nog goed en wat hebt u daarna gedaan?

Soms kost het gewoon tijd om de fout te vinden. Ik vind vaak fouten als ik bij de computer vandaan ben en mijn gedachten laat dwalen. De beste plaats om fouten te vinden is in de trein, onder de douche en in bed net voor het slapen gaan.

### A.3.5 Nee, ik heb echt hulp nodig

Het komt voor. Zelfs de beste programmeurs zitten soms vast. Soms werk je zolang aan een programma dat je de fout niet meer ziet. Een frisse blik is alles wat nodig is.

Wees goed voorbereid voordat u iemand anders gaat raadplegen. Het programma zou zo eenvoudig mogelijk moeten zijn en werk met de meest eenvoudige invoer waarbij het probleem optreedt. print instructies moeten op de juiste plaatsen staan (en de uitvoer daarvan moet begrijpelijk zijn).

U behoort het probleem goed genoeg te begrijpen om het beknopt te kunnen beschrijven.

Wanneer u iemand anders laat helpen, wees er dan zeker van dat de noodzakelijke informatie wordt gegeven:

-   Is er een foutmelding, wat is het en naar welk gedeelte van het programma verwijst deze?
-   Wat is het laatste dat u hebt gedaan voordat deze foutmelding optrad? Wat zijn de laatste regels code die u hebt geschreven of wat is het nieuwe testgeval waarop het mis gaat?
-   Wat hebt u tot nu toe geprobeerd en wat hebt u geleerd?

Wanneer u de fout vindt, neem dan even de tijd om te bedenken wat u zou hebben kunnen doen om deze sneller te vinden. De volgende keer als u iets gelijksoortigs tegenkomt, zult u de fout sneller kunnen vinden.

Onthoudt, het doel is niet alleen om het programma te laten werken. Het doel is om u te leren hoe het programma werkt.