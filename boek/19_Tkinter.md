[community/ThinkPython/HoofdstukNegentien - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien)

# Hoofdstuk 19 Case study: Tkinter

## 19.1 GUI

De meeste programma's die we tot nu toe hebben gezien, zijn tekst-gebaseerd. Maar veel programma's gebruiken een **grafische gebruikers interface**, ook bekend als **GUI** (Graphical User Interface).

Python biedt verschillende keuzes voor het schrijven van GUI-gebaseerde programma's. Hiervoor zijn onder andere Tkinter, wxPython en Qt beschikbaar. Elk van deze modules heeft zijn voors en tegens, vandaar dat er bij Python niet gekozen is voor één standaard.

In dit hoofdstuk wil ik Tkinter presenteren, omdat deze het eenvoudigste is om te starten. Het merendeel van de concepten in dit hoofdstuk is ook van toepassing op de andere GUI modules.

Tkinter is beschreven in verschillende boeken en op legio websites. Een van de beste online bronnen is _An Introduction to Tkinter_ door Fredrik Lundh.

Ik heb een module geschreven genaamd Gui.py, deze komt met Swampy mee. De module levert een vereenvoudigde interface naar de functies en klassen van Tkinter. De voorbeelden in dit hoofdstuk zijn gebaseerd op deze module.

Hierbij een voorbeeld dat een GUI aanmaakt en weergeeft:

Het aanmaken van een GUI vereist het importeren van GUI en het concretiseren van een GUI object:

function isnumbered(obj) { return obj.childNodes.length && obj.firstChild.childNodes.length && obj.firstChild.firstChild.className == 'LineNumber'; } function nformat(num,chrs,add) { var nlen = Math.max(0,chrs-(''+num).length), res = ''; while (nlen>0) { res += ' '; nlen-- } return res+num+add; } function addnumber(did, nstart, nstep) { var c = document.getElementById(did), l = c.firstChild, n = 1; if (!isnumbered(c)) { if (typeof nstart == 'undefined') nstart = 1; if (typeof nstep == 'undefined') nstep = 1; var n = nstart; while (l != null) { if (l.tagName == 'SPAN') { var s = document.createElement('SPAN'); var a = document.createElement('A'); s.className = 'LineNumber'; a.appendChild(document.createTextNode(nformat(n,4,''))); a.href = '#' + did + '\_' + n; s.appendChild(a); s.appendChild(document.createTextNode(' ')); n += nstep; if (l.childNodes.length) { l.insertBefore(s, l.firstChild); } else { l.appendChild(s); } } l = l.nextSibling; } } return false; } function remnumber(did) { var c = document.getElementById(did), l = c.firstChild; if (isnumbered(c)) { while (l != null) { if (l.tagName == 'SPAN' && l.firstChild.className == 'LineNumber') l.removeChild(l.firstChild); l = l.nextSibling; } } return false; } function togglenumber(did, nstart, nstep) { var c = document.getElementById(did); if (isnumbered(c)) { remnumber(did); } else { addnumber(did,nstart,nstep); } return false; } document.write('<a href="#" onclick="return togglenumber(\\'CA-6b50fca772f335b0f897fe4aee222ce97c526d4a\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-6b50fca772f335b0f897fe4aee222ce97c526d4a_1) from Gui import \*
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-6b50fca772f335b0f897fe4aee222ce97c526d4a_2) g = Gui()
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-6b50fca772f335b0f897fe4aee222ce97c526d4a_3) g.title('GUI')
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-6b50fca772f335b0f897fe4aee222ce97c526d4a_4) g.mainloop()

Zodra u deze code uitvoert, moet er een venster verschijnen met een leeg grijs vierkant en de titel GUI. De methode mainloop draait de **event loop** (gebeurtenis lus). Er wordt gewacht op een actie van de gebruiker en vervolgens zal dienovereenkomstig worden gereageerd. Dit is een oneindige lus, die blijft draaien totdat de gebruiker het venster sluit, of Ctrl-c indrukt, of iets anders doet dat zorgt dat het programma stopt.

Deze Gui doet niet zoveel omdat het geen widgets (dingetjes) heeft. Widgets zijn de elementen die een GUI body geven. Hieronder worden er een aantal genoemd:

**Knop (Button)**: Een widget dat tekst of een plaatje bevat en een actie uitvoert zodra erop gedrukt wordt.

**Doek (Canvas)**: Een gebied dat lijnen, rechthoeken, cirkels en andere vormen weer kan geven.

**Veld (Entry)**: Een plaats waar gebruikers tekst kunnen intypen.

**Schuifbalk (Scrollbar)**: Een widget dat het zichtbare gedeelte van een ander widget controleert.

**Raamwerk (Frame)**: Een container, vaak onzichtbaar, die andere widgets bevat.

Het lege grijze vierkant dat u ziet na het aanmaken van een GUI is een raamwerk. Zodra u een nieuw widget aanmaakt, wordt dit aan het raamwerk toegevoegd.

## 19.2 Knoppen en terugroepen

De methode bu maakt een widget van het type knop:

knop = g.bu(text='Druk me in')

De resultaatwaarde van bu is een knop-object. De knop die verschijnt in het raamwerk is een grafische weergave van dit object. U kunt de knop controleren door middel van het aanroepen van methoden.

De methode bu kan tot 32 parameters meekrijgen die het voorkomen en de functie van een knop controleren. Deze parameters worden opties genoemd. In plaats van waarden aan te leveren voor alle 32 opties, kunt u argumenten in de vorm van sleutelwoorden gebruiken, zoals text='Druk me in', om alleen de afwijkende opties te specificeren en voor de overige de standaardwaarden te gebruiken.

Zodra u een widget toevoegt aan een raamwerk wordt dit in "krimpfolie verpakt"; dat wil zegggen, het raamwerk krimpt tot aan de omvang van het widget. Voegt u meer widgets toe dan zal het raamwerk groeien om deze een plaats te geven.

De methode la maakt een widget van het type label:

label = g.la(text='Druk op de knop')

Standaard zal Tkinter de widgets van boven naar beneden stapelen en in het midden neerzetten. Zo dadelijk zullen we laten zien hoe we dit kunnen veranderen.

Drukt u op de knop, dan zal er weinig gebeuren. Dat komt omdat u deze niet hebt "aangesloten"; dat wil zeggen, u hebt niet gezegd wat er moet gebeuren!

De optie die het gedrag van een knop controleert is command. De waarde van command is een functie die wordt uitgevoerd als de knop wordt ingedrukt. Hieronder een voorbeeld van een functie die een nieuw Label aanmaakt:

document.write('<a href="#" onclick="return togglenumber(\\'CA-0c93dbf7bf25a7699bc431f798d97e5523eced51\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-0c93dbf7bf25a7699bc431f798d97e5523eced51_1) def make\_label():
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-0c93dbf7bf25a7699bc431f798d97e5523eced51_2)     g.la(text\='Dank u')

Nu kunnen we een knop aanmaken met deze functie als commando:

knop2 = g.bu(text='Nee, druk me in', command=make\_label)

Zodra u op de knop drukt, wordt make\_label uitgevoerd en moet een nieuw label verschijnen.

De waarde van de optie command is een functieobject, dat bekend staat als **terugroep (callback)**, omdat als u bu aanroept om een knop aan te maken, de volgorde van uitvoering wordt "teruggeroepen" als de gebruiker op de knop drukt.

Deze volgorde is kenmerkend voor door **gebeurtenis gedreven (event-driven) programmeren**. Acties van gebruikers, zoals indrukken van knoppen en toetsaanslagen, worden **gebeurtenissen (events)** genoemd. Bij gebeurtenis gedreven programmeren wordt de volgorde van uitvoering bepaald door acties van de gebruiker in plaats van door de programmeur.

De uitdaging van gebeurtenis gedreven programmeren is het construeren van een verzameling van widgets en terugbellers die correct werken (of tenminste juiste foutboodschappen weergeven) voor elke serie acties van de gebruiker.

**Oefening 19.1** Schrijf een programma dat een GUI aanmaakt met één knop. Zodra de knop wordt ingedrukt moet een tweede knop worden gemaakt. Wordt deze knop ingedrukt, dan moet een label worden gemaakt met de tekst: "Keurige klus!"

Wat gebeurt er als u de knop meerdere keren indrukt? U kunt mijn oplossing bekijken op [thinkpython.com/code/button\_demo.py](http://thinkpython.com/code/button_demo.py)

## 19.3 Widgets op het doek

Een van meest veelzijdige widgets is het doek (Canvas). Dit maakt een gebied aan voor het tekenen van lijnen, cirkels en andere vormen. Hebt u oefening 15.4 gemaakt? Dan bent u al bekend met het doek.

De methode ca maakt een nieuw doek aan:

canvas = g.ca(width=500, height=500)

width en height zijn de breedte en hoogte van het doek in pixels.

Nadat u een widget hebt gemaakt, kunt u altijd nog de waarden van de opties aanpassen met de config methode. Bijvoorbeeld de bg optie wijzigt de kleur van de achtergrond:

canvas.config(bg='white')

De waarde van bg is een string met de Engelse naam van de kleur. Het rijtje met toegestane namen van kleuren verschilt per uitvoering van Python, maar alle uitvoeringen leveren ten minste:

white       black
red         green      blue
cyan        yellow     magenta

Vormen op het doek worden **items** genoemd. Hieronder tekent de methode circle (u raadt het al) een cirkel:

item = canvas.circle(\[0,0\], 100, fill='red')

Het eerste argument is een paar coördinaten als middelpunt van de cirkel, het tweede argument is de straal.

Gui.py levert een standaard coördinatensysteem zoals we dat kennen uit de wiskunde: met het beginpunt in het midden van het doek en de positieve Y-as die omhoog wijst. Dit verschilt van andere grafische systemen waar het beginpunt zich in de linker bovenhoek bevindt en de Y-as naar beneden wijst.

De fill optie geeft aan dat de cirkel met de kleur rood wordt opgevuld.

De resultaatwaarde vanuit circle is een item-object dat een methode levert voor het aanpassen van het item op het doek. Bijvoorbeeld: u kunt config gebruiken om elke optie van de cirkel te wijzigen:

item.config(fill='yellow', outline='orange', width=10)

width is de dikte van de omtrek in pixels; outline is de kleur ervan.

**Oefening 19.2** Schrijf een programma dat een doek en een knop aanmaakt. Zodra de gebruiker op een knop drukt, moet een cirkel op het doek worden getekend.

## 19.4 Reeksen coördinaten

De rectangle methode krijgt een reeks coördinaten mee, die de tegenoverliggende hoeken van een rechthoek specificeren. Het volgende voorbeeld tekent een groene rechthoek met de linker onderhoek op de oorsprong en de rechter bovenhoek op (200, 100):

document.write('<a href="#" onclick="return togglenumber(\\'CA-a90e45a8aeaa9347c613843444ad1573de29b3e8\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a90e45a8aeaa9347c613843444ad1573de29b3e8_1) canvas.rectangle(\[\[0, 0\], \[200, 100\]\],
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a90e45a8aeaa9347c613843444ad1573de29b3e8_2)                   fill\='blue', outline\='orange', width\=10)

Deze manier van het benoemen van hoeken wordt **begrensde doos (bounding box)** genoemd omdat de twee punten de rechthoek begrenzen.

De methode oval krijgt een begrensde doos mee en tekent een ovaal binnen de gespecificeerde rechthoek:

canvas.oval(\[\[0, 0\], \[200, 100\]\], outline='orange', width=10)

De methode line krijgt een reeks coördinaten mee en tekent een lijn die de punten met elkaar verbindt. Dit voorbeeld tekent twee lijnen van een driehoek:

canvas.line(\[\[0, 100\], \[100, 200\], \[200, 100\]\], width=10)

