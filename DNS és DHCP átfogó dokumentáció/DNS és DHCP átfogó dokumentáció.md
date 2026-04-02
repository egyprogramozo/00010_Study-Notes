# DNS és DHCP átfogó dokumentáció

**Források és felhasznált eszközök:**

- [ChatGPT](https://chatgpt.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/) 

 A DNS és a DHCP két alapvető hálózati szolgáltatás, amelyek nélkül a modern hálózatok működése jóval nehézkesebb lenne. A DNS feladata, hogy a könnyen megjegyezhető neveket, például domainneveket, IP-címekre fordítsa le, így a felhasználóknak nem kell számsorokat megjegyezniük. A DHCP ezzel szemben automatikusan kiosztja a kliensek számára a szükséges hálózati beállításokat, például az IP-címet, az alhálózati maszkot, az átjárót és a DNS-szervert. A két szolgáltatás együtt biztosítja, hogy az eszközök gyorsan csatlakozhassanak a hálózathoz, és hatékonyan tudjanak kommunikálni egymással és az internetes szolgáltatásokkal.

## Rövid hálózati alapozás

**IP‑cím + alhálózati maszk + alapértelmezett átjáró + DNS szerverek** együtt adják ki a kliens alapvető hálózati működőképességét. Ha például van IP‑címed, de nincs gateway, tipikusan nem jutsz ki más hálózatokba; ha van IP és gateway, de rossz DNS szerver van beállítva, akkor gyakran “IP‑vel megy, névvel nem” jelenséget kapsz.

**Broadcast domain** (tipikusan egy VLAN) azt a 2. rétegbeli környezetet jelenti, ahol a broadcast forgalom (pl. ARP, DHCP Discover) eljut az eszközökhöz. A klasszikus DHCP induláskor broadcastot használ, ezért **alapesetben egy router alapértelmezés szerint nem továbbítja a broadcast kérést más alhálózatba**; ennek kezelésére való a DHCP relay / helper.

Ebből a pontból már könnyen kapcsolódik a két fő téma:

- **DHCP (Dynamic Host Configuration Protocol)**: automatikusan ad IP‑címet és kapcsolódó paramétereket (gateway, DNS szerver, DNS search suffix…).
- **DNS (Domain Name System)**: a neveket (pl. *intranet.cég.local*) lefordítja címekre és szolgáltatás‑információkra (A/AAAA, SRV, MX…).

## DNS alapjai és névfeloldás folyamata

A DNS (Domain Name System) egy **hierarchikus, elosztott névtér és adatbázis**, amelynek célja, hogy emberbarát neveket lehessen használni, miközben a hálózati kommunikáció címekhez (IP) kötődik. A DNS alapfogalmait és kliens–szerver működését a klasszikus specifikációk írják le.

### Szereplők: stub resolver, rekurzív resolver, autoritatív névszerver

A mindennapi gyakorlatban három “szereplőt” érdemes elkülöníteni:

**Stub resolver (kliensoldali feloldó)**

Az operációs rendszer része: “kérdez, de nem old meg mindent egyedül”. Olyan resolver, amely nem képes a teljes feloldást önállóan végigvinni, ezért tipikusan egy rekurzív resolverre támaszkodik.

**Rekurzív resolver (caching rekurzív DNS)**

Az a szerver (gyakran ISP‑nél, vállalatnál, routerben), amely a kliens helyett végigköveti a DNS-hierarchiát, és közben cache‑el. A DNS egyik skálázhatósági alapja, hogy agresszíven használ gyorsítótárat.

**Autoritatív névszerver**

Az a szerver (vagy szervercsoport), amely **egy adott zónára nézve “forráshitelű”**: az ott tárolt rekordok “a hivatalos válaszok”. A delegációk és zónák gondolatvilága a DNS alap specifikációiban jelenik meg.

### DNS hierarchia: root → TLD (Top-Level Domain) → delegált zónák

A DNS névtér csúcsa a **root zóna** (“.”). A root alá tartoznak a **TLD‑k** (pl. *.com*, *.hu*), azok alatt pedig a delegált tartományok és zónák. A feloldás során a rekurzív resolver először tipikusan root, majd TLD, majd az adott domain autoritatív szerverei felé lépked (pl. *example.com*), és a köztes eredményeket cache‑eli.

### Rekurzív és iteratív lekérdezés: mi történik “valójában”?

A DNS protokoll két tipikus működési módot különít el:

- **Rekurzív mód**: a kliens (stub resolver) azt kéri: *“old meg nekem teljesen”*. A rekurzív válasz lehet tényleges válasz, névhiba (NXDOMAIN), vagy átmeneti hiba.
- **Nem rekurzív / iteratív jellegű működés**: a megkérdezett szerver “a legjobb tudása szerint” válaszol (pl. referral: *“nem én tudom, de itt vannak az NS-ek, kérdezd őket”*).

A hétköznapi internet‑használatban a kliensed jellemzően **rekurzív kérést** küld a helyi/ISP rekurzív resolvernek, és **a rekurzív resolver** az, amely a hierarchián lépkedve iteratív jellegű kérdéseket tesz fel a root/TLD/autoritatív szervereknek.

### Cache és TTL: miért jelent a cache egyszerre teljesítményelőnyt és üzemeltetési korlátot?

A DNS rekordok időtartamát a **TTL (Time To Live)** határozza meg: azt, hogy egy válasz mennyi ideig tartható cache‑ben. A cache azért “jó”, mert gyorsít és csökkenti a terhelést, de néha “bosszantó”, mert változtatás után idő kell, amíg a gyorsítótárak frissülnek, és a változás érvényesül. A DNS cache‑elési szemlélete és a resolver működés lépései a klasszikus leírásokban is szerepelnek.

**Pozitív cache**: létező rekordok (pl. A/AAAA) tárolása TTL‑ig.

**Negatív cache**: “nem létezik” (NXDOMAIN) vagy “nincs ilyen típusú rekord” (NODATA) válaszok cache‑elése is lehetséges.

### DNS szállítás: UDP, TCP, EDNS

**Portok**: A hagyományos DNS az 53-as portot használja UDP-n és TCP-n is. A legtöbb hétköznapi lekérdezés UDP-n történik, míg bizonyos nagyobb vagy speciális válaszok TCP-t is igényelhetnek.

**TCP támogatás**: A modern követelmények szerint a DNS implementációknak támogatniuk kell a TCP‑t is (pl. nagy válaszok, megbízhatóság, egyes üzemeltetési elvárások miatt).

**512 bájtos “klasszikus” UDP limit és a bővítés**: A DNS eredetileg úgy lett tervezve, hogy UDP‑n tipikusan kicsi válaszok férjenek el. Az EDNS(0) és a kapcsolódó DNS-kiterjesztések szabványosítják a nagyobb válaszok és a kiegészítő képességjelzések kezelését.

**UDP (User Datagram Protocol)**

Ez egy kapcsolatmentes szállítási rétegbeli protokoll, vagyis gyorsan küld adatokat anélkül, hogy előtte tartós kapcsolatot építene fel a két fél között. Emiatt kisebb az overhead, de nincs benne beépített garancia arra, hogy minden csomag megérkezik, jó sorrendben érkezik meg, vagy egyáltalán visszaigazolást kap róla a küldő.

UDP példák:

- DNS (Domain Name System) lekérdezések nagy része
  
  Gyors névfeloldásra használják, ahol fontos a sebesség és általában elég egy rövid kérés-válasz.

- DHCP (Dynamic Host Configuration Protocol)
  
  Automatikusan IP-címet és egyéb hálózati beállításokat ad a klienseknek.

- NTP (Network Time Protocol)
  
  Az eszközök órájának pontos szinkronizálására szolgál a hálózaton.

- VoIP (Voice over IP) és sok videó-/hangstream
  
  Valós idejű hang- és médiaátvitelre jó, ahol a gyorsaság fontosabb, mint a tökéletes hibajavítás.

- online játékok egy része
  
  Gyors adatcserére használják, hogy minél kisebb legyen a késleltetés.

**TCP (Transmission Control Protocol)**

Ez szintén szállítási rétegbeli protokoll, de a UDP-vel szemben kapcsolat-orientált és megbízható adatátvitelt biztosít. Figyel a sorrendre, kezeli az elveszett csomagok újraküldését, és visszaigazolásokkal ellenőrzi, hogy az adatok ténylegesen megérkeztek-e.

TCP példák:

- HTTP (Hypertext Transfer Protocol) / HTTPS (Hypertext Transfer Protocol Secure)
  
  Weboldalak és webes szolgáltatások megbízható elérésére használják.

- SSH (Secure Shell)
  
  Titkosított távoli bejelentkezésre és parancssoros adminisztrációra szolgál.

- FTP (File Transfer Protocol)
  
  Fájlok átvitelére használják kliens és szerver között.

- SMTP (Simple Mail Transfer Protocol), IMAP (Internet Message Access Protocol), POP3 (Post Office Protocol version 3)
  
  E-mailek küldésére, illetve letöltésére vagy szinkronizálására szolgálnak.

- RDP (Remote Desktop Protocol)
  
  Távoli asztali kapcsolat létrehozására használják, például egy másik gép grafikus eléréséhez.

**EDNS (Extension Mechanisms for DNS)**

Ez nem egy külön új protokoll a DNS helyett, hanem a DNS kibővítése olyan plusz lehetőségekkel, amelyeket az eredeti DNS már nem tudott kényelmesen kezelni. Például segít nagyobb DNS-válaszok kezelésében és extra információk átadásában, miközben maga az alap DNS működés megmarad.

EDNS példák:

- nagyobb DNS-válaszok kezelése
  
  Arra jó, hogy a DNS a régi korlátoknál nagyobb adatokat is hatékonyabban tudjon visszaadni.

- DNSSEC (Domain Name System Security Extensions) támogatása
  
  Segít a nagyobb, aláírt DNS-válaszok kezelésében és ellenőrzésében.

- OPT rekord (Option record) használata DNS-üzenetben
  
  Kiegészítő információk átadására szolgál a DNS-kliens és a DNS-szerver között.

- ECS (EDNS Client Subnet)
  
  Bizonyos szolgáltatóknál arra használják, hogy a DNS-válasz jobban igazodjon a kliens földrajzi helyéhez.

- különféle DNS-bővítések átadása a klasszikus DNS-en belül
  
  Arra jó, hogy új funkciókat lehessen használni anélkül, hogy teljesen új DNS-protokollt kellene bevezetni.

## DNS rekordok, zónák és delegáció

A DNS alapvető adategysége a **resource record (RR)**. Egy RR mindig valamilyen *névhez* kötődik, és megmond valamit: címet, alias‑t, levelezési útvonalat, szolgáltatás‑helyet, policy‑t stb. A rekordformátumot és a klasszikus rekordtípusokat az alap specifikációk tartalmazzák, a típusok IANA regiszterben is követhetők. 

### Zóna és delegáció: mit jelent, hogy “ezért a részért én vagyok illetékes”?

**Zóna**: a DNS névtér egy “adminisztratív egysége”, amelyért egy autoritatív névszerver(ek) felel(nek). A delegáció azt jelenti, hogy a parent zóna NS rekordokkal “átadja” egy alzóna kiszolgálását.

Gyakorlati következmény: ha egy domainnél NS‑t váltasz, a világ nem a webtárhely-szolgáltatásból derül ki, hanem a delegációs lánc alapján megnézi, mely névszerverek autoritatívak.

### Rekordtípusok gyors áttekintése

- A (Address) – Egy domainnevet IPv4-címhez rendel.

- AAAA (Quad-A) – Egy domainnevet IPv6-címhez rendel.

- CNAME (Canonical Name) – Egy nevet egy másik domainnév aliasaként állít be.

- MX (Mail Exchanger) – Megadja, hogy egy domain e-mailjeit melyik levelezőszerver fogadja.

- NS (Name Server) – Megadja, mely névszerverek felelősek az adott zóna kiszolgálásáért.

- PTR (Pointer) – Fordított névfeloldásra szolgál, vagyis IP-címből nevet keres.

- TXT (Text) – Szöveges információk tárolására használják, például hitelesítési vagy ellenőrzési adatokhoz.

- SOA (Start of Authority) – A zóna alapvető adminisztratív adatait tartalmazza, például a fő névszervert és a frissítési paramétereket.

- SRV (Service) – Megadja, hogy egy adott szolgáltatás melyik szerveren és porton érhető el.

- CAA (Certification Authority Authorization) – Azt szabályozza, hogy mely hitelesítésszolgáltató adhat ki tanúsítványt a domainhez.

### Rekordtípusok részletesen

Az alábbi rekordok “kötelező tudás” sysadmin / üzemeltető szemléletben. A cél itt nem csak a definíció, hanem a **használat**, a **tipikus hibák**, és hogy a rekord hogyan illeszkedik a névfeloldási folyamatba.

#### A rekord

**Szerep**: név → IPv4 cím. A web, API, belső szolgáltatások alaprekordja.

**Mikor használod?**

Ha egy hostnévnek (pl. `app1.ceg.hu`) konkrét IPv4 címet akarsz adni.

**Példa (elméleti)**:

```txt
app1.ceg.hu.  300  IN  A     203.0.113.10
```

**Mire figyelj?**

- TTL: változó infrastruktúrán (pl. gyakori failover) rövidebb TTL kellhet, a stabil rendszereknél pedig a hosszabb TTL csökkenti a DNS terhelést.
- “IP‑vel megy, névvel nem” hibánál az A rekord (vagy AAAA) és a használt resolver cache‑e az első ellenőrzési pont.

#### AAAA rekord

**Szerep**: név → IPv6 cím. A DNS IPv6‑os kiterjesztése külön specifikációban van szabványosítva.

**Mikor használod?**

Ha a szolgáltatásod IPv6‑on is elérhető (vagy csak IPv6‑on).

**Példa**:

```txt
app1.ceg.hu.  300  IN  AAAA  2001:db8:1234::10
```

**Mire figyelj?**

- Dual‑stacknél a kliens döntési logikája (Happy Eyeballs) miatt előfordulhat, hogy az IPv6 útvonal hibája “furcsa” intermittáló hibákat okoz, mert az AAAA prioritást kaphat a próbálkozásban. (Ez már inkább kliens‑oldali viselkedés, de üzemeltetésben gyakori jelenség.)

#### CNAME rekord

**Szerep**: alias → “kanonikus név”. A CNAME kimondja: “ez a név valójában egy másik név”.

**Kulcsszabály (nagyon gyakori hiba!)**: ha egy néven CNAME van, **azon a néven nem lehet más adat** (más RR - resource record). Az alap DNS-koncepció írja le ezt az elvet.

**Mikor használod?**

- CDN (Content Delivery Network), SaaS integrációk (pl. `shop.ceg.hu` → `ceg.platform.example`).

**Példa**:

```txt
www.ceg.hu.  300  IN  CNAME  ceg.hu.
```

**Mire figyelj?**

- **Zóna apex (pl. `ceg.hu` “gyökér” név)** alá tipikusan nem tehetsz CNAME‑ot, mert a zóna tetején SOA és NS rekordoknak ott kell lenniük, és a CNAME “nem fér össze” más rekorddal.
- CNAME láncok (több alias egymás után) lassíthatnak és hibapontot adnak. Hibaelhárításnál mindig kövesd végig a láncot.

#### MX rekord

**Szerep**: e‑mail forgalom “hova menjen” egy domainhez. Az MX rekord formátuma és a preference/priority logikája szabványosítva van.

**Mikor használod?**

- Ha egy domain levelezését (pl. `ceg.hu`) valamilyen mail szerver(ek) kezelik.

**Példa**:

```txt
ceg.hu.  3600  IN  MX  10  mx1.mailhost.tld.
ceg.hu.  3600  IN  MX  20  mx2.mailhost.tld.
```

**Mire figyelj?**

- Alacsonyabb preference = előnyben.
- Gyakori hiba: MX cél (`mx1.mailhost.tld`) mögött nincs megfelelő A/AAAA. A DNS “megengedi”, de a levélkézbesítés meghiúsulhat.

#### NS rekord

**Szerep**: megmondja, mely névszerver(ek) autoritatívak egy delegált zónához. A klasszikus “DNS átállás” (névszerver csere) kulcsa.

**Mikor használod?**

- Zóna delegációkor és az autoritatív szerverek deklarálásakor.

**Mire figyelj?**

- **Glue**: ha az NS neve “a zónán belül van” (in‑bailiwick), akkor a parent zónának gyakran kiegészítő A/AAAA rekordot is adnia kell, különben körkörös függőség jön létre (nem tudod feloldani a NS nevét, mert ahhoz a NS‑t kéne elérni). A delegációs modell megértéséhez a hierarchia‑logika a lényeg.
- TTL és propagáció: NS váltásnál hosszabb idő kellhet, miközben a régi és új NS párhuzamosan lehetnek érvényben.

#### PTR rekord

**Szerep**: reverse DNS (IP → név). IPv4 esetén ez tipikusan az `in-addr.arpa` névtérben van, IPv6‑nál `ip6.arpa`. A PTR a standard rekordok között szerepel.

**Mikor használod?**

- Naplózás/forenzika, hálózati eszközök áttekinthetősége.
- Sok szolgáltatás (pl. e‑mail küldés) esetén reputáció és ellenőrzés miatt is fontos.

**Tipikus példa (IPv4)**:

```txt
10.113.0.203.in-addr.arpa. 3600 IN PTR  app1.ceg.hu.
```

**Mire figyelj?**

- Reverse DNS gyakran **nem azon a DNS zónán van, amit te kezelsz**, hanem az IP‑tartomány tulajdonosánál/ISP‑nél.
- Klasszikus üzemeltetési elvárás, hogy a PTR és az A rekord konzisztens legyen egymással, vagyis megvalósuljon a forward–reverse konzisztencia, és ez tipikus auditpont.

#### TXT rekord

**Szerep**: szabad formájú szöveg‑adatok. A gyakorlatban policy és verifikáció: SPF (Sender Policy Framework), DKIM (DomainKeys Identified Mail), DMARC (Domain-based Message Authentication, Reporting, and Conformance), domain‑ownership igazolások, stb. A TXT a klasszikus DNS rekordtípusok közé tartozik.

**Mire figyelj?**

- Karakter- és hosszkorlátok, valamint darabolás (DNS wire format) miatt egyes szolgáltatók a felhasználói felületen (User Interface) a TXT rekord értékét több részre bontva jelenítik meg, ami dokumentáláskor félreérthető lehet.

#### SOA rekord

**Szerep**: “start of authority”: a zóna adminisztratív metaadata. A SOA formátuma és szerepe DNS alapkövetelmény.

**Mit tartalmaz tipikusan?**

- primary NS (mname), felelős e‑mail (rname), serial, refresh/retry/expire/minimum értékek.

**Miért fontos üzemeltetésben?**

- Zónaátvitel (AXFR/IXFR) vezérlés, secondary szerverek frissítési ritmusa.
- A SOA rekord minimum mezőjét történetileg többféleképpen értelmezték, modern környezetben pedig főként a negatív cache kezeléséhez kapcsolják, például az NXDOMAIN válaszok gyorsítótárazásánál.

#### SRV rekord

**Szerep**: szolgáltatás‑hely (service location) rekord. Megmondja, hogy *adott szolgáltatás + protokoll + domain* esetén **melyik hoston és porton** érhető el a szolgáltatás, és milyen prioritással/súllyal.

**Mikor használod?**

- Vállalati szolgáltatás‑felfedezés (klasszikus példa: címtár/AD jellegű szolgáltatások, VoIP, XMPP, SIP), vagy bármely olyan rendszer, ahol nem csak a hostnév számít, hanem port és preferencia is.

**Példa**:

```txt
_service._tcp.ceg.hu.  300  IN  SRV  10  60  443  service1.ceg.hu.
_service._tcp.ceg.hu.  300  IN  SRV  20  40  443  service2.ceg.hu.
```

**Mire figyelj?**

- A kliensnek is “SRV‑tudatosnak” kell lennie: ha a szoftver nem kérdez SRV‑t, hiába van rekord.
- SRV‑nél a prioritás/súly logika **terheléselosztásra és failoverre** ad egy szabványos keretet, de csak azon belül, amire a kliens implementációja képes.

#### CAA rekord

**Szerep**: tanúsítvány‑kiadás korlátozása. A domain tulajdonosa deklarálhatja, mely hitelesítésszolgáltatók (CA‑k) jogosultak tanúsítványt kiadni a domainre. A CAA rekord célja a “félre‑kibocsátás” (mis‑issue) kockázat csökkentése, és RFC‑ben szabványosított.

**Tipikus példa (logikai)**:

```txt
ceg.hu.  3600  IN  CAA  0 issue "letsencrypt.org"
ceg.hu.  3600  IN  CAA  0 iodef "mailto:security@ceg.hu"
```

**Mire figyelj?**

- CAA bevezetése hasznos policy‑réteg, de nem “helyettesíti” a DNSSEC‑et vagy a certificate transparency logikát, ezért inkább “extra kontroll”.

## DHCP alapjai, működése és konfiguráció

A DHCP (Dynamic Host Configuration Protocol) a gyakorlatban a “hálózatba lépés” legfontosabb automatizmusa: egy kliens úgy lehet “plug and play”, hogy közben **helyes IP‑címet, maszkot, átjárót, DNS‑t, és sok egyéb paramétert** kap. A DHCP definíciója és alap modellje szabványosított, és a klasszikus RFC (Request for Comments)‑ek leírják a működését.

### DHCP kiosztási módok: automatic, dynamic, manual

A DHCP három alap kiosztási mechanizmust különít el:

- **Automatic allocation**: “kvázi végleges” cím kiosztás a kliensnek.
- **Dynamic allocation**: cím bérbeadása meghatározott időre (lease).
- **Manual allocation**: adminisztrátor által előre meghatározott fix IP-cím kiosztása, amely tipikusan reservation formájában jelenik meg a DHCP-ben.

A vállalati gyakorlatban a manual allocation tipikus megjelenési formája a reservation, vagyis amikor a szerver egy kliensazonosítóhoz vagy MAC-címhez fix IP-címet rendel.

Az automatic allocation ma már nem a legjellemzőbb működési mód. Inkább kisebb, ritkán változó hálózatokban, laborokban vagy egyszerű irodai környezetben lehet értelme, ahol hasznos, hogy a kliens automatikusan (nem statikusan) kap címet, de azt később is jellemzően megtartja.

### DORA folyamat: Discover → Offer → Request → Acknowledge

A DHCP alap tranzakciója a DORA (4 üzenet), amit a szabvány is név szerint tárgyal (DHCPDISCOVER, DHCPOFFER, DHCPREQUEST, DHCPACK).

| Lépés       | Magyar jelentés | Rövid magyarázat                                                                          |
| ----------- | --------------- | ----------------------------------------------------------------------------------------- |
| Discover    | Felderítés      | A kliens DHCP-szervert keres a hálózaton, mert még nincs érvényes IP-címe.                |
| Offer       | Felajánlás      | A DHCP-szerver felajánl egy elérhető IP-címet és a hozzá tartozó alapbeállításokat.       |
| Request     | Kérelem         | A kliens jelzi, hogy a felajánlott konfigurációt el szeretné fogadni.                     |
| Acknowledge | Visszaigazolás  | A szerver megerősíti a kiosztást, így a kliens használatba veheti a kapott beállításokat. |

**Miért broadcast az eleje?**

Induláskor a kliensnek még nincs IP-címe, ezért broadcast üzenettel próbál DHCP-szervert elérni a helyi hálózaton. Emiatt a DHCP klasszikusan UDP-t és broadcast kommunikációt használ.

**Melyik portok?**

A DHCPv4 a BOOTP történeti portjait használja:

- Server: 67/UDP (*bootps*)  
- Client: 68/UDP (*bootpc*)

### Lease életciklus: megújítás és rebinding

A lease (bérlet) azt jelenti: az IP kiosztásnak van érvényességi ideje, és a kliensnek meg kell újítania.

Gyakorlati (nagyon elterjedt) időzítés:  

- **T1 (renew)**: a lease idő ~50%-ánál a kliens megpróbálja az eredeti DHCP-szervernél megújítani az IP-cím bérletét.
- **T2 (rebind)**: ~87,5%-nál a kliens már más elérhető DHCP-szerverek felé is megpróbálja megújítani az IP-cím bérletét, hogy ne szakadjon meg a hálózati kapcsolat.

Ez üzemeltetésben azért kritikus, mert:

- redundáns DHCP környezetben a “rebind” egy tartalék megújítási mechanizmus,
- hálózati zavarnál a lease megújítás környékén “időszakos” eldobásokat láthatsz.

### Scope, exclusion, reservation, options: gyakorlati építőkockák

A DHCP gyakorlati beállításainak legfontosabb elemei a scope, az exclusion range, a reservation és a DHCP options. Ezek együtt határozzák meg, hogy a kliensek milyen IP-címet és milyen egyéb hálózati paramétereket kapnak. Az alábbiakban ezeknek a fő szerepét és gyakorlati jelentőségét tekintjük át.

- **Scope (pool)**
  
  Az a címtartomány, amelyből a DHCP-szerver IP-címeket oszthat ki a klienseknek. Például ilyen lehet a 10.10.20.100–10.10.20.200 közötti tartomány.

- **Exclusion range**
  
  A scope-on belüli olyan címtartomány, amelyet a DHCP-szerver nem oszthat ki. Ezt gyakran olyan eszközök számára tartják fenn, amelyek fix, kézzel beállított IP-címet használnak.

- **Reservation**
  
  Olyan beállítás, amelynél a DHCP-szerver egy adott klienshez, például annak MAC-címe vagy Client ID-ja alapján, mindig ugyanazt az IP-címet rendeli hozzá. Ezt gyakran „statikus DHCP”-nek is nevezik.

- **DHCP options (kiosztható paraméterek)**
  
  A DHCP nemcsak IP-címet ad a kliensnek, hanem különféle kiegészítő hálózati beállításokat is továbbít. Ezek az adatok a DHCP-üzenetek opció mezőjében szerepelnek, és ilyen opció lehet például az alhálózati maszk, az alapértelmezett átjáró, a DNS-szerver címe vagy a domainnév. Az egyes opciók formátumát és használatát szabványok határozzák meg.

Üzemeltetési szempontból a legkritikusabbak:

- **Gateway / default route** – Ez határozza meg, hogy a kliens merre érje el a saját hálózatán kívüli címeket. Ha hibás, akkor a kliens ugyan kaphat IP-címet, de más hálózatokat vagy az internetet már nem fogja elérni.
- **DNS-szerver címe(i)** – Ez adja meg, melyik DNS-szervert használja a kliens névfeloldásra. Ha hibás, akkor előfordulhat, hogy az IP-címek közvetlenül még működnek, de a nevekkel történő elérés már nem.

### DHCP relay: amikor több alhálózat/VLAN van

A DHCP relay/helper egy közvetítő a kliens és a DHCP-szerver között.

Azért van rá szükség, mert amikor egy kliens még nem kapott IP-címet, a DHCP-kérést általában broadcastként küldi ki a saját helyi hálózatára. A broadcast forgalmat a router alapból nem továbbítja más alhálózatok vagy VLAN-ok felé. Emiatt ha a DHCP-szerver nem ugyanabban a hálózatban van, a kliens önmagától nem érné el.

Ilyenkor jön képbe a DHCP relay. A relay szolgáltatás jellemzően a routeren vagy Layer 3 switchen fut, figyeli a kliens DHCP-kérését, majd azt továbbítja unicast formában a megfelelő DHCP-szerver felé. A szerver válaszát pedig visszajuttatja a klienshez. Így a DHCP-szerver lehet egy másik hálózatban is, mégis tud címet osztani.

Egyszerű példa: van egy kliens a 10.10.20.0/24 hálózatban, de a DHCP-szerver a 10.10.10.0/24 hálózatban van. Relay nélkül a kliens broadcastja nem jut át a routeren. DHCP relay használatával a router továbbítja a kérést a szerver felé, ezért a kliens mégis kap IP-címet.

Röviden: a DHCP relay arra jó, hogy egy központi DHCP-szerver több alhálózatot vagy VLAN-t is ki tudjon szolgálni anélkül, hogy minden hálózatba külön DHCP-szervert kellene tenni.

A relay szerepkört és a hozzá kapcsolódó információk átadását szabvány is tárgyalja, különösen a Relay Agent Information Option.

**Option 82 (Relay Agent Information Option)**

A relay a kliens kéréséhez “metaadatot” adhat (pl. melyik switch‑port/VLAN felől jött), és a szerver ezt policy‑kiosztásnál felhasználhatja.

### Mi történik, ha nincs DHCP?

Ha egy kliens DHCP‑re van állítva, de nem kap címet, akkor IPv4-en sok rendszer egy 169.254.x.x tartományba eső **link-local** címet konfigurál (Windows terminológiával: **APIPA**). Az IETF szabványosítja a 169.254.0.0/16 automatikus link‑local címzését.

A Microsoft dokumentáció leírja, hogy a 169.254.0.0–169.254.255.255 tartomány APIPA célra van fenntartva, és ezzel az eszköz alapesetben csak a helyi linken vagy helyi broadcast domainen belül tud kommunikálni, útválasztás (routing) nélkül.

## Gyakorlati hibakeresés, biztonság és kiegészítők

Ebben a részben a hibakereséshez használható gondolkodási sorrend, a legfontosabb eszközök és a tipikus gyakorlati forgatókönyvek kerülnek bemutatásra. Kiegészítésként szó lesz az ARP, a NAT és a gyakran használt portok szerepéről is, mert ezek szintén fontosak a hálózati problémák megértéséhez és elhárításához.

### A DNS hibakeresés logikai folyamata

A klasszikus “réteges” diagnosztika DNS‑hez:

1) **Van-e IP konfiguráció?**
   
   IP, mask, gateway, DNS szerverek, lease állapot.

