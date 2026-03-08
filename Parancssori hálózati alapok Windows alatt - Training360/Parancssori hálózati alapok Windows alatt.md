# **Parancssori hálózati alapok Windows alatt – gyors diagnosztika (`ipconfig`, `ping`, `tracert/pathping`, `nslookup`, `netstat`, `ssh/telnet`, `arp -a`, `route print`, PuTTY)**

**Források és felhasznált eszközök:**

- [Training360](https://www.training360.com/), [Gyártófüggetlen hálózati alapismeretek - 03 - Szolgáltatások és eszközök üzemeltetők számára](https://e-learning.training360.com/courses/gyartofuggetlen-halozati-alapismeretek3)

- [ChatGPT](https://chatgpt.com/), [DeepSeek](https://www.deepseek.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

A **parancssor** (angolul *Command Line Interface*, röviden **CLI**) olyan szöveges felület, amelyen keresztül a rendszer és a hálózati beállítások parancsokkal kérdezhetők le vagy módosíthatók. Hálózati hibakeresésben azért különösen értékes, mert nagyon gyorsan ad objektív adatokat (például **IP-cím**, **átjáró**, **DNS**, **útvonal**, **késleltetés**, **csomagvesztés**, **nyitott portok**), és sokszor akkor is használható, amikor a grafikus felület nem ad elég információt. A **CLI** előnye az is, hogy a lépések jól dokumentálhatók, ismételhetők (akár szkripttel is), és távoli rendszerekhez való kapcsolódáskor (például **SSH**-val) alapvető eszköz.

A hálózati hibaelhárítás egyik klasszikus logikája az, hogy először a helyi konfigurációt érdemes ellenőrizni (van-e érvényes **IP-cím**, megfelelő-e az **átjáró** és a **DNS**), utána a kapcsolatot (elérhető-e a gateway, van-e internet-elérés **IP szinten**), majd a névfeloldást (**DNS**), végül az útvonalat és a részleteket (hol akad el a forgalom, van-e **csomagvesztés**, fut-e gyanús kapcsolat). Az alábbi parancsok ezekhez adnak jól használható, alapszinttől haladóig terjedő diagnosztikai eszköztárat.

## **Mi az az IP-cím röviden, és miért fontos?**

Az **IP-cím** egy hálózati azonosító, amellyel egy eszköz (PC, telefon, szerver, router) elérhető egy **IP-hálózatban**. Gyakorlatiasan úgy érdemes rá gondolni, mint egy „címre”, ahová a hálózati csomagokat kézbesíteni lehet. A mindennapi hálózati működéshez általában három dolognak kell „rendben lennie”: legyen érvényes **IP-cím** (az eszköz azonosítható legyen a helyi hálózaton), legyen **alapértelmezett átjáró** (gateway – amin keresztül a helyi hálózaton túlra lehet menni), és legyen **DNS** (ami a neveket – például `google.com` – IP-címre fordítja). Ha ezek közül bármelyik hiányzik vagy hibás, a kapcsolat tipikusan nem fog megfelelően működni.

---

## **Tipikus IP-cím tartományok (gyors tájékozódáshoz)**

Az alábbiak nem szabályok minden esetre, hanem olyan tipikus minták, amelyek hibakereséskor sokat segítenek „ránézésre” megérteni, mi történik.

**Privát (belső) IPv4 tartományok** – ezek a legtöbb otthoni és vállalati LAN-ban előfordulnak (internet felől közvetlenül nem routolhatók):

- **10.0.0.0 – 10.255.255.255** (**10/8**) – gyakori vállalatoknál, nagyobb hálózatoknál

- **172.16.0.0 – 172.31.255.255** (**172.16/12**) – vállalati környezetben szintén gyakori

- **192.168.0.0 – 192.168.255.255** (**192.168/16**) – otthon, kis irodák, **SOHO (Small Office/Home Office)** routerek klasszikusa

**APIPA (Automatic Private IP Addressing)** – tipikusan hibaindikátor Windowsnál:

- **169.254.0.0 – 169.254.255.255** (**169.254/16**)
  Ha a gép ilyen címet kap, az gyakran azt jelenti, hogy **nem sikerült DHCP-től IP-t kérni**, ezért a rendszer automatikusan beállított egy „vész” címet. Ilyenkor lehet a gond Wi-Fi/kábel, DHCP szerver elérés, VLAN, switch, vagy a router oldala.

**Loopback / saját gép**:

- **127.0.0.1** (vagy a teljes **127/8** tartomány) – „ez a gép”, helyi tesztekhez; nem a hálózatra megy ki.

**Link-local IPv6** (IPv6 környezetben gyakori):

- **fe80::/10** – helyi link (szegmens) szintű kommunikáció; normális jelenség lehet, nem feltétlen hiba.

---

## **Gyakori protokollok fogalmai (TCP, UDP, HTTP(S), DNS, IMAP/IMAPS, stb.)**

A portok megértéséhez érdemes röviden tisztázni, mit jelentenek a leggyakoribb **protokollok** és rövidítések. A protokoll lényegében „szabályrendszer”, amely leírja, hogyan kommunikálnak az eszközök.

Az **IP** a hálózati szint alapja: ez „címez” és eljuttat csomagokat a forrás és a cél között. Erre épülnek a szállítási protokollok, leggyakrabban a **TCP** és az **UDP**.
A **TCP** (Transmission Control Protocol) **kapcsolatorientált**: mielőtt adatot küld, „felépít” egy kapcsolatot, gondoskodik a sorrendről és az újraküldésről, ezért megbízhatóbb, cserébe nagyobb a „többlet” (overhead). Tipikus TCP-s forgalom a **web (HTTP/HTTPS)**, az **SSH**, az **RDP**, az **IMAP**, stb.
Az **UDP** (User Datagram Protocol) **kapcsolat nélküli**: nem épít fel klasszikus kapcsolatot, nem garantálja a sorrendet vagy az újraküldést, viszont gyors és kicsi az overhead. Tipikusan UDP-t használ a **DNS** (legtöbbször), az **NTP** és sok valós idejű kommunikáció; ahol a sebesség és egyszerűség fontosabb, mint a „minden csomag biztosan megérkezzen” logika.

A „felsőbb” rétegekben találhatók az alkalmazási protokollok. A **HTTP** a web alap protokollja, a **HTTPS** ennek titkosított változata, amely **TLS**-t (Transport Layer Security) használ a forgalom védelmére. A **DNS** (Domain Name System) a neveket (pl. domain neveket) fordítja le IP-címekre. A levelezésnél gyakori az **IMAP** (e-mail olvasás/szinkron a szerverrel) és a **SMTP** (e-mail küldés). Sok protokollnak van „S” végű változata (pl. **IMAPS**, **POP3S**), ami általában azt jelenti, hogy a kapcsolat **TLS-sel titkosított**.
A fájlmegosztásnál Windows-környezetben gyakori az **SMB**. Távoli elérésnél a **SSH** a korszerű, biztonságos megoldás; a **Telnet** ezzel szemben titkosítatlan, ezért éles adminisztrációra ma már kerülendő.

Ezek a fogalmak azért hasznosak, mert amikor egy eszközön portokat és kapcsolatokat látni (például `netstat` kimenetben), a portszámok és a protokollok együtt adják meg, hogy valójában „milyen jellegű” kommunikáció zajlik.

---

## **Tipikus portok (alapok, amikhez a `netstat`, telnet/portteszt is kapcsolódik)**

A **port** egy logikai „kapu” egy IP-címen belül: ugyanazon IP-n több szolgáltatás is futhat egyszerre, és a port jelzi, melyik szolgáltatás kapja a forgalmat. Hibakeresésnél és biztonsági szemmel is sokat számít, ha a tipikus portok ismerősek, mert gyorsan észrevehető, mi „normális” és mi gyanús.

Gyakori, jól ismert portok:

- **80/TCP** – **HTTP** (titkosítás nélküli web)

- **443/TCP** – **HTTPS** (titkosított web)

- **53/UDP** és **53/TCP** – **DNS** (UDP a tipikus, TCP pl. nagy válaszoknál/zone transfernél)

- **22/TCP** – **SSH** (biztonságos távoli terminál)

- **23/TCP** – **Telnet** (nem titkosított, ma már kerülendő admin célra)

- **3389/TCP** – **RDP** (Windows távoli asztal)

- **445/TCP** – **SMB** (Windows fájlmegosztás; vállalatban gyakori, internet felé erősen kockázatos)

- **139/TCP** – NetBIOS/SMB régebbi komponensek

- **25/TCP**, **587/TCP** – **SMTP** (mail küldés; 587 gyakran submission)

- **110/TCP**, **995/TCP** – **POP3 / POP3S**

- **143/TCP**, **993/TCP** – **IMAP / IMAPS**

- **123/UDP** – **NTP** (időszinkron)

- **67/UDP**, **68/UDP** – **DHCP** (szerver/kliens; helyi hálózaton)

- **161/UDP** – **SNMP** (menedzsment; gyakori hálózati eszközökön)

Megjegyzés: a portok ismerete azért hasznos, mert például a **`netstat -ano`** kimenetében a portszámok alapján gyorsan lehet következtetni arra, milyen jellegű forgalom fut, illetve egy **telnetes porttesztnél** is ezek a klasszikus célpontok merülnek fel (például 443 elérhető-e).

---

## **`ipconfig`** – IP-konfigurációk megtekintése és bizonyos hálózati állapotok frissítése (Windows)

Az **`ipconfig`** parancs elsődleges célja a helyi hálózati beállítások gyors áttekintése. Ezzel ellenőrizhető, hogy egy adott hálózati adapter (vezetékes kártya, Wi-Fi, VPN adapter) milyen **IP-címet** kapott, milyen alhálózati maszkot használ, mi az **alapértelmezett átjáró** (default gateway), és mely **DNS szervereket** állított be a rendszer. Ezek az adatok kulcsfontosságúak, mert az internetkapcsolati hibák jelentős részénél már itt látszik az ok (például nincs gateway, rossz a DNS, vagy a gép nem kapott címet a **DHCP**-től).

A legegyszerűbb használat az `ipconfig`, amely rövid összefoglalót ad. Hibakereséshez még hasznosabb az **`ipconfig /all`**, mert részletesen megjeleníti többek között a DHCP használatát, a bérlet (**lease**) idejét, a DNS-suffixeket, a **MAC-címet**, és az adapterek állapotát. Tipikus jelenség, ha a rendszer a **169.254.x.x** tartományból kap címet (**APIPA**): ez gyakran arra utal, hogy a kliens nem érte el a DHCP-szervert, ezért automatikus „vész-IP-t” állított be. Ilyenkor a hiba oka lehet például Wi-Fi csatlakozási probléma, rossz jelszó, hibás kábel, rosszul működő router, vagy VLAN/switch oldal.

Az **`ipconfig`** nem csak megtekintésre szolgál. Az **`ipconfig /release`** és **`ipconfig /renew`** a DHCP-s cím elengedésére és újrakérésére használható, ami sokszor gyors megoldás, ha a kliens „beragadt” egy rossz bérletbe. Az **`ipconfig /flushdns`** a **DNS kliens gyorsítótárát** üríti, ami akkor lehet hasznos, ha korábban rossz címre oldotta fel a rendszer a nevet, vagy a DNS rekord időközben megváltozott. Az **`ipconfig /displaydns`** pedig megmutatja, milyen rekordokat tárol jelenleg a helyi **DNS cache**.

**Gyakorlati példa:** ha egy weboldal nem érhető el, az **`ipconfig /all`** alapján látható, hogy az **átjáró** hiányzik-e, a **DNS szerver** „szokatlan”-e (például talán egy VPN-é), vagy a gép valójában nem is kapott érvényes IP-t.

---

## **`ping`** – elérhetőség és késleltetés vizsgálata (ICMP)

A **`ping`** az egyik legalapvetőbb hálózati diagnosztikai eszköz. A lényege, hogy a cél felé **ICMP Echo Request** csomagokat küld, és méri, érkezik-e válasz (**Echo Reply**), illetve mennyi idő alatt. Ezzel gyorsan megállapítható, hogy a kommunikáció létrejön-e legalább hálózati szinten, és hogy a **késleltetés** (latency) milyen.

A `ping 8.8.8.8` jellegű teszt jó indikátor lehet arra, hogy van-e „internet **IP-szinten**” (hiszen itt nincs DNS, csak IP). A `ping google.com` már a **DNS-t** is bevonja, ezért ha az IP-címes ping működik, de a névvel nem, akkor erős a gyanú **DNS-problémára**. Fontos ugyanakkor, hogy a ping eredménye nem mindig döntő: sok szerver és hálózati eszköz biztonsági okból blokkolhatja az **ICMP-t**, vagy csak korlátozhatja a válaszadást. Emiatt a „Request timed out” nem mindig jelenti azt, hogy a cél nem érhető el, csak azt, hogy pingre nem válaszol.

Windows alatt gyakori opciók: a `-n` paraméterrel megadható a csomagok száma (például `ping -n 10 8.8.8.8`), a `-t` pedig folyamatos pinget indít megszakításig. IPv4/IPv6 teszthez használható a `-4` vagy `-6`. Hibakeresésben különösen figyelemre méltó, ha **csomagvesztés** tapasztalható, vagy a késleltetés erősen ingadozik (**jitter**), mert ez gyakran Wi-Fi interferenciára, torlódásra, rossz jelminőségre vagy útvonalproblémára utal.

---

## **`tracert`** és **`pathping`** – útvonal és hibapont azonosítása

A **`tracert`** (traceroute) arra szolgál, hogy megmutassa, milyen útvonalon jut el a forgalom a célig, vagy legalábbis milyen hálózati „ugrásokon” (**hopokon**) halad keresztül. Ennek alapja, hogy a csomagok **TTL** (Time To Live) értékét fokozatosan növeli, és figyeli, mely útválasztók „jelzik vissza”, hogy náluk járt a csomag. A parancs eredménye hoponként tipikusan több mért késleltetést mutat, így látszik, hol nő meg hirtelen a válaszidő, vagy hol szűnik meg a válaszadás.

A csillagok (`* * *`) gyakran azt jelentik, hogy az adott hop nem válaszol a traceroute jellegű kérdésre (ICMP Time Exceeded / válasz korlátozása). Ez önmagában nem mindig probléma; ha későbbi hopok megjelennek, akkor az útvonal tovább működik, csak a köztes eszköz nem „beszédes”.

A **`pathping`** ezzel szemben egyfajta kombinált eszköz: a traceroute jellegű útvonal-feltérképezés után több mérést végez, és képes statisztikát adni arról, hogy hol jelentkezik **csomagvesztés**. Ez különösen akkor értékes, ha a kapcsolat „szakad”, de nem egyértelmű, hogy helyi Wi-Fi gond, szolgáltatói probléma vagy távoli hálózati torlódás okozza. A **`pathping`** lassabb, mert sok mintát gyűjt, viszont cserébe jobban megmutathatja, melyik hop környékén romlik el a minőség.

---

## **`nslookup`** – DNS névfeloldás ellenőrzése és rekordok lekérdezése

A **`nslookup`** a **DNS** hibakeresés egyik klasszikus eszköze: segítségével ellenőrizhető, hogy egy domain névhez milyen IP-cím(ek) tartoznak, és hogy mely **DNS szerver** adja a választ. Ez azért fontos, mert sok „nincs internet” jellegű hiba valójában DNS-hiba: a gép maga képes lenne elérni IP-címeket, de nem tudja feloldani a neveket.

Az egyszerű `nslookup google.com` megmutatja a választ és gyakran az aktuálisan használt DNS szervert is. Ha a cél az, hogy összehasonlítás készüljön egy másik DNS-szel, akkor megadható konkrét szerver is, például `nslookup google.com 8.8.8.8`. Ezzel gyorsan kiderülhet, hogy a helyi DNS (például a router) hibázik-e, vagy a probléma az internetszolgáltatói DNS környékén van.

Az `nslookup` interaktív módban is használható, ahol beállítható a **rekordtípus**. Például `set type=mx` után egy domain megadásával a levelezési rekordok (**MX**) kérdezhetők le, `set type=txt` esetén pedig **TXT rekordok**. Tipikus hibaüzenet a „DNS request timed out”, ami utalhat DNS szerver elérhetetlenségre, tűzfalra, rossz VPN-re, vagy egyszerű hálózati kapcsolat hibára.

---

## **`netstat`** – hálózati kapcsolatok, hallgatózó portok, PID-ek

A **`netstat`** célja, hogy láthatóvá tegye a gép hálózati állapotát: milyen **TCP/UDP** kapcsolatok aktívak, mely portokon hallgat a rendszer (**LISTENING**), és milyen távoli címekkel van épp kapcsolatban. Üzemeltetésben jól használható például annak kiderítésére, miért nem indul egy szolgáltatás (mert egy portot már foglal valami), vagy hogy egy alkalmazás valóban kapcsolódik-e a várható célhoz. Biztonsági szemmel (SOC/IR) pedig segíthet kiszúrni gyanús kimenő kapcsolatokat, illetve váratlanul nyitott hallgató portokat.

A leggyakoribb kombináció a **`netstat -ano`**, mert ez numerikusan listáz (`-n`), minden kapcsolatot megmutat (`-a`), és kiírja a folyamat azonosítóját (**PID**) (`-o`). Ezzel a PID-del már könnyen beazonosítható a folyamat, például a `tasklist /fi "PID eq 1234"` paranccsal. A **`netstat -ab`** még beszédesebb lehet, mert megpróbálja a folyamat nevét/komponensét is mutatni, de ehhez gyakran **admin jogosultság** szükséges.

Fontos értelmezés, hogy az, ha sok kapcsolat látható, önmagában nem gyanús: böngésző, chat kliens, felhőszinkron, rendszerfolyamatok mind tarthatnak fenn több kapcsolatot. A problémásabb mintázat inkább az, ha ismeretlen folyamat ismeretlen külső IP-khez kapcsolódik szokatlan portokon, vagy ha indokolatlanul sok hallgatózó port jelenik meg.

---

## **`ssh`** és **`telnet`** – távoli elérés és portteszt (eltérő biztonsági szinttel)

Az **SSH** (Secure Shell) ma a biztonságos távoli parancssori elérés alapja. **Titkosított csatornát** biztosít, így a hitelesítés és a forgalom nem olvasható le egyszerűen hálózati lehallgatással. Az SSH-t tipikusan Linux/Unix szerverek, hálózati eszközök (switch, router), felhős VM-ek menedzsmentjére használják. Windows 10/11 környezetben gyakran elérhető az **`ssh`** kliens, így például `ssh felhasznalo@192.168.1.10` vagy `ssh -p 2222 felhasznalo@szerver.domain` formában lehet csatlakozni. Haladóbb környezetben jellemző a **kulcsalapú hitelesítés**, ami biztonságosabb, mint a puszta jelszó.

A **telnet** ezzel szemben történelmileg távoli terminál-protokoll, amely **nem titkosítja** a kommunikációt, ezért éles rendszerek adminisztrációjára ma már nem tekinthető biztonságosnak. Ugyanakkor a telnetnek van egy gyakorlati szerepe: egyszerű **TCP port-tesztként**. Ilyenkor például `telnet example.com 80` jelleggel ellenőrizhető, hogy a TCP kapcsolat létrejön-e egy adott portra. Windows alatt a telnet kliens sokszor külön Windows-szolgáltatásként engedélyezhető.

---

## **`arp -a`** – ARP-tábla megtekintése (ki „kicsoda” a helyi hálózaton)

Az **`arp -a`** parancs a gép **ARP-tábláját** (Address Resolution Protocol cache) listázza. Az ARP az a mechanizmus, amellyel az eszköz a **helyi hálózaton (LAN-on)** megtudja, hogy egy adott **IPv4-címhez** melyik **MAC-cím** (fizikai hálózati cím) tartozik. Erre azért van szükség, mert a helyi szegmensen a tényleges kézbesítés Ethernet/Wi-Fi szinten MAC-címekkel történik, miközben az alkalmazások IP-címekkel „gondolkodnak”. A Windows a feloldás eredményét egy ideig **cache-eli**, és ezt a gyorsítótárat látod `arp -a` kimenetben.

A parancs tipikusan több blokkot is mutathat, például adapterenként (vezetékes, Wi-Fi, VPN). A kimenetben általában látszik az **Interface** (a helyi IP, amelyhez a tábla tartozik), majd soronként a **Internet Address** (a cél IPv4), a **Physical Address** (MAC) és a **Type** (dinamikus/statikus). A **dynamic** bejegyzések tipikusan automatikusan kerülnek be (például amikor pingelsz egy belső címet vagy a gateway-t), míg a **static** ritkább, tudatos konfiguráció eredménye.

**Mire jó hibakeresésnél?**

* **LAN-elérés ellenőrzése:** ha például a gateway-t pingelve nincs válasz, `arp -a` segítségével látható, hogy legalább ARP szinten feloldódik-e a gateway IP-je (van-e hozzá MAC).
* **IP-ütközés / furcsa viselkedés gyanúja:** ha egy belső IP-hez „változó” vagy váratlan MAC-cím tartozik, az utalhat **IP-konfliktra** vagy hálózati anomáliára.
* **Alapszintű biztonsági indikáció:** ARP-szinten láthatóak a helyi eszközök lenyomatai; gyanús lehet, ha például a gateway IP-je mögött hirtelen más MAC jelenik meg (ez akár **ARP spoofing/MITM** gyanút is felvethet, bár önmagában még nem bizonyíték).

**Gyakorlati használat / tippek:**

* Friss ARP-bejegyzés „kikényszerítése”: futtass egy pinget egy belső címre (pl. `ping 192.168.1.1`), majd nézd meg újra az `arp -a` kimenetet.
* Ha nagyon „összekavarodott” a kép, az ARP-cache üríthető is: **`arp -d *`** (ehhez gyakran admin jog kell). Ezután a következő forgalom újra fel fogja építeni a táblát.

**Fontos megjegyzések:**

* Az **ARP csak IPv4-re** vonatkozik; IPv6 esetén a megfelelő mechanizmus a **Neighbor Discovery (NDP)** (Windowsban pl. `netsh interface ipv6 show neighbors` / PowerShell megfelelő parancsok).
* Az ARP-tábla **pillanatkép jellegű**: dinamikus bejegyzések idővel eltűnhetnek, és az is normális, ha csak azok az IP-k látszanak, amelyekkel a gép nemrég kommunikált.

**Gyakorlati példa:** ha „van Wi-Fi, de nincs net” jellegű hibánál a `ipconfig` szerint van IP és gateway, de a `ping <gateway>` nem megy, akkor `arp -a` megmutathatja, hogy a gateway IP-je feloldódik-e MAC-re. Ha **nincs** bejegyzés vagy nem épül fel, az gyakran **helyi L2/Wi-Fi/VLAN** jellegű problémára utal.

---

## **`route print`** – útvonalválasztási tábla (routing) megtekintése Windows alatt

A **`route print`** parancs a Windows **útvonalválasztási tábláját** listázza: megmutatja, hogy a gép a különböző célhálózatok felé **melyik átjárót (gateway-t)** és **melyik hálózati interfészt** használja, illetve milyen **prioritással (metric)**. Ez akkor különösen hasznos, ha a kapcsolat „látszólag rendben van” (van IP, van DNS), mégis bizonyos célok nem elérhetők, vagy több aktív adapter (Wi-Fi + Ethernet + VPN) miatt nem egyértelmű, merre megy ki a forgalom.

**Mire jó hibakeresésnél?**

- **Default route ellenőrzése:** a `0.0.0.0 / 0.0.0.0` bejegyzés mutatja az alapértelmezett útvonalat. Ha ez rossz gateway-re vagy nem várt interfészre mutat, az magyarázhat “van net néha / nincs net / csak VPN-en megy” jellegű hibákat.

- **Célhálózatra illeszkedő útvonal keresése:** ha például egy belső hálózatot nem érsz el (pl. `10.x` vagy `192.168.x`), a táblában látható, hogy van-e hozzá specifikus route, és az hová mutat.

- **Metric és preferencia:** ha több útvonal is “passzol” egy célra, a Windows a **konkrétabb prefixet**, majd a **kisebb metricet** részesíti előnyben – emiatt VPN vagy más adapter könnyen “elviheti” a forgalmat.

- **Persistent routes felismerése:** a **Persistent Routes** részben lévő bejegyzések kézzel felvitt, tartós útvonalak, amelyek váratlan viselkedést okozhatnak.

**Gyakorlati tipp:** ha nem egyértelmű, melyik útvonal érvényes egy konkrét cél IP-re, a `route print` kimenete alapján gyorsan látszik, hogy a gép **melyik hálózati irányba** próbálja küldeni a csomagokat.

---

## **PuTTY** – Windowsos távoli terminál kliensként

A **PuTTY** egy régóta népszerű Windowsos kliens, amelyet főként **SSH** kapcsolatokhoz használnak, de támogat **telnetet** és **soros** (serial/COM) kapcsolatot is. Gyakorlati értéke abban van, hogy egyszerűen kezelhető, könnyen menthetők benne a munkamenetek (**session**), így több szerverhez vagy hálózati eszközhöz gyorsan lehet csatlakozni azonos beállításokkal. A PuTTY első csatlakozáskor figyelmeztet a szerver **host key**-ére; ez biztonsági szempontból fontos, mert segít észrevenni, ha a célrendszer megváltozott, vagy ha „közbeékelődéses” (**MITM**) helyzet gyanúja áll fenn.

A PuTTY környezetében gyakori kiegészítő a **PuTTYgen**, amely kulcspárok generálására szolgál. Ezzel a PuTTY-hoz illeszkedő kulcsformátumok is kezelhetők, és **kulcsalapú SSH hitelesítés** állítható be. Hálózati eszközök első konfigurálásánál a PuTTY **serial módja** is kifejezetten hasznos, amikor konzolkábelen keresztül kell hozzáférni a készülékhez.

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