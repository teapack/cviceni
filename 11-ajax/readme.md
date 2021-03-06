# 11. Ajax, JS objekty

## Ajax

* asynchronous JavaScript and XML
* technologie, která umožňuje tvorbu asynchronních aplikací
* asynchronní = aplikace něco sama dělá v pozadí, aniž by to uživatel musel rozhodovat. Akce uživatele jsou nezávislé na akcích aplikace (kdyby byly závislé, pak by to bylo synchronní=sladěné).
* Ajax je standard při tvorbě moderních webových aplikací
* Ajax je všude
* Ajax jsou jen další funkce do JS. Prohlížeč "neumí Ajax", ve finále je to všechno zase jenom JS.
* z pohledu uživatele se na stránce něco samo děje bez toho, aby se stránka musela znovu načítat nebo aby bylo nutné přecházet mezi stránkami
* webové aplikace se chováním podobají desktopovým aplikacím
* příklady použití:
 * prohlížím Facebook a přijde upozornění, že mi zrovna teď někdo poslal zprávu
 * v Gmailu se zobrazí nový došlý mail, zatímco píšu mail někomu jinému
 * v Google Maps hýbu myší a postupně se donačítají mapové podklady
 * v Google Earth kolečkem přibližuju/oddaluji zemi a mapy se aktualizují
* **Pro zjednodušení budeme používat Ajax pomocí knihovny jQuery. Prohlížeče mají v čistém JS pro Ajax rozdílnou syntaxi a implementaci, jQuery zapouzdří kompatibilitu napříč různými browsery.**
* http://api.jquery.com/category/ajax/
* http://api.jquery.com/jquery.ajax/
* http://www.w3schools.com/ajax/
* http://www.w3schools.com/jquery/jquery_ajax_intro.asp


### Odeslání a zpracování XHR požadavku pomocí jQuery

* XHR = XMLHttpRequest objekt
* AJAX vytvoří XHR objekt, někam ho v pozadí (asynchronně) pošle a vrátí se mu výsledek, který nějak zpracujeme
* v jQuery se objekt jmenuje jQuery XMLHttpRequest (jqXHR)
* na objekt, ze kterého jsme zavolali nějakou Ajax funkci lze napojit tzv. callback metody, které se zavolají, když Ajax akce skončí
* základní funkce:

  * **jQuery.ajax()** - provede asynchronní HTTP request, základní low-level funkce, jednodušší je používat load() nebo get()

  * **.load()** - pošle HTTP request na serveru a získaná data umístí dovnitř elementu, ze kterého jsme load() zavolali. Předpokládá, že se vrátí HTML data.
    * lze napojit anonymní callback metodu, která se provede nakonec
    * z HTML dat na serveru jde vybrat selectorem jen část a tu umístit
    * **[práce s Ajax load](./11-ajax-load.html)**
    * http://api.jquery.com/load/

  * **jQuery.get()** - pošle HTTP GET request na server
    * zkrácená notace funkce jQuery.ajax()
    * lze přidat vlastní data
    * mime typ dat, které server poslal zpátky je odhadnut automaticky (typicky xml, json, html)
    * **[práce s Ajax get](./11-ajax-get.html)**
    * lze napojit callback funkce done, fail, always (viz dole)
    * http://api.jquery.com/jQuery.get/

  * **jQuery.getJSON()** - viz zpracování odpovědi ve formátu JSON

  * **jQuery.post()** - pošle HTTP POST request na server
    * zkrácená notace funkce jQuery.ajax(), typ HTTP metody nastaven explicitně na POST
    * lze napojit callback funkce done, fail, always (viz dole)
    * pokud odesíláme data z formuláře, je třeba je serializovat funkcí **.serialize()**, kterou pustíme rovnou na celý formulář
    * **[práce s Ajax post](./11-ajax-post.html)**
    * http://api.jquery.com/jQuery.post/
  