2) **IP‑szintű elérés működik?**
   
   Ha IP‑re ping megy, de névre nem, akkor nagy valószínűséggel DNS-probléma áll fenn.

3) **DNS feloldás működik-e és kivel?** 
   
   Melyik DNS szerver válaszol? Timeout? Rossz szerver? Cache?

4) **Cache és TTL jellegű problémák** 
   
   Helyi DNS cache ürítés, a kliens cache tartalmának megtekintése.

### Az nslookup gyakorlati használata

A **nslookup** a “klasszikus” Windows DNS parancssori diagnosztikai eszköz.

Segítségével ellenőrizhető a névfeloldás és a különböző DNS-rekordok. Megállapítható vele, hogy egy domainnév milyen IP-címre oldódik fel, melyik DNS-szerver válaszol, valamint hogy a hiba a DNS működésében vagy a kliens beállításaiban keresendő.

Az alábbiakban a napi üzemeltetés során gyakran használt minták kerülnek bemutatásra.

**Alap lekérdezés (melyik DNS-szervert használja a kliens?)**

Ezzel azt tudod megnézni, hogy a saját kliensed normál működés közben melyik DNS-szerveren keresztül próbálja feloldani a nevet, és attól milyen választ kap. Ez hibakeresésnél azért hasznos, mert gyorsan kiderül, hogy a helyben használt DNS-szerver jól működik-e, és egyáltalán azon keresztül rendben van-e a névfeloldás.

