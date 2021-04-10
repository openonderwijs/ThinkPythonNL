[community/ThinkPython/HoofdstukVijftien - Ubuntu NL wiki](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien)

# Hoofdstuk 15 Klassen en objecten

## 15.1 Zelf gedefinieerde typen

Veel van de ingebouwde typen uit Python zijn in de vorige hoofdstukken gebruikt. Nu is het de beurt aan een nieuw type. Als voorbeeld zullen we een type aanmaken genaamd Punt; deze vertegenwoordigt een punt in een twee dimensionale omgeving.

In wiskundige notaties worden punten vaak geschreven tussen haakjes en een komma tussen de coördinaten. Bijvoorbeeld: (0, 0) vertegenwoordigt het beginpunt en (_x, y_) vertegenwoordigt het punt dat _x_ eenheden naar rechts en _y_ eenheden naar boven, ten opzichte van het beginpunt ligt.

We kunnen op verschillende manieren punten definiëren in Python:

-   • We kunnen de coördinaten afzonderlijk in twee variabelen, x en y opslaan.  
    • We kunnen de coördinaten als elementen in een lijst of tupel opslaan.  
    • We kunnen een nieuw type aanmaken om punten als objecten weer te geven.  
    

Een nieuw type aanmaken is een beetje ingewikkelder dan de andere opties maar biedt veel voordelen, die dadelijk duidelijk worden.

Een zelf gedefinieerd type wordt wel een **Klasse** (class) genoemd. Een klassedefinitie lijkt hierop:

function isnumbered(obj) { return obj.childNodes.length && obj.firstChild.childNodes.length && obj.firstChild.firstChild.className == 'LineNumber'; } function nformat(num,chrs,add) { var nlen = Math.max(0,chrs-(''+num).length), res = ''; while (nlen>0) { res += ' '; nlen-- } return res+num+add; } function addnumber(did, nstart, nstep) { var c = document.getElementById(did), l = c.firstChild, n = 1; if (!isnumbered(c)) { if (typeof nstart == 'undefined') nstart = 1; if (typeof nstep == 'undefined') nstep = 1; var n = nstart; while (l != null) { if (l.tagName == 'SPAN') { var s = document.createElement('SPAN'); var a = document.createElement('A'); s.className = 'LineNumber'; a.appendChild(document.createTextNode(nformat(n,4,''))); a.href = '#' + did + '\_' + n; s.appendChild(a); s.appendChild(document.createTextNode(' ')); n += nstep; if (l.childNodes.length) { l.insertBefore(s, l.firstChild); } else { l.appendChild(s); } } l = l.nextSibling; } } return false; } function remnumber(did) { var c = document.getElementById(did), l = c.firstChild; if (isnumbered(c)) { while (l != null) { if (l.tagName == 'SPAN' && l.firstChild.className == 'LineNumber') l.removeChild(l.firstChild); l = l.nextSibling; } } return false; } function togglenumber(did, nstart, nstep) { var c = document.getElementById(did); if (isnumbered(c)) { remnumber(did); } else { addnumber(did,nstart,nstep); } return false; } document.write('<a href="#" onclick="return togglenumber(\\'CA-cb5418bba5be3b34294a2706136d8d90f8c8b380\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-cb5418bba5be3b34294a2706136d8d90f8c8b380_1) class Punt(object):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-cb5418bba5be3b34294a2706136d8d90f8c8b380_2)       """vertegenwoordigt een punt in een 2-D omgeving"""

Deze kop geeft aan dat de nieuwe klasse een Punt is van het soort object, dat een ingebouwd type is.

De body is een documentstring die uitleg geeft over de functie van de klasse. U kunt variabelen en functies definiëren binnenin een klassedefinitie maar we komen hier later op terug.

Het definiëren van een klasse genaamd Punt maakt een klasseobject aan.

document.write('<a href="#" onclick="return togglenumber(\\'CA-e60934df2b990cde293ca26a90809ab3fc4c792a\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-e60934df2b990cde293ca26a90809ab3fc4c792a_1) \>>> print Punt
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-e60934df2b990cde293ca26a90809ab3fc4c792a_2) <class '\_\_main\_\_.Punt'\>

Omdat Punt is gedefinieerd op het hoogste niveau, is zijn "volledige naam" \_\_main\_\_.Punt.

