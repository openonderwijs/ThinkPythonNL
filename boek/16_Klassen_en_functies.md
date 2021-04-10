[community/ThinkPython/HoofdstukZestien - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien)

# Hoofdstuk 16 Klassen and functies

## 16.1 Tijd

Als een ander voorbeeld van een door de gebruiker gedefinieerd type zullen we de klasse Tijd definiëren die de tijd van de dag registreert. De definitie ziet er zo uit:

function isnumbered(obj) { return obj.childNodes.length && obj.firstChild.childNodes.length && obj.firstChild.firstChild.className == 'LineNumber'; } function nformat(num,chrs,add) { var nlen = Math.max(0,chrs-(''+num).length), res = ''; while (nlen>0) { res += ' '; nlen-- } return res+num+add; } function addnumber(did, nstart, nstep) { var c = document.getElementById(did), l = c.firstChild, n = 1; if (!isnumbered(c)) { if (typeof nstart == 'undefined') nstart = 1; if (typeof nstep == 'undefined') nstep = 1; var n = nstart; while (l != null) { if (l.tagName == 'SPAN') { var s = document.createElement('SPAN'); var a = document.createElement('A'); s.className = 'LineNumber'; a.appendChild(document.createTextNode(nformat(n,4,''))); a.href = '#' + did + '\_' + n; s.appendChild(a); s.appendChild(document.createTextNode(' ')); n += nstep; if (l.childNodes.length) { l.insertBefore(s, l.firstChild); } else { l.appendChild(s); } } l = l.nextSibling; } } return false; } function remnumber(did) { var c = document.getElementById(did), l = c.firstChild; if (isnumbered(c)) { while (l != null) { if (l.tagName == 'SPAN' && l.firstChild.className == 'LineNumber') l.removeChild(l.firstChild); l = l.nextSibling; } } return false; } function togglenumber(did, nstart, nstep) { var c = document.getElementById(did); if (isnumbered(c)) { remnumber(did); } else { addnumber(did,nstart,nstep); } return false; } document.write('<a href="#" onclick="return togglenumber(\\'CA-f49826c67c5195df557ac1cd45c5add2ccb662d4\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f49826c67c5195df557ac1cd45c5add2ccb662d4_1) class Tijd(object):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f49826c67c5195df557ac1cd45c5add2ccb662d4_2)      """stelt de tijd van de dag voor.
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f49826c67c5195df557ac1cd45c5add2ccb662d4_3)  attributen: uur, minuut, seconde"""

We maken een nieuw Tijd object aan en kennen de attributen uren, minuten en seconden toe:

document.write('<a href="#" onclick="return togglenumber(\\'CA-78d39dabdc078c1d8151d029db8ee165f1573c2e\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-78d39dabdc078c1d8151d029db8ee165f1573c2e_1) tijd = Time()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-78d39dabdc078c1d8151d029db8ee165f1573c2e_2) tijd.uur = 11
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-78d39dabdc078c1d8151d029db8ee165f1573c2e_3) tijd.minuut = 59
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-78d39dabdc078c1d8151d029db8ee165f1573c2e_4) tijd.seconde = 30

Het toestandsdiagram voor het object Tijd ziet er zo uit:

-   ![boek025_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien?action=AttachFile&do=get&target=boek025_nl.png "boek025_nl.png")
    

**Oefening 16.1** Schrijf een functie genaamd print\_tijd die een Tijdobject ontvangt en deze weergeeft in het formaat uur:minuut:seconde. Aanwijzing: het patroon '%.2d' print een geheel getal, bestaande uit tenminste twee cijfers, en indien nodig een voorloopnul.

**Oefening 16.2** Schrijf een booleaanse functie genaamd is\_na dat twee Tijdobjecten ontvangt, t1 en t2, en True teruggeeft als t1 chronologisch volgt op t2. Anders moet het False teruggeven. Uitdaging: gebruik geen if instructie.

## 16.2 Pure functies

In de volgende paar secties, zullen we twee functies schrijven die tijdwaarden toevoegen. Deze demonstreren twee soorten functies: pure functies (pure functions) en veranderaars (modifiers). Zij demonstreren ook een ontwikkelplan dat ik **prototype en corrigeren** (prototype and patch) noem. Dit is een manier van aanpakken van complexe problemen door te beginnen met een simpel prototype en incrementeel de complicaties aan te pakken.

Hier is een eenvoudig prototype van voeg\_tijd\_toe:

document.write('<a href="#" onclick="return togglenumber(\\'CA-b80629225868628cb9b9436c421dcc34b20be2d3\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-b80629225868628cb9b9436c421dcc34b20be2d3_1) def voeg\_tijd\_toe(t1, t2):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-b80629225868628cb9b9436c421dcc34b20be2d3_2)       som = Time()
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-b80629225868628cb9b9436c421dcc34b20be2d3_3)       som.uur = t1.uur + t2.uur
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-b80629225868628cb9b9436c421dcc34b20be2d3_4)       som.minuut = t1.minuut + t2.minuut
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-b80629225868628cb9b9436c421dcc34b20be2d3_5)       som.seconde = t1.seconde + t2.seconde
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-b80629225868628cb9b9436c421dcc34b20be2d3_6) 
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-b80629225868628cb9b9436c421dcc34b20be2d3_7)       return som

De functie maakt een nieuw Tijdobject aan, initialiseert zijn attributen en geeft een referentie naar het nieuwe object terug. Dit wordt een **pure functie** genoemd omdat het geen objecten wijzigt, die als argumenten worden meegegeven. Ook heeft het geen effecten, zoals het weergeven van een waarde of het vragen om invoer aan de gebruiker, anders dan het teruggeven van een waarde.

Om deze functie te testen, zal ik twee Tijdobjecten maken; start bevat de starttijd van een film, zoals _Monty Python and the Holy Grail_ en duur bevat de looptijd van de film; deze is 1 uur en 35 minuten.

voeg\_tijd\_toe zoekt uit op welk tijdstip de film afgelopen is.

document.write('<a href="#" onclick="return togglenumber(\\'CA-8454082f2080898fe4563cb8c16afcb81270ed13\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_1) \>>>   start = Time()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_2) \>>>   start.uur = 9
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_3) \>>>   start.minuut = 45
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_4) \>>>   start.seconde = 0
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_5) 
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_6) \>>>   duur = Time()
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_7) \>>>   duur.uur = 1
 [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_8) \>>>   duur.minuut = 35
 [9](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_9) \>>>   duur.seconde = 0
 [10](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_10) 
 [11](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_11) \>>> afgelopen = voeg\_tijd\_toe(start, duur)
 [12](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_12) \>>> print\_time(afgelopen)
 [13](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-8454082f2080898fe4563cb8c16afcb81270ed13_13) 10:80:00

Het resultaat, 10:80:00 zal niet zijn wat u ervan verwachtte. Het probleem is dat deze functie niet werkt in het geval dat het aantal seconden of minuten boven de 60 uitkomt. Zodra dat gebeurt moeten we extra seconden naar de minutenkolom en extra minuten naar de urenkolom overhevelen.

Hierbij de verbeterde versie:

document.write('<a href="#" onclick="return togglenumber(\\'CA-f271d3efde5506cf0367ef7b6f12cbafdefed592\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_1) def voeg\_tijd\_toe(t1, t2):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_2)       som = Time()
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_3)       som.uur = t1.uur + t2.uur
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_4)       som.minuut = t1.minuut + t2.minuut
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_5)       som.seconde = t1.seconde + t2.seconde
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_6)       if som.seconde >= 60:
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_7)          som.seconde -= 60
 [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_8)          som.minuut += 1
 [9](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_9) 
 [10](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_10)       if som.minuut >= 60:
 [11](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_11)          som.minuut -= 60
 [12](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_12)          som.uur += 1
 [13](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_13) 
 [14](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-f271d3efde5506cf0367ef7b6f12cbafdefed592_14)       return som

Hoewel deze functie correct is, wordt deze wel erg groot. We komen later een korter alternatief tegen.

## 16.3 Veranderaars

Soms is het handig voor een functie om de als parameters ontvangen objecten te veranderen. In dat geval zijn de veranderingen zichtbaar voor de aanroeper. Functies die op deze manier werken, worden **veranderaars** (modifiers) genoemd.

verhoging, die een gegeven aantal seconden toevoegt aan het Tijdobject, kan natuurlijk als een veranderaar worden geschreven. Hier is een ruwe schets:

document.write('<a href="#" onclick="return togglenumber(\\'CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b_1) def verhoging(tijd, seconden):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b_2)       tijd.seconde += seconds
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b_3) 
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b_4)       if tijd.seconde >= 60:
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b_5)            tijd.seconde -= 60
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b_6)            tijd.minuut += 1
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b_7) 
 [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b_8)       if tijd.minuut >= 60:
 [9](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b_9)            tijd.minuut -= 60
 [10](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-eb82a55c19f32ce61fb088c400c2e0d313429d5b_10)            tijd.uur += 1

De eerste regel voert een simpele opdracht uit; de rest handelt de speciale zaken af zoals we die hiervoor zagen.