```powershell
nslookup www.example.com
```

**Konkrét resolverrel tesztelés (összehasonlítás)**

Nem a saját gép alapértelmezett DNS-beállítását használod, hanem te mondod meg, hogy melyik DNS-szervert kérdezze le. Így ugyanazt a nevet több különböző resolverrel is le tudod ellenőrizni, és össze tudod hasonlítani a válaszokat. Ez azért hasznos, mert segít eldönteni, hogy a probléma a saját beállított DNS-szervereddel van-e, vagy maga a rekord, illetve a névfeloldás hibás általánosan is.

```powershell
nslookup www.example.com 1.1.1.1
nslookup www.example.com 8.8.8.8
```

Ezzel gyorsan elkülöníthető, hogy a hiba a lokálisan használt DNS-szervernél van-e, vagy nem helyi, hanem általánosabb névfeloldási problémára utal az eredmény.

**Rekordtípus célzott lekérdezése**

Nemcsak az általános névfeloldás ellenőrizhető, hanem egy adott DNS-rekordtípus célzottan is lekérdezhető.

```powershell
nslookup -type=mx example.com
nslookup -type=ns example.com
nslookup -type=txt example.com
nslookup -type=soa example.com
```

Ezek a típusok mind a standard DNS-rekordkészlet részei, és üzemeltetésben gyakran szükség van ilyen lekérdezésekre (MX/TXT: levelezés; NS/SOA: delegáció és zónaállapot).

