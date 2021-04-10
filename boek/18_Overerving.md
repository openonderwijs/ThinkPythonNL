[community/ThinkPython/HoofdstukAchttien - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien)

> # Hoofdstuk 18 Overerving
> 
> In dit hoofdstuk zullen we klassen maken om speelkaarten, kaartstokken (stocks), en handen (hands) met (poker)kaarten voor te stellen. Als u niet weet hoe u poker moet spelen, kunt u er meer over te weten komen op [nl.wikipedia.org/wiki/Poker](http://nl.wikipedia.org/wiki/Poker). Maar het hoeft niet per se, want we zullen u vertellen wat u moet weten om de oefeningen te voltooien.
> 
> Als u niet bekend bent met Anglo-Amerikaanse speelkaarten, kunt u daarover het één en ander lezen op [nl.wikipedia.org/wiki/Speelkaart](http://nl.wikipedia.org/wiki/Speelkaart).
> 
> ## 18.1 Objecten voor kaarten
> 
> Er zitten tweeënvijftig kaarten in een kaartstok, waarbij elke kaart behoort tot één van de vier soorten en één van de dertien rangen. De soorten zijn Schoppen, Harten, Ruiten en Klaveren (in de dalende volgorde van bridge). De rangen zijn Aas, 2, 3, 4, 5, 6, 7, 8, 9, 10, Boer, Vrouw en Heer. Afhankelijk van het spel dat u speelt, kan een Aas hoger zijn dan een Heer of lager zijn dan een twee.
> 
> Als we een object willen definiëren om een speelkaart voor te stellen, is het snel duidelijk welke attributen we nodig hebben: rang en soort. Het is niet direct duidelijk van welk type die attributen zouden moeten zijn. Een mogelijkheid is om strings te gebruiken zoals 'klaveren' voor soort en 'Vrouw' voor rang. Een probleem met deze implementatie is echter dat het moeilijk is om kaarten te vergelijken en te beslissen welke van de twee een hogere rang of soort heeft.
> 
> Een alternatief is om integers te gebruiken om de rangen en de soorten te **coderen**. In deze context, betekent “coderen” dat we een integer hebben die een soort of rang voorstelt. Deze manier van coderen is niet bedoeld om geheim te zijn (dan gaat het over **cryptografie**).
> 
> Deze tabel laat bij wijze van voorbeeld de soorten en het bijbehorende nummer zien:
> 
> Schoppen → 3
> Harten   → 2
> Ruiten   → 1
> Klaveren → 0
> 
> Deze codering maakt het makkelijk om kaarten te vergelijken; omdat hogere soorten voorgesteld worden door hogere getallen, kunnen we soorten vergelijken door deze nummers te vergelijken.
> 
> De codering voor rangen is ook redelijk voor de hand liggend; elke rang wordt voorgesteld door hetzelfde getal en plaatjeskaarten stellen we zo voor:
> 
> Boer  → 11
> Vrouw → 12
> Heer  → 13
> 
> We gebruiken het → symbool om duidelijk te maken dat deze tabellen geen deel zijn van het Python programma. Deze zijn deel van het programmaontwerp, maar ze komen niet expliciet voor in de code. De klassendefinitie voor Kaart ziet er zo uit:
> 
> function isnumbered(obj) { return obj.childNodes.length && obj.firstChild.childNodes.length && obj.firstChild.firstChild.className == 'LineNumber'; } function nformat(num,chrs,add) { var nlen = Math.max(0,chrs-(''+num).length), res = ''; while (nlen>0) { res += ' '; nlen-- } return res+num+add; } function addnumber(did, nstart, nstep) { var c = document.getElementById(did), l = c.firstChild, n = 1; if (!isnumbered(c)) { if (typeof nstart == 'undefined') nstart = 1; if (typeof nstep == 'undefined') nstep = 1; var n = nstart; while (l != null) { if (l.tagName == 'SPAN') { var s = document.createElement('SPAN'); var a = document.createElement('A'); s.className = 'LineNumber'; a.appendChild(document.createTextNode(nformat(n,4,''))); a.href = '#' + did + '\_' + n; s.appendChild(a); s.appendChild(document.createTextNode(' ')); n += nstep; if (l.childNodes.length) { l.insertBefore(s, l.firstChild); } else { l.appendChild(s); } } l = l.nextSibling; } } return false; } function remnumber(did) { var c = document.getElementById(did), l = c.firstChild; if (isnumbered(c)) { while (l != null) { if (l.tagName == 'SPAN' && l.firstChild.className == 'LineNumber') l.removeChild(l.firstChild); l = l.nextSibling; } } return false; } function togglenumber(did, nstart, nstep) { var c = document.getElementById(did); if (isnumbered(c)) { remnumber(did); } else { addnumber(did,nstart,nstep); } return false; } document.write('<a href="#" onclick="return togglenumber(\\'CA-aba3d5bdeeebfd35f49646388a7e7eddef60572d\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-aba3d5bdeeebfd35f49646388a7e7eddef60572d_1) class Kaart(object):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-aba3d5bdeeebfd35f49646388a7e7eddef60572d_2)     """representeert een standaard speelkaart."""
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-aba3d5bdeeebfd35f49646388a7e7eddef60572d_3)     def \_\_init\_\_(self, soort\=0, rang\=2):
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-aba3d5bdeeebfd35f49646388a7e7eddef60572d_4)         self.soort = soort
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-aba3d5bdeeebfd35f49646388a7e7eddef60572d_5)         self.rang = rang
> 
> Zoals gewoonlijk heeft de init methode een optionele parameter voor elk attribuut. De standaardkaart is een klaveren 2.
> 
> Om een kaart te maken, roept u Kaart aan met de soort en rang die u wilt.
> 
> ruiten vrouw = Kaart(1, 12)
> 
> ## 18.2 Klassenattributen
> 
> Om Kaartobjecten te printen op een manier waarop mensen ze gemakkelijk kunnen lezen, moeten we de numerieke codes vertalen naar de voorgestelde rangen en soorten. Een goede manier om dit te doen is met lijsten van strings. We kennen deze lijsten toe aan klassenattributen.
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-3da8d8844966e7a69cb41cc9b87d7faf00310775\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-3da8d8844966e7a69cb41cc9b87d7faf00310775_1) \# in de klasse Kaart:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-3da8d8844966e7a69cb41cc9b87d7faf00310775_2) 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-3da8d8844966e7a69cb41cc9b87d7faf00310775_3)     soort\_namen = \['Klaveren', 'Ruiten', 'Harten', 'Schoppen'\]
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-3da8d8844966e7a69cb41cc9b87d7faf00310775_4)     rang\_namen = \[None, 'Aas', '2', '3', '4', '5', '6', '7',
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-3da8d8844966e7a69cb41cc9b87d7faf00310775_5)                   '8', '9', '10', 'Boer', 'Vrouw', 'Heer'\]
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-3da8d8844966e7a69cb41cc9b87d7faf00310775_6) 
>  [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-3da8d8844966e7a69cb41cc9b87d7faf00310775_7)     def \_\_str\_\_(self):
>  [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-3da8d8844966e7a69cb41cc9b87d7faf00310775_8)         return '%s %s' % (Kaart.soort\_namen\[self.soort\],
>  [9](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-3da8d8844966e7a69cb41cc9b87d7faf00310775_9)                           Kaart.rang\_namen\[self.rang\])
> 
> Variabelen zoals soort\_namen en rang\_namen, die gedefinieerd zijn in een klasse maar buiten een methode, worden klassenattributen genoemd omdat zij geassocieerd worden met het klassenobject Kaart. Deze term onderscheidt ze van variabelen als soort en rang, die **instantieattributen** worden genoemd omdat ze worden geassocieerd met een bepaalde instantie.
> 
> Beide soorten attributen worden benaderd met de puntnotatie. Bijvoorbeeld, in \_\_str\_\_, self is een Kaartobject en self.rang is de rang ervan. Zo is Kaart een klassenobject, en Kaart.rang\_namen is een lijst van strings geassocieerd met de klasse.
> 
> Elke kaart heeft een eigen soort en rang, maar er is maar 1 kopie van soort\_namen en van rang\_namen.
> 
> Dus de expressie Kaart.rang\_namen\[self.rang\] betekent “gebruik het attribuut rang van het object self als een index bij de lijst rang\_namen van de klasse Kaart, en selecteer de geschikte string.”
> 
> Het eerste element van rang\_namen is None want er is geen kaart met rang nul. Door het toevoegen van None zorgen we ervoor dat de index 2 wordt gecombineerd met de string '2', en de index 3 met de string '3', enzovoort. We hadden hiervoor ook een woordenboek kunnen gebruiken in plaats van een lijst.
> 
> Met de methoden tot nu toe kunnen we kaarten maken en laten zien:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-ca166285b1965d3864da04b9b5fc1bbaa4262883\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-ca166285b1965d3864da04b9b5fc1bbaa4262883_1) \>>> kaart1 = Kaart(2, 11)
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-ca166285b1965d3864da04b9b5fc1bbaa4262883_2) \>>> print kaart1
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-ca166285b1965d3864da04b9b5fc1bbaa4262883_3) Harten Boer
> 
> Hier is een diagram dat het Kaart klassenobject laat zien en een Kaartinstantie:
> 
> -   ![Boek026_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien?action=AttachFile&do=get&target=Boek026_nl.png "Boek026_nl.png")
>     
> 
> Kaart is een klassenobject, dus het heeft type type. kaart1 heeft type Kaart. (Om ruimte te besparen zijn de inhoud van soort\_namen en rang\_namen niet getekend).
> 
> ## 18.3 Vergelijken van kaarten
> 
> Voor ingebouwde typen zijn er voorwaardelijke operatoren (<, >, ==, enzovoort) voor het vergelijken van waarden en om te bepalen wanneer de ene operand groter, kleiner of gelijk is aan de andere. Voor typen die de gebruiker maakt, kan het gedrag van ingebouwde operatoren worden overschreven door een methode \_\_cmp\_\_ te definiëren.
> 
> \_\_cmp\_\_ heeft twee parameters, self en ander, en retourneert een positief getal als het eerste object groter is, een negatief getal als het tweede object groter is, en 0 als ze gelijk zijn.
> 
> De correcte ordening van kaarten is niet vanzelfsprekend. Welke is bijvoorbeeld beter, de klaveren 3 of de ruiten 2? De ene kaart heeft een hogere rang, maar de andere heeft een hogere soort. Om kaarten te vergelijken moet je beslissen wat het belangrijkste is, de rang of de soort.
> 
> Deze beslissing kan afhankelijk zijn van het spel dat wordt gespeeld. Maar om het eenvoudig te houden, maken we de (willekeurige) keuze dat de soort het belangrijkste is. Dus bijvoorbeeld alle schoppen kaarten zijn hoger dan alle ruiten kaarten, en de ruiten 2 is hoger dan de klaveren 3.
> 
> Na deze beslissing kunnen we \_\_cmp\_\_ schrijven:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-8e276bcb4befa957bb674714b7952723b0df3fcb\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_1) \# in de klasse Kaart:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_2) 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_3)     def \_\_cmp\_\_(self, ander):
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_4)         \# controleer de soorten
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_5)         if self.soort > ander.soort: return 1
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_6)         if self.soort < ander.soort: return -1
>  [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_7) 
>  [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_8)         \# soorten zijn hetzelfde... controleer rangen
>  [9](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_9)         if self.rang > ander.rang: return 1
>  [10](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_10)         if self.rang < ander.rang: return -1
>  [11](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_11) 
>  [12](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_12)         \# rangen ook hetzelfde... gelijkspel
>  [13](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-8e276bcb4befa957bb674714b7952723b0df3fcb_13)         return 0
> 
> U kunt dit korter schrijven met de tupelvergelijking:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-cae3c19c60eaf575922d92ccca6ddecf01c819a2\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cae3c19c60eaf575922d92ccca6ddecf01c819a2_1) \# in de klasse Kaart:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cae3c19c60eaf575922d92ccca6ddecf01c819a2_2) 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cae3c19c60eaf575922d92ccca6ddecf01c819a2_3)     def \_\_cmp\_\_(self, ander):
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cae3c19c60eaf575922d92ccca6ddecf01c819a2_4)         t1 = self.soort, self.rang
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cae3c19c60eaf575922d92ccca6ddecf01c819a2_5)         t2 = ander.soort, ander.rang
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cae3c19c60eaf575922d92ccca6ddecf01c819a2_6)         return cmp(t1, t2)
> 
> De ingebouwde functie cmp heeft dezelfde interface als de methode \_\_cmp\_\_: de methode krijgt twee waarden en retourneert een positief getal als de eerste groter is, een negatief getal als de tweede groter is, en 0 als ze gelijk zijn.
> 
> **Exercise 18.1** Schrijf een \_\_cmp\_\_ methode voor Tijd objecten. Hint: u kunt de tupelvergelijking gebruiken, maar ook integer aftrekken is een mogelijkheid.
> 
> ## 18.4 Stokken kaarten
> 
> Nu we Kaarten hebben, is de volgende stap om Stokken te definiëren. Omdat een stok kaarten bestaat uit kaarten, bevat elke stok een lijst van kaarten als attribuut.
> 
> Hieronder ziet u de klassendefinitie voor Stok. De init methode maakt het attribuut kaarten en genereert de standaard van 52 kaarten:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-a0a05e1285e77a9a3d6fa125398a7e5c68f2b0ef\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-a0a05e1285e77a9a3d6fa125398a7e5c68f2b0ef_1) class Stok(object):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-a0a05e1285e77a9a3d6fa125398a7e5c68f2b0ef_2)     def \_\_init\_\_(self):
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-a0a05e1285e77a9a3d6fa125398a7e5c68f2b0ef_3)         self.kaarten = \[\]
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-a0a05e1285e77a9a3d6fa125398a7e5c68f2b0ef_4)         for soort in range(4):
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-a0a05e1285e77a9a3d6fa125398a7e5c68f2b0ef_5)              for rang in range(1, 14):
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-a0a05e1285e77a9a3d6fa125398a7e5c68f2b0ef_6)                  kaart = Kaart(soort, rang)
>  [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-a0a05e1285e77a9a3d6fa125398a7e5c68f2b0ef_7)                  self.kaarten.append(kaart)
> 
> De gemakkelijkste manier om de stok te bevolken/vullen, is met een geneste loop. De buitenste loop nummert de soorten van 0 tot en met 3. De binnenste loop nummert de rangen van 1 tot en met 13. Elke iteratie maakt een nieuwe Kaart met de huidige soort en rang, en voegt de kaart (aan de achterkant) toe aan self.kaarten.
> 
> ## 18.5 Stok laten zien
> 
> Hier is een \_\_str\_\_ methode voor Stok:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-f5aa8ebdcb7ce375118d3389b914b417d53a77c5\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-f5aa8ebdcb7ce375118d3389b914b417d53a77c5_1) \# in de klasse Stok:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-f5aa8ebdcb7ce375118d3389b914b417d53a77c5_2) 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-f5aa8ebdcb7ce375118d3389b914b417d53a77c5_3)     def \_\_str\_\_(self):
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-f5aa8ebdcb7ce375118d3389b914b417d53a77c5_4)         res = \[\]
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-f5aa8ebdcb7ce375118d3389b914b417d53a77c5_5)         for kaart in self.kaarten:
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-f5aa8ebdcb7ce375118d3389b914b417d53a77c5_6)             res.append(str(kaart))
>  [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-f5aa8ebdcb7ce375118d3389b914b417d53a77c5_7)         return '\\n'.join(res)
> 
> Deze methode laat een efficiënte manier zien om een grote string te maken: een lijst opbouwen en dan join gebruiken. De ingebouwde functie str roept de \_\_str\_\_ methode aan bij elke kaart en retourneert de string representatie.
> 
> Omdat we join aanroepen op een nieuwe-regel karakter, worden de kaarten van elkaar gescheiden door nieuwe-regels. Hier ziet u het resultaat:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-0042b7aa0724dc0d66e42847a56af4afb268feb9\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-0042b7aa0724dc0d66e42847a56af4afb268feb9_1) \>>> stok = Stok()
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-0042b7aa0724dc0d66e42847a56af4afb268feb9_2) \>>> print stok
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-0042b7aa0724dc0d66e42847a56af4afb268feb9_3) Klaveren Aas
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-0042b7aa0724dc0d66e42847a56af4afb268feb9_4) Klaveren 2
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-0042b7aa0724dc0d66e42847a56af4afb268feb9_5) Klaveren 3
>  [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-0042b7aa0724dc0d66e42847a56af4afb268feb9_6) ...
>  [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-0042b7aa0724dc0d66e42847a56af4afb268feb9_7) Schoppen 10
>  [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-0042b7aa0724dc0d66e42847a56af4afb268feb9_8) Schoppen Boer
>  [9](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-0042b7aa0724dc0d66e42847a56af4afb268feb9_9) Schoppen Vrouw
>  [10](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-0042b7aa0724dc0d66e42847a56af4afb268feb9_10) Schoppen Heer
> 
> Hoewel het resultaat op 52 regels verschijnt, is het toch 1 lange string die nieuwe-regels bevat.
> 
> ## 18.6 Toevoegen, verwijderen, schudden en sorteren
> 
> Om de kaarten te delen willen we een methode die een kaart verwijdert van de stok en die de kaart retourneert. De lijstmethode pop is een geschikte manier om dat voor elkaar te krijgen:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-48a721aa85f12a76ad76529c568b3a1d8c367fe9\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-48a721aa85f12a76ad76529c568b3a1d8c367fe9_1) \# in de klasse Stok:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-48a721aa85f12a76ad76529c568b3a1d8c367fe9_2) 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-48a721aa85f12a76ad76529c568b3a1d8c367fe9_3)     def pop\_kaart(self):
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-48a721aa85f12a76ad76529c568b3a1d8c367fe9_4)         return self.kaarten.pop()
> 
> Omdat pop de _laatste_ kaart verwijdert van de lijst, delen we vanaf de onderkant van de stok. In het echte leven wordt delen vanaf de onderkant afgekeurd1, maar in deze context is het in orde.
> 
> Om een kaart toe te voegen gebruiken we de lijstmethode append:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-2e61d9d97f56497aaa8b3989c622fad59f40a190\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-2e61d9d97f56497aaa8b3989c622fad59f40a190_1) \# in de klasse Stok
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-2e61d9d97f56497aaa8b3989c622fad59f40a190_2)     def toevoegen\_kaart(self, kaart):
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-2e61d9d97f56497aaa8b3989c622fad59f40a190_3)         self.kaarten.append(kaart)
> 
> Een dergelijke methode, die een andere functie gebruikt zonder zelf veel werk te verrichten, wordt soms **fineer** genoemd. De metafoor komt uit de houtindustrie, waar nogal eens een dunne laag kwalitatief goed hout wordt vastgelijmd op de oppervlakte van een goedkopere houtsoort.
> 
> In dit geval definiëren we een “kleine” methode die een lijstoperatie gebruikt die geschikt is voor kaartstokken.
> 
> Als tweede voorbeeld kunnen we een Stokmethode schrijven genaamd schudden die de functie shuffle gebruikt van de random module:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-c6a29e5a15b9be1f769cbec0eac47658c28920b7\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-c6a29e5a15b9be1f769cbec0eac47658c28920b7_1) \# in de klasse Stok:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-c6a29e5a15b9be1f769cbec0eac47658c28920b7_2) 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-c6a29e5a15b9be1f769cbec0eac47658c28920b7_3)     def schudden(self):
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-c6a29e5a15b9be1f769cbec0eac47658c28920b7_4)         random.shuffle(self.kaarten)
> 
> Vergeet niet om random te importeren.
> 
> **Oefening 18.2** Schrijf een Stokmethode genaamd sorteren die de lijstmethode sort gebruikt om de kaarten van een Stok te sorteren. Om de sorteervolgorde te bepalen, maakt sorteren gebruik van de methode \_\_cmp\_\_ die we in de klasse Kaart hebben gedefinieerd.
> 
> ## 18.7 Overerving
> 
> De eigenschap die meestal in een adem wordt genoemd met object-georiënteerd programmeren is **overerving** . Overerving is de mogelijkheid om een nieuwe klasse te definieren als een aangepaste versie van een bestaande klasse.
> 
> Het wordt “overerving ” genoemd omdat de nieuwe klasse de methoden erft van de bestaande klasse. In deze metafoor wordt de bestaande klasse de **ouder** genoemd en de nieuwe klasse het **kind**.
> 
> Stel dat we bijvoorbeeld een klasse willen hebben voor het representeren van een “hand”, de verzameling kaarten die een speler vast heeft. Een hand is vergelijkbaar met een Stok: beiden bestaan uit een verzameling kaarten, en voor beiden zijn operaties nodig als toevoegen en verwijderen van kaarten.
> 
> Een hand verschilt ook van een stok; er zijn (te maken) operaties voor handen die niet zinvol zijn voor een stok. Bijvoorbeeld bij poker willen we twee handen vergelijken om te zien welke hand wint, en bij bridge willen we misschien wel een score berekenen voor een hand, zodat er geboden kan worden.
> 
> Deze relatie tussen klassen - hetzelfde, maar verschillende - leent zichzelf voor overerving.
> 
> De definitie van een kindklasse is als elke andere klassendefinitie, maar de naam van de ouderklasse verschijnt tussen haakjes:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-5e3e5c322891dd1d51f7fbcbbabfe25204baef1f\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-5e3e5c322891dd1d51f7fbcbbabfe25204baef1f_1) class Hand(Stok):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-5e3e5c322891dd1d51f7fbcbbabfe25204baef1f_2)     """representeert een hand met speelkaarten"""
> 
> Deze definitie laat zien dat Hand erft van Stok; dat betekent dat we methoden als pop\_kaart en toevoegen\_kaart kunnen gebruiken bij Handen en bij Stokken.
> 
> Hand erft ook \_\_init\_\_ van Stok, maar deze methode doet niet echt wat we willen: in plaats van de hand te voorzien van 52 nieuwe kaarten zou de initmethode voor Handen de cards moeten initialiseren met een lege lijst.
> 
> Als we een initmethode maken in de Hand klasse, wordt die van de Stok klasse overschreven:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-89f77ba6a6b33c920acb772e5982fa8d10e7e9e4\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-89f77ba6a6b33c920acb772e5982fa8d10e7e9e4_1) \# in de klasse Hand:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-89f77ba6a6b33c920acb772e5982fa8d10e7e9e4_2) 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-89f77ba6a6b33c920acb772e5982fa8d10e7e9e4_3)     def \_\_init\_\_(self, label\=''):
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-89f77ba6a6b33c920acb772e5982fa8d10e7e9e4_4)         self.kaarten = \[\]
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-89f77ba6a6b33c920acb772e5982fa8d10e7e9e4_5)         self.label = label
> 
> Dus als we een Hand creëren, gebruikt Python deze initmethode:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-fcc35426a7b0602203e8803dfc027938c9e35f64\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-fcc35426a7b0602203e8803dfc027938c9e35f64_1) \>>> hand = Hand('nieuwe hand')
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-fcc35426a7b0602203e8803dfc027938c9e35f64_2) \>>> print hand.kaarten
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-fcc35426a7b0602203e8803dfc027938c9e35f64_3) \[\]
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-fcc35426a7b0602203e8803dfc027938c9e35f64_4) \>>> print hand.label
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-fcc35426a7b0602203e8803dfc027938c9e35f64_5) nieuwe hand
> 
> Maar de andere methoden worden geërfd van Stok, dus we kunnen pop\_kaart en toevoegen\_kaart gebruiken om een kaart te delen.
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-83497a9f9123d4e3ec76a2aa26aaa700c8df0a2a\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-83497a9f9123d4e3ec76a2aa26aaa700c8df0a2a_1) \>>> stok = Stok()
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-83497a9f9123d4e3ec76a2aa26aaa700c8df0a2a_2) \>>> kaart = stok.pop\_kaart()
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-83497a9f9123d4e3ec76a2aa26aaa700c8df0a2a_3) \>>> hand.toevoegen\_kaart(kaart)
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-83497a9f9123d4e3ec76a2aa26aaa700c8df0a2a_4) \>>> print hand
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-83497a9f9123d4e3ec76a2aa26aaa700c8df0a2a_5) Schoppen Heer
> 
> Een natuurlijke volgende stap is deze code op te nemen (to encapsulate) in een methode genaamd bewegen\_kaarten:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-cdbd70953ee05fbf2fc67fe09cb1b075d08beb78\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cdbd70953ee05fbf2fc67fe09cb1b075d08beb78_1) \# in de klasse Stok:
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cdbd70953ee05fbf2fc67fe09cb1b075d08beb78_2) 
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cdbd70953ee05fbf2fc67fe09cb1b075d08beb78_3)     def bewegen\_kaarten(self, hand, aantal):
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cdbd70953ee05fbf2fc67fe09cb1b075d08beb78_4)         for i in range(aantal):
>  [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-cdbd70953ee05fbf2fc67fe09cb1b075d08beb78_5)             hand.toevoegen\_kaart(self.pop\_kaart())
> 
> bewegen\_kaarten heeft twee argumenten, een Handobject en het aantal te delen kaarten. De methode verandert zowel self als hand, en retourneert None.
> 
> In sommige spelen gaan kaarten van de de ene hand naar de andere, of van een hand terug naar de stok. U kunt bewegen\_kaarten gebruiken voor elk van deze operaties: self kan een Stok of een Hand zijn, en hand kan (ondanks de naam) ook een Stok zijn.
> 
> **Oefening 18.3** Schrijf een Stokmethode genaamd delen\_handen met twee parameters (het aantal handen en de kaarten per hand) die nieuwe Handobjecten creëert, het juiste aantal kaarten per hand deelt, en een lijst van Handobjecten retourneert.
> 
> Overerving is zeer bruikbaar. Sommige programma's, die repeterend zouden worden zonder overerving, kunnen nu eleganter worden geschreven. Overerving maakt het hergebruik van code mogelijk, omdat het gedrag (van kind-klassen) wordt aangepast zonder de ouder-klassen te veranderen. In sommige gevallen reflecteert de structuur van overerving de natuurlijke structuur van het probleem, waardoor het programma gemakkelijker te begrijpen is.
> 
> Anderzijds kan overerving ervoor zorgen dat programma's moeilijk te lezen zijn. Wanneer een methode wordt aangeroepen, is het soms niet duidelijk waar de definitie gevonden kan worden. De relevante code kan verdeeld zijn over meerdere modulen. Ook is het zo dat veel dingen die gedaan kunnen worden met overerving, ook net zo goed of beter gedaan kunnen worden zonder overerving.
> 
> ## 18.8 Klassendiagrammen
> 
> Tot nu toe hebben we stapeldiagrammen gebruikt voor het tonen van de toestand van een programma, en objectdiagrammen voor het tonen van de attributen van een object en hun waarden. Deze diagrammen zijn een momentopname tijdens het uitvoeren van een programma, dus ze veranderen als het programma wordt uitgevoerd.
> 
> Bovendien zijn de diagrammen gedetailleerd, voor sommige doeleinden te gedetailleerd. Een klassendiagram is een abstractere representatie van de programmastructuur. In plaats van individuele objecten te tonen, worden er klassen en relaties tussen klassen getoond.
> 
> Er zijn verschillende soorten relaties tussen klassen:
> 
> -   Objecten en de ene klasse kunnen referenties bevattten naar objecten in een andere klasse. Bijvoorbeeld elke Rechthoek bevat een referentie naar een Punt, en elke Stok bevat referenties naar meerder Kaarten. Dit soort relatie wordt **HEEFT-EEN** genoemd, zoals “een Rechthoek heeft een Punt.”
>     
> -   Een klasse kan erven van een andere, De relatie wordt **IS-EEN** genoemd, zoals “een Hand is een soort Stok.”
>     
> -   Een klasse kan afhankelijk zijn van een andere, in de zin dat door veranderingen in de ene klasse ook de andere klasse moet worden aangepast.
> 
> Een **klassendiagram** is een grafische representatie van deze relaties2. Bijvoorbeeld het onderstaande diagram toont de relaties tussen Kaart, Stok (hier nog Stapel genoemd) en Hand.
> 
> -   ![boek027_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien?action=AttachFile&do=get&target=boek027_nl.png "boek027_nl.png")
>     
> 
> De pijl met de driehoek als kop representeert een IS-EEN relatie; in dit geval laat het zien dat Hand erft van Stok.
> 
> De andere pijl met de standaardkop representeert een HEEFT-EEN relatie; in dit geval heeft een Stok referenties naar Kaartobjecten.
> 
> Het sterretje (\*) boven de standaard pijlkop is een **hoeveelheid**; het geeft aan hoeveel Kaarten een Stok heeft. Een hoeveelheid kan een getal zijn, zoals 52, een interval bijvoorbeeld 5..7, of een sterretje dat aangeeft dat een Stok een willekeurig aantal Kaarten kan hebben.
> 
> Een gedetailleerder diagram zou kunnen laten zien dat een Stok eigenlijk een _lijst_ van Kaarten bevat, maar ingebouwde typen als lijst en woordenboek worden meestal niet opgenomen in klassendiagrammen.
> 
> **Exercise 18.4** Lees TurtleWorld.py, World.py en Gui.py en teken een klassendiagram dat de relaties laat zien tussen deze klassen.
> 
> ## 18.9 Debuggen
> 
> Door overerving kan debuggen een uitdaging worden, want als u een methode aanroept bij een object, dan weet u misschien niet welke methode daadwerkelijk wordt aangeroepen.
> 
> Stel dat u een functie schrijft die werkt met Handobjecten. Dan wilt u dat de functie werkt met alle soorten Handen, zoals PokerHanden, BridgeHanden, enzovoort. Als je een methode aanroept als schudden, dan krijgt u misschien die van Stok, maar als één van de subklassen deze methode overschrijft, dan krijgt u die versie.
> 
> Elke keer als u onzeker bent over de uitvoering van een programma, dan is een eenvoudig hulpmiddel om print statements toe te voegen aan het begin van de belangrijke methoden. Als Stok.schudden een boodschap laat zien als Uitvoeren Stok.schudden, dan wordt duidelijk wat er gebeurt tijdens het uitvoeren.
> 
> Als alternatief kunt u de onderstaande functie gebruiken die de klasse retourneert waarin de methode wordt gedefinieerd. De functie heeft twee parameters, een object en een methodenaam (als een string).
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-d7b1cd575dd65c7ce0c481dfc02e7c88e801a702\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-d7b1cd575dd65c7ce0c481dfc02e7c88e801a702_1) def find\_defining\_class(obj, meth\_name):
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-d7b1cd575dd65c7ce0c481dfc02e7c88e801a702_2)     for ty in type(obj).mro():
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-d7b1cd575dd65c7ce0c481dfc02e7c88e801a702_3)         if meth\_name in ty.\_\_dict\_\_:
>  [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-d7b1cd575dd65c7ce0c481dfc02e7c88e801a702_4)             return ty
> 
> Een voorbeeld:
> 
> document.write('<a href="#" onclick="return togglenumber(\\'CA-7049fb9776b7609ac19d91f45541522fec3e9603\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#)
> 
>  [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-7049fb9776b7609ac19d91f45541522fec3e9603_1) \>>> hand = Hand()
>  [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-7049fb9776b7609ac19d91f45541522fec3e9603_2) \>>> print find\_defining\_class(hand, 'schudden')
>  [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukAchttien#CA-7049fb9776b7609ac19d91f45541522fec3e9603_3) <class '\_\_main\_\_.Stok'\>
> 
> Dus de schudden methode voor deze Hand is die van Stok.
> 
> find\_defining\_class gebruikt de mro om de lijst te krijgen van klassenobjecten (types) waarin naar de methode wordt gezocht. “MRO” is de afkorting van “method resolution order.”
> 
> Hier is een suggestie voor het ontwerpen van programma's: als u een methode overschrijft, dan moet de nieuwe interface hetzelfde zijn als de oude. Dus met dezelfde parameters, hetzelfde resultaattype en dezelfde pre- en postcondities. Als u zich hieraan houdt, dan zult u zien dat elke functie, ontworpen om te werken met een instantie van een superklasse (als een Stok), ook zal werken met instanties van subklassen (als Hand of [PokerHand](https://wiki.ubuntu-nl.org/PokerHand)).
> 
> Als u deze regel schendt, valt uw code uiteen als een (sorry) stok kaarten.
> 
> ## 18.10 Woordenlijst
> 
> **coderen**: Een waardenverzameling representeren door gebruik te maken van een andere waardenverzameling, en het construeren van een afbeelding tussen deze verzamelingen.
> 
> **klassenattribuut**: Een attribuut geassocieerd met een klassenobject. Klassenattributen worden gedefinieerd binnen een klassendefinitie maar buiten elke methode.
> 
> **instantie-attribuut**: Een attribuut geassocieerd met een instantie van een klasse.
> 
> **fineer**: Een methode of functie die een andere interface geeft aan een tweede functie zonder zelf veel te berekenen.
> 
> **overerving**: De mogelijkheid een nieuwe klasse te definiëren die een aangepaste versie is van een al bestaande klasse.
> 
> **ouderklasse**: De klasse waarvan het kind erft.
> 
> **kindklasse**: Een nieuwe klasse gecreëerd door overerving van een bestaande klasse; ook wel “subklasse” genoemd.
> 
> **IS-EEN relatie**: De relatie tussen een kind- en een ouderklasse.
> 
> **HEEFT-EEN relatie**: De relatie tussen twee klassen waarbij instanties van de ene klasse referenties bevatten naar instanties van de andere klasse.
> 
> **klassendiagram**: Een diagram dat de klassen in een programma laat zien en de onderlinge relaties.
> 
> **hoeveelheid**: Een notatie in een klassendiagram die laat zien hoeveel referenties er zijn naar de andere klasse, voor een HEEFT-EEN relatie.
> 
> ## 18.11 Oefeningen
> 
> **Oefening 18.5** Hieronder ziet u de mogelijke handen van poker, in volgorde van opklimmende waarde (en afnemende kans):
> 
> **pair**: twee kaarten met dezelfde rang
> 
> **two pair**: twee paren kaarten met dezelfde rang
> 
> **three of a kind**: drie kaarten met dezelfde rang
> 
> **straight**: vijf kaarten met opeenvolgende rangen (azen kunnen hoog of laag zijn, dus Aas-2-3-4-5 is een straight en ook 10-Boer-Vrouw-Heer-Aas, maar Vrouw-Heer-Aas-2-3 is geen straight.)
> 
> **flush**: vijf kaarten van dezelfde soort
> 
> **full house**: drie kaarten met dezelfde rang, twee kaarten met een andere
> 
> **four of a kind**: vier kaarten met dezelfde rang
> 
> **straight flush**: vijf opeenvolgende kaarten (zie hierboven) en van dezelfde soort
> 
> Het doel van deze opgaven is de kans te bepalen op elk van deze handen.
> 
> 1.  Download de volgende bestanden van [thinkpython.com/code](http://thinkpython.com/code):
>     
>     -   Card.py : Een complete versie van de Kaart-, Stok- en Handklassen (nu Card, Deck and Hand genaamd) van de klassen uit dit hoofdstuk.  
>         PokerHand.py : Een incomplete implementatie van een klasse ter representatie van een pokerhand, en wat code om te testen.
>         
> 2.  Als je PokerHand.py uitvoert, worden er zes 7-kaarten pokerhanden gedeeld en wordt gecontroleerd om te zien of één van de handen een flush bevat. Lees deze code voordat u verder gaat.
>     
> 3.  Voeg aan PokerHand.py methoden toe genaamd has\_pair, has\_twopair, enzovoort. De methoden retourneren True or False afhankelijk van of de hand wel/niet aan de bijbehorende criteria voldoet. Uw code moet werken voor “handen” met een willekeurig aantal kaarten (hoewel 5 en 7 het meeste worden gebruikt).
>     
> 4.  Schrijf een methode classify die eerst bepaalt wat de hoogste classificatie is voor een hand en vervolgens die classificatie vastlegt in het label attribuut. Bijvoorbeeld een 7-kaart hand kan een flush en een pair bevatten; het label moet dan “flush” worden.
>     
> 5.  Als u zeker weet dat de classificatie-methoden werken, dan is de volgende stap de kansen van de verschillende handen te bepalen. Schrijf een functie PokerHand.py die een stok kaarten schudt, verdeelt over de handen, de handen classificeert, en het aantal keren telt dat de verschillende classificaties verschijnen.
>     
> 6.  Maak een tabel van de classificaties en de bijbehorende kansen. Voer het programma uit met grotere en nog grotere aantallen handen, totdat de uitvoerwaarden convergeren c.q. niet teveel meer varieren. Vergelijk uw resultaten met de waarden van [wikipedia.org/wiki/Hand\_rankings](http://wikipedia.org/wiki/Hand_rankings).
>     
> 
> **Oefening 18.6** In deze oefening wordt TurtleWorld uit hoofdstuk 4 gebruikt. U gaat code schrijven zodat turtles het spel Tag spelen. Als u niet bekend bent met de regels van Tag, kijk dan op [wikipedia.org/wiki/Tag\_(game)](http://wikipedia.org/wiki/Tag_(game)).
> 
> 1.  Download [thinkpython.com/code/Wobbler.py](http://thinkpython.com/code/Wobbler.py) en voer het uit. U moet een TurtleWorld zien met drie turtles. Als u op de Runknop drukt, gaan de turtles willekeurig aan het wandelen.
>     
> 2.  Lees de code en zorg ervoor dat u begrijpt hoe de code werkt. De Wobbler klasse erft van Turtle, wat inhoudt dat de Turtle methoden lt, rt, fd en bk werken bij Wobblers.  
>     De stepmethode wordt aangeroepen door TurtleWorld. Eerst wordt steer aangeroepen zodat de turtle in de gewenste richting draait, daarna wobble met een willekeurige draai (in verhouding met de turtle’s onhandigheid), en tenslotte move zodat enkele pixels voorwaarts wordt bewogen afhankelijk van turtle’s snelheid.
>     
> 3.  Maak een bestand genaamd Tagger.py. Importeer alles van Wobbler, definieer dan een klasse Tagger die erft van Wobbler. Roep make\_world aan met het Tagger klasseobject als een argument.
>     
> 4.  Voeg een steer methode toe aan Tagger om die van Wobbler te overschrijven. Schrijf als eerste een versie waarbij de turtle naar de oorsprong wijst/kijkt. Hint: gebruik de wiskundefunctie atan2 en de turtle attributen x, y en heading.
>     
> 5.  Verander steer zodat de turtles zich netjes gedragen. Voor het debuggen zult u misschien de Stepknop willen gebruiken, die step éénmaal aanroept voor elke turtle.
>     
> 6.  Verandersteer zodat elke turtle wijst/kijkt naar de buur die het dichtste bij is. Hint: turtles hebben een attribute world, een referentie naar de TurtleWorld waarin ze leven, en de TurtleWorld heeft een attribuut animals, een lijst van alle turtles in de wereld.
>     
> 7.  Verander steer zodat de turtles Tag spelen. U kunt methoden toevoegen aan Tagger en u kunt steer en \_\_init\_\_ overschrijven. Maar u kunt step, wobble of move niet veranderen of overschrijven. Bovendien mag steer de kop van de turtle veranderen, maar niet de positie.
>     
> 
> Pas de regels aan en uw steer methode om het spel (kwalitatief) te verbeteren, bijvoorbeeld door het voor de langzame turtle mogelijk te maken de snellere turtles the "Taggen".
> 
> U kunt mijn oplossing vinden op [thinkpython.com/code/Tagger.py](http://thinkpython.com/code/Tagger.py).
> 
> * * *
> 
> 1 Zie wikipedia.org/wiki/Bottom\_dealing.
> 
> 2 De gebruikte diagrammen lijken veel op UML (zie wikipedia.org/wiki/Unified\_Modeling\_Language); wel zijn enkele vereenvoudigingen aangebracht.