De methode polygon krijgt dezelfde argumenten maar tekent de laatste lijn van de veelhoek (indien noodzakelijk) en kleurt deze in:

document.write('<a href="#" onclick="return togglenumber(\\'CA-e065f179818ecb16b779ff395d3293119047c1f3\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-e065f179818ecb16b779ff395d3293119047c1f3_1) canvas.polygon(\[\[0, 100\], \[100, 200\], \[200, 100\]\],
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-e065f179818ecb16b779ff395d3293119047c1f3_2)                  fill\='red', outline\='orange', width\=10)

## 19.5 Meer widgets

Tkinter levert twee widgets zodat de gebruikers teksten kan typen: een Entry widget, deze heeft één enkele regel en een Text widget, deze heeft meerdere regels.

De methode en maakt een nieuwe Entry:

entry = g.en(text='standaard tekst')

De optie text biedt de mogelijkheid om tekst in de Entry op te voeren zodra deze is aangemaakt. De methode get geeft de inhoud van de Entry terug (deze kan gewijzigd zijn door de gebruiker):

document.write('<a href="#" onclick="return togglenumber(\\'CA-db4b8c5c8b24a16ce6f1fe3401284f74e1e6e116\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-db4b8c5c8b24a16ce6f1fe3401284f74e1e6e116_1) \>>> entry.get()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-db4b8c5c8b24a16ce6f1fe3401284f74e1e6e116_2) 'standaard tekst'

De methode te maakt een Text widget aan:

text = g.te(width=100, height=5)

width en height zijn de afmetingen van de widget in tekens en regels.

De methode insert plaatst tekst in het Text widget:

text.insert(END, 'een regel met tekst\\n')

END is een speciale index die het laatste teken aanwijst in het Text widget.

U kunt ook een karakter specificeren via een index met puntnotatie, zoals 1.3; de regelnummers staan voor de punt en het kolomnummer achter de punt. Het volgende voorbeeld voegt de string ' eerste' in na het derde karakter van de eerste regel.

\>>> text.insert(1.3, ' eerste')

De methode get leest de tekst uit het widget met een start- en eindindex als argumenten. Het volgende voorbeeld levert de complete tekst van het widget op:

document.write('<a href="#" onclick="return togglenumber(\\'CA-c77eef211e30c5c85d8f228e2933385010cb4695\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-c77eef211e30c5c85d8f228e2933385010cb4695_1) \>>> text.get(1.0, END)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-c77eef211e30c5c85d8f228e2933385010cb4695_2) 'een eerste regel met tekst'

De methode delete verwijdert tekst uit het widget. Het volgende voorbeeld verwijdert alles, behalve de eerste drie karakters:

document.write('<a href="#" onclick="return togglenumber(\\'CA-4c15d8087fd73b499f2ab795bc15b4de4ac7142d\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-4c15d8087fd73b499f2ab795bc15b4de4ac7142d_1) \>>> text.delete(1.3, END)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-4c15d8087fd73b499f2ab795bc15b4de4ac7142d_2) \>>> text.get(0.0, END)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-4c15d8087fd73b499f2ab795bc15b4de4ac7142d_3) 'een'

**Oefening 19.3** Pas uw oplossing van oefening 19.2 aan, door het toevoegen van een Entry widget en een tweede knop. Zodra de gebruiker op de tweede knop drukt, moet de naam van de ingetypte kleur worden uitgelezen en worden gebruikt om de kleur van de cirkel aan te passen. Gebruik config voor het wijzigen van de bestaande cirkel, maak dus geen nieuwe aan.

Uw programma moet overweg kunnen met het geval dat de gebruiker de kleur van een cirkel probeert te wijzigen, terwijl de cirkel nog niet is aangemaakt. In dat geval is de naam van de kleur niet geldig.

Mijn oplossing is te vinden op [thinkpython.com/code/circle\_demo.py](http://thinkpython.com/code/circle_demo.py).

## 19.6 Widgets inpakken

Tot dusverre hebben we widgets in één enkele kolom opgestapeld maar in de meeste GUI's is de layout complexer. Hieronder ziet u een licht vereenvoudigde versie van TurtleWorld (zie hoofdstuk 4).

-   ![book028.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien?action=AttachFile&do=get&target=book028.png "book028.png")
    

In deze paragraaf komt in een aantal stappen de code aan bod voor het maken van deze GUI. U kunt het complete voorbeeld downloaden van [thinkpython.com/code/SimpleTurtleWorld.py](http://thinkpython.com/code/SimpleTurtleWorld.py).

Op het hoogste niveau bevat deze GUI twee widgets, een Canvas en een Frame, gearrangeerd in een rij. Dus de eerste stap is de rij te creëren:

document.write('<a href="#" onclick="return togglenumber(\\'CA-5dce7adb4e8d0c6c62026560948cd71cbc2e4560\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-5dce7adb4e8d0c6c62026560948cd71cbc2e4560_1) class SimpleTurtleWorld(TurtleWorld):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-5dce7adb4e8d0c6c62026560948cd71cbc2e4560_2)     """Deze klasse is identiek aan TurtleWorld, maar de code
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-5dce7adb4e8d0c6c62026560948cd71cbc2e4560_3)  voor de layout van de GUI is vereenvoudigd, ter verduidelijking"""
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-5dce7adb4e8d0c6c62026560948cd71cbc2e4560_4)     def setup(self):
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-5dce7adb4e8d0c6c62026560948cd71cbc2e4560_5)         self.row()
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-5dce7adb4e8d0c6c62026560948cd71cbc2e4560_6)         ...

De functie setup creëert en arrangeert de widgets. Het arrangeren van widgets in een GUI wordt **packing** genoemd.

De methode row creëert een rij-raamwerk (frame) en maakt dat raamwerk het “huidige raamwerk”. Totdat dit frame wordt gesloten of een ander frame wordt gecreëerd, worden alle volgende widgets aan deze rij toegevoegd.

Hier is de code voor het creëren van het doek en het raamwerk (dat de andere widgets bevat): het Canvas