Het klasseobject is net een fabriek die objecten aanmaakt. Om een Punt aan te maken roept u Punt aan alsof het een functie is.

document.write('<a href="#" onclick="return togglenumber(\\'CA-76221dd0456713f60de8fc9606bf69c604abdb34\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-76221dd0456713f60de8fc9606bf69c604abdb34_1) \>>> blanco = Punt()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-76221dd0456713f60de8fc9606bf69c604abdb34_2) \>>> print blanco
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-76221dd0456713f60de8fc9606bf69c604abdb34_3) <\_\_main\_\_.Punt instance at 0xb7e9d3ac\>

De antwoordwaarde is een verwijzing naar een Punt object, die we aan blanco toe wijzen. Een nieuw object aanmaken wordt **instantiation** (concretisering) genoemd en het object is een **instantie** van een klasse.

Wanneer u een instantie print, vertelt Python u tot welke klasse deze behoort en waar deze in het geheugen is opgeslagen; het voorvoegsel 0x betekent dat het volgende getal hexadecimaal is.

## 15.2 Attributen

U kunt waarden aan een instantie toekennen met behulp van de punt-notatie:

document.write('<a href="#" onclick="return togglenumber(\\'CA-3142417ef7861c90722e6242040e141ab80afed6\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3142417ef7861c90722e6242040e141ab80afed6_1) \>>> blanco.x = 3.0
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3142417ef7861c90722e6242040e141ab80afed6_2) \>>> blanco.y = 4.0

Deze zinsbouw komt overeen met de zinsbouw voor het selecteren van een variabele uit een module zoals math.pi of string.whitespace. In dit geval echter kennen we de waarden toe aan benoemde elementen van een object. Deze elementen worden **attributen** genoemd.

Het volgende diagram geeft het resultaat weer van deze toewijzing. Een statusdiagram dat een object en zijn attributen weergeeft wordt een **objectdiagram** genoemd:

-   ![boek022_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien?action=AttachFile&do=get&target=boek022_nl.png "boek022_nl.png")
    

De variabele blanco verwijst naar een Punt object dat twee attributen bevat. Elk attribuut verwijst naar een floating-point getal.

U kunt de waarde van een attribuut lezen door gebruik te maken van dezelfde zinsbouw:

document.write('<a href="#" onclick="return togglenumber(\\'CA-d728e811424d3d82fbd8436757355ef3ff6f8969\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-d728e811424d3d82fbd8436757355ef3ff6f8969_1) \>>> print blanco.y
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-d728e811424d3d82fbd8436757355ef3ff6f8969_2) 4.0
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-d728e811424d3d82fbd8436757355ef3ff6f8969_3) \>>> x = blanco.x
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-d728e811424d3d82fbd8436757355ef3ff6f8969_4) \>>> print x
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-d728e811424d3d82fbd8436757355ef3ff6f8969_5) 3.0

De expressie blanco.x betekent: "Ga naar het object blanco; verwijs naar en haal de waarde van x op". In dit geval kennen we de waarde toe aan een variabele genaamd x. Er bestaat geen conflict tussen de variabele x en het attribuut x.

U kunt de punt-notatie gebruiken als onderdeel van iedere expressie. Bijvoorbeeld:

document.write('<a href="#" onclick="return togglenumber(\\'CA-fb7552711907594f16cd2b29df7875d7d387c3ab\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-fb7552711907594f16cd2b29df7875d7d387c3ab_1) \>>> print '(%g, %g)' % (blanco.x, blanco.y)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-fb7552711907594f16cd2b29df7875d7d387c3ab_2) (3.0, 4.0)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-fb7552711907594f16cd2b29df7875d7d387c3ab_3) \>>> afstand\= math.sqrt(blanco.x\*\*2 + blanco.y\*\*2)
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-fb7552711907594f16cd2b29df7875d7d387c3ab_4) \>>> print afstand
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-fb7552711907594f16cd2b29df7875d7d387c3ab_5) 5.0

U kunt een instantie doorgeven als een argument op de gebruikelijke manier. Bijvoorbeeld:

document.write('<a href="#" onclick="return togglenumber(\\'CA-b0f0d3068cb6dc052bffdeec2a10f2df63dd7b28\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-b0f0d3068cb6dc052bffdeec2a10f2df63dd7b28_1) def print\_punt(p):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-b0f0d3068cb6dc052bffdeec2a10f2df63dd7b28_2)       print '(%g, %g)' % (p.x, p.y)