**Reverse lookup (PTR ellenőrzés)**

Az is könnyen ellenőrizhető, hogy egy IP-címhez tartozik-e visszafelé feloldható domainnév, vagyis létezik-e hozzá PTR rekord.

```powershell
nslookup 203.0.113.10
```

Ha nincs PTR rekord, az egy webes szolgáltatás működését önmagában nem feltétlenül befolyásolja, azonban levelezési környezetben, naplóelemzésnél vagy auditálás során már problémát okozhat. A PTR a klasszikus DNS-rekordtípusok közé tartozik, és az IP-címhez tartozó név visszafelé történő feloldását teszi lehetővé.

**Mit jelentenek a tipikus hibák?**

- `DNS request timed out`
  
  Ez általában azt jelenti, hogy a kliens nem kapott időben választ a megadott DNS-szervertől. Ennek oka lehet, hogy a DNS-szerver nem érhető el, a forgalmat tűzfal blokkolja, hibás az útvonal, a VPN más DNS-t kényszerít, vagy egyszerűen rossz DNS-beállítás van megadva.

- `NXDOMAIN`
  
  Ez azt jelenti, hogy a lekérdezett név nem létezik a DNS-ben. Vagyis a DNS-szerver elérhető volt, a lekérdezés technikailag működött, de a keresett domainnévhez nem talált rekordot. Bizonyos esetekben a korábban eltárolt negatív cache is befolyásolhatja ezt az eredményt.