* callback funkce (jde je napojit např. na metody .ajax(), get(), post()):

  * **jqXHR.done()** - callback funkce, zavolá se v případě úspěšného requestu (všechno dopadlo dobře :). *Nahrazuje metodu jqXHR.success(), která je od jQuery 1.8 deprecated.*

  * **jqXHR.fail()** - callback funkce, zavolá se v případě neúspěšného requestu (někde nastala chyba). *Nahrazuje metodu jqXHR.error(), která je od jQuery 1.8 deprecated.*

  * **jqXHR.always()** - callback funkce, zavolá se vždy (ať už nastala nebo nenastala chyba). *Nahrazuje metodu jqXHR.complete(), která je od jQuery 1.8 deprecated.*

### Ajax events (události)

* lze registrovat události, které Ajax za běhu vyvolává a nějak na ně reagovat
* třeba při odeslání velkého souboru jde zobrazit rotující kolečko, aby uživatel věděl, že má čekat
* události se typicky napojují přímo na JS document objekt
  * **.ajaxStart()** - spustí se, pokud odstartuje první Ajax request na stránce
  * **.ajaxStop()** - spustí se, pokud se doběhnou **všechny** Ajax requesty na stránce
  * **.ajaxComplete()** - spustí se, pokud doběhne **jakýkoli** Ajax request
  * **.ajaxSuccess()** - spustí se, pokud **jakýkoli** Ajax request doběhne správně
  * **.ajaxError()** - spustí se, pokud **jakýkoli** Ajax request skončí s chybou
  * **.ajaxSend()** - spustí se před odesláním **jakékoli** Ajax requestu
* **[práce s Ajax events](./11-ajax-events.html)**
* http://api.jquery.com/category/ajax/global-ajax-event-handlers/


### Zpracování odpovědi ve formátu JSON a XML

#### JSON
  * **jQuery.getJSON()** - pošle HTTP GET request na server, chce vrátit JSON (JavaScript Object Notation, data ve formátu kratším než XML ;)
  * zkrácená notace funkce jQuery.get(), atribut dataType nastaven explicitně na JSON (říkáme serveru, ať nám vrátí typ dat JSON)
  * lze napojit callback funkce done, fail, always (viz dole)
  * **[práce s Ajax getJSON](./11-ajax-get-json.html)**
  * http://api.jquery.com/jQuery.getJSON/

#### XML
  * použijeme **jQuery.get()**, typ dat je inteligentně rozpoznán
  * vrácená data jsou rovnou ve formátu XML, nemusíme je tedy převádět z textu do XML, apod.
  * **[práce s Ajax a XML](./11-ajax-xml.html)**
  * https://api.jquery.com/jQuery.parseXML/
  * http://api.jquery.com/jQuery.get/


### Aktualizace části stránky na základě odpovědi XHR

  * viz minulé příklady, např. **[práce s Ajax getJSON](./11-ajax-get-json.html)** nebo **[práce s Ajax a XML](./11-ajax-xml.html)**


---


## Objekty v JavaScriptu

* **objekt = něco, s čím můžu v aplikaci "hýbat"**
* OOP = objektově orientované programování = tvorba vlastního světa v kódu
* ve světě jsou objekty, proto programujeme tak, že tvoříme objekty a říkáme, co mají dělat (umět) a jak se mají chovat (reagovat na vstupy, události)
* objekt má typicky nějaké vlastnosti (hodnoty, atributy) a funkce (v některých programovacích jazycích jsou to "metody"), pomocí kterých s objektem můžu pracovat
* analogie s autem: auto je objekt, jeho vlastosti jsou např. "barva, typ, SPZ". Funkce jsou "nastartuj, zrychli, brzdi, blikej".
* **[práce s objekty - konstruktory, inicializátory](./11-js-objects.html)**
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object


## Prototypes

* **prototype = rozšíření funkce o další vlastnosti (atributy, funkce) pro všechna další volání**
* **POZOR: rozšiřujeme pouze vlastní funkce, nikoli cizí, mohlo by to vést k chybám. Nikdy nerozšiřujeme standardní JavaScript objekty!**
* paralela s rozšířením třídy (Class) v Javě. Každá nová instance z této rozšířené třídy bude mít tyto nové vlastnosti.
* **[práce s prototypy](./11-js-prototypes.html)**
* http://www.w3schools.com/js/js_object_prototypes.asp


## Výchozí JavaScriptové objekty