document.write('<a href="#" onclick="return togglenumber(\\'CA-1842e8ad240f8106ab33580f7bdc4e8ddb9ea27b\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-1842e8ad240f8106ab33580f7bdc4e8ddb9ea27b_1)     self.canvas = self.ca(width\=400, height\=400, bg\='white')
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-1842e8ad240f8106ab33580f7bdc4e8ddb9ea27b_2)     self.col()

Het eerste widget in de kolom is een grid raamwerk, met vier knoppen die twee-aan-twee zijn gearrangeerd.

document.write('<a href="#" onclick="return togglenumber(\\'CA-9bbf08bc5cbdc96fd7cd47e91f45625583e04b04\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-9bbf08bc5cbdc96fd7cd47e91f45625583e04b04_1)     self.gr(cols\=2)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-9bbf08bc5cbdc96fd7cd47e91f45625583e04b04_2)     self.bu(text\='Print canvas', command\=self.canvas.dump)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-9bbf08bc5cbdc96fd7cd47e91f45625583e04b04_3)     self.bu(text\='Quit', command\=self.quit)
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-9bbf08bc5cbdc96fd7cd47e91f45625583e04b04_4)     self.bu(text\='Make Turtle', command\=self.make\_turtle)
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-9bbf08bc5cbdc96fd7cd47e91f45625583e04b04_5)     self.bu(text\='Clear', command\=self.clear)
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-9bbf08bc5cbdc96fd7cd47e91f45625583e04b04_6)     self.endgr()

De methode gr creëert de grid; het argument is het aantal kolommen. Widgets in de grid worden van links naar rechts, en van boven naar beneden toegevoegd.

De eerste knop gebruikt self.canvas.dump als terugroep; de tweede gebruikt self.quit. Dit zijn **gebonden methoden**, dat wil zeggen dat ze geassocieerd zijn met een bepaald object. Als ze worden aangeroepen, worden ze aangeroepen op het object.

Het volgende widget in de kolom is een rij Frame dat een knop en een Entry bevat:

document.write('<a href="#" onclick="return togglenumber(\\'CA-f2cd5038aa6a326916e0ec7cca84e0758be07a53\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-f2cd5038aa6a326916e0ec7cca84e0758be07a53_1)     self.row(\[0,1\], pady\=30)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-f2cd5038aa6a326916e0ec7cca84e0758be07a53_2)     self.bu(text\='Run file', command\=self.run\_file)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-f2cd5038aa6a326916e0ec7cca84e0758be07a53_3)     self.en\_file = self.en(text\='snowflake.py', width\=5)
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-f2cd5038aa6a326916e0ec7cca84e0758be07a53_4)     self.endrow()

Het eerste argument van row is een lijst gewichten die bepaalt hoe extra ruimte wordt verdeeld tussen de widgets. De lijst \[0,1\] houdt in dat alle extra ruimte wordt toegekend aan het tweede widget, de Entry. Als u deze code uitvoert en het window vergroot, dan zult u zien dat Entry groter wordt maar de knop niet.

De optie pady zorgt voor extra ruimte in de _y_ richting; de extra ruimte is 30 pixels aan de boven- en aan de onderkant.

De methode endrow stopt de rij met widgets, dus de volgende widgets worden opgenomen in de kolom raamwerk. Gui.py heeft een stack van raamwerken.

-   Als u row, col of gr gebruikt om een raamwerk te maken, komt het op de top van de stack terecht en wordt het het huidige raamwerk.
    
-   Als u endrow, endcol of endgr gebruikt om een raamwerk te sluiten, wordt het van stack gehaald en het vorige raamwerk, nu op de top van de stack, wordt het huidige raamwerk.
    

De methode run\_file leest de inhoud van de Entry, gebruikt die inhoud als bestandsnaam, leest de bestandsinhoud en geeft die door aan run\_code. self.inter is een interpreter-object dat een string ontvangt en vervolgens uitvoert als Python code.

document.write('<a href="#" onclick="return togglenumber(\\'CA-a92ce526599be0dc96d6a44ad84ac950a1630017\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a92ce526599be0dc96d6a44ad84ac950a1630017_1)     def run\_file(self):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a92ce526599be0dc96d6a44ad84ac950a1630017_2)         filename = self.en\_file.get()
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a92ce526599be0dc96d6a44ad84ac950a1630017_3)         fp = open(filename)
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a92ce526599be0dc96d6a44ad84ac950a1630017_4)         source = fp.read()
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a92ce526599be0dc96d6a44ad84ac950a1630017_5)         self.inter.run\_code(source, filename)

De laatste twee widgets zijn een Text widget en een knop:

document.write('<a href="#" onclick="return togglenumber(\\'CA-9b8e5548790bb6f6ea96bd378ec53325eb3afc71\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-9b8e5548790bb6f6ea96bd378ec53325eb3afc71_1)     self.te\_code = self.te(width\=25, height\=10)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-9b8e5548790bb6f6ea96bd378ec53325eb3afc71_2)     self.te\_code.insert(END, 'world.clear()\\n')
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-9b8e5548790bb6f6ea96bd378ec53325eb3afc71_3)     self.te\_code.insert(END, 'bob = Turtle(world)\\n')
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-9b8e5548790bb6f6ea96bd378ec53325eb3afc71_4)     self.bu(text\='Run code', command\=self.run\_text)

De methode run\_text is hetzelfde als run\_file behalve dat run\_text de code neemt van het Text widget in plaats vanuit een bestand:

document.write('<a href="#" onclick="return togglenumber(\\'CA-4335d151c22fb4b72606eae9d32288097114d6c6\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-4335d151c22fb4b72606eae9d32288097114d6c6_1)     def run\_text(self):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-4335d151c22fb4b72606eae9d32288097114d6c6_2)         source = self.te\_code.get(1.0, END)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-4335d151c22fb4b72606eae9d32288097114d6c6_3)         self.inter.run\_code(source, '<user-provided code>')