- Van válasz, de az eredmény hibás
  
  Ilyenkor a DNS-szerver ugyan válaszol, de nem azt az adatot adja vissza, amit várnál. Ennek oka lehet hibás zónaadat, rossz delegáció, split-DNS probléma, vagy olyan elavult adat, amely még cache-ből érkezik.

### DNS biztonsági és privacy szempontok

**DNS spoofing / cache poisoning**

A DNS‑történelem egyik klasszikus problémája, hogy a resolver cache‑ébe hamis rekord kerülhet, és onnantól a kliensek rossz IP‑re mennek. A jelenséget a CERT is úgy írja le, mint támadást, ahol a támadó “hamis DNS információt juttat a cache‑be”.

Modern megfogalmazás szerint a cache poisoning során hamis DNS-adat kerül a gyorsítótárba, ami hibás névfeloldási válaszokhoz vezethet.

**Védekezési irányok (rendszerszinten)**

- **DNSSEC**: a DNSSEC kiterjesztések célja, hogy **eredet‑hitelességet és adatintegritást** adjanak a DNS válaszokhoz (nem titkosítás, hanem validálhatóság).
- **Forged answer elleni “keményítés”**: léteznek olyan ajánlások, amelyek a DNS implementációk viselkedését standardizálják/erősítik, hogy kevésbé fogadjanak el hamis válaszokat.

**DNS privacy**

A DNS lekérdezések “metaadata” (mit kérdezel le) érzékeny lehet. A DNS privacy kérdéskörét külön RFC elemzi, és ez a téma ma már a mindennapi üzemeltetésben is releváns (különösen vállalati környezetben, ahol a központi DNS‑policy, szűrés, naplózás elvárás).

**Titkosított transzportok**

- **DNS over TLS (DoT)**: Olyan megoldás, amely a DNS-forgalmat TLS (Transport Layer Security) -sel titkosított kapcsolaton továbbítja, így nehezebb lehallgatni vagy módosítani a lekérdezéseket útközben.
- **DNS over HTTPS (DoH)**: Olyan megoldás, amely a DNS-lekérdezéseket HTTPS-forgalomba ágyazva továbbítja, így a névfeloldás jobban beleolvad a szokásos webes forgalomba.

Port oldalon ez üzemeltetési szinten is látszik:

- DoT tipikusan **853/TCP** (IANA: `domain-s`).

