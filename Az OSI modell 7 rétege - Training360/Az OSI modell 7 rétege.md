## Az OSI modell 7 rétege

**Források és felhasznált eszközök:**

- [Training360](https://www.training360.com/), [IT Essentials - 01 - Hálózati alapismeretek tanfolyam](https://e-learning.training360.com/courses/1it-essentials)

- [ChatGPT](https://chatgpt.com/), [DeepSeek](https://www.deepseek.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

Az **OSI modell** egy **7 rétegű gondolkodási keret**, ami segít egységesen leírni, hogyan jut el az adat két végpont között – és főleg azt, hogy **hol romolhat el**, mit jelent egy hiba, és **melyik komponens/protokoll** a felelős.

## 7. Alkalmazási réteg (Application)

**Mit csinál?** 

Az a réteg, amit a felhasználó “lát”: **alkalmazásprotokollok** és szolgáltatások.

Gyakorlatban itt a **konkrét hálózati szolgáltatás** viselkedéséről beszélünk: a böngésző weboldalt kér le (HTTP/HTTPS), a kliens névfeloldást végez (DNS), levelet küld/fogad (SMTP/IMAP), távoli belépést indít (SSH/RDP). Ez a réteg írja le, hogy “mit akarunk elérni” a hálózaton, és a hibák gyakran itt jelennek meg a legérthetőbben (pl. hibakód, elutasítás, időtúllépés), miközben az ok lehet alatta is.

**Adatút (küldő oldal, “darabolás/hozzáadás”):** itt keletkezik a **hasznos adat (payload)** az alkalmazás nyelvén (pl. HTTP kérés, DNS lekérdezés). A TCP/IP modellben ez a rész jellemzően az **Application réteg** (ami nagyjából az OSI 5–7 tartományát fedi). Innen lefelé haladva a rétegek a payload köré **plusz információt** tesznek, hogy a hálózat kezelni tudja.

**Példák / protokollok:** HTTP/HTTPS, DNS, SMTP/IMAP, SSH, RDP, SMB (részben), NTP.

**Tipikus hibák:**

- “Nem jön be az oldal”, “nem megy a névfeloldás”, “nem érkezik meg az email”, “időeltérés miatt hibázik valami”.

**Mit ellenőrzöl gyorsan?**

- URL/DNS: `nslookup`, `dig`

- HTTP: böngésző devtools, `curl`

- Email: MX rekordok, SMTP logok

- Idő: NTP státusz

**Biztonsági szempontból:**

Itt vannak a leggyakoribb támadási felületek: webes sebezhetőségek, rosszindulatú letöltések, DNS manipuláció, jogosulatlan távoli elérés (pl. RDP/SSH). Az alkalmazáslogok (web/app logok, DNS query log, proxy log) gyakran a leghasznosabb nyomok.

## 6. Megjelenítési réteg (Presentation)

**Mit csinál?**

Adat **formátum**, **kódolás**, **tömörítés**, **titkosítás** (fogalmi szinten).

Ez a réteg azt fogja meg, hogy a küldött adat **milyen alakban** érkezzen meg a másik oldalra: milyen karakterkódolást használ (pl. UTF-8), milyen adatformátumban van (pl. JSON/XML), van-e tömörítés (pl. gzip), illetve hogyan történik a titkosítás és visszafejtés logikája. A modern hálózatokban a titkosított kommunikáció miatt ez különösen fontos: itt dől el, hogy a felek egyáltalán **kompatibilisek-e** egymással (tanúsítvány, TLS verzió, cipher), és ha nem, akkor tipikusan “nem megy a HTTPS” jellegű hibát kapsz.

**Adatút (küldő oldal):** ezen a ponton a payload gyakran **átalakításon** megy át (kódolás/formátum), esetleg **tömörítésen**, majd titkosítás esetén “becsomagolódik” (pl. TLS). Itt tipikusan nem “darabolás” történik hálózati mérethatár szerint, hanem **a tartalom előkészítése** úgy, hogy alatta a szállítás és útvonalválasztás már egységesen kezelhető legyen.

**Példák:** TLS/SSL (gyakran ide sorolják), JSON/XML, UTF-8, Base64, gzip.

**Tipikus hibák:**

- Titkosítási/kompatibilitási gondok: “TLS handshake failed”, rossz tanúsítvány, nem egyező cipher, sérült/rosszul kódolt payload.

**Mit ellenőrzöl?**

- TLS inspection/proxy bontás okozta mellékhatások

- TLS verziók/cipher-ek kompatibilitása

- Tanúsítvány érvényesség, lánc, hostname egyezés

**Biztonsági szempontból:**

A titkosítás egyszerre véd és “eltakar”: hálózaton kevesebbet látsz a tartalomból, ezért felértékelődnek a metaadatok (pl. tanúsítványok, kapcsolati jellemzők, forgalmi mintázat).

## 5. Viszonyréteg (Session)

**Mit csinál?**

Kapcsolatok **felépítése, fenntartása, bontása**; “beszélgetés” állapota.

Itt a fókusz azon van, hogy a kommunikáció ne csak különálló üzenetek sorozata legyen, hanem egy **összefüggő munkamenet**, amit a két oldal “azonosít” és kezel (pl. bejelentkezett állapot, újracsatlakozás, időtúllépés, session-élettartam). Sok rendszerben ez több rétegen “szétterül”, de OSI szemlélettel ide sorolható minden, ami a kapcsolat logikai állapotát kezeli. Tipikus jelenség: a hálózat “látszólag megy”, de az alkalmazás mégis kidob vagy megszakad, mert a session-állapot valahol elveszik (pl. NAT/tűzfal timeout, load balancer viselkedés).

Gyakorlatban ez a réteg a leginkább **“elmosódott”**: a legtöbb modern megoldásban a session nagy része **az alkalmazásrétegben** jelenik meg (pl. HTTP session cookie, JWT token), miközben a “kapcsolat életben tartásának” több eleme **a 4. réteghez (TCP)** kötődik. Ettől még hibakeresésnél hasznos külön gondolkodni róla, mert a tünetek gyakran “session-jellegűek”.

**Adatút (küldő oldal):** itt a kommunikáció tipikusan kap valamilyen **állapot- vagy azonosító kontextust** (pl. “melyik munkamenethez tartozik”), amit a rendszer a későbbi kéréseknél is figyelembe vesz. A TCP/IP modellben ez gyakran az alkalmazási logika része (nem mindig “külön doboz”), de hibakeresésnél hasznos külön gondolni rá, mert a “random megszakad” jellegű gondok sokszor itt érnek tetten.

**Példák:** RPC, NetBIOS session (régebbi), egyes auth/SSO folyamatok “session” logikája.

**Tipikus hibák:**

- Véletlenszerű megszakadások, “timeout”, újratárgyalás, session-újrahasznosítás gondok.

**Mit ellenőrzöl?**

- Időtúllépési beállítások, állapottáblák (tűzfal), load balancer session persistency, NAT timeouts.

**Biztonsági szempontból:**

Gyakori téma a session hijacking, tokenek ellopása/újrajátszása, és a nem megfelelő session-kezelés (pl. túl hosszú élettartam).

## 4. Szállítási réteg (Transport)

**Mit csinál?**

Végpontok közti **megbízható** (TCP) vagy **gyors/“best effort”** (UDP) adatátvitel, **portok**.

Ez a réteg biztosítja a végpontok közti adatátvitel “szabályait”: TCP esetén kapcsolatot épít, visszaigazol, sorrendben tart, újraküld; UDP esetén minimális többlettel, gyorsan továbbít. A portok itt adnak értelmet annak, hogy ugyanaz a gép egyszerre több szolgáltatást futtathat: IP a célgépet azonosítja, a port pedig azt, **melyik szolgáltatáshoz/folyamathoz** tartozik a forgalom. Hibaelhárításnál itt nagyon gyakori a “port nincs nyitva / szűrve van / félbemarad a kapcsolat” jellegű probléma.

**Adatút (küldő oldal, ez a klasszikus “darabolás”):** itt történik a **szegmentálás** TCP-nél (vagy UDP datagram képzés). A rendszer a nagyobb alkalmazás-adatfolyamot olyan méretű részekre bontja, amit a hálózat kényelmesen tud vinni, majd hozzáad egy **transport fejlécet**: forrás/cél **portok**, TCP esetén tipikusan **sorszám (sequence)**, visszaigazolás (ACK), vezérlő flag-ek (SYN/FIN), stb. Ekkor a payload neve gyakran **TCP szegmens** vagy **UDP datagram**. TCP/IP modellben ez a **Transport layer**.

**Kulcsfogalmak:** TCP 3-way handshake (SYN, SYN-ACK, ACK), újraküldés, ablakméret; UDP kapcsolat nélküli.

**Példák:** TCP (web, SSH, RDP), UDP (DNS, VoIP, NTP, streaming).

**Tipikus hibák:**

- Port zárva / szűrve, fél-nyitott kapcsolatok, csomagvesztés miatti retransmission, MTU/fragmentációból fakadó furcsaságok.

**Mit ellenőrzöl?**

- `Test-NetConnection <host> -Port <p>` / `telnet` / `nc`

- Tűzfal szabályok, NAT, állapottábla telítődés

- `netstat -ano`, `ss -tulpn`

**Biztonsági szempontból:**

Itt jön képbe a portscan, SYN flood, szokatlan portok, és a “miért van ennek a gépnek ennyi outbound kapcsolata?” jellegű vizsgálat. Sokszor már a kapcsolati metaadatok is erős jelzést adnak.

## 3. Hálózati réteg (Network)

**Mit csinál?**

**IP-címzés** és **útvonalválasztás** (routing) hálózatok között.

Ez a réteg felel azért, hogy a forgalom **külön hálózatok között** is eljusson a célhoz. Itt dől el, milyen IP-címet használ a gép, mi az alapértelmezett átjáró, és a routerek milyen útvonal alapján továbbítják a csomagot. A routing logikája (akár statikus, akár dinamikus) lényegében az, hogy a hálózati eszköz eldöntse: “a következő ugrás merre van a cél felé”. Tipikus problémák, amikor a helyi hálózat rendben van, de “kifelé” nem megy, vagy bizonyos irányokba elérhetetlen (hibás route, ACL, aszimmetria).

**Adatút (küldő oldal):** a transport “csomagra” rákerül az **IP fejléc**, ami tartalmazza többek között a **forrás és cél IP-címet**, és olyan mezőket, amik az útvonalon való továbbítást segítik (pl. TTL/Hop Limit, protokoll jelölés). Innentől gyakran **IP csomagnak (packet)** hívjuk. TCP/IP modellben ez az **Internet layer**.

**Példák:** IPv4/IPv6, ICMP, routing (OSPF/BGP – gyakorlati világban ide kapcsolódik), IPsec (fogalmilag ide is köthető).

**Tipikus hibák:**

- Rossz IP/gateway, hibás route, aszimmetrikus útvonal, ACL (Access Control List) blokkolás, ICMP (Internet Control Message Protocol) tiltás miatti nehezebb diagnosztika.

**Mit ellenőrzöl?**

- `ipconfig /all` / `ip a`

- `ping`, `tracert`/`traceroute`, `pathping`

- Routing táblák, router ACL-ek

**Biztonsági szempontból:**

Ide tartozhatnak a gyanús tunneling minták, szokatlan ICMP aktivitás, illetve a szegmentáció/útvonal-szabályok (ki honnan hova érhet el) – ami sok támadásnál döntő.

## 2. Adatkapcsolati réteg (Data Link)

**Mit csinál?**

Helyi hálózaton (LAN) **keretezés**, **MAC címzés**, **switching**, VLAN-ok.

Ez a réteg a “helyi hálózati szállítás” világa: ugyanabban a LAN-ban (tipikusan **egy VLAN-on belül**) a csomagok Ethernet/Wi-Fi keretekbe kerülnek, és a **switch** a MAC címek alapján dönt a továbbításról (**switching**). Fontos különbség, hogy ez a réteg egy **közvetlenül összekapcsolt** szegmensen belül működik: amint át kell lépni egy másik hálózatba (másik IP alhálózatba / másik VLAN-ba), a **3. réteg (routing)** lép működésbe egy routeren vagy L3 switche-n keresztül. Emiatt sok “rejtélyes” hiba innen jön: rossz VLAN-ba került egy port, trunk/access mismatch, loop vagy ARP-probléma miatt a gépek “nem találják egymást” akkor sem, ha IP szinten elvileg minden jól néz ki.

**Adatút (küldő oldal):** az IP packet kap egy **L2 fejlécet** (tipikusan **forrás és cél MAC cím**, és opcionálisan **802.1Q VLAN tag**), valamint gyakran egy **ellenőrző összeget** a keret végén (FCS/CRC – “trailer” jellegű). Innentől **keretnek (frame)** nevezzük.

Lényeges: **routeren/L3 hopon áthaladva az L2 keret mindig újraképződik**, ezért a **MAC címek szakaszonként (hoponként) változnak**. Ez az oka annak, hogy a csomag “elveszíti” az eredeti MAC-címeket a routeren túl: a MAC csak a *következő* helyi szakaszra érvényes, míg az IP címek (routinghoz) end-to-end értelmezettek.

**Példák / technológiák:** Ethernet (802.3), Wi-Fi (802.11), VLAN (802.1Q), ARP, STP.

**Tipikus hibák:**

- Rossz VLAN, trunk/access mismatch, loop (STP gondok), ARP problémák, duplex/negotiation gondok.

**Mit ellenőrzöl?**

- Switch port mód (access/trunk), VLAN tags

- ARP tábla: `arp -a`

- MAC address table, STP állapot

**Biztonsági szempontból:**

Itt jelennek meg a klasszikus LAN-támadások: ARP spoofing, MAC flooding, “rogue” eszközök. Emiatt fontosak a switch oldali védelmek (környezettől függően).

## 1. Fizikai réteg (Physical)

**Mit csinál?**

A bitek tényleges átvitele: kábel, csatlakozó, rádió, jelminőség.

Ez a legalapabb réteg: itt nem protokollokról beszélünk, hanem arról, hogy a jel fizikailag **átmegy-e stabilan**. Ide tartozik a kábelezés minősége, a csatlakozók, az optikai modulok, a Wi-Fi jel erőssége és a zavarás is. Ha itt gond van, az magasabb rétegeken nagyon különböző tünetekben jelenhet meg (szakadozás, csomagvesztés, CRC hibák, link fel-le áll), ezért IT üzemeltetésben mindig érdemes “alul” is ellenőrizni, mielőtt bonyolultabb okokat keresel.

**Adatút (küldő oldal, “utolsó lépés”):** az L2 keret bitekre bomlik, és a fizikai közeg (réz/optika/radio) továbbítja. **A fogadó oldalon ugyanez történik visszafelé (decapsulation):** a bitekből keret lesz, a keretből IP csomag, abból TCP szegmens/UDP datagram, majd a felső rétegek visszaállítják a formátumot/titkosítást és végül az alkalmazás megkapja az eredeti payloadot.

**Példák:** UTP/FTP kábelek, optika, SFP-k, Wi-Fi jel, patch panel, PoE.

**Tipikus hibák:**

- Nincs link, instabil link, CRC error, gyenge Wi-Fi jel, rossz kábel/port, hibás SFP.

**Mit ellenőrzöl?**

- Link LED, port error számlálók, kábelteszt, Wi-Fi RSSI/SNR, interferencia.

**Biztonsági szempontból:**

Itt inkább fizikai védelem: illetéktelen hozzáférés, bedugott “ismeretlen” eszközök, rogue AP, kábelezés kontroll.

## Példa: egy HTTPS kérés útja (és egy tipikus hiba rétegenkénti értelmezése)

Tegyük fel, hogy a felhasználó **nem tud elérni egy belső webalkalmazást** (HTTPS), pl. `https://intra.ceg.local`.

### A “normál” út (küldőtől a fogadóig)

1. **L7 Application:** a böngésző létrehozza a kérést (HTTP request).

2. **L6 Presentation:** TLS-t használunk; a handshake után a HTTP adat titkosítva megy.

3. **L5 Session:** a munkamenet állapotát az alkalmazás kezeli (pl. cookie/token), és a kliens konzisztensen ugyanahhoz a “sessionhöz” tartozó kéréseket küld.

4. **L4 Transport:** TCP; a kliens a cél **443** portra épít kapcsolatot, a forgalom TCP szegmensekre bontva megy.

5. **L3 Network:** IP csomagok keletkeznek (forrás/cél IP, TTL, stb.), a router(ek) útvonal alapján továbbítanak.

6. **L2 Data Link:** az IP csomagok keretekbe kerülnek (MAC címek + esetleg VLAN tag); a switch a VLAN-on belül továbbít. Routeren átlépve új L2 keret képződik a következő szakaszra.

7. **L1 Physical:** bitek mennek a kábelen/optikán/rádión.

**Fogadó oldalon ugyanez történik visszafelé (decapsulation):** bitek → keret → IP csomag → TCP szegmens → (TLS visszafejtés) → az alkalmazás megkapja a kérést. A válasz (weboldal tartalma) ugyanígy megy vissza.

### Beépített hiba: L1–L2 rendben, de L3-on elakad (útvonal hiányzik)

Most nézzük a klasszikus üzemeltetési esetet:

- **L1 rendben:** a link LED zöld, nincs látványos porthiba.

- **L2 rendben:** a kliens a megfelelő VLAN-ban van, a switch oldalon a MAC tábla is “életszerű”.

- **L3 hiba:** `ping`/`tracert` a szerver hálózata felé nem megy, vagy a traceroute megáll a default gateway-nél. Ennek tipikus oka: **hibás/hiányzó route**, rossz L3 ACL, vagy rossz szegmentációs szabály.

- Következmény **L4-től felfelé:** a TCP kapcsolat felépítése sem tud megtörténni (nem lesz SYN-ACK), ezért a böngészőben ez gyakran “timeout / site can’t be reached” formában jelenik meg, és TLS-ig el sem jut a folyamat.

Ez jól mutatja, miért erős az OSI-s gondolkodás: az “alkalmazás nem megy” jellegű panasz mögött sokszor egy alacsonyabb réteg (itt L3) a gyökérok.

## Záró gondolatok

Az OSI modell nem a valós hálózatok teljesen pontos leképezése, hanem egy hasznos gondolkodási keret. Abban segít, hogy a hibákat, protokollokat és biztonsági jelenségeket rétegenként tudjuk értelmezni. Üzemeltetésben és kiberbiztonságban ezért ma is nagyon hasznos: nem azért, mert minden tökéletesen belefér a 7 rétegbe, hanem mert segít gyorsabban megtalálni, hol keresd a problémát.

## Fogalomtár (rövid magyarázatok)

- **TLS / SSL:** Titkosított kommunikációs réteg (pl. HTTPS). A gyakorlatban “SSL”-t is mondanak, de jellemzően TLS fut.

- **TLS handshake:** Kapcsolatfelépítés titkosított csatornán: egyeztetés a titkosításról és tanúsítvány ellenőrzés. Hibája gyakran “HTTPS nem megy” tünet.

- **Tanúsítvány (certificate) és lánc:** A szerver azonosítására szolgál; a lánc azt jelenti, hogy a tanúsítvány megbízható CA-ig visszavezethető. Lejárat/hostname hiba tipikus gond.

- **Cipher suite:** Titkosítási algoritmusok és paraméterek csomagja. Ha nincs közös a klienssel, handshake hiba.

- **SNI:** TLS-ben a kért domain neve a kapcsolat elején; segít több weboldalt kiszolgálni ugyanazon IP-n.

- **TLS inspection (proxy bontás):** Vállalati megoldás, ahol a proxy “középre áll” és ellenőrizhetővé teszi a titkosított tartalmat. Kompatibilitási gondokat is okozhat.

- **Session / token:** Session = munkamenet állapota; token = “bizonyíték”, hogy a kliens jogosult (pl. login után).

- **Session hijacking:** Munkamenet átvétele ellopott token/cookie alapján.

- **NAT (és NAT timeout):** Cím/port fordítás (belső → külső). Timeout: meddig tartja nyilván a kapcsolat állapotát.

- **Load balancer session persistency (stickiness):** Beállítás, hogy egy kliens kérései ugyanarra a backend szerverre menjenek a session alatt.

- **SYN / 3-way handshake:** TCP kapcsolat felépítése 3 lépésben. Szűrés/túlterhelés esetén gyakran itt akad el.

- **MTU és fragmentáció:** Maximális átvihető csomagméret. Rossz MTU/fragmentáció “furcsán” elakadó forgalmat okozhat.

- **Flow / 5-tuple:** Forrás IP, cél IP, forrás port, cél port, protokoll. Ez a forgalom **legpontosabb alap-azonosítója** hálózati megfigyelésben és biztonságban (pl. tűzfali logok, NetFlow/IPFIX). Titkosított forgalomnál is kulcs, mert a payload nem látszik, de a metaadatok (melyik host, melyik port, milyen irány, milyen protokoll) ezek mentén jól korrelálhatók és elemezhetők.

- **ICMP:** Diagnosztikai/vezérlő forgalom (pl. ping). Tiltása nehezítheti a hibakeresést.

- **Tunneling:** Forgalom becsomagolása más protokollba (VPN-nél normális, rosszindulatúan elrejtésre is használható).

- **VLAN (802.1Q):** Logikai hálózati szeparáció ugyanazon fizikai infrastruktúrán.

- **Trunk vs Access port:** Az access port egyetlen VLAN-hoz tartozó végponti port, míg a trunk port több VLAN forgalmát viszi címkézve, tipikusan uplink, virtualizáció vagy router felé.

- **ARP:** IP → MAC feloldás helyi hálózaton, hogy a keret a megfelelő eszközhöz menjen.

- **ARP spoofing:** Hamis ARP válaszokkal forgalom eltérítése/figyelése.

- **STP (Spanning Tree):** Loop megelőzés switch hálózatban; loop esetén “broadcast storm” is kialakulhat.

- **MAC flooding:** Switch MAC táblájának túlterhelése hamis címekkel, hogy a forgalom szélesebb körben továbbítódjon.

- **DHCP snooping / DAI:** Switch védelmi funkciók: rogue DHCP és ARP hamisítás ellen (környezettől függően).

- **PoE:** Tápellátás Ethernet kábelen (AP, IP telefon, kamera).

- **SFP:** Cserélhető optikai/réz modul hálózati eszközökben.

- **RSSI/SNR:** Wi-Fi jel erősség és jel–zaj arány; stabilitásra/átviteli minőségre utal.

- **CRC error:** Kerethiba jelzés; gyakran kábel/port/jelminőség problémát jelez.

---

# Ajánló és jogi nyilatkozat

Ez az összefoglaló egy tanulást segítő, tömör kivonat, amely a lényegi gondolatokat rendezi egymás mellé, de nem helyettesíti az eredeti képzést. Őszintén ajánlom, hogy a témák mélyebb és pontosabb megértéséhez ismerkedj meg az eredeti képzéssel is. A teljes tananyag rendszerint részletes magyarázatokat, kontextust, lépésről lépésre bemutatott folyamatokat és gyakori hibákra felhívó tippeket kínál. Gyakran tartoznak hozzá videók, illusztrációk, letölthető segédanyagok és gyakorlati feladatok, amelyek jelentősen felgyorsítják a fejlődést és elmélyítik a tudást.

Több eredeti képzés elvégzése után hivatalos tanúsítványt vagy igazolást is biztosít a szervező, amely szakmai előnyt és hitelességet adhat a résztvevőnek. Tiszteletben tartva a szerzők jogait és munkáját, ez a jegyzet csupán a tájékozódást és az ismétlést támogatja. Ha lehetőséged van, javaslom az eredeti képzés megvásárlását vagy elérését, mert így hozzáférsz a legfrissebb, naprakész tartalmakhoz. A teljes anyag sokszor közösségi fórumot, visszajelzést, mentorálást és kérdés-válasz lehetőségeket is biztosít.

Érdemes a hivatalos forrásokat követni, mert a frissítések, kiegészítések és pontosítások ott jelennek meg először. Ez a jegyzet a saját értelmezést tükrözi, és tömörsége miatt kimaradhatnak árnyalatok vagy részletek. Amennyiben eltérés merülne fel, mindenben az eredeti képzés tartalma az irányadó. Bátorítalak, hogy látogasd meg az eredeti képzés felületét, nézd végig a videókat, tanulmányozd az illusztrációkat és végezd el a kapcsolódó feladatokat. Így teljesebb képet kapsz, gyorsabban fejlődsz, és tartós, gyakorlatias tudást építesz. Köszönettel és elismeréssel ajánlom az eredeti képzés megismerését.

**Licenc és jogi nyilatkozat**

Ez a jegyzet a **Creative Commons Nevezd meg! – Ne add el! 4.0 (CC BY‑NC 4.0)** licenc feltételei szerint terjeszthető és felhasználható.

A felhasználás feltételei:

- A szerző és a forrás egyértelmű feltüntetése kötelező.

- Kereskedelmi felhasználás nem engedélyezett.

A jegyzet az eredeti forrás(ok) tartalmának összefoglalása és/vagy átdolgozása. Az eredeti művek szerzői jogi védelem alatt lehetnek, és ezen jogok az eredeti szerző(ke)t illetik. Az itt közölt licenc kizárólag a jegyzet szerzőjének saját hozzájárulására vonatkozik.

# Recommendation and Legal Disclaimer

This summary is a concise, study‑support aid that places the core ideas side by side, but does not replace the original training. I sincerely recommend that, for a deeper and more accurate understanding of the topics, you also review the original training. The complete material typically offers detailed explanations, context, step‑by‑step processes, and tips highlighting common mistakes. It often includes videos, illustrations, downloadable resources, and practical exercises that can significantly accelerate progress and deepen knowledge.

After completing several original trainings, the organizer may also provide an official certificate or confirmation, which can offer a professional advantage and add credibility for the participant. Respecting the authors’ rights and work, this note serves solely to support orientation and review. If possible, I recommend purchasing or accessing the original training, as this grants you the most up‑to‑date content. The full material often includes community forums, feedback, mentoring, and Q&A opportunities.

Following the official sources is advisable, as updates, additions, and corrections are published there first. This note reflect personal interpretation, and due to its brevity, nuances or details may be omitted. In the event of any discrepancy, the content of the original training shall prevail. I encourage you to visit the original training platform, watch the videos, study the illustrations, and complete the related exercises. This will give you a more complete understanding, help you progress faster, and build lasting, practical knowledge. With gratitude and respect, I recommend exploring the original training.

**License and Legal Notice**

This note may be distributed and used under the terms of the **Creative Commons Attribution–NonCommercial 4.0 (CC BY‑NC 4.0)** license.

Conditions of use:

- Clear attribution of the author and source is required.
- Commercial use is not permitted.

This note is a summary and/or adaptation of the content from the original source(s). The original works may be protected by copyright, and such rights belong to the original author(s). The license stated here applies only to the original contributions of the note’s author.