print\_punt krijgt een punt als argument mee en geeft dit weer in een wiskundige notatie. Om dit aan te roepen geeft u blanco als een argument mee:

document.write('<a href="#" onclick="return togglenumber(\\'CA-d2dd1be0786a0683ece43d00f7e6d482b87c824f\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-d2dd1be0786a0683ece43d00f7e6d482b87c824f_1) \>>> print\_punt(blanco)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-d2dd1be0786a0683ece43d00f7e6d482b87c824f_2) (3.0, 4.0)

Binnenin de functie is p een alias voor blanco, dus als de functie p wijzigt, verandert blanco ook.

**Oefening 15.1** Schrijf een functie genaamd afstand die de twee punten als argumenten meekrijgt en de afstand tussen die twee teruggeeft.

## 15.3 Rechthoeken

Soms ligt het voor de hand wat de attributen voor een object zijn maar in andere gevallen moet u zelf een beslissing nemen. Bijvoorbeeld: Stel u voor dat u een klasse ontwerpt die rechthoeken vertegenwoordigt. Welke attributen zou u gebruiken om de locatie en de afmeting van een rechthoek te specificeren? U kunt de hoek negeren om het simpel te houden en aannemen dat de rechthoek of verticaal of horizontaal is.

Er bestaan tenminste twee mogelijkheden:

-   • U kunt een hoek van de rechthoek (of het centrum), de breedte en de hoogte specificeren.  
    • U kunt de tegenovergestelde hoeken specificeren.
    

Op dit moment is het moeilijk te zeggen welke mogelijkheid beter is, dus zullen we de eerste mogelijkheid uitwerken, gewoon als voorbeeld.

Hierbij de klasse definitie:

document.write('<a href="#" onclick="return togglenumber(\\'CA-3c4d60d97ee6041602e3de67f048dec6faeb884a\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3c4d60d97ee6041602e3de67f048dec6faeb884a_1) class rechthoek(object):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3c4d60d97ee6041602e3de67f048dec6faeb884a_2)       """vertegenwoordigt een rechthoek.
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3c4d60d97ee6041602e3de67f048dec6faeb884a_3)  attributen: breedte, hoogte en hoek.
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3c4d60d97ee6041602e3de67f048dec6faeb884a_4)  """

de documentstring heeft de volgende attributen: breedte en hoogte zijn getallen, hoek is een Punt object die de linker onderhoek aanduidt.

Om een rechthoek af te beelden moet u een instantie aanmaken voor een rechthoekobject en waarden toekennen aan de attributen:

document.write('<a href="#" onclick="return togglenumber(\\'CA-28d0e307bc80b99663b4c6450bb2274436305bed\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-28d0e307bc80b99663b4c6450bb2274436305bed_1) doos = rechthoek()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-28d0e307bc80b99663b4c6450bb2274436305bed_2) doos.breedte = 100.0
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-28d0e307bc80b99663b4c6450bb2274436305bed_3) doos.hoogte = 200.0
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-28d0e307bc80b99663b4c6450bb2274436305bed_4) doos.hoek = Punt()
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-28d0e307bc80b99663b4c6450bb2274436305bed_5) doos.hoek.x = 0.0
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-28d0e307bc80b99663b4c6450bb2274436305bed_6) doos.hoek.y = 0.0

De expressie doos.hoek.x betekent: "Ga naar het object doos; verwijs naar en selecteer het attribuut genaamd hoek, ga vervolgens naar dat object en selecteer het attribuut genaamd x".

De figuur geeft de status van dit object weer:

-   ![boek023_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien?action=AttachFile&do=get&target=boek023_nl.png "boek023_nl.png")
    

Een object dat een attribuut is van een ander object is **ingesloten**.

## 15.4 Instantie als antwoordwaarde

Functies kunnen instanties teruggeven. Bijvoorbeeld: zoek\_het\_midden krijgt een Driehoek als een argument mee en geeft een Punt terug die de coördinaten van het midden van de Rechthoek bevat:

document.write('<a href="#" onclick="return togglenumber(\\'CA-134d069978f0775cb6490794a4a93724bf555f57\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-134d069978f0775cb6490794a4a93724bf555f57_1) def zoek\_het\_midden(doos):
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-134d069978f0775cb6490794a4a93724bf555f57_2)      p = Punt()
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-134d069978f0775cb6490794a4a93724bf555f57_3)      p.x = doos.hoek.x + doos.breedte/2.0
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-134d069978f0775cb6490794a4a93724bf555f57_4)      p.y = doos.hoek.y + doos.hoogte/2.0
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-134d069978f0775cb6490794a4a93724bf555f57_5)      return p

Hierbij een voorbeeld die doos als een argument doorgeeft en het resultaat, Punt, toekent aan midden:

document.write('<a href="#" onclick="return togglenumber(\\'CA-2be8148fb5b88e4e9c5f6180ccd2f41315285d65\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2be8148fb5b88e4e9c5f6180ccd2f41315285d65_1) \>>> center = zoek\_het\_midden(doos)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2be8148fb5b88e4e9c5f6180ccd2f41315285d65_2) \>>> print\_punt(midden)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2be8148fb5b88e4e9c5f6180ccd2f41315285d65_3) (50.0, 100.0)

## 15.5 Objecten zijn te wijzigen

U kunt de staat van een object wijzigen door iets aan zijn attributen toe te wijzen. Bijvoorbeeld: de grootte van een rechthoek wijzigen zodat de positie veranderd kan worden door de waarden van de breedte of de hoogte aan te passen:

document.write('<a href="#" onclick="return togglenumber(\\'CA-45f97052e41908293558455a6059447c60fa2c74\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-45f97052e41908293558455a6059447c60fa2c74_1) doos.breedte\= doos.breedte\+ 50
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-45f97052e41908293558455a6059447c60fa2c74_2) doos.hoogte\= doos.hoogte\+ 100

U kunt ook een functie schrijven die de objecten aanpast. Bijvoorbeeld: groei\_driehoek krijgt een rechthoekobject en twee getallen dbreedte en dhoogte deze getallen worden opgeteld bij de breedte en de hoogte van de rechthoek:

document.write('<a href="#" onclick="return togglenumber(\\'CA-dbdcdaf4392d980d79873b688772d2c6a6ffeb85\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-dbdcdaf4392d980d79873b688772d2c6a6ffeb85_1) def groei\_rechthoek(recht, dbreedte, dhoogte) :
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-dbdcdaf4392d980d79873b688772d2c6a6ffeb85_2)      recht.breedte += dbreedte
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-dbdcdaf4392d980d79873b688772d2c6a6ffeb85_3)      recht.hoogte += dhoogte

Hierbij een voorbeeld dat het effect demonstreert:

document.write('<a href="#" onclick="return togglenumber(\\'CA-2d31cee69a803b13c1e63e1aed082f2b80ef93e9\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2d31cee69a803b13c1e63e1aed082f2b80ef93e9_1) \>>> print doos.breedte 
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2d31cee69a803b13c1e63e1aed082f2b80ef93e9_2) 100.0
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2d31cee69a803b13c1e63e1aed082f2b80ef93e9_3) \>>> print doos.hoogte 
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2d31cee69a803b13c1e63e1aed082f2b80ef93e9_4) 200.0
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2d31cee69a803b13c1e63e1aed082f2b80ef93e9_5) \>>> groei\_rechthoek(doos, 50, 100)
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2d31cee69a803b13c1e63e1aed082f2b80ef93e9_6) \>>> print doos.breedte 
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2d31cee69a803b13c1e63e1aed082f2b80ef93e9_7) 150.0
 [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2d31cee69a803b13c1e63e1aed082f2b80ef93e9_8) \>>> print doos.hoogte 
 [9](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2d31cee69a803b13c1e63e1aed082f2b80ef93e9_9) 300.0

Binnenin de functie is recht een alias voor doos, dus als u de functie recht aanpast, wijzigt doos.