### DHCP biztonság: rogue DHCP és DHCP starvation

**Rogue DHCP**: ha valaki illetéktelen DHCP-szervert helyez üzembe a hálózaton, az klienseket félrekonfigurálhat (rossz gateway, rossz DNS, MITM‑szerű terelés). A védekezés egyik tipikus L2 eszköze a **DHCP snooping**, ami trusted/untrusted portokra bont, és szűri a “DHCP szerver jellegű” forgalmat az end‑user portokon.

**DHCP starvation**: IP készlet kimerítése sok hamis igénnyel, ami gyakran együtt jár rogue DHCP‑val. A védekezésben a DHCP snooping és port‑szintű kontrollok relevánsak.

### ARP röviden: miért releváns DNS/DHCP mellett?

Az ARP (IPv4) arra való, hogy a helyi hálózaton az eszköz megtalálja, hogy egy adott IPv4 címhez melyik MAC cím tartozik. Az ARP protokollcímek (pl. IP) → lokális hálózati címek (pl. Ethernet) leképezését segíti.

Az `arp -a` parancs és az ARP cache hibakeresési szerepe is fontos, mert segít ellenőrizni, hogy a gép milyen IP-címekhez milyen MAC-címeket társít a helyi hálózaton. Ezzel gyorsan kideríthető, hogy egy adott eszköz, például az alapértelmezett átjáró, valóban elérhető-e helyi szinten, és létrejött-e hozzá a megfelelő ARP-bejegyzés. Hibakeresésnél ez különösen hasznos, mert megmutathatja, hogy a probléma már a helyi hálózati szinten jelentkezik-e, vagy csak magasabb rétegben, például IP- vagy DNS-szinten.

### NAT röviden: mit csinál és mit nem?

A NAT (Network Address Translation) lényege, hogy **címeket (és gyakran portokat) fordít “belső” és “külső” hálózat között**. A “Basic NAT” és a port‑fordítással járó változatok (NAPT) klasszikus leírását RFC, tehát egy hivatalosan közzétett szakmai specifikáció tárgyalja.

Fontos tisztázás:

- A NAT **nem DNS**: nem neveket old fel, nem tart nyilván rekordokat.  
- A NAT **nem DHCP**: nem oszt IP‑t a kliensednek (legfeljebb a routered DHCP‑t is futtat, de az egy másik szolgáltatás).

### Protokollok és jól ismert portok: DNS/DHCP szemmel

A portszámok hivatalos nyilvántartásáért az IANA (Internet Assigned Numbers Authority) felel.

A DNS/DHCP, valamint a gyakran használt hálózati és üzemeltetési protokollok portjai áttekintő jelleggel:

| Protokoll / szolgáltatás | Port / transzport         | Megjegyzés                                                                                    |
| ------------------------ | ------------------------- | --------------------------------------------------------------------------------------------- |
| **TCP/IP**               | N/A                       | Alapprotokoll-készlet, nem egyetlen konkrét porthoz kötődik.                                  |
| **ICMP**                 | N/A                       | Hibajelzésre és diagnosztikára használják, például ping esetén.                               |
| NetBEUI                  | N/A                       | Nem TCP/IP-alapú protokoll, ezért nem klasszikus TCP/UDP porthoz kötődik.                     |
| NetBIOS                  | 137/UDP, 138/UDP, 139/TCP | Régebbi Windows hálózati névfeloldási és fájlmegosztási környezetekben jellemző.              |
| **DNS**                  | 53/UDP, 53/TCP            | Általános névfeloldás.                                                                        |
| mDNS                     | 5353/UDP                  | Helyi hálózaton működő névfeloldás, például kis hálózatokban vagy zeroconf környezetben.      |
| **DHCPv4**               | 67/UDP, 68/UDP            | 67/UDP: szerver, 68/UDP: kliens.                                                              |
| **DHCPv6**               | 547/UDP, 546/UDP          | 547/UDP: szerver, 546/UDP: kliens.                                                            |
| **NTP**                  | 123/UDP                   | Időszinkronizálás.                                                                            |
| **HTTP**                 | 80/TCP                    | Webforgalom.                                                                                  |
| **HTTPS**                | 443/TCP                   | Titkosított webforgalom.                                                                      |
| **FTP**                  | 20/TCP, 21/TCP            | 21/TCP: vezérlőkapcsolat, 20/TCP: klasszikus adatkapcsolat aktív módban.                      |
| **TFTP**                 | 69/UDP                    | Egyszerű fájlátvitelre használják, főleg hálózati eszközök és bootolási környezetek esetén.   |
| **SSH**                  | 22/TCP                    | Távoli, titkosított parancssoros elérés.                                                      |
| SFTP                     | 22/TCP                    | Az SSH File Transfer Protocol tipikusan az SSH fölött működik.                                |
| **Telnet**               | 23/TCP                    | Titkosítatlan távoli parancssoros elérés.                                                     |
| **SMTP**                 | 25/TCP                    | E-mail továbbítás / küldés.                                                                   |
| **POP3**                 | 110/TCP                   | E-mailek letöltése.                                                                           |
| **IMAP**                 | 143/TCP                   | E-mailek elérése és szinkronizálása.                                                          |
| IMAPS                    | 993/TCP                   | Titkosított IMAP.                                                                             |
| POP3S                    | 995/TCP                   | Titkosított POP3.                                                                             |
| LDAP                     | 389/TCP, 389/UDP          | Címtárszolgáltatások elérése, például Active Directory vagy más LDAP-alapú rendszerek esetén. |
| LDAPS                    | 636/TCP                   | Titkosított LDAP-kapcsolat.                                                                   |
| Kerberos                 | 88/TCP, 88/UDP            | Hitelesítési protokoll, különösen Active Directory környezetben fontos.                       |
| **SNMP**                 | 161/UDP                   | Hálózati eszközök felügyelete és lekérdezése.                                                 |
| Syslog                   | 514/UDP                   | Naplóüzenetek hálózati továbbítására használják.                                              |
| **SMB**                  | 445/TCP                   | Windows fájl- és nyomtatómegosztás.                                                           |
| **RDP**                  | 3389/TCP                  | Távoli asztali kapcsolat; IANA név: `ms-wbt-server`.                                          |

Megjegyzés: a portszám csak az alapértelmezett szolgáltatási portot jelzi, de önmagában nem garantálja a forgalom valódi jellegét. Üzemeltetésnél ezért nem elég csak a portszámot nézni.

## Összefoglalás

A DNS és a DHCP a modern IP–alapú hálózatok két meghatározó alap szolgáltatása. A DHCP feladata, hogy a kliensek automatikusan megkapják a működéshez szükséges hálózati paramétereket, például az IP–címet, az alhálózati maszkot, az alapértelmezett átjárót és a DNS–szerver címét. A DNS ezzel szemben a névfeloldást végzi, vagyis a könnyen megjegyezhető neveket IP–címekhez és egyéb szolgáltatásinformációkhoz rendeli. A két szolgáltatás együtt teszi lehetővé, hogy egy kliens gyorsan csatlakozzon a hálózatra, majd elérje a kívánt erőforrásokat és szolgáltatásokat.

