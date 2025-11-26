# SIEM és SOC - Átfogó Áttekintés a Kiberbiztonságban

**Források és felhasznált eszközök:**

- [Copilot](https://copilot.microsoft.com/), [ChatGPT](https://chatgpt.com/), [DeepSeek](https://www.deepseek.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

A modern **kiberbiztonsági környezetben** a cégek és szervezetek adatvédelme érdekében különféle módszerek és eszközök állnak rendelkezésre. Egyre gyakoribbak a kibertámadások és az adatvédelmi incidensek: 2023-ban a globális adatszivárgások átlagos költsége körülbelül 4,45 millió dollár volt az IBM Cost of a Data Breach 2023 jelentése szerint. Ugyanakkor a szakemberek hiánya miatt **automatikus és félautomatikus megoldásokra** (mint a SIEM, EDR, SOAR), valamint egy **központosított biztonsági műveleti központra** (SOC) van szükség a valós idejű észleléshez és válaszadáshoz.

Az alábbiakban részletesen bemutatom a **SIEM** (Security Information and Event Management) technológiáját és a **SOC** (Security Operations Center) működését, azok lépéseit, feladatait és
kölcsönhatását.

## Mi az a SIEM?

A SIEM egy **biztonsági információ- és eseménykezelő rendszer** (Security Information and Event Management).

A SIEM célja, hogy egyetlen központi platformon gyűjtse, tárolja és elemezze a szervezet összes biztonsági relevanciájú napló- (log) és eseményadatát. A Microsoft definíciója szerint a SIEM megoldások valós időben gyűjtenek, aggregálnak és elemeznek nagy mennyiségű adatot az egész szervezet alkalmazásaiból, eszközeiből, kiszolgálóiból és felhasználóiból. Ezáltal átfogó képet nyújtanak a szervezet biztonsági állapotáról.

A SIEM megoldások eredetileg a 2000-es évek elején jelentek meg a Gartner által definiált SIM (Security Information Management) és SEM (Security Event Management) egyesítéseként. Manapság a SIEM a kiberfenyegetések észlelésének és reagálásának nélkülözhetetlen eszköze, és a SOC-ok (biztonsági műveleti központok) számára lehetővé teszi a biztonsági események **gyors és hatékony kezelését**.

**A SIEM főbb lépései és összetevői:**

A SIEM rendszerek működésének kulcsa az adatok begyűjtése és elemzése.

A folyamat lépései a következők:

- **Adatgyűjtés (Loggyűjtés):**
  
  A SIEM valós időben begyűjti az eseményeket és naplókat a különböző forrásokból (például tűzfalakból, szerverekből, végpontokból, alkalmazásokból, hálózati eszközökből, felhőszolgáltatásokból stb.). Ez magában foglalhat központi naplógyűjtést (pl. syslog), ügynökök telepítését végpontokon, illetve API-kon és naplófájlokon keresztüli hozzáférést.

- **Normalizáció és aggregálás:**
  
  A begyűjtött adatokat a SIEM szabványos formátumokká alakítja (normalizálja), így különféle rendszerekből származó naplók összevethetők és elemezhetők egységesen. Az aggregálás során a hasonló bejegyzéseket csoportosítja.

- **Korreláció és elemzés:**
  
  A SIEM korrelációs szabályokat és algoritmusokat alkalmaz a normalizált adatokon, hogy mintázatokat és anomáliákat keressen. Például egyetlen esemény önmagában nem feltétlenül gyanús, de ha több helyen ismétlődő mintázatot talál (pl. rövid időn belüli többszöri sikertelen bejelentkezés és azt követő sikeres belépés egy idegen helyről), akkor azt **lehetséges brute-force támadásként** jelzi. A gyártók egyre inkább mesterséges intelligenciát és gépi tanulást építenek a SIEM-be, hogy jobbá tegyék az anomália-azonosítást és csökkentsék a téves riasztásokat.

- **Riasztások és jelzések:**
  
  A SIEM folyamatosan generál valós idejű riasztásokat, ha a korreláció vagy az anomália-észlelés potenciális fenyegetést jelez. A riasztások rendszerint súlyossági szintekhez (alacsony, közepes, magas, kritikus) vannak rendelve, és egy központosított irányítópulton érhetők el az elemzők számára. Egy riasztáshoz kapcsolódhat automatizált beavatkozás is (pl. fiók zárolása), de általában egy biztonsági elemzőt értesít a vizsgálat megkezdéséhez.

- **Tárolás és nyomon követés:**
  
  A SIEM megoldások adatbázisban vagy adattárházban tárolják a naplókat, hogy hosszú távú vizsgálatokra, trendek elemzésére, vagy szabályozási megfelelés igazolására is alkalmasak legyenek. A korábbi adatok visszakereshetők, ami segíti a forenzikus elemzéseket és az auditigényeket.

A SIEM rendszerek fő összetevői a naplókezelés, az eseménykorreláció, a folyamatos megfigyelés és az incidenskezelés támogatása.

A SIEM erőteljes eszköz az átfogó láthatóság biztosítására: például a SIEM egyetlen, központosított felületet ad a biztonsági csapatnak, ahol minden forrás adatai megjelennek.

**SIEM előnyei:**

- A SIEM alkalmazása jelentősen   növeli a biztonsági látókört és felgyorsítja az incidensválasz folyamatát.

- Egy jó SIEM átláthatóvá teszi a szervezet valós idejű biztonsági helyzetét, lehetővé téve a fenyegetések gyors felismerését és rangsorolását.

- Emellett a SIEM segít csökkenteni a hamis riasztásokat: a korrelációs szabályok és az intelligens elemzés kiszűrik a téves pozitívokat, így a biztonsági elemzők a valódi fenyegetésekre koncentrálhatnak.

- A SIEM megfelelőségi előnyei közé tartozik, hogy automatikus audit- és riportfunkcióival könnyebben teljesíthetők a szabályozói követelmények (pl. GDPR, HIPAA, PCI-DSS).

**Összességében** a SIEM használata megelőzheti a költséges adatvesztést és büntetéseket, miközben erősíti az IT-biztonságot.

## A SIEM működése és legfontosabb lépései

A SIEM konkrét működését a gyakorlatban a következő lépések szemléltetik – ezeket a folyamatokat a bevezetőben már áttekintettük, de itt részletesebben is ismertetjük:

**1. Adatgyűjtés (Logging & Data Collection):**

A SIEM begyűjti az eseményeket minden forrásból. Ide tartoznak a rendszer- és alkalmazásnaplók (CPU események, alkalmazáshibák), hálózati naplók (tűzfal-forgalom, switchek), biztonsági eszközök (IDS/IPS, antivírus riasztások), valamint minden felhasználói tevékenység (bejelentkezések, jogosultság-változtatások stb.). Ez valós időben, ügynökök vagy központi naplózási megoldások segítségével történik.

**2. Normalizáció és összegzés:**

A SIEM rendszerek átalakítják az összevont naplókat egy egységes formátumba. Ezzel a különböző források adatai összehasonlíthatók lesznek. Például a beépített normálformátum segít abban, hogy a különböző gyártótól származó tűzfal- vagy szervernaplók esetében is azonos jellegű információ legyen kiolvasható.

**3. Korreláció és anomália-észlelés:**

A feldolgozott adatokat a SIEM megvizsgálja szabályok és algoritmusok mentén. Egyszerű példával élve: ha **többszörös sikertelen bejelentkezés** után rövid időn belül sikeres belépés történik, ez korrelált riasztás lehet (brute-force gyanú). A SIEM a korreláció során **mintázatokat és anomáliákat** keres. A gépi tanulásos kiegészítők egyre pontosabban felismernek ismeretlen fenyegetéseket is, az előzményadatok alapján megtanulják a „normál” működést, és az ettől eltérő viselkedést (pl. szokatlan hálózati forgalom) jelzik.

**4. Riasztás létrehozása:**

Ha a korreláció valószínűsíthető támadást vagy szokatlan viselkedést talál, a SIEM azonnal riaszt egy biztonsági elemzőt vagy automatikus válaszlépést indíthat (pl. egy felhasználói fiók ideiglenes blokkolását). A riasztások általában kategóriákba és súlyossági szintekbe (alacsony, közepes, magas, kritikus) vannak sorolva, hogy a SOC-csapat gyorsan prioritásba helyezhesse a vizsgálatot. A SIEM irányítópultja felügyeli az összes aktív és múltbeli riasztást, így a csapat nyomon követheti a válaszlépéseket és az incidensek státuszát.

**5. Elemzés és válasz:**

A SIEM felgyorsítja a biztonsági elemzők munkáját: a központosított naplótárolón keresztül könnyen felderíthetők a korábbi események, így a csapat **gyorsabban válaszolhat** az incidensekre. Például, ha egy felhasználó fiókját feltörték, a SIEM segítségével visszakövethető a támadás teljes útvonala, megtalálhatók a fertőzött gépek és a támadók által használt technikák. A SIEM logjai alapján a SOC elkülönítheti a veszélyforrást (pl. karanténba helyezhet egy vizsgálat alatt álló szervert), frissítheti a biztonsági szabályokat és riportokat készíthet a tanulságokról.

E folyamat során tehát a SIEM-szoftver *együttesen kezeli az adatgyűjtést, normalizálást, korrelációt és riasztást*, hogy a biztonsági csapatok átlátható és hatékony felügyeletet kapjanak.

**Összefoglalva** a SIEM-technológia segít abban, hogy „akadálytalanul” lássuk a hálózatot és az eszközöket, észleljük a gyanús viselkedést, és a lehető legrövidebb idő alatt reagáljunk rá.

## Mi az a SOC?

A SOC (Security Operations Center, magyarul **biztonsági műveleti központ**) a szervezet *biztonsági védelmi egysége*, amely folyamatosan figyeli és kezeli a biztonsági eseményeket.

Egy SOC lehet házon belüli csapat vagy külső szolgáltató (SOC-as-a-Service), de lényege mindig központosítottan **emberi elemzőkből, folyamatokból és technológiákból** áll össze. A Microsoft szerint a SOC „egy központosított funkció vagy csapat, amely a szervezet kiberbiztonsági helyzetének javításáért, valamint a fenyegetések megelőzéséért, észleléséért és elhárításáért felelős”. A SOC csapata valós időben felügyeli az azonosítókat, végpontokat, szervereket, adatbázisokat, hálózati alkalmazásokat, webhelyeket és más rendszereket, hogy észlelje a lehetséges kibertámadásokat.

**Feladatok és működés:**

A SOC célja, hogy a fenyegetéseket *proaktívan kezelje*: folyamatosan gyűjti és elemzi a biztonsági információkat, kutatja az új veszélyeket, és ha incidens történik, azonnal reagál. A SOC tipikusan *24/7* működik, hogy azonnal észlelje és korlátozza a támadást.

Fő feladatai közé tartozik a hálózat és rendszerperemek monitorozása, a behatolások korai felismerése, a fenyegetések nyomon követése és a reagálás az incidensekre. Ha például egy vállalat sikeres támadás áldozatává válik, a SOC felelős a fenyegetés eltávolításáért és az érintett rendszerek helyreállításáért. Emellett a SOC dokumentálja az eseményeket, javító intézkedéseket vezet be, és gondoskodik a megfelelésről.

**Szerepkörök és összetevők:**

A SOC tevékenységét személyek és eszközök együttműködése teszi hatékonnyá.

Tipikus szerepkörök egy SOC-ban:

- SOC-menedzser (vezető),

- biztonsági elemzők különböző szinteken (Tier 1 triage-analitikusok, Tier 2 incidenskezelők, Tier 3 fenyegetésvadászok),

- biztonsági építész

- és megfelelőségi auditor.

E csapat felügyeli az összes használt eszközt és technológiát, például firewalleket, végpontvédelmi szoftvereket és SIEM-megoldásokat, valamint kialakítja a biztonsági folyamatokat.

A SOC feladatai között megtalálható a teljes eszközleltár kezelése, rendszeres karbantartás és felkészülés, folyamatos monitorozás, fenyegetésészlelés, naplókezelés, incidenskezelés és utólagos forenzika.

Emellett a SOC javítja a vállalat biztonságát azzal, hogy redukálja a támadási felületet, kutatja a feltárt kockázatokat, és optimalizálja a védekezési stratégiát.

**SOC működése példa szerint:**

A SOC a SIEM eszközök által szolgáltatott riasztásokat és logokat használja a napi műveletekhez. A SOC-elemzők különbséget tesznek hamis pozitív riasztás (false positive) és valós incidens között, fontossági sorrendet állítanak fel a fenyegetések súlyossága alapján, és elindítják a válaszlépéseket.

A SOC csapata együttműködik a szervezet többi részével (pl. hálózatüzemeltetés, IT-üzemeltetés, IT-részleg), és jelentéseket készít a vezetés és szabályozó hatóságok számára is.

Összességében a **SOC feladata** a vállalat biztonságának fenntartása: az eszközök és folyamatok monitorozása, incidensek kezelése, fenyegetések felderítése, és a reagálás koordinálása.

Ahogy a Microsoft fogalmaz: „A SOC olyan személyekből, eszközökből és folyamatokból áll, amelyek segítenek megvédeni a szervezetet a kibertámadásoktól”.

Egy erős SOC megléte azért fontos, mert egy helyen összpontosítja a védelmi tevékenységeket, ezáltal hatékonyabb és gyorsabb a védelem megvalósítása.

## A SIEM és a SOC kapcsolata

A SIEM és a SOC szorosan összefonódó fogalmak: a SIEM egy technológiai eszköz, míg a SOC egy szervezeti és működési keret. Egyszerűen fogalmazva, a **SIEM a SOC „műszerei” közé tartozik**. A SOC csapata a SIEM adatait használja az események felismeréséhez és kezeléséhez.

A Microsoft leírása szerint a SOC „az eszközök és folyamatok gyűjteménye, amely a kibertámadások elleni védekezésért felel”, és egyik eszköz, amit használ, a SIEM. Ugyanitt hozzáteszik, hogy **a SIEM összesíti a naplófájlokat, és elemzéssel valamint automatizálással érzékeli a lehetséges fenyegetéseket** a SOC tagjai számára, akik ezt követően döntenek a válaszlépésekről. Tehát a SIEM az információforrás, a SOC a döntéshozó és cselekvő egység.

A gyakorlatban ez úgy működik, hogy a SIEM rendszer folyamatosan küldi a figyelmeztetéseket és jelentéseket a SOC felé. A SOC-elemzők például azt látják a SIEM irányítópultján, hogy egy gyanús IP-cím többször próbálkozott bejelentkezni. Erre egy elemző felveszi a kapcsolatot az érintett részleggel, közben a SOC automatizált szabályozások vagy SOAR- (Security Orchestration, Automation and Response) integrációk révén beavatkozhatnak (pl. zárolhatják a támadó IP-t). A SIEM további adatokat szolgáltat a vizsgálathoz, a SOC pedig összehangolja a válaszlépéseket (pl. a rendszergazdák útján karanténba helyezik az érintett gépet).

A **SOC hatékonysága** nagyban növelhető a SIEM használatával. Egy modern SIEM rendszer „jelentősen csökkenti a SOC-ban végzett manuális munka mennyiségét” – írják a Microsoft anyagai. A központosított irányítópult és a korrelált események révén a csapatok gyorsabban azonosítják a súlyos incidenseket, és a SIEM által létrehozott riportok és elemzések segítik az együttműködést. Emellett a SOC a SIEM és az XDR megoldások által gyűjtött adatokat együtt használja, hogy szűrje az álpozitív riasztásokat és rangsorolja a valós fenyegetéseket.

**Összefoglalva:**

A SOC-t a *személyek, folyamatok és eszközök együtteseként* definiáljuk, míg a SIEM a *technológiai eszköz*, mely összesíti a logokat és észleli a fenyegetéseket a SOC számára. A SIEM tehát a SOC „központi idegrendszere”: adatokat gyűjt és elemez, a SOC pedig emberi erőforrással vizsgálja a SIEM jelzéseit, és végrehajtja a szükséges biztonsági intézkedéseket. A kettő együttműködése alapozza meg a szervezet valós idejű védekezését, és lehetővé teszi a gyors reakciót a kibertámadásokra.

## Példák és esettanulmány

Egy **példa** szemlélteti a SIEM és SOC együttes működését:

Tegyük fel, hogy egy közepes méretű vállalatnál bevezetésre kerül egy új SIEM rendszer. A SIEM elkezdi összegyűjteni az adatokat az összes végpontról, szerverről és biztonsági eszközről. Egy nap a SIEM riasztást ad: több sikertelen belépési kísérlet történt egy alkalmazásfelhasználói fióknál, majd hirtelen sikeres bejelentkezés egy távoli országból. A SIEM ezt korrelálva „súlyos” riasztást generál.

A SOC első szintű (Tier 1) elemzője triázsolja a riasztást: látja, hogy a fiók valóban a forgalmas időszakon kívül aktiválódott.

Ennek alapján a Tier 2 szintű incidensválasz elemző bevonásra kerül, aki mélyebb vizsgálatot kezd. A vizsgálat megállapítja, hogy a felhasználó eszköze kompromittálódott.

A SOC ennek hatására azonnal blokkolja a fiókot, és a fenyegetett végpontot elszigetelik a hálózattól. A SOC irányítópultjáról pedig részletes riport készül az ügyről, amely tartalmazza a támadó IP-címét és az alkalmazott módszert (például a jelszófeltörést). Az esetet a SOC riasztási folyamatában lezárják, majd a SIEM naplóiból visszakeresve dokumentálják a támadás láncolatát. A tanulságok alapján a SOC módosítja a SIEM korrelációs szabályait (szigorúbban szűri a nemzetközi belépéseket), és tájékoztatja a vállalati informatikai vezetést az új fenyegetésfeltárási rutinokról.

Ez a folyamat jól mutatja, hogyan egészíti ki egymást a technológiai és az emberi komponens: a SIEM *azonnal jelezte* a gyanús eseményt, a SOC pedig *megvizsgálta*, *reagált* és *megelőző lépéseket tett* a károk elkerülésére. Hasonló forgatókönyvek gyakoriak azoknál a szervezeteknél, amelyek élesben használják a SIEM-et és a SOC-ot együtt.

## „Triázs” (angolul: triage)

Amikor a SIEM vagy más eszköz riasztást (alert) küld, a SOC elemzőnek (SOC analyst) meg kell vizsgálnia, hogy az **valódi veszély-e, vagy csak hamis pozitív** (false positive).

A triázs során az elemző **prioritást állít fel**: melyik riasztás igényel azonnali reagálást, melyik vizsgálható később, és melyik hagyható figyelmen kívül.

**Példa:**

Egy SIEM riasztás érkezik, hogy valaki háromszor rossz jelszóval próbált belépni → lehet, hogy csak a felhasználó felejtette el a jelszót.

Egy másik riasztás, hogy admin jogosultságú felhasználó az éjszaka közepén jelentkezett be külföldről → sokkal súlyosabb, azonnali vizsgálatot igényel.

A triázs lényege: **szűrés és priorizálás**, hogy a SOC ne vesszen el a több száz/ezernyi napi riasztásban, hanem a valóban fontosakat kezelje először.

## Fontos kifejezések (magyar–angol)

A kiberbiztonsági szakterületen számos műszaki kifejezést angolul használunk. Az alábbi listában néhány gyakran használt fogalmat és rövidítést közlünk magyarul, majd angol megfelelőjét:

- **Biztonsági információ- és eseménykezelés (SIEM)** – *Security Information and Event Management*
  
  A SIEM egy központosított rendszer, amely gyűjti és tárolja a különböző eszközök és alkalmazások naplóit (logjait), majd ezeket normalizálva elemzi és korrelálja. Célja, hogy valós időben észleljen gyanús eseményeket, riasztást generáljon és hosszú távú naplótárolást, megfelelőségi riportokat biztosítson. Gyakorlati haszna: egyetlen felületen láthatóvá teszi a szervezet biztonsági állapotát és segíti az incidensvizsgálatot.

- **Biztonsági műveleti központ (SOC)** – *Security Operations Center*
  
  A SOC egy szervezeti egység (emberek, folyamatok, eszközök együttese), amely folyamatosan (általában 24/7) figyeli, elemzi és kezeli a biztonsági eseményeket. A SOC használhat SIEM-et és más eszközöket; feladata a riasztások triázsa, incidenskezelés, fenyegetésvadászat és helyreállítás. Lényeg: a SOC dönt és cselekszik, míg a SIEM információt szolgáltat.

- **Behatolásészlelő rendszer (IDS)** – *Intrusion Detection System*
  
  Az IDS passzívan figyeli a hálózati forgalmat vagy rendszereket, és riaszt, ha ismert támadási mintázatot vagy gyanús viselkedést talál. Nem minden IDS avatkozik be automatikusan (az IPS-zel ellentétben); gyakran jelzésrendszerként szolgál a SOC/SIEM számára. Jó IDS-sel gyorsan felfedezhetők ismert támadási jelek.

- **Behatolásmegelőző rendszer (IPS)** – *Intrusion Prevention System*
  
  Az IPS hasonló az IDS-hez, de aktívan képes blokkolni vagy megszakítani a gyanús forgalmat (például letilt egy IP-címet vagy kapcsolatot). Az IPS célja, hogy automatikusan megelőzze a sikeres támadásokat ahelyett, hogy csak riasztana. Fontos: ha rosszul konfigurálják, hamisan blokkolhat legit forgalmat is.

- **Végponti észlelés és válasz (EDR)** – *Endpoint Detection and Response*
  
  Az EDR egy végpontokra telepített ügynök + központi platform kombinációja, amely folyamatosan gyűjti a végponti eseményeket (fájlműveletek, folyamatok, hálózati kapcsolatok) és lehetővé teszi a részletes vizsgálatot, izolálást és reagálást. Különösen hasznos a végpontokon végzett célzott támadások (pl. zsarolóprogramok) észlelésére és eltávolítására. Az EDR gyakran integrálható SIEM-mel és SOAR-ral.

- **Kiterjesztett észlelés és válasz (XDR)** – *Extended Detection and Response*
  
  Az XDR több forrásból (végpontok, hálózat, e-mail, felhő stb.) gyűjt adatot és integrált, kontextusgazdag riasztásokat hoz létre. A cél, hogy a különböző rendszerek közötti összefüggéseket jobban lássa, és ezáltal pontosabb, automatizált válaszokat tegyen lehetővé. Gyakorlatban az XDR csökkenti a zajt és gyorsítja az incidenskezelést.

- **Biztonsági automatizálás és reagálás (SOAR)** – *Security Orchestration, Automation and Response*
  
  A SOAR rendszerek automatizálják és megszervezik a biztonsági műveleteket: például egy riasztásból előre definiált forgatókönyv indul, lekérdezések futnak, és bizonyos lépéseket automatikusan végrehajtanak (fiók zárolása, IP blokkolása, ticket létrehozása). Célja: gyorsabb, konzisztens reagálás és az ismétlődő manuális feladatok csökkentése. A SOAR gyakran integrálódik SIEM-mel és egyéb eszközökkel.

- **Felhasználó- és entitás viselkedéselemzés (UEBA)** – *User and Entity Behavior Analytics*
  
  A UEBA a felhasználók és entitások (gépek, szolgáltatások) viselkedését elemzi, anomáliákat keresve a korábbi normál viselkedéshez képest. Nem csak szabályokra támaszkodik, hanem statisztikákra és gépi tanulásra is, így hatékony a belső fenyegetések és jogosultság-visszaélések felismerésében. Jó kiegészítője a SIEM-nek, mert csökkentheti a hamis riasztásokat.

- **Fenyegetésintelligencia** – *Threat Intelligence*
  
  A fenyegetésintelligencia strukturált információ (pl. rossz IP-címek, rosszindulatú domain-ek, TTP-k — tactics, techniques, procedures) a támadókról és módszereikről. Ezeket az adatokat be lehet etetni a SIEM/IPS/EDR rendszerekbe, hogy gyorsabban és pontosabban azonosítsuk a fenyegetéseket. Két fajtája: stratégiai (trendek) és műveleti/technikai (konkrét IoC-k — Indicators of Compromise).

- **MITRE ATT&CK** – *MITRE Adversarial Tactics, Techniques, and Common Knowledge* (nyílt fenyegetéselemzési keretrendszer)
  
  A MITRE ATT&CK egy nyílt, strukturált repertoár (táblázat) a támadók taktikáiról és technikáiról (pl. credential dumping, lateral movement). Segít rendszerezni, hogy egy adott incidens során a támadó milyen lépéseket használt, és hol vannak védelmi hiányok. Széles körben használják fenyegetés-modellezésre, vizsgálati forgatókönyvek készítésére és gap-analízisre.

- **Adathalászat (phishing)** – *Phishing*
  
  A phishing célja, hogy megtévessze a felhasználót (e-mail, hamis weboldal), és így megszerezzen hitelesítési adatokat, pénzt vagy érzékeny információkat. Gyakori formái: célzott spear-phishing és tömeges email-kampányok. A védelem része a felhasználói oktatás, e-mail szűrés és URL-ellenőrzés.

- **Zsarolóprogram (ransomware)** – *Ransomware*
  
  A zsarolóprogram olyan rosszindulatú szoftver, amely titkosítja az adatokat, majd váltságdíjat követel a visszafejtésért. Gyorsan terjedhet hálózaton belül és súlyos üzleti leállást okozhat. Megelőzése: patch-menedzsment, EDR, rendszeres biztonsági mentések és hálózati szeparáció.

- **Incidens** – *Incident*
  
  Incidens minden olyan esemény, amely sérti vagy veszélyezteti egy rendszer biztonságát (pl. jogosulatlan hozzáférés, malware fertőzés). Az incidenskezelés (Incident Response) célja az észlelés, izolálás, eltávolítás, helyreállítás és a tanulságok levonása. Fontos, hogy legyen előre definiált IR-folyamat és szerepkörök (playbookok).

- **Sérülékenység (vulnerabilitás)** – *Vulnerability*
  
  Sérülékenység egy rendszer, alkalmazás vagy konfiguráció gyengesége, amelyet egy támadó kihasználhat. A sérülékenység-menedzsment folyamata a feltérképezés, kockázat-értékelés és javítás (patching vagy konfigurációváltoztatás). CVE-azonosítók (Common Vulnerabilities and Exposures) segítik a nyomon követést.

- **Napló (log)** – *Log*
  
  A log egy eseményről készült automatikus feljegyzés (például bejelentkezés, fájlművelet, hálózati kapcsolat), amely forrásrendszerenként eltérő formátumú lehet. A naplók elemzése alapvető a nyomon követéshez, forenzikához és megfeleléshez. A SIEM a naplókat gyűjti, normalizálja és elemzi.

- **Riasztás** – *Alert*
  
  A riasztás egy észlelt, potenciálisan veszélyes esemény vagy korreláció eredménye, amit a SIEM, EDR vagy egyéb rendszer generál. Fontos a riasztás prioritása (severity) és a triage folyamata, hogy a SOC erőforrásai a valódi incidensekre koncentráljanak. A rossz riasztáskezelés túlterhelheti a csapatot.

- **Támadási felület (attack surface)** – *Attack Surface*
  
  Az attack surface azoknak a rendszereknek, szolgáltatásoknak és interfészeknek az összessége, amelyeken keresztül egy támadó hozzáférhet vagy kárt okozhat. Minél nagyobb és kevésbé kontrollált az attack surface, annál nagyobb a kockázat. Csökkentése: felesleges szolgáltatások lekapcsolása, hálózati szegmentálás, erős hozzáférés-szabályozás.

- **Eseménykezelés (event management)** – *Event Management*
  
  Eseménykezelés alatt a biztonsági (és operatív) események gyűjtését, feldolgozását, korrelációját és nyomon követését értjük. A cél, hogy minden releváns eseményből megfelelő kontextust nyerjünk, és szükség esetén riasztást hozzunk létre. Ez a SIEM alapfunkcióinak egyik fő területe.

- **Megfelelőségi jelentéstétel** – *Compliance Reporting*
  
  A compliance reporting olyan riportok és auditok készítése, amelyek bizonyítják, hogy a szervezet megfelel adott szabályozásoknak (pl. GDPR, PCI-DSS, HIPAA). A SIEM és a SOC logjai és auditfunkciói gyakran használhatók ezekhez a jelentésekhez. Jó dokumentálás és hosszú távú logmegőrzés szükséges a szabályozói elvárások teljesítéséhez.