**Oefening 15.2** Schrijf een functie genaamd verplaats\_rechthoek die een rechthoek en twee getallen dx}} en {{{dy meekrijgt. Deze moet de locatie van de rechthoek veranderen door dx op te tellen bij de x coördinaat van de hoek en dy op te tellen bij de y coördinaat van de hoek.

## 15.6 Kopiëren

Het gebruik van aliassen kan een programma moeilijk leesbaar maken omdat veranderingen op één plaats onverwachte wijzigingen op een andere plaats tot gevolg heeft. Het is moeilijk om alle variabelen bij te houden die mogelijk naar een ander gegeven object verwijzen..

Kopiëren van een object is vaak een alternatief voor een alias. De kopie module bevat een functie genaamd copy die een object kan dupliceren:

document.write('<a href="#" onclick="return togglenumber(\\'CA-3b07f9f6331b2f9e29c6e6e7d16eb3279a0aa223\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3b07f9f6331b2f9e29c6e6e7d16eb3279a0aa223_1) \>>> p1 = Punt()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3b07f9f6331b2f9e29c6e6e7d16eb3279a0aa223_2) \>>> p1.x = 3.0
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3b07f9f6331b2f9e29c6e6e7d16eb3279a0aa223_3) \>>> p1.y = 4.0
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3b07f9f6331b2f9e29c6e6e7d16eb3279a0aa223_4) \>>> import copy
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-3b07f9f6331b2f9e29c6e6e7d16eb3279a0aa223_5) \>>> p2 = copy.copy(p1)

p1 en p2 bevatten dezelfde gegevens maar ze zijn niet hetzelfde Punt.

document.write('<a href="#" onclick="return togglenumber(\\'CA-62c82e524eb6bdaf1c67b614505fc8b158d5bb2b\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-62c82e524eb6bdaf1c67b614505fc8b158d5bb2b_1) \>>> print\_punt(p1)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-62c82e524eb6bdaf1c67b614505fc8b158d5bb2b_2) (3.0, 4.0)
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-62c82e524eb6bdaf1c67b614505fc8b158d5bb2b_3) \>>> print\_punt(p2)
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-62c82e524eb6bdaf1c67b614505fc8b158d5bb2b_4) (3.0, 4.0)
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-62c82e524eb6bdaf1c67b614505fc8b158d5bb2b_5) \>>> p1 is p2
 [6](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-62c82e524eb6bdaf1c67b614505fc8b158d5bb2b_6) False
 [7](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-62c82e524eb6bdaf1c67b614505fc8b158d5bb2b_7) \>>> p1 == p2
 [8](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-62c82e524eb6bdaf1c67b614505fc8b158d5bb2b_8) False

De is operator geeft aan dat p1 en p2 niet hetzelfde object zijn; dat is ook wat we verwachten. Maar u zou kunnen verwachten dat \== wel waar zou zijn dus een True op zou leveren, omdat deze punten dezelfde gegevens bevatten. Echter voor instanties is het standaard gedrag van de \== operator hetzelfde als de is operator. Deze controleert de identiteit van het object, niet de gelijkwaardigheid van het object. Dit gedrag kan veranderd worden, later zullen we zien hoe.

Gebruikt u copy.copy om een rechthoek te dupliceren, dan zult u zien dat deze het object rechthoek kopieert maar niet het ingesloten object Punt.

document.write('<a href="#" onclick="return togglenumber(\\'CA-16fdbff6a4f256663e863eda09661146b2385d9c\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-16fdbff6a4f256663e863eda09661146b2385d9c_1) \>>> doos2 = copy.copy(doos)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-16fdbff6a4f256663e863eda09661146b2385d9c_2) \>>> doos2 is box
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-16fdbff6a4f256663e863eda09661146b2385d9c_3) False
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-16fdbff6a4f256663e863eda09661146b2385d9c_4) \>>> doos2.hoek is doos.hoek
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-16fdbff6a4f256663e863eda09661146b2385d9c_5) True

Zie hier hoe het object diagram eruit ziet:

-   ![boek024_nl.png](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien?action=AttachFile&do=get&target=boek024_nl.png "boek024_nl.png")
    

Deze bewerking wordt een **oppervlakkige kopie** genoemd, omdat deze het object en bijbehorende referenties kopieert maar niet de ingesloten objecten.

Voor de meeste applicaties is dit precies wat u zou willen. In dit voorbeeld, het aanroepen van groei\_rechthoek zal één van de rechthoeken de andere niet beïnvloeden maar het aanroepen van verplaats\_rechthoek op één van de twee zal beiden beïnvloeden! Dit gedrag is verwarrend en foutgevoelig.

Gelukkig heeft de copy module een methode genaamd deepcopy die niet alleen het object kopieert, maar ook de objecten waar deze naar verwijst en de objecten waar _deze_ vervolgens naar verwijzen, enzovoorts. Daarom is het niet verrassend dat deze bewerking een **diepe kopie** wordt genoemd.

