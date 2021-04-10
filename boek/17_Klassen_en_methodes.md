[community/ThinkPython/HoofdstukZeventien - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien)

> # Hoofdstuk 17 Klassen en methodes
> 
> ## 17.1 Object-georiënteerde functies
> 
> Python is een **object-oriented programming language** (object-georiënteerde programmeertaal); dit houdt in dat deze functies levert die object-georiënteerd programmeren ondersteunen.
> 
> Het is niet gemakkelijk uit te leggen wat object-georiënteerd programmeren is, maar we zijn al wel verschillende aspecten tegengekomen:
> 
> -   • Programma's worden gemaakt met objectdefinities en functiedefinities; veel programmeerwerk wordt uitgedrukt in operators en objecten.  
>       
>     • Elke definitie van een object correspondeert met een object of concept in de echte wereld; de functies die uitgevoerd worden op het betreffende object staan in verbinding met de operaties die ook uitgevoerd worden in de echte wereld.
>     
> 
> Bijvoorbeeld: De klasse Tijd, gedefinieerd in hoofdstuk 16, komt overeen met de manier waarop mensen de tijd registreren en de gedefinieerde functies komen overeen met die zaken die mensen doen met tijden. Op dezelfde manier corresponderen de klassen Punt en rechthoek met de wiskundige concepten van een punt en een rechthoek.
> 
> Tot nu toe hebben we nog niet de voordelen benut van de mogelijkheden die Python biedt voor object-georiënteerd programmeren. Deze mogelijkheden zijn niet strikt noodzakelijk, de meeste leveren een alternatieve zinsbouw voor zaken die we al hebben uitgevoerd. Maar in veel gevallen is het alternatief beknopter en ondersteunt deze beter de structuur van het programma.
> 
> Bijvoorbeeld: in het programma Tijd bestaat er geen voor de hand liggende verbinding tussen de klassedefinitie en de functiedefinities die daarop volgen. Na wat onderzoek wordt het duidelijk dat elke functie tenminste één Tijd object als argument gebruikt.
> 
> Deze observatie is de motivatie voor **methodes**; een methode is een functie die verbonden is met een specifieke klasse. We hebben methodes gezien voor strings, lijsten, woordenboeken en tupels. In dit hoofdstuk zullen we methodes definiëren voor door de gebruiker gedefinieerde typen.
> 
> Methodes zijn in semantisch opzicht hetzelfde als functies, maar er zijn twee verschillen qua zinsbouw:
> 
> -   • Methodes worden binnen een klassedefinitie gedefinieerd om de relatie tussen de klasse en de methode expliciet te maken.  
>       
>     • De zinsbouw voor het aanroepen van een methode is anders dan de zinsbouw voor het aanroepen voor een functie.
>     
> 
> In de volgende paragrafen zullen we de functies uit de twee vorige hoofdstukken nemen en deze omzetten naar methodes. Deze transformatie is zuiver mechanisch; u kunt dit eenvoudig uitvoeren door een aantal stappen te volgen. Hebt u een goed gevoel bij het omzetten van de ene vorm naar de andere, dan bent u in staat om de beste vorm te kiezen voor alles wat u wilt programmeren.
> 
> ## 17.2 Objecten printen
> 
> In hoofdstuk 16 hebben we een klasse Tijd gedefinieerd. In oefening 16.1 hebt u de functie print\_tijd geschreven:
> 
> function isnumbered(obj) { return obj.childNodes.length && obj.firstChild.childNodes.length && obj.firstChild.firstChild.className == 'LineNumber'; } function nformat(num,chrs,add) { var nlen = Math.max(0,chrs-(''+num).length), res = ''; while (nlen>0) { res += ' '; nlen-- } return res+num+add; } function addnumber(did, nstart, nstep) { var c = document.getElementById(did), l = c.firstChild, n = 1; if (!isnumbered(c)) { if (typeof nstart == 'undefined') nstart = 1; if (typeof nstep == 'undefined') nstep = 1; var n = nstart; while (l != null) { if (l.tagName == 'SPAN') { var s = document.createElement('SPAN'); var a = document.createElement('A'); s.className = 'LineNumber'; a.appendChild(document.createTextNode(nformat(n,4,''))); a.href = '#' + did + '\_' + n; s.appendChild(a); s.appendChild(document.createTextNode(' ')); n += nstep; if (l.childNodes.length) { l.insertBefore(s, l.firstChild); } else { l.appendChild(s); } } l = l.nextSibling; } } return false; } function remnumber(did) { var c = document.getElementById(did), l = c.firstChild; if (isnumbered(c)) { while (l != null) { if (l.tagName == 'SPAN' && l.firstChild.className == 'LineNumber') l.removeChild(l.firstChild); l = l.nextSibling; } } return false; } function togglenumber(did, nstart, nstep) { var c = document.getElementById(did); if (isnumbered(c)) { remnumber(did); } else { addnumber(did,nstart,nstep); } return false; } document.write('<a href="#" onclick="return togglenumber(\\'CA-711bd85f1574dfd018dbb911aa2d99d135b2cace\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-711bd85f1574dfd018dbb911aa2d99d135b2cace_1) class Tijd(object):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-711bd85f1574dfd018dbb911aa2d99d135b2cace_2)       """stelt de tijd van de dag voor.
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-711bd85f1574dfd018dbb911aa2d99d135b2cace_3)  attributen: uur, minuut, seconde"""
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-711bd85f1574dfd018dbb911aa2d99d135b2cace_4) def print\_tijd(tijd):
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-711bd85f1574dfd018dbb911aa2d99d135b2cace_5)       print '%.2d:%.2d:%.2d' % (tiid.uur, tijd.minuut, tijd.seconde)
> 
> Bij het aanroepen van deze functie moet u een Tijd object als argument meegeven:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-c3a57810866c53cace56fd558f95f51b8233a49b\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-c3a57810866c53cace56fd558f95f51b8233a49b_1) \>>> start = Tijd()
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-c3a57810866c53cace56fd558f95f51b8233a49b_2) \>>> start.uur = 9
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-c3a57810866c53cace56fd558f95f51b8233a49b_3) \>>> start.minuut = 45
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-c3a57810866c53cace56fd558f95f51b8233a49b_4) \>>> start.seconde = 00
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-c3a57810866c53cace56fd558f95f51b8233a49b_5) \>>> print\_tijd(start)
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-c3a57810866c53cace56fd558f95f51b8233a49b_6) 09:45:00
> 
> Voor het maken van print\_tijd volgens een methode hoeven we alleen de functiedefinitie binnen in de klassedefinitie te plaatsen. Let op de verandering van het inspringen.
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-09d9a91aacf8e2ca0960647280d5f78f8f05a502\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-09d9a91aacf8e2ca0960647280d5f78f8f05a502_1) class Tijd(object):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-09d9a91aacf8e2ca0960647280d5f78f8f05a502_2)       def print\_tijd(tijd):
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-09d9a91aacf8e2ca0960647280d5f78f8f05a502_3)            print '%.2d:%.2d:%.2d' % (tijd.uur, tijd.minuut, tijd.seconde)
> 
> We kunnen op twee manieren print\_tijd aanroepen. De eerste (en minst gebruikelijke) manier is om de zinsbouw van een functie te gebruiken:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-e61f054489678d6caede1ccf309de2190c7af312\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-e61f054489678d6caede1ccf309de2190c7af312_1) \>>> Tijd.print\_tijd(start)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-e61f054489678d6caede1ccf309de2190c7af312_2) 09:45:00
> 
> Bij deze manier van puntnotatie is tijd de naam van de klasse en print\_tijd de naam van de methode. start is meegegeven als een parameter.
> 
> De tweede (en beknoptere) manier is om de zinsbouw van een methode te gebruiken:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-f75b2e3ac8659fabf9bc01c98db6566e561fa4d7\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-f75b2e3ac8659fabf9bc01c98db6566e561fa4d7_1) \>>> start.print\_tijd()
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-f75b2e3ac8659fabf9bc01c98db6566e561fa4d7_2) 09:45:00
> 
> Bij deze manier van puntnotatie is print\_tijd de naam van de methode (nogmaals) en start is het object waarvan de methode is aangeroepen; dit wordt het onderwerp genoemd. Net zoals het onderwerp van een zin inhoudt waar de zin over gaat, gaat het onderwerp van een methodeaanroep, over dat waar de methode over gaat.
> 
> In de methode wordt het onderwerp toegekend aan de eerste parameter, dus in dit geval is start toegekend aan tijd.
> 
> Volgens afspraak wordt de eerste parameter van een methode self genoemd, zodat het gebruikelijker is om print\_tijd op deze manier te schrijven:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-1db32bff9f842e006f64926ceab0882a536d1346\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1db32bff9f842e006f64926ceab0882a536d1346_1) class tijd(object):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1db32bff9f842e006f64926ceab0882a536d1346_2)        def print\_tijd(self):
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1db32bff9f842e006f64926ceab0882a536d1346_3)             print '%.2d:%.2d:%.2d' % (self.uur, self.minuut, self.seconde)
> 
> De reden voor deze afpraak is een impliciete metafoor:
> 
> -   • De zinsbouw voor een functieaanroep, print\_time(start), suggereert dat de functie een actieve agent is. Deze zegt zoiets als, "Hé print\_tijd! Hier heb je een object om te printen".  
>       
>     • Bij object-geörienteerd programmeren zijn de objecten de actieve agenten. Een methode aanroep als start.print\_tijd() zegt "Hé start! Print jezelf alsjeblieft".
>     
> 
> Deze verandering van perspectief is misschien beleefder, maar het ligt niet voor de hand dat deze nuttiger is. In de voorbeelden die we tot nu toe gezien hebben, is dat wellicht niet zo. Maar soms maakt het verplaatsen van de verantwoordelijkheid van functies naar objecten het mogelijk om functies te schrijven die breder inzetbaar zijn en het maakt het gemakkelijker om code te onderhouden en te hergebruiken.
> 
> **Oefening 17.1** Herschrijf tijd\_naar\_int (van paragraaf 16.4) als een methode. Waarschijnlijk is int\_to\_tijd niet geschikt om te herschrijven als een methode, het is niet duidelijk welk object je moet aanroepen!
> 
> ## 17.3 Nog een voorbeeld
> 
> Hierbij de versie van verhoging (uit paragraaf 16.3) herschreven als een methode:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-5a4f21ce78d6f03b545efa9ab07244b5b1c976a4\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-5a4f21ce78d6f03b545efa9ab07244b5b1c976a4_1) \# In de klasse tijd:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-5a4f21ce78d6f03b545efa9ab07244b5b1c976a4_2)        def verhoging(tijd, seconden):
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-5a4f21ce78d6f03b545efa9ab07244b5b1c976a4_3)             seconden += self.tijd\_naar\_int()
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-5a4f21ce78d6f03b545efa9ab07244b5b1c976a4_4)             return int\_naar\_tijd(seconden)
> 
> Deze versie veronderstelt dat tijd\_naar\_int als een methode is geschreven, net zoals in Oefening 17.1. Merk ook op dat dit een pure functie is, dus geen veranderaar.
> 
> Op deze manier roep je verhoging aan:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-63aba79ed70a3db196f2a1163666b28476d6c882\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-63aba79ed70a3db196f2a1163666b28476d6c882_1) \>>> start.print\_tijd()
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-63aba79ed70a3db196f2a1163666b28476d6c882_2) 09:45:00
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-63aba79ed70a3db196f2a1163666b28476d6c882_3) \>>> einde = start.verhoging(1337)
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-63aba79ed70a3db196f2a1163666b28476d6c882_4) \>>> einde.print\_tijd()
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-63aba79ed70a3db196f2a1163666b28476d6c882_5) 10:07:17
> 
> Het onderwerp start wordt toegekend aan de eerste parameter, self. Het argument, 1337, wordt toegekend aan de tweede parameter, seconden.
> 
> Dit mechanisme kan verwarrend zijn, zeker wanneer u een fout maakt. Bijvoorbeeld: roept u verhoging aan met twee argumenten, dan krijgt u:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-f57b5105caea71c5817e51e4d211acebb216d69f\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-f57b5105caea71c5817e51e4d211acebb216d69f_1) \>>> einde = start.verhoging(1337, 460)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-f57b5105caea71c5817e51e4d211acebb216d69f_2) TypeError: verhoging() takes exactly 2 arguments (3 given)
> 
> Deze foutmelding is op het eerste gezicht verwarrend, omdat er tussen de haakjes slechts twee argumenten staan. Maar het onderwerp wordt ook beschouwd als een argument en dat maakt totaal drie.
> 
> ## 17.4 Een ingewikkelder voorbeeld
> 
> is\_na (uit Oefening 16.2) is iets ingewikkelder omdat het twee Tijd objecten meekrijgt als parameters. In dit geval is het gebruikelijk om de eerste parameter self te noemen, de tweede parameter other:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-b862255338ced88f48ca80c6c3a33640cfbf3b8d\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-b862255338ced88f48ca80c6c3a33640cfbf3b8d_1) \# in klasse tijd:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-b862255338ced88f48ca80c6c3a33640cfbf3b8d_2)        def is\_na(self, other):
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-b862255338ced88f48ca80c6c3a33640cfbf3b8d_3)            return self.tijd\_naar\_int() > other.tijd\_naar\_int()
> 
> Om deze methode te gebruiken, moet u die door middel van één object aanroepen en het andere object als argument meegeven:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-3ba66dc2db7c7c9256769e999faab873b77a7e93\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-3ba66dc2db7c7c9256769e999faab873b77a7e93_1) \>>> einde.is\_na(start)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-3ba66dc2db7c7c9256769e999faab873b77a7e93_2) True
> 
> Het leuke aan deze zinsbouw is dat het bijna leest als Nederlands: "einde is na start"?
> 
> ## 17.5 De init methode
> 
> De init methode (afkorting voor “initialization” (_initialisatie_)) is een speciale methode die wordt aangeroepen wanneer een object wordt geïnitialiseerd. De volledige naam is \_\_init\_\_ twee onderlijningtekens gevolgd door init en vervolgens nogmaals twee onderlijningtekens. Een init methode voor de klasse Tijd kan er zo uit zien:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-8b9d788564a6edd366d980e0fddb74b5cec01752\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-8b9d788564a6edd366d980e0fddb74b5cec01752_1) \# inside class Tijd:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-8b9d788564a6edd366d980e0fddb74b5cec01752_2)        def \_\_init\_\_(self, uur\=0, minuut\=0, seconde\=0):
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-8b9d788564a6edd366d980e0fddb74b5cec01752_3)            self.uur = uur
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-8b9d788564a6edd366d980e0fddb74b5cec01752_4)            self.minuut = minuut
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-8b9d788564a6edd366d980e0fddb74b5cec01752_5)            self.seconde = seconde
> 
> Het is gebruikelijk dat de parameters van \_\_init\_\_ dezelfde namen hebben als hun attributen. De instructie
> 
> -   self.uur = uur
>     
> 
> slaat de waarde van de parameter uur op als een attribuut van self.
> 
> De parameters zijn optioneel, dus als u Tijd zonder argumenten aanroept krijgt u de standaardwaarden.
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-7c415210455efc565f100de31a1e1039c5261369\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-7c415210455efc565f100de31a1e1039c5261369_1) \>>> tijd = Tijd()
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-7c415210455efc565f100de31a1e1039c5261369_2) \>>> tijd.print\_tijd()
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-7c415210455efc565f100de31a1e1039c5261369_3) 00:00:00
> 
> Als u één argument meegeeft wordt uur overschreven:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-9f5b0313f83561452f5239480edafa030a0527db\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9f5b0313f83561452f5239480edafa030a0527db_1) \>>> tijd = Tijd(9)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9f5b0313f83561452f5239480edafa030a0527db_2) \>>> tijd.print\_tijd()
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9f5b0313f83561452f5239480edafa030a0527db_3) 09:00:00
> 
> Geeft u twee argumenten mee, dan overschrijven ze uur en minuut.
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-c7f639312fa977d7c41ca9028bf285be7406b38e\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-c7f639312fa977d7c41ca9028bf285be7406b38e_1) \>>> tijd = Tijd(9, 45)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-c7f639312fa977d7c41ca9028bf285be7406b38e_2) \>>> tijd.print\_tijd()
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-c7f639312fa977d7c41ca9028bf285be7406b38e_3) 09:45:00
> 
> En geeft u drie argumenten mee, dan overschrijven ze alle drie de standaardwaarden.
> 
> **Oefening 17.2** Schrijf een init methode voor de klasse Punt die x en y als optionele parameters mee krijgt en deze toekent aan de overeenkomstige attributen.
> 
> ## 17.6 De str methode
> 
> \_\_str\_\_ is een speciale methode, net zoals \_\_init\_\_, die verondersteld wordt om een stringrepresentatie van een object terug te geven.
> 
> Hierbij een voorbeeld van een str methode voor Tijd objecten:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-1ab8b6c0eca5733771e080d970052ff766c36d31\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1ab8b6c0eca5733771e080d970052ff766c36d31_1) \# in class Tijd:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1ab8b6c0eca5733771e080d970052ff766c36d31_2)      def \_\_str\_\_(self):
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1ab8b6c0eca5733771e080d970052ff766c36d31_3)            return '%.2d:%.2d:%.2d' % (self.uur, self.minuut, self.seconde)
> 
> Wanneer u een object print gebruikt, roept Python de str methode aan:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-1e64a972d02831b2ecb129f9a96d85b90956f132\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1e64a972d02831b2ecb129f9a96d85b90956f132_1) \>>> tijd = Tijd(9, 45)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1e64a972d02831b2ecb129f9a96d85b90956f132_2) \>>> print tijd 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1e64a972d02831b2ecb129f9a96d85b90956f132_3) 09:45:00
> 
> Wanneer ik een nieuwe klasse schrijf, begin ik bijna altijd met \_\_init\_\_ te schrijven, dat maakt het gemakkelijker om objecten en \_\_str\_\_ te concretiseren en dat is handig bij het debuggen.
> 
> **Oefening 17.3** Schrijf een str methode voor de klasse Punt. Maak een Punt object en print deze.
> 
> ## 17.7 Operator overbelasting
> 
> Door andere speciale methodes te definiëren, kunt u het gedrag van operators bij door gebruiker gedefinieerde types specificeren. Bijvoorbeeld: definieert u een methode genaamd \_\_add\_\_ voor de klasse Tijd, dan kunt u de + operator gebruiken op Tijdobjecten.
> 
> Zie hieronder hoe een definitie eruit kan zien:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-95cb818b80f43498e22b33736a7c7c0ca847ddde\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-95cb818b80f43498e22b33736a7c7c0ca847ddde_1) \# in klasse Tijd:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-95cb818b80f43498e22b33736a7c7c0ca847ddde_2)      def \_\_add\_\_(self, andere):
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-95cb818b80f43498e22b33736a7c7c0ca847ddde_3)            seconden = self.tijd\_naar\_int() + andere.tijd\_naar\_int()
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-95cb818b80f43498e22b33736a7c7c0ca847ddde_4)            return int\_naar\_tijd(seconden )
> 
> En zo kunt u deze toepassen:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-37131c8b728de2e361ea2e82ea6ac91699f25cb2\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-37131c8b728de2e361ea2e82ea6ac91699f25cb2_1) \>>> start = Tijd(9, 45)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-37131c8b728de2e361ea2e82ea6ac91699f25cb2_2) \>>> duur = Tijd(1, 35)
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-37131c8b728de2e361ea2e82ea6ac91699f25cb2_3) \>>> print start + duur
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-37131c8b728de2e361ea2e82ea6ac91699f25cb2_4) 11:20:00
> 
> Past u de + operator toe op Tijdobjecten, dan zal Python \_\_add\_\_ aanroepen. Drukt u het resultaat af, dan roept Python \_\_str\_\_ aan. Er gebeurt dus heel wat achter de coulissen!
> 
> Het gedrag van een operator veranderen, zodat deze werkt met een door gebruiker gedefinieerd type, wordt **operator overbelasting** genoemd. Voor elke operator in Python bestaat een overeenkomstige speciale methode zoals \_\_add\_\_. Meer details zijn te vinden bij [docs.python.org/ref/specialnames.html](http://docs.python.org/ref/specialnames.html).
> 
> **Oefening 17.4** Schrijf een {{{add} methode voor de klasse Punt.
> 
> ## 17.8 Type-gebaseerd versturen
> 
> In de voorgaande paragraaf hebben we twee Timeobjecten toegevoegd maar u zou wellicht een geheel getal willen toevoegen aan een Tijdobject. De volgende versie van \_\_add\_\_ controleert het type van other en roept of voeg\_tijd\_toe of verhoging aan:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-9d716b644adc571fc0d023297833f5a182d17df4\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_1) \# in klasse Tijd:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_2) 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_3)      def \_\_add\_\_(self, other):
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_4)           if isinstance(other, Tijd):
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_5)                 return self.voeg\_tijd\_toe(other)
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_6)           else:
>  [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_7)                 return self.verhoging(other)
>  [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_8) 
>  [9](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_9)      def add\_tijd(self, other):
>  [10](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_10)           seconden = self.tijd\_naar\_int() + other.tijd\_naar\_int()
>  [11](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_11)           return int\_naar\_tijd(seconden)
>  [12](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_12) 
>  [13](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_13)      def verhoging(self, seconden):
>  [14](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_14)           seconden += self.tijd\_naar\_int()
>  [15](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-9d716b644adc571fc0d023297833f5a182d17df4_15)           return int\_naar\_tijd(seconden)
> 
> De ingebouwde functie isinstance krijgt een waarde en een klasseobject mee en geeft True terug als de waarde een instantie van een klasse is.
> 
> Is other een Tijdobject, dan roept \_\_add\_\_, add\_tijd aan. Anders wordt aangenomen dat de parameter een getal is en roept deze verhoging aan. Deze operatie wordt **type-gebaseerd versturen** genoemd, omdat deze de berekening naar een andere methode verstuurt, gebaseerd op het type van de argumenten.
> 
> Hierbij de voorbeelden die de + operator gebruiken met verschillende typen:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-1932f644f734e0260478c4edc48ea13dfd3ed878\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1932f644f734e0260478c4edc48ea13dfd3ed878_1) \>>> start = Tijd(9, 45)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1932f644f734e0260478c4edc48ea13dfd3ed878_2) \>>> duur = Tijd(1, 35)
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1932f644f734e0260478c4edc48ea13dfd3ed878_3) \>>> print start + duur
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1932f644f734e0260478c4edc48ea13dfd3ed878_4) 11:20:00
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1932f644f734e0260478c4edc48ea13dfd3ed878_5) \>>> print start + 1337
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-1932f644f734e0260478c4edc48ea13dfd3ed878_6) 10:07:17
> 
> Helaas is deze inrichting van de optelling niet verwisselbaar. Is een geheel getal de eerste operand dan krijgt u:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-577dcb7cd8b5c6869894c248d9fd9bfe75f77227\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-577dcb7cd8b5c6869894c248d9fd9bfe75f77227_1) \>>> print 1337 + start
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-577dcb7cd8b5c6869894c248d9fd9bfe75f77227_2) TypeError: unsupported operand type(s) for +: 'int' and 'instance'
> 
> Het probleem is, dat in plaats van te vragen aan het Tijdobject een geheel getal op te tellen, vraagt Python aan een geheel getal om een Tijdobject op te tellen en deze weet niet hoe dat moet. Maar er bestaat een slimme oplossing voor dit probleem: de speciale methode \_\_radd\_\_; dit staat voor "right-side add" (aan de rechterkant toevoegen). Deze methode wordt aangeroepen als een Tijdobject aan de rechterkant verschijnt van de + operator. Hierbij de definitie:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-24e5519e9cc7214968ecf8d352867c0519d2aa6b\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-24e5519e9cc7214968ecf8d352867c0519d2aa6b_1) \# in klasse Tijd:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-24e5519e9cc7214968ecf8d352867c0519d2aa6b_2)      def \_\_radd\_\_(self, other):
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-24e5519e9cc7214968ecf8d352867c0519d2aa6b_3)            return self.\_\_add\_\_(other)
> 
> En zo wordt deze toegepast:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-de006bbca9c06b6021f214055f568d02d686868c\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-de006bbca9c06b6021f214055f568d02d686868c_1) \>>> print 1337 + start
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-de006bbca9c06b6021f214055f568d02d686868c_2) 10:07:17
> 
> **Oefening 17.5** Schrijf een add methode voor Punten die of voor een Puntobject of voor een tupel werkt:
> 
> -   • Is de tweede operand een Punt, dan moet de methode een nieuw Punt teruggeven waarbij de _x_ coördinaat de som is van de _x_ coördinaten van de operands en voor de _y_ coördinaten geldt hetzelfde.  
>       
>     • Is de tweede operand een tupel, dan moet de methode het eerste element van de tupel optellen bij de _x_ coördinaat en het tweede element optellen bij de _y_ coördinaat en een nieuw Punt teruggeven met het resultaat.
>     
> 
> ## 17.9 Polymorfisme
> 
> Type-gebaseerd versturen is handig als u het nodig hebt maar (gelukkig) is dit niet altijd nodig. U kunt dit vaak voorkomen door functies te schrijven die correct omgaan met argumenten van verschillende typen.
> 
> Veel van de functies die we hebben geschreven voor strings zullen werken voor elk soort reeksen. Bijvoorbeeld: in paragraaf 11.1 hebben we histogram gebruikt om het aantal keren te tellen dat een letter voorkomt in een woord.
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-4bd7043938e11c04d36b6263ae8319f265784bc0\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-4bd7043938e11c04d36b6263ae8319f265784bc0_1) def histogram(s):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-4bd7043938e11c04d36b6263ae8319f265784bc0_2)      d = woordenboek()
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-4bd7043938e11c04d36b6263ae8319f265784bc0_3)      for c in s:
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-4bd7043938e11c04d36b6263ae8319f265784bc0_4)            if c not in d:
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-4bd7043938e11c04d36b6263ae8319f265784bc0_5)                 d\[c\] = 1
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-4bd7043938e11c04d36b6263ae8319f265784bc0_6)            else:
>  [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-4bd7043938e11c04d36b6263ae8319f265784bc0_7)                 d\[c\] = d\[c\]+1
>  [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-4bd7043938e11c04d36b6263ae8319f265784bc0_8)      return d
> 
> Deze functie werkt ook voor lijsten, tupels en zelfs voor woordenboeken, zolang als de elementen van s te hashen zijn, zodat deze bruikbaar zijn als sleutels in d.
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-d78d0c5f825a3e0a7160c0aea884efdbe7707f2f\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-d78d0c5f825a3e0a7160c0aea884efdbe7707f2f_1) \>>> t = \['spam', 'ei', 'spam', 'spam', 'ham', 'spam'\]
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-d78d0c5f825a3e0a7160c0aea884efdbe7707f2f_2) \>>> histogram(t)
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-d78d0c5f825a3e0a7160c0aea884efdbe7707f2f_3) {'ham': 1, 'ei': 1, 'spam': 4}
> 
> Functies die werken met verschillende typen worden polymorf (veelvormig) genoemd. Polymorfisme kan hergebruik van code ondersteunen. Bijvoorbeeld de ingebouwde functie sum; deze telt elementen uit een reeks op en werkt zolang de elementen uit de reeks het optellen ondersteunen.
> 
> Aangezien Tijdobjecten een add methode leveren werken ze met sum:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-950a4cfdd1580dea7448c5839ef331bfed22d469\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-950a4cfdd1580dea7448c5839ef331bfed22d469_1) \>>> t1 = Tijd (7, 43)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-950a4cfdd1580dea7448c5839ef331bfed22d469_2) \>>> t2 = Tijd (7, 41)
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-950a4cfdd1580dea7448c5839ef331bfed22d469_3) \>>> t3 = Tijd (7, 37)
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-950a4cfdd1580dea7448c5839ef331bfed22d469_4) \>>> totaal = sum(\[t1, t2, t3\])
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-950a4cfdd1580dea7448c5839ef331bfed22d469_5) \>>> print totaal
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-950a4cfdd1580dea7448c5839ef331bfed22d469_6) 23:01:00
> 
> In het algemeen geldt dat als alle operaties in een functie werken met een gegeven type, dan werkt de functie met dat type.
> 
> De beste soort Polymorfisme is de onbedoelde soort, waarbij u ontdekt dat een functie, die u al geschreven had, kan worden gebruikt voor een type dat niet gepland was.
> 
> ## 17.10 Debuggen
> 
> Attributen toevoegen aan objecten is toegestaan op iedere plaats in het programma waar code wordt uitgevoerd, maar bent u een voorstander van de typetheorie, dan is het een dubieuze praktijk om objecten te hebben van hetzelfde type, met verschillende sets aan attributen. Een doorgaans goed idee is het initialiseren van alle attributen voor objecten met de init methode.
> 
> Weet u niet zeker of een object een specifiek attribuut heeft, dan kunt u de ingebouwde functie hasattr gebruiken (zie paragraaf 15.7).
> 
> Een andere manier van benaderen van attributen van een object is via het speciale attribuut \_\_dict\_\_; dit is een woordenboek die attribuutnamen (als strings) koppelt aan waarden:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-ef3c84d2e479dbfef5362050fa24b8aa4eb0cb13\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-ef3c84d2e479dbfef5362050fa24b8aa4eb0cb13_1) \>>> p = Punt(3, 4)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-ef3c84d2e479dbfef5362050fa24b8aa4eb0cb13_2) \>>> print p.\_\_dict\_\_
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-ef3c84d2e479dbfef5362050fa24b8aa4eb0cb13_3) {'y': 4, 'x': 3}
> 
> Voor debug doeleinden zult u het wellicht handig vinden om deze functie bij de hand te hebben:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-a6918f05450e30197d18d8f3968e7f41a6bd14ce\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-a6918f05450e30197d18d8f3968e7f41a6bd14ce_1) def print\_attributen(obj):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-a6918f05450e30197d18d8f3968e7f41a6bd14ce_2)       for attr in obj.\_\_dict\_\_:
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-a6918f05450e30197d18d8f3968e7f41a6bd14ce_3)            print attr, getattr(obj, attr)
> 
> print\_attributen doorloopt de items in het woordenboek met de objecten en drukt elke attribuutnaam af met zijn overeenkomstige waarde.
> 
> De ingebouwde functie getattr krijgt een object mee en een attribuutnaam (als een string) en geeft de waarde van het attribuut terug.
> 
> ## 17.11 Woordenlijst
> 
> **object-georiënteerde taal**: Een taal die mogelijkheden biedt zoals een zinsbouw voor door de gebruiker gedefinieerde klassen en methodes, die object-georiënteerd programmeren ondersteunt.
> 
> **object-georiënteerd programmeren**: Een manier van programmeren waarbij gegevens en de operaties, die deze bewerken, zijn georganiseerd in klassen en methodes.
> 
> **methode**: Een functie die in een klassedefinitie wordt gedefinieerd en wordt aangeroepen op verzoek van die klasse.
> 
> **onderwerp**: Het object waarmee een methode wordt aangeroepen.
> 
> **operator overbelasting**: Het gedrag van een operator, zoals +, veranderen, zodanig dat deze werkt met een door de gebruiker gedefinieerd type.
> 
> **type-gebaseerd versturen**: Een programmeerpatroon dat het type van een operand controleert en verschillende functies aanroept voor verschillende types.
> 
> **Polymorfisme**: Heeft betrekking op een functie die kan werken met meerdere typen.
> 
> ## 17.12 Oefeningen
> 
> **Oefening 17.6** Deze Oefening is een waarschuwing voor één van de meest voorkomende, en moeilijk te vinden, fouten in Python.
> 
> 1.  Schrijf een definitie voor een klasse genaamd Kangoeroe met de volgende methoden:
>     
>     -   (a) Een \_\_init\_\_ methode die een attribuut genaamd inhoud\_buidel als een lege lijst initialiseert.  
>         (b) Een methode genaamd stop\_in\_buidel die een object van een willekeurig type meekrijgt en deze aan inhoud\_buidel toevoegt.  
>         (c) Een \_\_str\_\_ methode die een string weergave van het Kangoeroe object teruggeeft en de inhoud van de buidel.  
>           
>         
>         Test uw code door twee Kangoeroe objecten aan te maken; deze toe te kennen aan de variabelen genaamd kangoe and roe en daarna roe toe te voegen aan de inhoud van de buidel van kangoe.
>         
> 2.  Download [thinkpython.com/code/BadKangaroo.py](http://thinkpython.com/code/BadKangaroo.py). Dit bevat een oplossing voor het voorgaande probleem maar dan met een grote vervelende fout. Zoek de fout op en verbeter die. Loopt u vast dan kunt u [thinkpython.com/code/GoodKangaroo.py](http://thinkpython.com/code/GoodKangaroo.py) downloaden; deze legt het probleem uit en laat een oplossing zien.
>     
> 
> **Oefening 17.7** Visual is een Pythonmodule die 3-D plaatjes levert. Deze wordt niet altijd meegeleverd bij de Python installatie. Het kan dus zijn dat u deze moet installeren vanuit de software bibliotheek of vanaf [vpython.org](http://vpython.org).
> 
> Het volgende voorbeeld maakt een 3-D ruimte aan die 256 units breed, lang en hoog is en het plaatst het "centrum" op het punt (128, 128, 128). Daarna tekent deze code een blauwe bol.
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-61609f751c404baed49547c1869ecd89e72d3aec\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-61609f751c404baed49547c1869ecd89e72d3aec_1) from visual import \*
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-61609f751c404baed49547c1869ecd89e72d3aec_2) 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-61609f751c404baed49547c1869ecd89e72d3aec_3) scene.range = (256, 256, 256)
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-61609f751c404baed49547c1869ecd89e72d3aec_4) scene.centrum = (128, 128, 128)
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-61609f751c404baed49547c1869ecd89e72d3aec_5) 
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-61609f751c404baed49547c1869ecd89e72d3aec_6) kleur = (0.1, 0.1, 0.9)                      \# voornamelijk blauw
>  [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-61609f751c404baed49547c1869ecd89e72d3aec_7) sphere(pos\=scene.centrum, radius\=128, color\=kleur)
> 
> color is een RGB tupel, dat wil zeggen, de elementen zijn Rood-Groen-Blauw met niveaus tussen 0.0 en 1.0 (Zie [nl.wikipedia.org/wiki/RGB-kleursysteem](http://nl.wikipedia.org/wiki/RGB-kleursysteem)).
> 
> Draait u deze code, dan ziet u een venster met een zwarte achtergrond en een blauwe bol. Draait u het scrollwieltje van de muis dan zoomt u in of uit. U kunt één en ander laten roteren door te slepen met de rechtermuisknop ingedrukt, maar met maar één bol op het scherm is het lastig om enig verschil te zien.
> 
> De volgende lus maakt een kubus van de bollen:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-3ba72d3d5a2959d657b176cb192c164e0543a8f8\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-3ba72d3d5a2959d657b176cb192c164e0543a8f8_1) t = range(0, 256, 51)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-3ba72d3d5a2959d657b176cb192c164e0543a8f8_2) for x in t:
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-3ba72d3d5a2959d657b176cb192c164e0543a8f8_3)       for y in t:
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-3ba72d3d5a2959d657b176cb192c164e0543a8f8_4)            for z in t:
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-3ba72d3d5a2959d657b176cb192c164e0543a8f8_5)                  pos = x, y, z
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZeventien#CA-3ba72d3d5a2959d657b176cb192c164e0543a8f8_6)                  sphere(pos\=pos, radius\=10, color\=kleur)
> 
> 1.  Plaats deze code in een script en zorg ervoor dat dat werkt.
> 2.  Pas het programma zodanig aan dat elke bol in de kubus de kleur heeft aangenomen die overeenkomt met zijn positie in de RGB ruimte. Let erop dat de coördinaten in het bereik van 0–255 vallen, maar de RGB tupels vallen in het bereik van 0.0–1.0.
> 3.  Download [thinkpython.com/code/color\_list.py](http://thinkpython.com/code/color_list.py) en gebruik de functie read\_colors om een lijst met beschikbare kleuren, hun namen en RGB waarden op uw systeem aan te maken. Teken voor elke genoemde kleur een bol in de positie die overeenkomt met zijn RGB waarden.
>     
> 
> Mijn oplossing is te zien op [thinkpython.com/code/color\_space.py](http://thinkpython.com/code/color_space.py).