Helaas verschillen de details van de widget layout in andere talen, en in andere Python modules. Tkinter heeft bijvoorbeeld al drie verschillende mechanismen voor het arrangeren van de widgets. Deze mechanismen worden **geometry managers** genoemd. In deze paragraaf wordt de “grid” geometry manager gebruikt; de andere heten “pack” and “place”.

Gelukkig zijn de meeste concepten van deze paragraaf toepasbaar bij andere GUI modules en andere talen.

## 19.7 Menu's en callables

Een Menuknop is een widget dat eruit ziet als een knop, maar als erop wordt gedrukt, verschijnt er een menu. Als de gebruiker een item selecteert, verdwijnt het menu.

Hier is de code voor het maken van een menuknop voor kleurselectie (u kunt de code downloaden van [thinkpython.com/code/menubutton\_demo.py](http://thinkpython.com/code/menubutton_demo.py)):

document.write('<a href="#" onclick="return togglenumber(\\'CA-b01b0769877ea3fa847f617a9f9516a66f8723cc\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b01b0769877ea3fa847f617a9f9516a66f8723cc_1) g = Gui()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b01b0769877ea3fa847f617a9f9516a66f8723cc_2) g.la('Select a color:')
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b01b0769877ea3fa847f617a9f9516a66f8723cc_3) colors = \['red', 'green', 'blue'\]
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b01b0769877ea3fa847f617a9f9516a66f8723cc_4) mb = g.mb(text\=colors\[0\])

De methode mb creëert de menuknop. Aanvankelijk is de tekst op de knop de standaard kleur. De volgende loop maakt een menu-item voor elke kleur:

document.write('<a href="#" onclick="return togglenumber(\\'CA-03b84050a98e13048b4c832b32a64d3bbf5265f0\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-03b84050a98e13048b4c832b32a64d3bbf5265f0_1) for color in colors:
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-03b84050a98e13048b4c832b32a64d3bbf5265f0_2)     g.mi(mb, text\=color, command\=Callable(set\_color, color))

Het eerste argument van mi is de menuknop waarmee deze items worden geassocieerd.

De command optie is een Callable object, wat iets nieuws is. Tot nu toe hebben we functies en gebonden methoden gebruikt als terugroep, wat goed werkt als er geen argumenten aan de functie hoeven te worden doorgegeven. Anders moet er een Callable object worden gecreëerd dat de functie bevat (bijvoorbeeld set\_color) en de bijbehorende argumenten (zoals color).

Het Callable object slaat een referentie op naar de functie en de argumenten als attributen. Later, als de gebruiker klikt op het menu-item, wordt met terugroep de functie aangeroepen en de opgeslagen argumenten doorgegeven.

Hieronder ziet u een implementatie van set\_color:

document.write('<a href="#" onclick="return togglenumber(\\'CA-3e0fcdeffb973019af9305e2e0d85533fbd5e5cc\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-3e0fcdeffb973019af9305e2e0d85533fbd5e5cc_1) def set\_color(color):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-3e0fcdeffb973019af9305e2e0d85533fbd5e5cc_2)     mb.config(text\=color)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-3e0fcdeffb973019af9305e2e0d85533fbd5e5cc_3)     print color

Als de gebruiker een menu-item selecteert en set\_color wordt aangeroepen, dan laat de menuknop de nieuw-geselecteerde kleur zien. Ook wordt die kleur zichtbaar. Als u dit voorbeeld probeert, dan zult u zien dat set\_color wordt aangeroepen wanneer u een item selecteert (en _niet_ wordt aangeroepen wanneer u het Callable object creëert).

## 19.8 Binding

Een **binding** is een associatie van een widget, een gebeurtenis (event) en een terugroep: als er iets gebeurt met/op het widget, dan vindt de terugroep plaats.

Meerdere widgets hebben standaard bindingen. Bijvoorbeeld als u op een knop drukt, dan verandert de standaard binding de "verschijning" van de knop waardoor hij ingedrukt lijkt. Als u de knop loslaat, dan verschijnt de knop weer op de oude manier en vindt de terugroep plaats zoals aangegeven met de command option.

U kunt de bind methode gebruiken om deze standaard bindingen te overschrijven, of om nieuwe bindingen toe te voegen. De onderstaande code maakt bijvoorbeeld een binding voor een doek (de code van deze paragraaf is te downloaden van [thinkpython.com/code/draggable\_demo.py](http://thinkpython.com/code/draggable_demo.py)):

ca.bind('<ButtonPress-1>', make\_circle)

Het eerste argument is een event string; dit event wordt getriggerd als de gebruiker de linker muisknop indrukt. Andere muisevents zijn bijvoorbeeld ButtonMotion, ButtonRelease en Double-Button.

Het tweede argument is een event handler. Een event handler is een functie of een gebonden methode (als een terugroep), maar een belangrijk verschil is dat een event handler een Event object als parameter heeft. Hier is een voorbeeld:

document.write('<a href="#" onclick="return togglenumber(\\'CA-09279f7f1a5691778a937fdc1f4b556606c4ecc6\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-09279f7f1a5691778a937fdc1f4b556606c4ecc6_1) def make\_circle(event):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-09279f7f1a5691778a937fdc1f4b556606c4ecc6_2)     pos = ca.canvas\_coords(\[event.x, event.y\])
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-09279f7f1a5691778a937fdc1f4b556606c4ecc6_3)     item = ca.circle(pos, 5, fill\='red')

Het Event object bevat informatie over het type gebeurtenis en details zoals de coördinaten van de muispijl. In dit voorbeeld hebben we de locatie van de muisklik nodig. Deze waarden worden “pixel coördinaten” genoemd en worden gedefinieerd door het onderliggende grafische systeem. De methode canvas\_coords vertaalt ze naar “doek coördinaten”, die compatibel zijn met doek methoden als circle.

Voor Entry widgets wordt over het algemeen het <Return> event gebonden, wat wordt getriggerd wanneer de gebruiker een Return- of Enter-toets indrukt. Zo maakt de volgende code een knop en een Entry:

document.write('<a href="#" onclick="return togglenumber(\\'CA-12e63aa643aa4a6d2091e2ae1f699f7f34975952\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-12e63aa643aa4a6d2091e2ae1f699f7f34975952_1) bu = g.bu('maak tekst item', make\_text)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-12e63aa643aa4a6d2091e2ae1f699f7f34975952_2) en = g.en()
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-12e63aa643aa4a6d2091e2ae1f699f7f34975952_3) en.bind('<Return>', make\_text)

make\_text wordt aangeroepen als op de knop wordt gedrukt, of als de gebruiker op de Return-toets drukt tijdens het intypen van de Entry. Om dit mogelijk te maken, hebben we een functie die als commando kan worden aangeroepen (met geen argumenten) of als een event handler (met een Event als argument):

document.write('<a href="#" onclick="return togglenumber(\\'CA-d1f3c3a8495a665a945ca418c0dbd103d8a0623f\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-d1f3c3a8495a665a945ca418c0dbd103d8a0623f_1) def make\_text(event\=None):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-d1f3c3a8495a665a945ca418c0dbd103d8a0623f_2)     text = en.get()
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-d1f3c3a8495a665a945ca418c0dbd103d8a0623f_3)     item = ca.text(\[0,0\], text)

De functie make\_text krijgt een inhoud van de Entry en laat die inhoud zien als een tekst-item op het doek.

Het is ook mogelijk om bindingen te creëren voor doek-items. Hieronder ziet u een klassendefinitie voor Draggable, een kindklasse van Item die zorgt voor bindingen voor het implementeren van "drag-and-drop" mogelijkheden.

document.write('<a href="#" onclick="return togglenumber(\\'CA-a3e9c7a8e016a725ae4af71ffe151da9a441b505\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a3e9c7a8e016a725ae4af71ffe151da9a441b505_1) class Draggable(Item):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a3e9c7a8e016a725ae4af71ffe151da9a441b505_2)     def \_\_init\_\_(self, item):
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a3e9c7a8e016a725ae4af71ffe151da9a441b505_3)         self.canvas = item.canvas
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a3e9c7a8e016a725ae4af71ffe151da9a441b505_4)         self.tag = item.tag
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a3e9c7a8e016a725ae4af71ffe151da9a441b505_5)         self.bind('<Button-3>', self.select)
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a3e9c7a8e016a725ae4af71ffe151da9a441b505_6)         self.bind('<B3-Motion>', self.drag)
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-a3e9c7a8e016a725ae4af71ffe151da9a441b505_7)         self.bind('<Release-3>', self.drop)

De init methode heeft een Item als parameter. De attributen van het Item worden gekopieerd en dan worden bindingen gecreëerd voor drie gebeurtenissen: indrukken van een knop, bewegen van de knop, en loslaten van een knop

De event handler select slaat de coördinaten van de huidige gebeurtenis op en de originele kleur van het item, daarna verandert de kleur in geel:

document.write('<a href="#" onclick="return togglenumber(\\'CA-f6d926db9c13e1c23ef7379ee465ea98337f9d50\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-f6d926db9c13e1c23ef7379ee465ea98337f9d50_1)     def select(self, event):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-f6d926db9c13e1c23ef7379ee465ea98337f9d50_2)         self.dragx = event.x
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-f6d926db9c13e1c23ef7379ee465ea98337f9d50_3)         self.dragy = event.y
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-f6d926db9c13e1c23ef7379ee465ea98337f9d50_4)         self.fill = self.cget('fill')
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-f6d926db9c13e1c23ef7379ee465ea98337f9d50_5)         self.config(fill\='yellow')

De methode cget staat voor “get configuration”, met een optie als string argument, en als resultaat de huidige waarde van die optie.

De functie drag berekent hoever het object is bewogen ten opzichte van de startpositie, zorgt vervolgens voor een update van de opgeslagen coördinaten, en beweegt tenslotte het item.

document.write('<a href="#" onclick="return togglenumber(\\'CA-921c90397fb9b09b0d6ffc24d92f5ffd1af73b4f\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-921c90397fb9b09b0d6ffc24d92f5ffd1af73b4f_1)     def drag(self, event):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-921c90397fb9b09b0d6ffc24d92f5ffd1af73b4f_2)         dx = event.x - self.dragx
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-921c90397fb9b09b0d6ffc24d92f5ffd1af73b4f_3)         dy = event.y - self.dragy
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-921c90397fb9b09b0d6ffc24d92f5ffd1af73b4f_4)         self.dragx = event.x
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-921c90397fb9b09b0d6ffc24d92f5ffd1af73b4f_5)         self.dragy = event.y
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-921c90397fb9b09b0d6ffc24d92f5ffd1af73b4f_6)         self.move(dx, dy)

Hier wordt met pixel coördinaten gerekend; er is geen reden om over te stappen naar doekcoördinaten.

Uiteindelijk wordt met drop de originele kleur van het item hersteld.

document.write('<a href="#" onclick="return togglenumber(\\'CA-248f528eb2794ab77496ef94f4cc6c4efb3a9a1b\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-248f528eb2794ab77496ef94f4cc6c4efb3a9a1b_1)     def drop(self, event):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-248f528eb2794ab77496ef94f4cc6c4efb3a9a1b_2)         self.config(fill\=self.fill)

U kunt de Draggable klasse gebruiken voor het toevoegen van "drag-and-drop" mogelijkheden aan een bestaand item. Hier is bijvoorbeeld een aangepaste versie van make\_circle, die circle gebruikt om een Item te creëren en Draggable om te zorgen voor drag-and-drop:

document.write('<a href="#" onclick="return togglenumber(\\'CA-aea92eeddef3bccdec73fb6e6259e3e440f5f28b\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-aea92eeddef3bccdec73fb6e6259e3e440f5f28b_1) def make\_circle(event):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-aea92eeddef3bccdec73fb6e6259e3e440f5f28b_2)     pos = ca.canvas\_coords(\[event.x, event.y\])
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-aea92eeddef3bccdec73fb6e6259e3e440f5f28b_3)     item = ca.circle(pos, 5, fill\='red')
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-aea92eeddef3bccdec73fb6e6259e3e440f5f28b_4)     item = Draggable(item)