A dokumentáció bemutatta a DNS működésének logikáját a hierarchikus névtértől és a rekurzív feloldástól kezdve a rekordtípusokon, a cache–elésen és a TTL szerepén át egészen a gyakorlati hibakeresésig. Külön hangsúlyt kaptak a legfontosabb rekordtípusok, például az A, AAAA, CNAME, MX, NS, PTR, TXT, SOA, SRV és CAA rekordok, valamint az, hogy ezek milyen tipikus üzemeltetési helyzetekben és hibákban jelennek meg. A DHCP oldalán a dokumentum részletesen végigvette a kiosztási módokat, a DORA folyamatot, a lease életciklusát, a scope, exclusion, reservation és options elemek szerepét, továbbá a DHCP relay működését több alhálózatot vagy VLAN–t tartalmazó környezetben.

A gyakorlati rész azt is megmutatta, hogy a hálózati problémák megértéséhez nem elég önmagukban a DNS– vagy DHCP–beállításokat nézni. Fontos szerepet kap a hibakeresésben az ARP, a NAT, az IP–konfiguráció, a gateway, a cache állapota, valamint a kliens és a szerver közötti teljes logikai folyamat átlátása is. A névfeloldási hibák, a rossz DHCP–opciók, a hibás delegációk vagy a nem megfelelő rekordok mind olyan problémák, amelyek hasonló tüneteket okozhatnak, ezért a rendszerezett, lépésről lépésre haladó hibakeresés kulcsfontosságú.

Biztonsági és üzemeltetési szempontból is jól látható, hogy a DNS és a DHCP nem pusztán kényelmi szolgáltatások. A DNS cache poisoning, a rogue DHCP, a DHCP starvation, valamint a titkosított DNS–transzportok és a DNSSEC mind azt mutatják, hogy ezek a szolgáltatások a hálózat megbízhatóságát, biztonságát és működőképességét közvetlenül befolyásolják. Összességében a DNS és a DHCP megértése nemcsak elméleti tudás, hanem alapvető rendszergazdai és hálózatüzemeltetési készség is.

## Fogalomtár

**A rekord** – Olyan DNS–rekord, amely egy domainnevet IPv4–címhez rendel.

**AAAA rekord** – Olyan DNS–rekord, amely egy domainnevet IPv6–címhez rendel.

**APIPA** – Az Automatic Private IP Addressing rövidítése. Olyan automatikus IPv4–címzést jelent, amelyet a rendszer DHCP hiányában a 169.254.0.0/16 tartományból választ.

**ARP** – Az Address Resolution Protocol rövidítése. Arra szolgál, hogy egy IPv4–címhez tartozó MAC–címet fel lehessen oldani a helyi hálózaton.

**Autoritatív névszerver** – Olyan DNS–szerver, amely egy adott zóna hiteles rekordjait szolgáltatja.

**AXFR** – Teljes zónaátvitelt jelent két DNS–szerver között.

**Broadcast** – Olyan hálózati kommunikációs forma, amikor egy csomag a helyi hálózat minden érintett eszközéhez eljut.

**Broadcast domain** – Az a 2. rétegbeli hálózati tartomány, amelyen belül a broadcast forgalom minden érintett eszközhöz eljut.

**CAA rekord** – Azt szabályozza, hogy mely hitelesítésszolgáltatók adhatnak ki tanúsítványt egy adott domainhez.

**Cache** – Gyorsítótár, amely ideiglenesen tárolja a korábban lekérdezett adatokat.

**Cache poisoning** – Olyan támadás, amely során hamis adat kerül a gyorsítótárba, és ez hibás válaszokhoz vezethet.

**CDN** – A Content Delivery Network rövidítése. Földrajzilag elosztott kiszolgálórendszer, amely a tartalmak gyorsabb és hatékonyabb kiszolgálását segíti.

**Certificate Transparency** – Olyan nyilvános naplózási modell, amely segít nyomon követni a kiadott digitális tanúsítványokat.

**CNAME rekord** – Alias rekord, amely egy nevet egy másik, kanonikus névre irányít.

**DHCPOFFER** – A DHCP–szerver ajánlata a kliens felé a címkiosztási folyamat során.

**DHCP** – A Dynamic Host Configuration Protocol rövidítése. Olyan protokoll, amely automatikusan IP–címet és egyéb hálózati paramétereket oszt ki a klienseknek.

**DHCPACK** – A szerver visszaigazoló üzenete, amely véglegesíti a kiosztást.

**DHCPDISCOVER** – A kliens első DHCP–üzenete, amellyel DHCP–szervert próbál elérni a hálózaton.

**DHCP helper / relay** – Olyan köztes funkció, amely más alhálózatból is eljuttatja a DHCP–kéréseket a szerverhez.

**DHCP options** – A DHCP–ben továbbított kiegészítő paraméterek. Ilyen lehet például a gateway, a DNS–szerver vagy a domainnév.

**DHCPREQUEST** – A kliens üzenete, amellyel elfogadja a felajánlott konfigurációt.

**DHCP snooping** – Olyan 2. rétegbeli védelmi mechanizmus, amely segít kiszűrni a jogosulatlan DHCP–szervereket.

**Delegáció** – Az a DNS–művelet, amikor egy zóna egy részének kiszolgálását NS rekordokkal átadják egy másik zónának vagy névszervernek.

**Dig** – Parancssori DNS–diagnosztikai eszköz, amely részletes DNS–lekérdezésekhez és hibakereséshez használható.

**DNS** – A Domain Name System rövidítése. Hierarchikus névfeloldó rendszer, amely neveket IP–címekhez és más adatokhoz rendel.

**DNS cache poisoning** – Olyan támadás, amely hamis DNS–adatot juttat a resolver gyorsítótárába.

**DNSSEC** – A Domain Name System Security Extensions rövidítése. A DNS–adatok hitelességének és sértetlenségének ellenőrzését szolgáló kiterjesztés.

**DoH** – A DNS over HTTPS rövidítése. DNS–lekérdezéseket továbbít HTTPS–en keresztül.

**DoT** – A DNS over TLS rövidítése. DNS–lekérdezéseket továbbít TLS–sel védett kapcsolaton keresztül.

**DORA** – A Discover, Offer, Request, Acknowledge rövidítése. A DHCP címkiosztási folyamat négy alaplépését jelöli.

**Dual–stack** – Olyan hálózati működés, ahol egy rendszer egyszerre használ IPv4– és IPv6–címzést is.

**EDNS** – Az Extension Mechanisms for DNS rövidítése. A DNS kibővítésére szolgál, például nagyobb válaszok és extra információk kezelésére.

**ECS** – Az EDNS Client Subnet rövidítése. Olyan EDNS–kiterjesztés, amely a kliens hálózati helyzetéhez igazodó válaszadást segítheti.

**Exclusion range** – Olyan IP–tartomány a DHCP scope–on belül, amelyet a szerver nem oszt ki.

**Failover** – Olyan működési mód, amikor hiba esetén egy tartalék rendszer vagy útvonal veszi át a szolgáltatás szerepét.

**Forward lookup** – Név alapján történő lekérdezés, amely IP–címet vagy más DNS–adatot ad vissza.

**Glue rekord** – A delegáció működéséhez szükséges kiegészítő A vagy AAAA rekord. Erre akkor van szükség, ha az NS neve a delegált zónán belül van.

**Happy Eyeballs** – Olyan kliensoldali működési logika, amely IPv4 és IPv6 között igyekszik a gyorsabban elérhető kapcsolatot választani.

**Hostnév** – Egy eszköz vagy szolgáltatás neve a hálózatban vagy a DNS–ben.

**ICMP** – Az Internet Control Message Protocol rövidítése. Hibajelzésre és diagnosztikára használják, például ping esetén.