Is deze functie correct? Wat gebeurt er als de parameter seconden groter is dan 60?

In dat geval is het niet genoeg om één keer iets over te dragen. We moeten dat blijven doen totdat tijd.seconde kleiner is dan 60. Een oplossing is het vervangen van de if instructie door een while instructie. Dat zorgt ervoor dat de functie correct werkt maar het is niet erg efficiënt.

**Oefening 16.3** Schrijf een correcte versie van verhoging die geen enkele lus bevat.

Alles wat met veranderaars kan worden gedaan, kan ook met pure functies (pure functions) worden gedaan. In feite accepteren bepaalde programmeertalen alleen pure functies. Er is enig bewijs dat programma's die pure functies gebruiken sneller te ontwikkelen en minder foutgevoelig zijn dan programma's die veranderaars gebruiken. Maar in bepaalde gevallen zijn veranderaars handig en programma's met veel functies zijn wel eens minder efficiënt.

In het algemeen is mijn aanbeveling om pure functies te schrijven wanneer het mogelijk is en veranderaars alleen te gebruiken wanneer er een overduidelijk voordeel is te behalen. Deze aanpak wordt wel een **functionele programmeerstijl** genoemd.

**Oefening 16.4** Schrijf een "pure" versie van verhoging die een nieuw Tijdobject aanmaakt en teruggeeft, in plaats van het wijzigen van de parameter.

## 16.4 Prototype ontwikkeling of plannen

Het gedemonstreerde ontwikkelplan wordt "prototype en corrigeer" (prototype and patch) genoemd. Voor elke functie schreef ik een prototype die de basisberekening uitvoerde; die ik vervolgens testte en waarin ik ondertussen de fouten corrigeerde.

Deze aanpak kan effectief zijn, in het bijzonder als u geen diepgaande kennis hebt over het probleem. Maar correcties op correcties maken de code onnodig gecompliceerd, omdat het veel speciale gevallen kent. Ook wordt de code onbetrouwbaar, omdat onduidelijk is of we alle fouten hebben gevonden.

Een alternatief is **geplande ontwikkeling**, waarbij een op hoog niveau inzicht hebben in het probleem, het programmeren een stuk eenvoudiger maakt. In dit geval is het inzicht dat het Tijdobject eigenlijk een driecijferig nummer is met grondtal 60 (zie [nl.wikipedia.org/wiki/Sexagesimaal](http://nl.wikipedia.org/wiki/Sexagesimaal))! Het tweede attribuut is de "enen kolom", Het minuut attribuut is de "zestig kolom" en het uur attribuut is de "zesendertighonderd kolom".

Toen we voeg\_tijd\_toe en verhoging schreven, hebben we effectief een optelling met grondtal 60 uitgevoerd, daarom moesten we van de ene kolom naar de andere overdragen.

Deze waarneming suggereert een andere aanpak van het complete probleem, we kunnen het Tijdobject omzetten naar gehele getallen en gebruikmaken van het feit dat de computer kan rekenen met gehele getallen.

Hierbij een functie die de tijden omzet in gehele getallen:

document.write('<a href="#" onclick="return togglenumber(\\'CA-fd490bd4322487ad05a5611e7e79aa7bee30ef37\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-fd490bd4322487ad05a5611e7e79aa7bee30ef37_1) def tijd\_naar\_int(tijd):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-fd490bd4322487ad05a5611e7e79aa7bee30ef37_2)      minuten = tijd.uur \* 60 + tijd.minuut
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-fd490bd4322487ad05a5611e7e79aa7bee30ef37_3)      seconden = minuten \* 60 + tijd.seconde
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-fd490bd4322487ad05a5611e7e79aa7bee30ef37_4) 
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-fd490bd4322487ad05a5611e7e79aa7bee30ef37_5)      return seconden

En hieronder de functie die gehele getallen omzet in Tijd (ik herinner u eraan dat divmod het eerste argument deelt door het tweede en het quotiënt en de rest als een koppel terug geeft).

document.write('<a href="#" onclick="return togglenumber(\\'CA-be69ecb67c336d1998d77bf0b931040c063e9d75\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-be69ecb67c336d1998d77bf0b931040c063e9d75_1) def int\_naar\_tijd(seconds):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-be69ecb67c336d1998d77bf0b931040c063e9d75_2)      tijd = Time()
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-be69ecb67c336d1998d77bf0b931040c063e9d75_3)      minuten, tijd.seconde = divmod(seconds, 60)
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-be69ecb67c336d1998d77bf0b931040c063e9d75_4)      tijd.uur, tijd.minuut = divmod(minutes, 60)
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-be69ecb67c336d1998d77bf0b931040c063e9d75_5) 
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-be69ecb67c336d1998d77bf0b931040c063e9d75_6)      return tijd