Dit voorbeeld demonstreert één van de voordelen van overerving: u kunt de mogelijkheden van een ouderklasse veranderen, zonder de definitie van die klasse aan te passen. Dit is met name zinvol als u het gedrag wilt veranderen van een klasse die u niet zelf hebt geschreven.

## 19.9 Debuggen

Eén van de uitdagingen van GUI programmeren is om bij te houden welke dingen gebeuren als de GUI wordt gemaakt, en welke later gebeuren als reactie op handelingen van de gebruiker.

Bijvoorbeeld, bij het opzetten van een terugroep is een veel voorkomende fout de functie aan te roepen in plaats van het doorgeven van een referentie naar de functie:

document.write('<a href="#" onclick="return togglenumber(\\'CA-b2b18e06a44a90123b6b7ee120ba1cdf0f5b3181\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b2b18e06a44a90123b6b7ee120ba1cdf0f5b3181_1) def de\_terugroep():
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b2b18e06a44a90123b6b7ee120ba1cdf0f5b3181_2)     print 'Called.'
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b2b18e06a44a90123b6b7ee120ba1cdf0f5b3181_3) 
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b2b18e06a44a90123b6b7ee120ba1cdf0f5b3181_4) g.bu(text\='This is wrong!', command\=de\_terugroep())

Als u deze code uitvoert, zult u zien dat de\_terugroep meteen wordt aangeroepen, en dat dan de knop wordt gemaakt. Wanneer u op de knop drukt, dan gebeurt er niets, want de resultaatwaarde van de\_terugroep is None. Over het algemeen wilt u niet een terugroep laten plaatsvinden bij het opzetten van de GUI; de terugroep moet alleen optreden als respons op een gebruikershandeling.

Een andere uitdaging van GUI programmeren is, dat u geen controle hebt over de uitvoervolgorde. Welke delen van het programma moeten worden uitgevoerd, en in welke volgorde, wordt bepaald door gebruikershandelingen. Dat betekent dat u het programma zodanig moet ontwerpen dat het correct werkt met elke mogelijke volgorde van gebeurtenissen.

Bijvoorbeeld de GUI van oefening 19.3 heeft twee widgets: de ene voor het creëren van een cirkel-item en de andere voor het veranderen van de kleur van de cirkel. Als de gebruiker de cirkel creëert en dan de kleur verandert, is er niets aan de hand. Maar wat te doen, als de gebruiker de kleur verandert van een cirkel die nog niet bestaat? Of als er meerdere cirkels worden gecreëerd?

Als het aantal widgets toeneemt, dan is het steeds moeilijker om alle mogelijke reeksen gebeurtenissen te voorzien. Een manier om hieraan tegemoet te komen is om de toestand van het systeem op te nemen in een object en dan na te denken over:

-   Wat zijn de mogelijke toestanden? In het cirkelvoorbeeld zijn er twee toestanden: vóór het creëren van de eerste cirkel door de gebruiker, en erna.
-   Welke gebeurtenissen kunnen er in elke toestand plaatsvinden? In het voorbeeld kan de gebruiker één van de beide knoppen indrukken, of stoppen.
-   Wat is het gewenste resultaat voor elk van de toestand-gebeurtenis paren? Omdat er twee toestanden zijn en twee knoppen, kunnen er vier toestand-gebeurtenis paren worden geanalyseerd.
-   Wat kan een overgang veroorzaken van de ene toestand naar de andere? In dit geval is er een overgang als de gebruiker de eerste cirkel creëert.

Mogelijkerwijs ziet u heil in het definieren en controleren van invarianten, die altijd moeten gelden los van de reeks gebeurtenissen.

Deze aanpak van GUI programmeren kan u helpen bij het schrijven van correcte code zonder elke mogelijke reeks van gebruikergebeurtenissen te hoeven testen.

## 19.10 Woordenlijst

**GUI**: Graphical User Interface.

**widget**: Een element van een GUI, bijvoorbeeld een knop, een menu, een tekst Entry veld, enzovoort.

**optie**: Een waarde om de verschijning of functie van een widget te besturen/veranderen.

**sleutelwoordargument**: Een argument om een parameternaam aan te geven als onderdeel van een functieaanroep.

**terugroep (callback)**: Een functie geassocieerd met een widget die wordt aangeroepen als de gebruiker iets doet (met/op het widget).

**gebonden methode**: Een methode geassocieerd met een specifieke instantie.

**gebeurtenis gedreven programmeren**: Een programmeerstijl waarbij de uitvoervolgorde wordt bepaald door gebruikersacties.

**gebeurtenis (event)**: Een gebruikersactie, zoals een muisklik of het indrukken van een toets, waarop de GUI moet reageren.

**event loop**: Een oneindige loop die wacht op gebruikeracties en reacties.

**item**: Een grafisch element op een doekwidget.

**begrenzende doos (bounding box)**: Een rechthoek die een verzameling items omvat. Meestal wordt de rechthoek gespecificeerd met twee overstaande hoeken.

**pack**: Het arrangeren en tonen van de elementen van een GUI.

**geometry manager**: Een systeem voor widgets-packing.

**binding**: Een associatie van een widget, een gebeurtenis (event) en een event handler. De event handler wordt aangeroepen als er iets gebeurt met/op het widget.

## 19.11 Oefeningen

**Oefening 19.4** In deze oefening gaat u een imageviewer schrijven. Een eenvoudig voorbeeld:

document.write('<a href="#" onclick="return togglenumber(\\'CA-0668f04654c4ca50f35e94382681d26321ae76bc\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-0668f04654c4ca50f35e94382681d26321ae76bc_1) g = Gui()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-0668f04654c4ca50f35e94382681d26321ae76bc_2) canvas = g.ca(width\=300)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-0668f04654c4ca50f35e94382681d26321ae76bc_3) photo = PhotoImage(file\='danger.gif')
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-0668f04654c4ca50f35e94382681d26321ae76bc_4) canvas.image(\[0,0\], image\=photo)
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-0668f04654c4ca50f35e94382681d26321ae76bc_5) g.mainloop()