**IANA** – Az Internet Assigned Numbers Authority rövidítése. A protokollparaméterek, portszámok és több internetes regiszter hivatalos nyilvántartásáért felel.

**IMAP** – Az Internet Message Access Protocol rövidítése. E–mail hozzáférési és szinkronizálási protokoll.

**In–bailiwick** – Olyan helyzet, amikor egy névszerver neve ugyanazon delegált zónán belül található, ezért glue rekordra lehet szükség.

**IP–cím** – Hálózati cím, amely egy eszközt azonosít egy IP–hálózatban.

**ISP** – Az Internet Service Provider rövidítése. Internetszolgáltatót jelent.

**Iteratív lekérdezés** – Olyan DNS–lekérdezési mód, amikor a szerver a legjobb tudása szerint válaszol, és szükség esetén másik szerver felé irányítja a kérdezőt.

**IXFR** – Inkrementális zónaátvitelt jelent, vagyis csak a változások kerülnek továbbításra két DNS–szerver között.

**Kerberos** – Hálózati hitelesítési protokoll, amely különösen Active Directory környezetben fontos.

**Lease** – DHCP–bérlet. Azt az időtartamot jelenti, ameddig a kliens használhat egy kiosztott IP–címet.

**Link–local cím** – Olyan cím, amely csak a helyi linken vagy helyi hálózati szegmensben használható.

**MAC–cím** – A hálózati interfész hardverszintű azonosítója.

**Manual allocation** – Olyan DHCP–kiosztási mód, ahol a kliens előre meghatározott címet kap.

**mDNS** – A Multicast DNS rövidítése. Helyi hálózaton működő névfeloldási megoldás, amely központi DNS–szerver nélkül is képes neveket feloldani.

**MX rekord** – A domain levelezéséért felelős szervereket jelöli ki.

**NAPT** – A Network Address and Port Translation rövidítése. A NAT egyik változata, amely cím– és portfordítást is végez.

**NAT** – A Network Address Translation rövidítése. Hálózati címfordítást jelent belső és külső hálózatok között.

**Negatív cache** – Olyan gyorsítótárazás, amikor a rendszer a nem létező névre vagy hiányzó rekordtípusra adott DNS–választ is eltárolja.

**NODATA** – Olyan DNS–válasz, ahol a név létezik, de a kért rekordtípus nem.

**NS rekord** – Meghatározza, mely névszerverek autoritatívak egy adott zónára.

**nslookup** – Parancssori DNS–diagnosztikai eszköz, amellyel névfeloldás és különböző rekordtípusok ellenőrizhetők.

**NXDOMAIN** – Olyan DNS–válasz, amely szerint a lekérdezett név nem létezik.

**Option 82** – A DHCP Relay Agent Information Option neve. Olyan metaadatot jelent, amelyet a relay továbbíthat a szerver felé.

**Parent zóna** – A delegáció szempontjából felsőbb szintű DNS–zóna.

**POP3** – A Post Office Protocol version 3 rövidítése. E–mail letöltésére szolgáló protokoll.

**Pozitív cache** – Olyan gyorsítótárazás, amikor a rendszer létező rekordokra kapott válaszokat tárol el egy ideig.

**PTR rekord** – Reverse DNS–rekord, amely IP–címből név feloldását teszi lehetővé.

**Recursive resolver** – Olyan DNS–feloldó, amely a kliens helyett végigviszi a teljes névfeloldási folyamatot.

**Rekurzív lekérdezés** – Olyan DNS–lekérdezési mód, amikor a kérdező teljes választ vár a kiszolgálótól, nem csak továbbirányítást.

**Reservation** – DHCP–ben előre lefoglalt fix IP–cím egy adott klienshez.

**Resolver** – Olyan kliensoldali vagy szerveroldali összetevő, amely DNS–nevek feloldását végzi.

**Resource record (RR)** – A DNS alapvető adategysége.

**Reverse lookup** – IP–cím alapján történő névlekérdezés.

**Rebinding** – A DHCP lease–megújítás olyan fázisa, amikor a kliens már nem csak az eredeti szervertől fogadhat el megújítást.

**Rogue DHCP** – Jogosulatlan DHCP–szerver a hálózaton, amely félrekonfigurálhatja a klienseket.

**Root zóna** – A DNS–hierarchia legfelső szintje.

**RDP** – A Remote Desktop Protocol rövidítése. Távoli grafikus asztali kapcsolat létrehozására szolgál.

**RFC** – A Request for Comments rövidítése. Az internetes és hálózati technológiákhoz kapcsolódó szabványok és műszaki leírások egyik alapvető dokumentumtípusa.

**SaaS** – A Software as a Service rövidítése. Olyan szolgáltatási modell, ahol egy alkalmazás interneten keresztül, szolgáltatásként érhető el.

**Scope** – DHCP–ben a kiosztható IP–címkészlet.

**Serial** – A SOA rekord egyik mezője, amely a zóna verzióját jelzi, és segíti a másodlagos szerverek frissítését.

**SMB** – A Server Message Block rövidítése. Fájl– és nyomtatómegosztási protokoll, különösen Windows környezetben elterjedt.

**SNMP** – A Simple Network Management Protocol rövidítése. Hálózati eszközök felügyeletére és lekérdezésére használják.

**SOA rekord** – Olyan rekord, amely a zóna adminisztratív metaadatait tartalmazza.

**Split–DNS** – Olyan megoldás, ahol ugyanahhoz a névhez belső és külső környezetben eltérő DNS–válasz tartozhat.

**SRV rekord** – Olyan rekord, amely megadja, hogy egy szolgáltatás melyik szerveren és porton érhető el.

**Stub resolver** – Kliensoldali feloldó, amely egy rekurzív resolverhez fordul a névfeloldásért.

**Syslog** – Naplóüzenetek hálózati továbbítására szolgáló protokoll vagy szolgáltatás.

**T1** – A DHCP lease első megújítási időpontja. Ez tipikusan a bérleti idő felénél következik be.

**T2** – A DHCP lease második megújítási fázisa. Ilyenkor a kliens már nem csak az eredeti szervertől kérhet megújítást.

**TCP** – A Transmission Control Protocol rövidítése. Kapcsolatorientált, megbízható szállítási rétegbeli protokoll.

**TLD** – A Top–Level Domain rövidítése. A domainnév legfelső szintjét jelenti, például a .hu vagy a .com részt.

**TLS** – A Transport Layer Security rövidítése. Olyan titkosítási protokoll, amely biztonságos adatátvitelt biztosít a hálózaton.

**TLV** – A Type–Length–Value rövidítése. Olyan adatformátum, amely típus, hossz és érték mezőkből áll.

**TTL** – A Time To Live rövidítése. DNS–ben azt adja meg, meddig tartható gyorsítótárban egy rekord.

**TXT rekord** – Szöveges adatokat tároló DNS–rekord.

**UDP** – A User Datagram Protocol rövidítése. Kapcsolatmentes szállítási rétegbeli protokoll, amely gyors, de nem garantál megbízható kézbesítést.

**VLAN** – A Virtual Local Area Network rövidítése. Logikailag elkülönített hálózati szegmenst jelent.

**Zóna** – A DNS névtér adminisztratív egysége, amelyért egy vagy több autoritatív névszerver felel.

**Zóna apex** – A DNS–zóna legfelső, gyökérszintű neve az adott zónán belül, ahol bizonyos rekordtípusok együttélése korlátozott lehet.