U moet er mogelijk even over nadenken en testen uitvoeren om u ervan te overtuigen dat deze functies correct zijn. Een manier om deze te testen, is om te controleren dat tijd\_naar\_int(int\_naar\_tijd(x)) == x voor een groot aantal waarden van x geldt. Dit is een voorbeeld van een controle op consequentie.

Bent u er eenmaal van overtuigd dat de functies correct zijn, dan zijn deze te gebruiken om voeg\_tijd\_toe te herschrijven:

document.write('<a href="#" onclick="return togglenumber(\\'CA-6de487a0d4e83e13b128335fb944ff6f35a60aef\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-6de487a0d4e83e13b128335fb944ff6f35a60aef_1) def voeg\_tijd\_toe(t1, t2):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-6de487a0d4e83e13b128335fb944ff6f35a60aef_2)      seconden = tijd\_naar\_int(t1) + tijd\_naar\_int(t2)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-6de487a0d4e83e13b128335fb944ff6f35a60aef_3) 
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-6de487a0d4e83e13b128335fb944ff6f35a60aef_4)      return int\_naar\_tijd(seconden)

Deze versie is korter dan de oorspronkelijke en eenvoudiger te controleren.

**Oefening 16.5** Herschrijf verhoging door van tijd\_naar\_int en int\_naar\_tijd gebruik te maken.

In sommige opzichten is het omzetten van grondtal 60 naar grondtal 10 en weer terug lastiger dan met tijden te werken. Grondtallen omzetten is abstracter en intuïtief werken we beter met tijden.

Maar als we het inzicht hebben om tijd te behandelen als getallen met grondtal 60 en tijd besteden aan het schrijven van conversie functies (tijd\_naar\_int en int\_naar\_tijd), krijgen we een programma dat korter, eenvoudiger te lezen en te debuggen is en betrouwbaarder werkt.

Het is ook gemakkelijker om later onderdelen toe te voegen. Bijvoorbeeld: twee Tijden van elkaar aftrekken om de duur te bepalen. De naïeve aanpak zou de implementatie zijn van aftrekking met lenen. Door de conversie functies te gebruiken wordt dit eenvoudiger en waarschijnlijk eerder correct.

Ironisch genoeg is het moeilijker maken van een probleem (of meer algemeen) aan de andere kant weer gemakkelijker (omdat er minder speciale gevallen en minder kansen op fouten zijn).

## 16.5 Debuggen

Een Tijdobject is goed opgezet als de waarden voor minuten en seconden tussen de 0 en 60 liggen (inclusief 0 maar geen 60) en als de uren positief zijn. uren en minuten moeten gehele waarden zijn, maar voor seconds mogen we cijfers achter de komma toestaan.

Dit soort vereisten worden **invarianten** (invariants) genoemd, omdat deze altijd waar moeten zijn. Anders gezegd: als deze niet waar zijn, is er iets verkeerd gegaan.

Code schrijven om uw invarianten te controleren helpt u om de fouten en hun oorzaken te vinden. Bijvoorbeeld: u kunt een functie hebben zoals geldige\_tijd die een Tijdobject ontvangt en False teruggeeft als deze een invariant schendt:

document.write('<a href="#" onclick="return togglenumber(\\'CA-1893101162e4be13aa3d780f95f570597d50815b\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1893101162e4be13aa3d780f95f570597d50815b_1) def geldige\_tijd(time):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1893101162e4be13aa3d780f95f570597d50815b_2)        if tijd.uren < 0 or tijd.minuten < 0 or tijd.seconden < 0:
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1893101162e4be13aa3d780f95f570597d50815b_3)            return False
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1893101162e4be13aa3d780f95f570597d50815b_4) 
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1893101162e4be13aa3d780f95f570597d50815b_5)        if tijd.minuten >= 60 or tijd.seconden >= 60:
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1893101162e4be13aa3d780f95f570597d50815b_6)            return False
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1893101162e4be13aa3d780f95f570597d50815b_7) 
 [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1893101162e4be13aa3d780f95f570597d50815b_8)        return True

Controleer aan het begin van elke functie de argumenten om er zeker van te zijn dat deze geldig zijn:

document.write('<a href="#" onclick="return togglenumber(\\'CA-5d238ad61fd8a7e0ed6177af34a38a93f6a9b3dd\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-5d238ad61fd8a7e0ed6177af34a38a93f6a9b3dd_1) def voeg\_tijd\_toe(t1, t2):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-5d238ad61fd8a7e0ed6177af34a38a93f6a9b3dd_2)        if not geldige\_tijd(t1) or not geldige\_tijd(t2):
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-5d238ad61fd8a7e0ed6177af34a38a93f6a9b3dd_3)            raise ValueError, 'ongeldig tijd object in voeg\_tijd\_toe'
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-5d238ad61fd8a7e0ed6177af34a38a93f6a9b3dd_4) 
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-5d238ad61fd8a7e0ed6177af34a38a93f6a9b3dd_5)        seconden = tijd\_naar\_int(t1) + tijd\_naar\_int(t2)
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-5d238ad61fd8a7e0ed6177af34a38a93f6a9b3dd_6) 
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-5d238ad61fd8a7e0ed6177af34a38a93f6a9b3dd_7)        return int\_naar\_tijd(seconden)

Of u kunt een assert instructie gebruiken, die een gegeven invariant controleert en een foutmelding geeft als het fout gaat:

document.write('<a href="#" onclick="return togglenumber(\\'CA-1bf16dcb0e749b8b4607a7e257d173350d395c51\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1bf16dcb0e749b8b4607a7e257d173350d395c51_1) def voeg\_tijd\_toe(t1, t2):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1bf16dcb0e749b8b4607a7e257d173350d395c51_2)        assert geldige\_tijd(t1) and geldige\_tijd(t2)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1bf16dcb0e749b8b4607a7e257d173350d395c51_3)        seconden = tijd\_naar\_int(t1) + tijd\_naar\_int(t2)
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1bf16dcb0e749b8b4607a7e257d173350d395c51_4) 
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukZestien#CA-1bf16dcb0e749b8b4607a7e257d173350d395c51_5)        return int\_naar\_tijd(seconden)

assert instructies zijn handig omdat deze code - die met normale vergelijkingen werkt - zich onderscheidt van code die op fouten controleert.

## 16.6 Woordenlijst

**prototype en corrigeren**: Een ontwikkelplan dat het schrijven van een ruw ontwerp omvat plus het testen en corrigeren van fouten zodra die zijn gevonden.

**Geplande ontwikkeling**: Een ontwikkelplan dat op hoog niveau inzicht in het probleem en meer planning vereist dan incrementeel ontwikkelen of prototype-ontwikkeling.

**pure functie**: Een functie die geen enkele van de objecten die zij ontvangt, zoals argumenten, wijzigt. De meeste pure functies zijn productief.

**veranderaar**: Een functie, die één of meer objecten, die als argumenten meegegeven zijn, wijzigt. De meeste veranderaars zijn niet zo productief.

**functionele programmeerstijl**: Een stijl van programmaontwerp waarin hoofdzakelijk pure functies gebruikt zijn.

**invariant**: Een conditie die altijd "true" dient te zijn tijdens de uitvoering van een programma.

## 16.7 Oefeningen

**Oefening 16.6** Schrijf een functie genaamd vermenigvuldig\_tijd die een Tijdobject en een getal ontvangt en een nieuw Tijdobject teruggeeft dat het product bevat van de oorspronkelijke Tijd en het getal.

Gebruik daarna vermenigvuldig\_tijd om een functie te schrijven die een Tijdobject ontvangt, dat de aankomsttijd (de tijd wordt op 0 gestart) in een race voorstelt, en een getal, dat de afstand voorstelt; en een Tijdobject teruggeeft, dat de gemiddelde snelheid voor moet stellen (km per uur).

**Oefening 16.7** Schrijf een klassedefinitie voor een Datumobject die de attributen dag, maand en jaar heeft. Schrijf een functie genaamd verhoog\_datum die het Datumobject datum ontvangt en een geheel getal n, en een nieuw Datumobject teruggeeft, dat de dag n dagen na datum voorstelt. Aanwijzing: "September heeft dertig dagen ..." Uitdaging: gaat uw functie correct om met schrikkeljaren? Zie [nl.wikipedia.org/wiki/Schrikkeljaar](http://nl.wikipedia.org/wiki/Schrikkeljaar).

**Oefening 16.8** De datetime module levert datum en tijd objecten die gelijk zijn aan de Datum- en Tijdobjecten in dit hoofdstuk maar deze leveren een uitgebreide set aan methoden en operatoren. Lees de documentatie erop na bij [docs.python.org/lib/datetime-date.html](http://docs.python.org/lib/datetime-date.html).

1.  Gebruik de datetime module om een programma te schrijven dat de huidige datum ophaalt en de dag van de week print.  
    
2.  Schrijf een programma dat een verjaardag als invoer ontvangt en de leeftijd van de gebruiker en het aantal dagen, uren, minuten en seconden tot aan zijn volgende verjaardag print.