### Window
* reprezentuje otevřené okno prohlížeče
* **default objekt, funkce jako alert(), confirm() apod. bez určení objektu jsou metody objektu window, ve skutečnosti se volá window.alert(), atd.**
* některé z metod objektu window:
  * **document()** - odkaz na DOM objekt, reprezentující celý HTML DOM stránky
  * **alert()** - zobrazí upozornění. Browser může potlačit volání, pokud si to uživatel přeje, na zobrazení tedy nelze spoléhat.
  * **confirm()** - dialogové okno OK/Cancel. Používáme např. pro potvrzení odeslání nebo smazání formuláře.
  * **blur()** - zruší zaměření okna (udělá ho neaktivní)
  * **focus()** - zaměří okno (udělá ho aktivní)
  * **getSelectionText()** - získá text, který uživatel na stránce označil
  * **open()** - otevře nové okno, parametr je URL
  * **close()** - zavře aktivní okno
  * **print()** - pošle stránku na tiskárnu (jako kdybychom zvolili Print z menu nebo stiskli CTRL+P)
  * **prompt()** - zeptá se uživatele na vstup - nejde kontrolovat, doporučuji využít normální formulář
  * **resizeTo()** - změní velikost okna na zadaný počet pixelů (výška, šířka)
  * **[práce s window objektem](./11-js-window.html)**
  * http://www.w3schools.com/jsref/obj_window.asp

### History
* reprezentuje historii stránek, na kterých uživatel byl
* z bezpečnostních důvodů nejde získat seznam stránek, pouze se mezi nimi pohybovat dopředu/zpět
* atributy:
  * length - počet položek v historii
* metody:
  * **back()** - jdi zpět o 1 krok. Stejně jako by uživatel kliknul na "Zpět" v browseru.
  * **forward()** - jdi dopředu o 1 krok. Stejně jako by uživatel kliknul na "Vpřed" v browseru.
  * **go()** - jdi na stránku z historie. Kladné číslo - počet kroků vpřed, záporné číslo = počet kroků zpět. Akceptuje i URL.
* **[práce s history objektem](./11-js-history.html)**
* http://www.w3schools.com/jsref/obj_history.asp


### Location
* reprezentuje aktuální URL
* atributy:
  * **hash** - nastaví nebo vrátí odkaz v rámci stránky v URL (část za #)
  * **host** - nastaví nebo vrátí hostname (název serveru) a port v URL
  * **hostname** - nastaví nebo vrátí hostname (název serveru) v URL
  * **href** - nastaví nebo vrátí celou URL
  * **origin** - vrátí protokol, hostname a port URL
  * **pathname** - nastaví nebo vrátí cesta v URL (část za serverem a portem)
  * **port** - nastaví nebo vrátí port v URL
  * **protocol** - - nastaví nebo vrátí protokol v URL (http, https, ftp, apod.)
  * **search** - nastaví nebo vrátí querystring (proměnné v URL, např. jmeno=Frusciante)	
* metody:
  * **assign()** - přejde na jinou URL, aktuální URL **bude** v historii
  * **reload()** - znovu nahraje aktuální URL
  * **replace()** - přepíše aktuální URL novou URL, stará URL **nebude** v historii
* **[práce s location objektem](./11-js-location.html)**
* http://www.w3schools.com/jsref/obj_location.asp


### Math
* matematické operace v JS
* konstanty (jen část):
  * **Math.PI**
  * **Math.E** 
* metody (jen část):
  * **random()** - náhodné číslo v intervalu &lt;0;1)
  * **ceil()** - zaokrouhlení nahoru na celé číslo
  * **floor()** - zaokrouhlení dolů na celé číslo
  * **round()** - zaokrouhlení dolů nebo nahoru na celé číslo (podle toho, co je blíž, od 5 zaokrouhluje nahoru)
  * **sqrt()** - druhá odmocnina
  * **pow()** - umocnění, 3^3=27
  * **sin()**
  * **cos()**
  * **tan()**
  * **na cotg přímo metoda není, počítá se jako 1/tan(x)**
* **[práce s Math objektem](./11-js-math.html)**
* http://www.w3schools.com/js/js_math.asp
* http://www.w3schools.com/jsref/jsref_obj_math.asp


## Časování
* https://developer.mozilla.org/en-US/Add-ons/Code_snippets/Timers
* http://www.w3schools.com/js/js_timing.asp
