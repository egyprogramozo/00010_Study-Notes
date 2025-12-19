# RAID dokumentáció – típusok, tervezés, üzemeltetés, kockázatok és kiberbiztonsági összefüggések

A RAID (Redundant Array of Independent Disks) több fizikai lemezt egy logikai tárolóegységgé szervez.

**Források és felhasznált eszközök:**

- [Training360](https://www.training360.com/), [IT Essentials - 03 - Szerverek telepítése és konfigurálása](https://e-learning.training360.com/courses/3it-essentials)

- [ChatGPT](https://chatgpt.com/), [DeepSeek](https://www.deepseek.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

## 1. Bevezetés: mire való a RAID, és mire nem

A RAID lényegében egy tárolóoldali “üzemfolytonossági” réteg: csökkenti annak az esélyét, hogy egyetlen lemezhibától azonnal megálljon a rendszer vagy elérhetetlenné váljanak az adatok.

A RAID megoldásokat általában három cél valamelyikéért (vagy kombinációjáért) használjuk:

- **teljesítmény** (párhuzamos olvasás/írás),

- **rendelkezésre állás** (lemezkiesés túlélése),

- illetve **kapacitáskezelés** (egy nagy kötetként használható tárterület).

Fontos tisztázni, hogy a RAID nem adatmentés. A RAID tipikusan **hardverhibák** (különösen lemezhiba) ellen segít, de **nem véd** a logikai események ellen: véletlen törlés, felülírás, fájlrendszer-korrupció, hibás admin művelet, jogosultsági hiba, és különösen **ransomware** esetén a RAID gyakran ugyanazzal a lendülettel teríti szét a problémát, ahogy a normál adatot. Emiatt a RAID-et úgy érdemes felfogni, mint egy réteget a “folyamatos működéshez”, ami fölé kötelezően kell egy **snapshot/backup/immutábilis mentés** stratégia.

## 2. Alapelvek: striping, mirroring, paritás – mit jelent ez a gyakorlatban?

A RAID-ek nagy része három építőkockából rakható össze.

- A **striping** (csíkozás) azt jelenti, hogy az adat blokkokra bontva több lemezre kerül; így a rendszer párhuzamosan tud dolgozni a lemezekkel, ami jelentős teljesítménynövekedést adhat. A striping önmagában nem redundáns: ha bármelyik lemez kiesik, a csíkozott adat “darabokra törik”.

- A **mirroring** (tükrözés) ezzel szemben redundanciát ad: ugyanaz az adat több lemezen is megvan, így egy lemezhiba esetén a rendszer tovább tud működni, mert a másik lemezről olvas. A teljesítmény jellemzően olvasásnál javulhat, írásnál inkább a vezérlő/implementáció dönt.

- A **paritás** (parity) a striping mellé egy olyan többletinformációt ad, amiből lemezhiba esetén az elveszett adat visszaszámolható. Ez kapacitásban hatékonyabb, mint a tükör, de írási műveleteknél tipikusan többletterhelést okoz (paritásszámítás, extra írások).

Üzemeltetési szempontból a RAID-eknél két állapot kulcsfontosságú.

- A **degraded** állapot azt jelzi, hogy a tömb még működik, de egy lemez kiesett, a redundancia csökkent, a teljesítmény sokszor romlik, és nő a kockázat.

- A **rebuild** pedig az a folyamat, amikor cserelemez behelyezése után a rendszer visszaépíti az adatot (tükörből másol, vagy paritásból számol). A rebuild időszaka tipikusan a legkritikusabb: a megmaradt lemezek intenzív terhelést kapnak, és ha ilyenkor jön egy második hiba, bizonyos RAID szinteknél adatvesztés lehet a vége.

## 3. RAID szintek: mit kapsz, mit fizetsz érte, és mikor érdemes

### RAID 0 – striping (sebesség, redundancia nélkül)

A RAID 0 két vagy több lemezt csíkoz össze.

Előnye, hogy jelentős teljesítménynövekedést adhat és a teljes kapacitás kihasználható.  Hátránya, hogy **nincs redundancia**: egyetlen lemezhiba esetén adatvesztés következhet be, a tömb pedig használhatatlanná válhat.

Dokumentációs nyelven ezt úgy érdemes rögzíteni, hogy RAID 0 csak olyan adatra való, amely **pótolható**, vagy amelyről külön, megbízható mentési/újragenerálási folyamat van.

Tipikus “jó” felhasználási eset a scratch/cache, videós vágóanyag átmeneti tárolása, build output, ideiglenes lab-adat.

### RAID 1 – mirroring (egyszerű és stabil)

A RAID 1 lényege, hogy ugyanaz az adat párhuzamosan, két lemezre kerül rögzítésre.

A rendelkezésre állás szempontjából nagyon erős és könnyen érthető: egy lemez kiesését tipikusan gond nélkül túléli. A kapacitás ára az, hogy a nettó kapacitás egy párnál a kisebb lemez mérete lesz (tehát nagyjából “felezés”).

Kiberbiztonsági és adatbiztonsági oldalról fontos kimondani: a tükör **minden logikai hibát is tükröz** (törlés, titkosítás, korrupció), tehát RAID 1 mellé ugyanúgy kell snapshot/backup.

Gyakorlati ajánlás: OS/boot meghajtónak vagy kritikus, kisebb adatnak tipikusan kiváló.

### RAID 5 – striping + 1 paritás (kapacitáshatékony, de érzékenyebb)

A RAID 5 legalább három lemezt igényel, és egy lemez kiesését képes túlélni.

Sokáig “arany középút” volt, mert jól használja a kapacitást, és olvasásban erős lehet. Az üzemeltetési valóság azonban az, hogy modern, nagy kapacitású HDD-knél a rebuild nagyon hosszú lehet, és a rebuild alatti terhelés növeli a másodlagos hiba kockázatát. Írásban paritás miatt jellemző a büntetés, különösen kis, random írásoknál.

Ha RAID 5-öt választasz, azt érdemes a dokumentációban “olvasásorientált, mérsékelt írású terhelésekre” és megfelelő monitoring/mentés mellett ajánlani, illetve jelezni, hogy nagy diszkek és soklemezű tömbök esetén gyakran RAID6/RAID10 a konzervatívabb döntés.

### RAID 6 – striping + 2 paritás (biztonságosabb nagy tömbökhöz)

A RAID 6 legalább négy lemezt igényel, és **két lemez** kiesését is túléli.

Ez különösen fontos nagy kapacitású lemezeknél, ahol a rebuild hossza és a “második hiba” kockázata a mindennapi üzemeltetés része. Az ára a nagyobb paritás overhead, ami írási teljesítményben jobban látszik, mint RAID 5-nél.

Tipikus helye NAS és nagy fájltároló rendszerek, ahol fontos a tárhelyhatékonyság és a “két hiba túlélése” reális követelmény.

### RAID 10 – mirror + stripe (teljesítmény és rendelkezésre állás együtt)

A RAID 10 (1+0) legalább négy lemezt igényel, párokban tükröz, majd a párok között csíkoz.

Ez gyakorlatban az egyik legjobb kompromisszum: nagyon jó random I/O teljesítmény, és a rebuild általában gyorsabb/kevésbé kockázatos, mert tükrökből másol, nem paritásból számol. A nettó kapacitás ára itt is kb. 50%.

Kiberbiztonsági/SOC jellegű környezetekben, ahol sok írás és keresés van (loggyűjtés, indexelés, VM-ek, adatbázisok), a RAID10 gyakran egy biztonságos alapértelmezett választás a kapacitáscsökkenés vállalása mellett.

A RAID 10 hibatűrése erősen függ a kiesések eloszlásától. Elméletileg akár a lemezek feléig is kieshetnek adatvesztés nélkül, **feltéve, hogy a kiesett lemezek mind különböző tükörpárokból származnak.** A legrosszabb esetben viszont, ha egy tükörpár mindkét tagja meghibásodik, a tömb adatvesztéssel összeomlik (ez tipikusan akkor történik meg, ha egy lemezhiba után a következő kiesés ugyanannak a tükörpárnak a másik lemezét érinti). Emiatt a RAID 10 gyakorlati hibatűrése 1 és N/2 lemez között változhat, a hibák eloszlásától függően.

### RAID 50 / RAID 60 – csoportos paritás, jobb skálázás

Ezek több RAID5/RAID6 csoport összecsíkozásai.

A cél nagy rendszereknél a teljesítmény és a rebuild-kockázat ésszerűbb elosztása. Cserébe a tervezés bonyolultabb: nem mindegy, hány lemez van egy al-csoportban, és milyen kiesési mintákat akarsz túlélni.

Tipikusan vállalati tárolóknál vagy nagy NAS rendszereknél jön elő.

### JBOD / SPAN – “nem RAID”, de gyakori

JBOD-nál a lemezek külön-külön látszanak, SPAN-nál össze vannak fűzve egy kötetbe.

Redundancia nincs, ezért csak akkor jó döntés, ha a fölérendelt adatvédelmi stratégia (backup, replikáció, objektumtár) ezt tudatosan kezeli.

## 4. Gyors összehasonlítás (döntéstámogatás)

| Szint   | Minimum lemez | Túlélhető lemezhiba | Nettó kapacitás | Tipikus erősség     | Tipikus gyengeség                           |
| ------- | ------------- | ------------------- | --------------- | ------------------- | ------------------------------------------- |
| RAID 0  | 2             | 0                   | N*              | sebesség            | nincs redundancia (lemezhiba = adatvesztés) |
| RAID 1  | 2             | 1                   | ~50%            | egyszerű, stabil    | “mindent tükröz” (hibát is)                 |
| RAID 5  | 3             | 1                   | (N−1)           | jó kapacitás        | paritás-írás büntetés, rebuild kockázat     |
| RAID 6  | 4             | 2                   | (N−2)           | nagy tömb biztonság | írásban még drágább                         |
| RAID 10 | 4             | 1–N/2**             | ~50%            | VM/DB/log I/O       | kapacitás “drága”                           |

*N = a lemezek száma a tömbben.

**RAID10-ben a túlélhető lemezhibák száma attól függ, hogy a kiesések különböző tükörpárokat érintenek-e; egy tükörpár mindkét lemezének kiesése adatvesztést okoz (legrosszabb esetben akkor, ha a következő kiesés ugyanannak a tükörpárnak a másik lemezét érinti).

## 5. Megvalósítási módok: hardver RAID, szoftver RAID, “alaplapi RAID”

A RAID kiválasztásakor nem csak a RAID-szint a döntési szempont, hanem az is, hogy **hol és hogyan** valósul meg a megoldás.

### Hardver RAID

Hardver RAID esetén külön vezérlő (RAID HBA/controller) kezeli a tömböt, sokszor saját cache-sel és fejlettebb menedzsmenttel.

Előnye lehet a stabilitás, az akkumulátoros/flash-es write cache (áramkimaradásnál kritikus), és a kiforrott riasztási/karbantartási funkciók.

Hátrányként dokumentálni kell a vendor lock-in jelenséget: vezérlőhiba esetén olykor azonos vagy kompatibilis vezérlő szükséges a visszaállításhoz, illetve a “fekete doboz” jelleg miatt könnyebb elsiklani korai jelek felett, ha nincs jó monitoring.

Hardver RAID esetén külön kockázat, hogy maga a RAID vezérlő is meghibásodhat, és bizonyos megoldásoknál ez single point of failure-t jelenthet: ha a vezérlő kiesik, a tömb átmenetileg elérhetetlenné válhat, illetve helyreállításhoz gyakran azonos vagy kompatibilis vezérlő szükséges. Emiatt kritikus a RAID konfiguráció (és firmware/driver verziók) dokumentálása és biztonsági mentése, valamint egy kompatibilis tartalék vezérlő (vagy előre definiált beszerzési/DR eljárás) rendelkezésre állása, hogy egy vezérlőhiba ne okozzon aránytalanul hosszú kiesést.

### Szoftver RAID

Szoftver RAID esetén az operációs rendszer vagy a fájlrendszer végzi a redundancia logikát. Linuxon klasszikus az mdadm, Windows környezetben Storage Spaces, haladó tárolóknál pedig ZFS/RAIDZ.

Ennek előnye a rugalmasság és az átláthatóság, illetve bizonyos rendszereknél (pl. ZFS) erős integrált adatvédelem (checksum, scrub) a “csendes korrupció” ellen.

Hátránya lehet a nagyobb erőforrásigény és az, hogy implementáció-függően változik a teljesítmény és a feature-készlet.

### Alaplapi RAID

Az alaplapi RAID (sokszor “fakeRAID”) a kettő között van: BIOS/UEFI felületen konfigurálod, de a driver és az OS sokat számít. Otthon lehet kényelmes, de kritikus helyen dokumentáld a hordozhatósági kockázatokat: költöztetésnél, recovery-nél kellemetlen meglepetéseket adhat.

## 6. SSD/NVMe sajátosságok RAID-ben (amire érdemes külön figyelni)

SSD-k és NVMe-meghajtók esetén a RAID megválasztásánál több, elsőre nem nyilvánvaló tényezőt is figyelembe kell venni.

- TRIM/UNMAP átadás (pass-through): ha a RAID réteg nem adja át jól, hosszabb távon romolhat a teljesítmény és nőhet a write amplification.

- Paritásos RAID (5/6) SSD-n sokszor működik, de kis random írásoknál a paritás overhead és az SSD belső menedzsmentje együtt kellemetlen teljesítményprofilt adhat. Nagy I/O igényű, vegyes terhelésekre SSD-vel gyakran a RAID10 vagy szoftveres mirror jellegű megoldás hálásabb.

- NVMe-nél a “sok kis gyors lemezből építsünk egy nagyot” gondolat csábító, de a hibakezelés és a hosszú távú viselkedés miatt gyakran jobb a célterhelésre optimalizált, rétegezett tárolás (külön OS, külön adat, külön log/scratch), és fölötte korrekt snapshot/backup.

## 7. A legnagyobb kockázat: rebuild időszak és másodlagos hibák

RAID5/6 esetén a rebuild nem csak egy “várjunk kicsit” folyamat. A rebuild alatt a megmaradt lemezek folyamatosan olvasnak (és a rendszer paritást számol/ír), ami megnöveli a terhelést és felhozza a felszínre a rejtett hibákat.

Minél nagyobbak a lemezek és minél több lemezből áll a tömb, annál tovább tart, és annál inkább valós kockázat a második hiba. Ez az oka annak, hogy modern nagy diszkek mellett a RAID6 vagy RAID10 gyakran konzervatívabb választás, még ha papíron a RAID5 “elégnek tűnik” is.

Fontos kiemelni, hogy a rebuild általánosan is kritikus időszak bármely RAID szintnél: RAID1/10 esetén ugyan nem paritásból történik a visszaépítés, hanem tükörből másolás, de a megmaradt lemezek terhelése és a csökkent redundancia miatt a rendszer ilyenkor is sérülékenyebb, ezért a monitoring és a gyors beavatkozás kulcsfontosságú.

## 8. “Silent corruption” és fájlrendszer-szintű védelem

A RAID önmagában nem minden esetben védi ki a csendes bit-hibákat (amikor egy blokk tartalma megváltozik anélkül, hogy klasszikus lemezhibát látnál).

Itt a fájlrendszer szerepe a kulcs: olyan rendszerek, amelyek **checksumot** tárolnak és rendszeresen **scrub**-olnak (ellenőriznek), képesek a redundanciából korrigálni a hibát, és nem csak “továbbvinni” a sérült adatot.

Ez adatbiztonsági szemszögből fontos különbség: a redundancia és az integritás nem ugyanaz.

## 9. Kiberbiztonsági nézőpont: RAID mint rendelkezésre állás, és mi kell mellé

Kiberbiztonsági szempontból a RAID elsődlegesen a **hardveres meghibásodás miatti kiesés** ellen véd, és ezzel csökkenti a szolgáltatáskimaradás kockázatát. Ugyanakkor a modern fenyegetések többsége logikai jellegű: ransomware, credential kompromittáció, szándékos törlés, adatmanipuláció. Ezek ellen a RAID nem véd, sőt néha gyorsítja a káreseményt (gyors storage → gyors titkosítás). Ezért egy korrekt “RAID + adatvédelem” dokumentációban a RAID mellé kötelezően oda kell tenni a következő elvet: a mentésnek és a visszaállításnak ellenállónak kell lennie támadás esetén is.

Gyakorlati megfogalmazásban ez általában **3-2-1** jellegű mentést jelent, kiegészítve **immutábilis** vagy legalábbis erősen védett (külön hitelesítés, külön admin domain, write-once policy) réteggel. Snapshot jó, de ha a támadó storage admin jogot szerez, a snapshot is törölhető; ezért kell offsite/immutábilis komponens.

SOC/monitorozási oldalról a RAID események (degraded, rebuild, SMART trendek, media error, CRC error) nagyon jó korai indikátorok. Ezeket érdemes logolni és riasztani, mert egy “lassan romló” tömbből nagyon gyorsan lehet incidens, ha a második hiba rosszkor jön.

## 10. Jó üzemeltetési gyakorlat

A RAID rendszert nem elég “egyszer beállítani”. Üzemeltetési minimum, hogy legyen riasztás a degraded állapotra, legyen látható a rebuild állapota, és legyen rendszeres egészségellenőrzés. A tárolók világában fontos a periodikus ellenőrzés (scrub/patrol read), mert ez időben előhozza a rejtett hibákat, nem a rebuild közepén.

Áramellátásnál egy UPS nem “kényelmi extra”: írás közbeni áramvesztés korrupciót és hosszas helyreállítást okozhat. Hardver RAID-nél a write cache védelme (BBU/CacheVault) különösen kritikus, mert nélküle vagy kockázatosabb a gyors cache, vagy kénytelen vagy letiltani és bukod a teljesítményt.

Végül: a mentés csak akkor ér valamit, ha vissza is tudod állítani. Dokumentációs minimum egy rendszeres restore teszt (akár csak mintafájlokkal), és annak rögzítése, hogy egy RAID-kiesés vagy tömbcsere esetén pontosan mi a recovery eljárás.

## 11. Monitoring és riasztás – konkrét metrikák és jelzések

Egy RAID/tárolórendszer üzemeltetésében a monitoring célja nem csak az, hogy “észrevegyük, ha baj van”, hanem hogy **minél korábban lássuk a trendet** (romló lemez, növekvő hibaszámok, hőmérsékleti gondok), és még azelőtt tudjunk beavatkozni, hogy a tömb degradált állapotba kerülne vagy rebuild közben kényszerhelyzet alakulna ki. A riasztások beállításánál érdemes külön kezelni a **hardver (SMART)**, a **RAID-vezérlő / tömbállapot**, valamint a **fájlrendszer (scrub/checksum)** jelzéseit, mert ezek más típusú hibákat fognak meg.

A **SMART attribútumok** a fizikai lemez állapotáról adnak korai indikációkat. Kiemelten figyelendők:

- a **reallocated sector count** (átmozgatott/áthelyezett szektorok, a lemez romlásának erős jele),

- a **pending sectors** (olvasási problémás, “várakozó” szektorok, rebuildnél különösen veszélyes),

- az **uncorrectable errors** (nem javítható hibák),

- valamint a **temperature** (tartósan magas hőmérséklet gyorsíthatja a meghibásodást és hibák számát).

A SMART értékeknél önmagában a küszöbérték is számít, de a gyakorlatban sokszor még fontosabb a **trend**: ha egy számláló növekedésnek indul, azt érdemes azonnal komolyan venni.

A **RAID-specifikus metrikák** már közvetlenül a tömb állapotát jelzik. Kritikus riasztási esemény a **degraded állapot**, a **rebuild megindulása**, illetve a rebuild “elakadása” vagy hibával megállása. Hasznos operatív mutató a **rebuild progress (%)**, mert ebből látszik, mennyi ideig maradunk kockázati ablakban. Ugyanígy érdemes figyelni a **media errors** jellegű hibákat (vezérlő által jelentett lemez/olvasási/írási hibák), valamint a **patrol read / scrub állapotát és eredményét**, mivel ezek hozzák felszínre a rejtett hibákat még akkor, amikor a tömb látszólag egészséges.

Ha a tárolóoldalon checksumos fájlrendszer vagy tárolóréteg fut (például ZFS), akkor a **scrub futásának státusza** és a scrub által talált/javított hibák száma külön riasztási kategóriát érdemel. ZFS esetén például a **zpool status** kimenet, illetve a scrub eredményei (talált checksum hibák, javítások) közvetlenül jelzik az integritási problémákat, amelyeket a klasszikus RAID önmagában nem mindig fog fel.

Eszközoldalon Linuxon tipikus alap a **smartd** (SMART figyelés és riasztás), kiegészítve a RAID-vezérlő vagy tároló gyártói eszközeivel. Gyakori vállalati példák: **Dell OMSA**, **HP SSACLI**, illetve más vendor tooling a tömbállapot, rebuild és vezérlőhibák lekérdezésére. Környezetfüggően nagyon hatékony megoldás az **SNMP** és a **trap-ek** használata, mert így a tároló a monitoring rendszer felé aktívan tud riasztást küldeni (nem csak “lekérdezésre” vár). ZFS rendszereknél a rendszeres **zpool status** ellenőrzés és a scrub ütemezése a minimum, mert ez ad integritás-szintű visszajelzést a tárolt adatról.

## 12. Gyakorlati ajánlások tipikus célokra (röviden, de konkrétan)

Ha egy PC/munkaállomás esetén a cél az, hogy az OS és a mindennapi munka stabil legyen, a RAID1 jó alap OS-nek, és mellé külön mentés. Ha sok VM fut, sok a random I/O (lab, szerverjelleg), a RAID10 tipikusan “biztos választás”. Ha NAS jellegű, soklemezes nagy tárhely kell, a RAID6 gyakran jobb nyugalmat ad, mint a RAID5, különösen nagy diszkeknél.

## 13. RAID modern környezetekben (felhő, HCI)

A RAID fogalma modern környezetekben sem “tűnt el”, de a legtöbb esetben már nem úgy jelenik meg, hogy az üzemeltető explicit módon kiválaszt egy RAID-szintet és lemezekből tömböt épít. Felhőben és sok hiper-konvergens (HCI) architektúrában a redundanciát, teljesítményt és hibatűrést egy magasabb absztrakciós réteg biztosítja: a háttérben továbbra is létezhet lemezszintű redundancia, de a felhasználó jellemzően szolgáltatás-szintű döntéseket hoz (milyen típusú tárolót használ, milyen replikációs vagy tartóssági opcióval), és ezek “lefordulnak” a platform belső megvalósítására.

Felhős környezetben a tárolás tipikusan több kategóriára bomlik: blokk tár (volume), objektumtár és fájltár. A redundancia és a rendelkezésre állás sokszor a szolgáltatás alap része, és a platform a háttérben automatikusan kezeli a lemezhibákat, node-kieséseket, sőt akár teljes fizikai meghibásodásokat is. Ettől azonban nem szabad azt a következtetést levonni, hogy a “felhős redundancia” egyenlő az adatmentéssel. A szolgáltatói hibatűrés elsősorban a hardver- és infrastruktúra-hibák következményeit csökkenti (RTO jelleg), miközben a logikai események — véletlen törlés, felülírás, hibás automatizmus, jogosultsági tévedés, illetve ransomware vagy credential kompromittáció miatti rombolás — ugyanúgy képesek adatvesztést okozni. A gyakorlatban ez azt jelenti, hogy felhőben is külön rétegként kell kezelni a visszaállíthatóságot: verziózás, snapshot, elkülönített backup, illetve ahol lehetséges, immutábilis mentés bevezetése továbbra is alapkövetelmény.

Teljesítmény szempontból felhőben a “RAID-szint” helyett a tároló szolgáltatás profilja, illetve annak korlátai a meghatározók: késleltetés, IOPS, throughput, és a szolgáltató által megadott tartóssági/availability modell. A tervezésben ezért a hagyományos kérdés (“RAID5 vagy RAID10?”) gyakran így fordul át: “a workloadnak (terhelésnek) gyors, alacsony késleltetésű blokk tár kell, vagy inkább objektumtár, és mi a replikáció/regionális elhelyezés stratégiája?” Ezzel párhuzamosan a klasszikus lemezszintű rebuild folyamatot sokszor a platform belső “self-healing” mechanizmusai váltják ki: a kieső komponensek pótlása automatikus, és üzemeltetői oldalról inkább a szolgáltatási események és limit-ek figyelése válik lényeggé.

HCI környezetben (például olyan megoldásoknál, ahol compute és storage ugyanazon node-okban él) a redundancia jellemzően szoftveresen, node-ok között valósul meg. Itt a lemezszintű RAID helyett gyakori megközelítés a replikáció (például több példányban tárolt adat) vagy erasure coding jellegű elosztott védelem. Ez funkcionálisan hasonló problémát old meg, mint a RAID: kiesések túlélése és folyamatos működés biztosítása, de a “hiba domén” már nem egyetlen lemez, hanem egy teljes node (csomópont), sőt akár egy rack vagy zóna. Emiatt az üzemeltetés fókusza is változik: nem csak a diszkek egészségét kell nézni, hanem a node-ok állapotát, a cluster (klaszter) újraegyensúlyozását, a replikációs késleltetést, valamint a “rebuild” helyett a rebalance/reprotect jellegű folyamatok időtartamát és terhelési hatását.

Kiberbiztonsági szempontból a modern környezetek egyik legfontosabb különbsége, hogy a tároló “vezérlése” sokszor API-kon és menedzsment síkon keresztül történik, így a tároló védelmének kritikus pontja a hozzáférés-kezelés. A helytelen jogosultságok, túl széles admin szerepkörök, kompromittált hitelesítő adatok vagy rosszul védett automatizmusok nagyobb kockázatot jelentenek, mint a klasszikus “egy diszk meghal” forgatókönyv. Emiatt felhőben és HCI-ben különösen fontos a legkisebb jogosultság elve, a többfaktoros hitelesítés, a menedzsment sík hálózati szeparációja ahol értelmezhető, a naplózás és riasztás (ki hozott létre/törölt snapshotot, ki módosított policy-t, ki kapcsolt ki verziózást), valamint az immutábilis/offsite mentési réteg. Röviden: a redundancia sokszor “adott”, de a visszaállíthatóság és a rombolás elleni védelem továbbra is tudatos tervezést igényel.

Összefoglalva, a RAID modern környezetekben inkább mint tervezési elv él tovább: a cél a kiesések túlélése és a szolgáltatásfolytonosság, csak a megvalósítás sok esetben kikerül a klasszikus lemez-tömb szintről, és platform- vagy klaszter-szintre emelkedik. A dokumentációs gondolkodás mégis ugyanaz marad: tisztázni kell, milyen hibák ellen véd a rendszer (hardver/infrastruktúra), milyen hibák ellen nem (logikai és támadási események), és milyen kontrollok biztosítják a helyreállíthatóságot (snapshot, verziózás, mentés, immutability, tesztelt restore).

## 14. Összegzés – a RAID helye a teljes adatvédelemben

A RAID a tárolóoldali tervezés egyik alap eszköze, de a szerepét érdemes pontosan elhelyezni a teljes adatvédelmi modellben. A RAID elsődlegesen a **rendelkezésre állást** és az **üzemfolytonosságot** támogatja azzal, hogy lemezhiba esetén is működőképes maradhat a rendszer, illetve csökkenti az azonnali kiesés kockázatát. Ez azonban nem helyettesíti a helyreállíthatóságot: a logikai hibák (véletlen törlés, felülírás, fájlrendszer-korrupció) és a támadási események (különösen ransomware vagy credential kompromittáció) ellen a RAID önmagában nem nyújt védelmet, ezért a **snapshot és backup** réteg célja a gyors és megbízható visszaállítás, lehetőleg immutábilis és/vagy offsite megoldással kiegészítve.

A redundancia mellett külön dimenzió az **adat integritása**: a csendes adatkorruptáció és egyes tárolóhibák csak akkor kezelhetők megbízhatóan, ha a tárolóréteg vagy fájlrendszer **checksum** alapú ellenőrzést és rendszeres scrub-ot biztosít, így nem csak a kiesést, hanem az adat épségét is kontrollálni tudjuk. Mindezeket a gyakorlatban a **monitoring és riasztás** teszi üzemeltethetővé: a SMART trendek, a RAID események (degraded, rebuild), valamint a scrub eredmények korai jelzései lehetővé teszik a proaktív beavatkozást, és csökkentik annak esélyét, hogy a hiba a legrosszabb pillanatban, rebuild közben vagy mentés nélkül csapódjon ki.

Összefoglalva: a RAID a **rendelkezésre állás** rétege, a snapshot/backup a **visszaállíthatóság** rétege, a checksum/scrub az **integritás** rétege, a monitoring pedig a **proaktív üzemeltetés** rétege. A stabil és biztonságos tárolás ezek együttese, nem egyetlen technológia kiválasztása.

## 15. Fogalomtár (RAID és kapcsolódó adatbiztonsági/kiberbiztonsági fogalmak)

**Array / Tömb** – Több fizikai lemezből összeállított logikai tárolóegység (RAID tömb), amit az operációs rendszer egy vagy több kötetként lát.

**Block / Blokk** – A tárolás és adatmozgatás alapegysége (tipikusan 4 KB / 4096 bájt, vagy nagyobb). RAID esetén a blokkok a lemezek között oszlanak meg.

**Stripe / Csík** – A stripe egy olyan adatszegmens, amely a tömb több lemezén “szétterítve” jelenik meg (striping). Egy stripe több stripe unit-ból áll.

**Striping / Csíkozás (RAID 0 jelleg)** – Adatok blokkokra bontva több lemezre kerülnek párhuzamosan. Növeli a teljesítményt, de önmagában nem ad redundanciát.

**Stripe size / Chunk size (csíkméret)** – A striping granularitása: mekkora adatdarab kerül egy lemezre, mielőtt a következő lemezre vált. Rosszul választva teljesítményproblémákat okozhat (főleg vegyes, random I/O terhelésnél).

**Mirroring / Tükrözés (RAID 1 jelleg)** – Az adatok két (vagy több) lemezre azonosan íródnak. Lemezhiba esetén a másik példányból működik tovább a rendszer.

**Parity / Paritás (RAID 5/6 jelleg)** – Olyan redundáns információ, amelyből egy (RAID5) vagy két (RAID6) lemez kiesése után az adat visszaállítható. Írásnál extra műveletekkel jár.

**Single parity / Double parity** – RAID5 (egy paritás) vs. RAID6 (kettő paritás). A “double parity” nagyobb kiesést tűr, de írásban drágább.

**Redundancy / Redundancia** – Többlet (tükör/paritás), amely lehetővé teszi a kiesések túlélését. Nem azonos az adatmentéssel.

**Fault tolerance / Hibatűrés** – A rendszer képessége arra, hogy bizonyos meghibásodások mellett is működőképes maradjon (pl. 1-2 lemezhiba túlélése).

**Degraded mode / Degradált állapot** – A RAID tömb még működik, de egy vagy több komponens kiesett, a redundancia csökkent, a kockázat és gyakran a terhelés nő.

**Rebuild / Újraépítés** – Kiesett lemez cseréje után a tömb visszaállítása: tükörből másolás (RAID1/10) vagy paritásból számolás (RAID5/6). Kritikus időszak: terheli a megmaradt lemezeket.

**Resilver (gyakori ZFS kifejezés)** – ZFS-ben a rebuild megfelelője; jellemzően “csak a szükséges” blokkokat építi vissza, implementációfüggő előnyökkel.

**Hot spare / Meleg tartaléklemez** – Előre bekötött, üres lemez, ami hiba esetén automatikusan beugorhat a rebuildhez. Csökkentheti a kitettségi időt.

**Cold spare / Hideg tartaléklemez** – Nincs a rendszerbe építve, csak tartalékban van. Hiba esetén kézzel kell cserélni.

**Hot swap / Forrócsere** – Lemezcsere leállítás nélkül (megfelelő backplane/vezérlő kell hozzá). Üzemfolytonosság szempontból fontos.

**MTTD / MTTA / MTTR** – Mean Time to Detect / Acknowledge / Recover – észlelési, reagálási, helyreállítási idők. Tárolóhibák riasztásánál és üzemeltetési SLA-knál releváns.

**IOPS** – Input/Output Operations Per Second. Főleg random terhelésnél mérvadó teljesítménymutató (VM-ek, adatbázis, log indexelés).

**Throughput / Sávszélesség (MB/s, GB/s)** – Szekvenciális adatátviteli teljesítmény. Nagy fájlok másolásánál, videónál jellemzően fontosabb, mint az IOPS.

**Latency / Késleltetés** – Egy I/O művelet válaszideje. Sok kicsi műveletnél és interaktív terheléseknél kritikus.

**Write penalty (RAID5/6)** – Paritásos RAID-nél egy logikai írás több fizikai műveletet igényel (olvas–módosít–ír jelleg), ezért az írás “drágább”.

**Read-modify-write (RMW)** – A paritás frissítésének tipikus mintája: régi adat/paritás olvasása → új paritás számolása → adat + paritás visszaírása. Különösen kis írásoknál fáj.

**Consistency / Konzisztencia** – Az adatstruktúrák és metadata összhangja. Áramkimaradás, vezérlőhiba vagy bug okozhat konzisztencia-problémát.

**File system corruption / Fájlrendszer-korrupció** – A fájlrendszer struktúráinak sérülése. A RAID ettől nem véd automatikusan; UPS, journaling, snapshotok és jó üzemeltetés csökkentik a kockázatot.

**Silent data corruption (bit rot) / Csendes adatkorruptáció** – Olyan adatromlás, ami nem feltétlen jár látható hibával, csak később derül ki (pl. megnyitáskor). Checksum-os fájlrendszerek + scrub segítenek.

**Checksum / Ellenőrzőösszeg** – Integritás-ellenőrző érték. Ha tárolórétegen/fájlrendszeren elérhető és scrub-olható, erős védelmet ad silent corruption ellen.

**Scrub / Patrol read** – Időszakos háttér-ellenőrzés. Scrub inkább checksum-alapú integritásellenőrzés (pl. ZFS), patrol read inkább vezérlő oldali proaktív olvasási teszt és hibafelderítés.

**SMART** – A lemezek önmonitorozási adatai (hibaszámlálók, áthelyezett szektorok, hőmérséklet stb.). Trendekből előre jelezhető meghibásodás.

**URE (Unrecoverable Read Error) / Nem javítható olvasási hiba** – Olvasási hiba, amit a lemez nem tud korrigálni. Rebuild alatt különösen kritikus, mert adatvesztéshez vezethet (RAID-szinttől függően).

**BBU / CacheVault (write cache védelem)** – RAID vezérlő írási gyorsítótárának (cache) áramkimaradás elleni védelme. Nélküle a write-back cache kockázatos vagy tiltásra kerülhet.

**Write-back cache / Write-through cache** – Write-back: gyors, de védelem kell (BBU/CacheVault). Write-through: biztonságosabb, de lassabb, mert a vezérlő megvárja a lemezre írást.

**TRIM / UNMAP** – SSD-knek szóló jelzés a felszabadított blokkokról. Ha RAID rétegen nem jut át jól, hosszabb távon romolhat a teljesítmény.

**HDD vs SSD vs NVMe** – HDD: nagy kapacitás, olcsóbb, nagyobb latencia. SSD: alacsony latencia, jó random I/O. NVMe: SSD PCIe-n, még alacsonyabb latencia és nagy sávszél.

**Hardware RAID / Hardver RAID** – Dedikált vezérlő kezeli a tömböt. Előny: cache, menedzsment, offload. Hátrány: költség, kompatibilitás, vendor lock-in.

**Software RAID / Szoftver RAID** – OS vagy fájlrendszer kezeli a redundanciát. Előny: rugalmasság, átláthatóság. Hátrány: implementációfüggő teljesítmény, erőforrás-igény.

**FakeRAID / Alaplapi RAID** – BIOS-szintű “RAID”, ami sokszor driver/OS függő. Kényelmes lehet, de recovery/migráció szempontból kockázatosabb.

**HBA (Host Bus Adapter)** – Olyan vezérlő, ami “csak” átadja a lemezeket (nem feltétlen RAID-ezik). ZFS jellegű rendszereknél gyakori, mert a fájlrendszer kezeli a redundanciát.

**RAIDZ / RAIDZ2 / RAIDZ3 (ZFS)** – ZFS paritásos megoldásai (1/2/3 paritás). Nem “klasszikus RAID5/6”, hanem ZFS-integrált, checksum-alapú védelemmel és scrubbal.

**Snapshot / Pillanatkép** – Egy időpontbeli állapot rögzítése (általában gyors és helytakarékos). Véletlen törlés és korai ransomware ellen hasznos, de admin kompromittáció esetén törölhető.

**Backup / Biztonsági mentés** – Külön tárolt másolat visszaállításhoz. Akkor jó, ha tesztelt a restore, és támadás esetén sem törölhető könnyen.

**3-2-1 szabály** – 3 példány az adatról, 2 különböző médiumon, 1 offsite. Ransomware korában érdemes kiegészíteni immutábilis/air-gapped komponenssel.

**Immutable backup / Immutábilis mentés** – Olyan mentés, amit egy meghatározott ideig nem lehet törölni vagy módosítani (WORM policy). Ransomware ellen kiemelten értékes.

**Air-gapped backup** – Fizikailag vagy logikailag leválasztott mentés. Nehezebb kompromittálni, de üzemeltetése kényesebb.

**Ransomware** – Zsarolóvírus, amely titkosítja az adatot. RAID nem véd ellene; snapshot + immutábilis/offsite backup ad valós védelmet.

**Least privilege / Legkisebb jogosultság elve** – A tároló admin felületek és mentések hozzáférését minimalizálni kell. Egy kompromittált admin fiók storage-oldali katasztrófát okozhat.

**Management VLAN / Menedzsment hálózat** – Elkülönített hálózat admin felületeknek (iDRAC/iLO/NAS GUI). Csökkenti a támadási felületet.

**Monitoring / Alerting** – Állapotfigyelés és riasztás (degraded, rebuild, SMART, hőmérséklet, hibaszámlálók). SOC környezetben ez tipikus korai jelzőrendszer.

**SLA / RTO / RPO** – SLA: szolgáltatási vállalás. RTO: mennyi idő alatt kell helyreállni. RPO: mennyi adatvesztés fér bele (mennyi a maximum “visszaugrás”). RAID főleg RTO-n segít, backup RPO-n.

**Disaster Recovery (DR) / Katasztrófa-helyreállítás** – Eljárások és infrastruktúra nagyobb eseményekre (tűz, lopás, totális storage-hiba, ransomware). RAID önmagában nem DR.

**Credential kompromittáció** – Olyan biztonsági esemény, amikor a támadó megszerzi vagy átveszi az irányítást hitelesítő adatok felett (felhasználónév+jelszó, hozzáférési token, session cookie, API/SSH kulcs, MFA megkerülésével szerzett belépés), és ezekkel jogos felhasználóként tud hozzáférni rendszerekhez, szolgáltatásokhoz vagy admin felületekhez.

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