De functie PhotoImage leest een bestand en retourneert een PhotoImage object dat Tkinter kan tonen. Canvas.image zet het plaatje op het doek (canvas), gecentreerd op de gegeven coördinaten. Het is ook mogelijk plaatjes te plaatsen op labels, knoppen en andere widgets.

document.write('<a href="#" onclick="return togglenumber(\\'CA-8496a13a38274edd6a24b4178b7db4d547869306\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-8496a13a38274edd6a24b4178b7db4d547869306_1) g.la(image\=photo)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-8496a13a38274edd6a24b4178b7db4d547869306_2) g.bu(image\=photo)

PhotoImage kan slechts met enkele grafische formaten overweg, bijvoorbeeld GIF and PPM. We kunnen de Python Imaging Library (PIL) gebruiken om andere bestanden te lezen.

De naam van de PIL module is Image, maar Tkinter definieert een object met dezelfde naam. Om een conflict te voorkomen kunt u import as als volgt gebruiken:

document.write('<a href="#" onclick="return togglenumber(\\'CA-d9167b7da6b3e1b74054ae556002d14b637026d4\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-d9167b7da6b3e1b74054ae556002d14b637026d4_1) import Image as PIL
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-d9167b7da6b3e1b74054ae556002d14b637026d4_2) import ImageTk

De eerste regel importeert Image en geeft hieraan de lokale naam PIL. De tweederegel importeert ImageTk, zodat een PIL image kan worden geconverteerd naar een Tkinter PhotoImage. Hier is een voorbeeld:

document.write('<a href="#" onclick="return togglenumber(\\'CA-b4c88dc8a63b7b380500d3db797380cfb03ab8bd\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b4c88dc8a63b7b380500d3db797380cfb03ab8bd_1) image = PIL.open('allen.png')
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b4c88dc8a63b7b380500d3db797380cfb03ab8bd_2) photo2 = ImageTk.PhotoImage(image)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukNegentien#CA-b4c88dc8a63b7b380500d3db797380cfb03ab8bd_3) g.la(image\=photo2)

1.  Download image\_demo.py, danger.gif en allen.png van [thinkpython.com/code](http://thinkpython.com/code). Run image\_demo.py. Misschien moet u PIL en ImageTk installeren. Ze bevinden zich waarschijnlijk in uw software repository. Zo niet, dan kunt u ze downloaden van [pythonware.com/products/pil/](http://pythonware.com/products/pil/).
    
2.  Verander in image\_demo.py de naam van PhotoImage van photo2 in photo en voer het programma opnieuw uit. U zult de tweede PhotoImage zien, maar niet de eerste.  
      
    Het probleem is dat bij het hertoewijzen van photo de referentie naar de eerste PhotoImage wordt overschreven, waardoor deze verdwijnt. Hetzelfde gebeurt als u een PhotoImage toekent aan een lokale variabele; na de beëindiging van de functie is de PhotoImage verdwenen.  
      
    Om dit probleem te voorkomen, moet je een referentie opslaan voor elke PhotoImage die u wilt behouden. Hiervoor kunt u een globale variabele gebruiken, of PhotoImages opslaan in een datastructuur of als een attribuut van een object.  
      
    Het bovenstaande kan tot frustatie leiden. Daarom wil ik u waarschuwen (en is “Danger!” zichtbaar op het voorbeeldplaatje).
    
3.  Begin met dit voorbeeld en schrijf daarna een programma waaraan de naam van een map wordt meegegeven en dat alle bestanden langsloopt, waarbij elk bestand wordt getoond dat PIL herkent als een image. U kunt een try statement gebruiken voor het afvangen van de bestanden, die PIL niet herkent.  
      
    Als de gebruiker op een afbeelding klikt, moet het programma de volgende afbeeling laten zien.
    
4.  PIL heeft meerdere methoden voor het bewerken van afbeeldingen. Voor informatie kunt u terecht op [pythonware.com/library/pil/handbook](http://pythonware.com/library/pil/handbook). Als uitdaging kunt u enkele methoden kiezen en een GUI ontwerpen om die methoden toe te passen op afbeeldingen.
    

Een eenvoudige oplossing is te downloaden van [thinkpython.com/code/ImageBrowser.py](http://thinkpython.com/code/ImageBrowser.py)

**Oefening 19.5** Een grafische vectoreditor is een programma waarmee gebruikers vormen kunnen tekenen en bewerken op het beeldscherm, Ook kan uitvoer worden gegenereerd in het grafische vectorformaat als Postscript of SVG1.

Schrijf een eenvoudige vectoreditor door Tkinter te gebruiken. Gebruikers moeten minstens lijnen, cirkels en rechthoeken kunnen tekenen, en Canvas.dump wordt gebruikt voor het genereren van een Postscript beschrijving van de inhoud van het doek.

Als uitdaging kunt u toestaan dat gebruikers items selecteren en van grootte veranderen op het doek.

**Oefening 19.6** Gebruik Tkinter om een eenvoudige webbrowser te schrijven. De browser moet een Text widget hebben waar de gebruiker een URL kan ingeven en een doek voor het tonen van de inhoud van de pagina.

U kunt de urllib module gebruiken voor het downloaden van bestanden (zie oefening 14.5) en de HTMLParser module om de HTML tags te parseren (zie [docs.python.org/lib/module-HTMLParser.html](http://docs.python.org/lib/module-HTMLParser.html)).

Uw browser moet minstens om kunnen gaan met platte tekst en hyperlinks. Als uitdaging kunt u aandacht besteden aan: achtergrondkleuren, tags om tekst te formatteren en afbeeldingen.

* * *

1 Zie wikipedia.org/wiki/Vector\_graphics\_editor.