document.write('<a href="#" onclick="return togglenumber(\\'CA-6efabd3f0c206b425f99cc9def4f1f80e8fc5e80\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-6efabd3f0c206b425f99cc9def4f1f80e8fc5e80_1) \>>> doos3 = copy.deepcopy(box)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-6efabd3f0c206b425f99cc9def4f1f80e8fc5e80_2) \>>> doos3 is doos
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-6efabd3f0c206b425f99cc9def4f1f80e8fc5e80_3) False
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-6efabd3f0c206b425f99cc9def4f1f80e8fc5e80_4) \>>> doos3.corner is doos.corner
 [5](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-6efabd3f0c206b425f99cc9def4f1f80e8fc5e80_5) False

doos3 en doos zijn totaal gescheiden objecten.

**Oefening 15.3** Schrijf een versie van verplaats\_rechthoek die een nieuwe rechthoek aanmaakt en een nieuwe rechthoek teruggeeft, in plaats van de oude aan te passen.

## 15.7 Debuggen

Zodra u met object gaat werken, zult u waarschijnlijk nieuwe uitzonderingen ontdekken. Probeert u een attribuut te benaderen dat niet bestaat dan krijgt u een AttributeError:

document.write('<a href="#" onclick="return togglenumber(\\'CA-2c1af25486c35932bdcc6b1874c6cda0c488c876\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2c1af25486c35932bdcc6b1874c6cda0c488c876_1) \>>> p = Punt()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2c1af25486c35932bdcc6b1874c6cda0c488c876_2) \>>> print p.z
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-2c1af25486c35932bdcc6b1874c6cda0c488c876_3) AttributeError: Point instance has no attribute 'z'

Bent u er niet zeker van tot welk type het object behoort, dan kunt u dat vragen:

document.write('<a href="#" onclick="return togglenumber(\\'CA-ce3aa1aafc9928a584d335eeaa5b474ee9299105\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-ce3aa1aafc9928a584d335eeaa5b474ee9299105_1) \>>> type(p)
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-ce3aa1aafc9928a584d335eeaa5b474ee9299105_2) <type '\_\_main\_\_.Punt'\>

Weet u niet zeker of een object een specifiek attribuut heeft, dan kunt u de ingebouwde functie gebruiken hasattr:

document.write('<a href="#" onclick="return togglenumber(\\'CA-7d2f839e917b9bedd81ab6ca4a63bc1cdeb2e78a\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-7d2f839e917b9bedd81ab6ca4a63bc1cdeb2e78a_1) \>>> hasattr(p, 'x')
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-7d2f839e917b9bedd81ab6ca4a63bc1cdeb2e78a_2) True
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-7d2f839e917b9bedd81ab6ca4a63bc1cdeb2e78a_3) \>>> hasattr(p, 'z')
 [4](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-7d2f839e917b9bedd81ab6ca4a63bc1cdeb2e78a_4) False

Het eerste argument kan elk object zijn; het tweede argument is een string die de naam bevat van het attribuut.

## 15.8 Woordenlijst

**klasse**: Een door de gebruiker gedefinieerd type. Een klassedefinitie maakt een nieuw klasseobject aan.

**klasseobject**: Een object dat informatie bevat over een door de gebruiker gedefinieerd type. Het klasseobject kan gebruikt worden om instanties van het type te maken.

**instantie**: Een object dat tot een klasse behoort.

**attribuut**: Een van de benoemde waarden verbonden met een object.

**ingesloten (object)**: Een object dat is opgeslagen als een attribuut van een ander object.

**oppervlakkige kopie**: Om de inhoud van een object te kopiëren, inclusief alle verwijzingen naar ingesloten objecten. Geëffectueerd door de "copy" functie in de "copy" module.

**diepe kopie**: Om de inhoud van een object te kopiëren tezamen met de ingesloten objecten en ieder object daar weer binnenin, enzovoorts. Geëffectueerd door de "deepcopy" functie in de "copy" module.

**objectdiagram**: Een diagram dat de objecten, hun attributen en de waarden van de attributen weergeeft.

## 15.9 Oefeningen

**Oefening 15.4** World.py, dit is een onderdeel van Swampy (zie hoofdstuk 4) en bevat een klassedefinitie voor een door de gebruiker gedefinieerd type genaamd World. U kunt dit als volgt importeren:

from World import World

Deze versie van de import instructie importeert de World klasse uit de World module. De volgende code maakt een World object aan en roept de mainloop methode aan, die wacht op de gebruiker.

document.write('<a href="#" onclick="return togglenumber(\\'CA-7a1dd2c287e1755374c0957f2b5a2fbbc78d940f\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-7a1dd2c287e1755374c0957f2b5a2fbbc78d940f_1) world = World()
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-7a1dd2c287e1755374c0957f2b5a2fbbc78d940f_2) world.mainloop()

Een venster moet verschijnen met een titelbalk en een leeg vierkant. We zullen het venster gebruiken voor het tekenen van Punten, Rechthoeken en andere figuren. Voeg de volgende regels toe vóór de aanroep van mainloop en voer het programma opnieuw uit.

document.write('<a href="#" onclick="return togglenumber(\\'CA-8af98724cf58e3bf6084524488842e1b8144d19d\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)

 [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-8af98724cf58e3bf6084524488842e1b8144d19d_1) doek = world.ca(breedte\=500, hoogte\=500, achtergrond\='white')
 [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-8af98724cf58e3bf6084524488842e1b8144d19d_2) bdoos = \[\[-150,-100\], \[150, 100\]\]
 [3](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-8af98724cf58e3bf6084524488842e1b8144d19d_3) doek.rechthoek(bdoos, omtrek\='black', breedte\=2, vulling\='green4')

U moet een groene rechthoek met een zwarte omtrek zien. De eerste regel maakt het doek aan, die in het venster als een wit vierkant verschijnt. Het doekobject levert methoden zoals rechthoek voor het tekenen van verschillende figuren.

bdoos is een lijst die een "begrensde doos" van de rechthoek vertegenwoordigt. Het eerste paar coördinaten zijn die van de linker onderhoek van de rechthoek, het tweede paar zijn die van de rechter bovenhoek.

U kunt een cirkel als volgt tekenen:

doek.cirkel(\[-25,0\], 70, omtrek=None, vulling='red')

De eerste parameter is het coördinatenpaar voor het middelpunt van de cirkel, de tweede parameter is de straal.

Voegt u deze regels toe aan het programma, dan is het resultaat de nationale vlag van Bangladesh (zie [nl.wikipedia.org/wiki/Vlaggen\_van\_de\_wereld](http://nl.wikipedia.org/wiki/Vlaggen_van_de_wereld)).

1.  Schrijf een functie genaamd teken\_rechthoek die een doek en een rechthoek meekrijgt als argumenten en een afbeelding van een rechthoek op het doek tekent.
    
2.  Voeg een attribuut, genaamd kleur, toe aan uw rechthoekobjecten en pas teken\_rechthoek aan zodat deze het attribuut kleur gebruikt als opvulkleur.
    
3.  Schrijf een functie genaamd teken\_punt die een doek en een Punt als argumenten meekrijgt en een afbeelding van een punt op het doek tekent.
    
4.  Definieer een nieuwe klasse genaamd Cirkel met geschikte attributen en maak een aantal Cirkelobjecten. Schrijf een functie genaamd teken\_cirkel die een cirkel op het doek tekent.
    
5.  Schrijf een programma die de nationale vlag van de Tsjechische republiek tekent. Tip: U kunt een polygoon als volgt tekenen:
    
    document.write('<a href="#" onclick="return togglenumber(\\'CA-0496fb1926aa45253c2f459a4029c1f7865f92c6\\', 1, 1);" \\ class="codenumbers">Regelnummers aan/uit<\\/a>'); [Regelnummers aan/uit](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#)
    
     [1](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-0496fb1926aa45253c2f459a4029c1f7865f92c6_1) punten = \[\[-150,-100\], \[150, 100\], \[150, -100\]\]
     [2](https://wiki.ubuntu-nl.org/community/ThinkPython/HoofdstukVijftien#CA-0496fb1926aa45253c2f459a4029c1f7865f92c6_2) doek.polygoon(punten, vulling\='blue')
    

Ik heb een klein programmaatje geschreven dat alle beschikbare kleuren opsomt; dit is te downloaden bij [thinkpython.com/code/color\_list.py](http://www.thinkpython.com/code/color_list.py).