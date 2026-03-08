# Felhőszolgáltatások

**Források és felhasznált eszközök:**

- [Training360](https://www.training360.com/), [Gyártófüggetlen hálózati alapismeretek - 03 - Szolgáltatások és eszközök üzemeltetők számára](https://e-learning.training360.com/courses/gyartofuggetlen-halozati-alapismeretek3)

- [ChatGPT](https://chatgpt.com/), [DeepSeek](https://www.deepseek.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

A **felhőszolgáltatások (cloud computing)** olyan informatikai szolgáltatások összefoglaló neve, amelyeknél számítási kapacitás, tárhely, hálózati funkciók, adatbázisok, fejlesztői platformok vagy akár kész alkalmazások érhetők el az interneten keresztül, igény szerint. A „felhő” kifejezés azt jelenti, hogy a háttérben futó infrastruktúra nem a saját telephelyen üzemel, hanem egy szolgáltató nagy, professzionálisan menedzselt adatközpontjaiban. A felhasználó oldaláról ez jellemzően úgy jelenik meg, hogy az erőforrások gyorsan létrehozhatók, rugalmasan méretezhetők, és a fogyasztás mérhető, így sok esetben **használat alapú díjazással (pay-as-you-go)** vehetők igénybe.

## **A felhő fő jellemzői (miért más, mint a “sima” hoszting?)**

A felhő egyik lényegi sajátossága, hogy a szolgáltatás jellemzően **önkiszolgáló módon** érhető el: egy adminisztrációs felületen vagy **API-n** keresztül percek alatt létrehozható egy virtuális szerver, egy tárhely vagy egy adatbázis.

Ezek az erőforrások általában **megosztott kapacitáspoolból** származnak, vagyis a szolgáltató nagy mennyiségű hardvert üzemeltet, és ebből osztja ki logikailag elkülönítve az ügyfelek számára a szükséges részt.

Emellett a felhő alapvető értéke a **rugalmasság és skálázhatóság**: ha egy alkalmazás terhelése megnő, az erőforrások gyorsan növelhetők, ha pedig csökken, visszavehetők.

Végül fontos jellemző még a **mérhetőség**, mert a szolgáltató szinte mindent mér, naplóz és számlázási egységekre bont, például processzoridőre, tárolt adatmennyiségre, kérésszámra vagy hálózati adatforgalomra.

## **Szolgáltatási modellek: SaaS, PaaS, IaaS és “serverless”**

A felhőszolgáltatások típusait többféleképpen szokás csoportosítani. Az egyik legfontosabb felosztás az úgynevezett **szolgáltatási modellek** szerinti.

A SaaS, PaaS és IaaS közti egyik legfontosabb különbség az, hogy meddig a szolgáltató felelőssége az üzemeltetés, és mettől a megrendelőé a kontroll.
SaaS esetén a szolgáltató adja és üzemelteti a teljes alkalmazást, ezért a megrendelő oldalán jellemzően a felhasználók, jogosultságok, beállítások és adatok kezelése marad.

PaaS esetén a szolgáltató már nem kész alkalmazást ad, hanem egy menedzselt platformot, így ő kezeli az infrastruktúrát, az alap operációs rendszert és a futtatókörnyezetet, míg a megrendelő a saját alkalmazásáért, konfigurációjáért és adataiért felel.

IaaS esetén a szolgáltató főként az alap infrastruktúrát biztosítja, de a virtuális gépek operációs rendszere, a frissítés, a hardening, az alkalmazások és sok biztonsági beállítás már a megrendelő kezében marad.

Általánosan igaz, hogy minél lejjebb megyünk SaaS → PaaS → IaaS irányba, annál nagyobb a kontroll a megrendelőnél, de annál nagyobb az üzemeltetési felelősség is.

### SaaS

A **SaaS (Software as a Service)** kész alkalmazást jelent: ilyen például a **Microsoft 365**, a Google Workspace, a Salesforce, a Jira vagy a Slack.

Ebben az esetben a szolgáltató adja a teljes alkalmazást és annak üzemeltetését, a felhasználó pedig a beállításokért, a **jogosultságokért** és a benne tárolt **adatok** kezeléséért felel.

A SaaS általában gyorsan bevezethető, viszont cserébe kisebb a testreszabhatóság, és különösen fontos a megfelelő **identitás- és hozzáféréskezelés (IAM)**, mert a hibás hozzáférések jellemzően az egyik leggyakoribb kockázati forrást jelentik.

### PaaS

A **PaaS (Platform as a Service)** egy lépéssel lejjebb helyezkedik el: itt nem egy kész alkalmazásról van szó, hanem egy menedzselt **futtatókörnyezetről**. Tipikus példa lehet egy webalkalmazás-futtató szolgáltatás vagy egy **menedzselt adatbázis (DBaaS)**.

Ilyenkor a szolgáltató sok terhet levesz az üzemeltető válláról (például az alap operációs rendszer és bizonyos komponensek frissítése, skálázási mechanizmusok), miközben a felhasználó a saját **kódjáért**, konfigurációjáért és adataiért felel.

A PaaS gyakran ideális kompromisszum: gyors, kényelmes, viszont előfordulhat, hogy a szolgáltató által adott „keretek” korlátozzák a specializált igényeket, illetve később nehezebb lehet más platformra átállni.

### IaaS

Az **IaaS (Infrastructure as a Service)** a legnagyobb kontrollt adja: a szolgáltató infrastruktúrát biztosít (virtuális gépeket, hálózatot, tárolót), de az operációs rendszer, a **patch-elés**, a **hardening**, sok biztonsági beállítás és az alkalmazás teljes üzemeltetése az ügyfélnél marad.

Ez a modell közelebb áll a klasszikus rendszergazdai gondolkodáshoz, ugyanakkor több felelősséget és több hibalehetőséget is jelent.

A modern felhővilágban gyakran külön névvel említik a **serverless** és **eseményvezérelt** szolgáltatásokat is (például **FaaS, Functions-as-a-Service**), ahol nem kell szerverekkel foglalkozni, csak a futtatandó logikát adják meg, a háttér-infrastruktúrát pedig teljesen a szolgáltató menedzseli.

### **Mini-összehasonlítás (gyors fejtágító)**

| Modell   | Sebesség     | Kontroll | Üzemeltetés      | Tipikus példa            |
| -------- | ------------ | -------- | ---------------- | ------------------------ |
| **SaaS** | nagyon gyors | alacsony | minimális        | Microsoft 365            |
| **PaaS** | gyors        | közepes  | alacsony-közepes | App Service / Managed DB |
| **IaaS** | közepes      | magas    | magas            | VM-ek + saját stack      |

## **Telepítési modellek: public, private, hybrid, multi-cloud**

A másik fontos csoportosítás a **telepítési modellek** szerinti felosztás.

A **public cloud** a legelterjedtebb: ilyen esetben a szolgáltató infrastruktúráján több ügyfél osztozik logikai elkülönítéssel.

A **private cloud** ezzel szemben egy szervezet számára dedikált környezet, amely lehet saját adatközpontban vagy külső szolgáltatónál is, de a fő cél a **kontroll** és a **szabályozottság**, illetve sokszor a legacy rendszerekkel való kompatibilitás.

A **hybrid cloud** azt jelenti, hogy a szervezet egyszerre használ saját (**on-prem**) és public felhős rendszereket, és a kettő integráltan működik.

A **multi-cloud** pedig több felhőszolgáltató egyidejű használatát jelenti; ennek oka lehet üzleti kockázatcsökkentés, eltérő szolgáltatáselőnyök kihasználása vagy például földrajzi, jogi megfontolások.

## **Előnyök: gyorsaság, skálázás, modern szolgáltatások**

A felhő leggyakrabban említett előnyei közé tartozik a **gyorsaság** és a **rugalmasság**. Sok szervezet számára óriási előny, hogy nem kell hónapokig infrastruktúrát tervezni, beszerzést intézni és telepíteni; a környezet percek alatt felépíthető, és ugyanolyan gyorsan le is bontható.

A **méretezhetőség** szintén kulcselőny: ha egy webalkalmazás terhelése szezonálisan változik, a felhőben megoldható, hogy csúcsidőben több erőforrás álljon rendelkezésre, csendes időszakban pedig csökkenjen a kapacitás.

Emellett gyakran előny a **költségmodell** is: a klasszikus, nagy beruházásokat igénylő eszközbeszerzés (**CAPEX**) helyett sok esetben elszámolható, működési jellegű költség (**OPEX**) keletkezik, és a kiadások jobban igazíthatók a tényleges használathoz.

A felhő másik komoly értéke, hogy általában **„világszintű” építőkockákat ad**: több régióban elérhető szolgáltatásokat, terheléselosztást, tartalomkiszolgálást (**CDN**), magas rendelkezésre állású megoldásokat és **menedzselt** komponenseket, amelyek hagyományos környezetben jóval nagyobb mérnöki és üzemeltetési munkát igényelnének.

## **Hátrányok és kockázatok: lock-in, költségek, félrekonfigurálás**

A hátrányok és kockázatok között az első helyen gyakran a szolgáltatóhoz kötöttség (**vendor lock-in**) szerepel. Minél inkább speciális, egyedi szolgáltatói komponensekre épül egy rendszer, annál nehezebb lehet később átállni másik szolgáltatóra vagy visszahozni on-prem környezetbe.

Ugyanilyen fontos kockázat a költségek kiszaladása: a felhőben nagyon könnyű gyorsan erőforrásokat létrehozni, viszont ha nincs megfelelő kontroll, címkézési (**tagging**) rend, **budget alert** és folyamatos költségfigyelés, akkor meglepetések érhetik a szervezetet. Tipikus “rejtett” költség lehet például az **adatkiáramlás (egress)** díja vagy az elfelejtett, feleslegesen futó erőforrások költsége.

A harmadik nagy kockázati terület a **biztonság**: nem azért, mert a felhő „alapból” veszélyesebb lenne, hanem mert a komplexitás és a rengeteg konfigurációs lehetőség miatt könnyű hibázni. A felhős incidensek jelentős része gyakran rossz jogosultságokból, túl széles hozzáférésekből, nyitva felejtett erőforrásokból vagy nem megfelelő naplózásból ered.

## **Szabályozás és megfelelés: GDPR, NIS2 és ISO 27001 szemszögből (felhőhasználatnál)**

### **GDPR: szerepek, szerződések, adattovábbítás**

**GDPR** oldalról felhő esetén a kulcskérdés, hogy ki milyen szerepben van: a szervezet tipikusan **adatkezelő (controller)**, a felhőszolgáltató pedig **adatfeldolgozó (processor)** (szolgáltatástól függően lehet más is). Ilyenkor a GDPR elvárja, hogy a feldolgozás **szerződésen vagy más jogi aktuson** alapuljon (gyakorlatban tipikusan **DPA**), és külön szabályozza többek között az **alvállalkozók (sub-processorok)** bevonását is.

A gyakori félreértéssel szemben a GDPR általános szabályként **nem mondja ki**, hogy a személyes adatoknak „kötelezően EU-ban kell maradniuk”. Viszont az EU/EGT-n kívüli adattovábbításokat a GDPR **V. fejezete (Art. 44–50)** szigorúan szabályozza, és ilyen esetekben megfelelő jogalap és garanciák szükségesek; tipikus megoldás a **Standard Contractual Clauses (SCC)** alkalmazása, amelyeket az Európai Bizottság modernizált formában is közzétett.

Ezért választ sok szervezet felhőben **EU-régiót** és átlátható **adatrezidenciát**: nem „automatikus kötelezettségként”, hanem megfelelési és kockázatcsökkentési okból.

### **NIS2: kockázatkezelés, beszállítók, incidensjelentés**

**NIS2** oldalról a fókusz a szervezeti **kiberbiztonsági kockázatkezelési intézkedéseken**, a beszállítói/szolgáltatói lánc (a felhő is ide tartozik) kontrollján, valamint a jelentős incidensek **többlépcsős bejelentési kötelezettségén** van.

A NIS2 szerinti tipikus ütemezés: **24 órán belül előzetes jelzés (early warning)**, **72 órán belül incidens-értesítés**, majd **végső jelentés legkésőbb egy hónapon belül** (és szükség esetén köztes/progress jelentések).

Felhőhasználatnál ez a gyakorlatban azt is jelenti, hogy célszerű olyan szerződéses és üzemeltetési rendet kialakítani, amely biztosítja: a szolgáltató időben átadja a bejelentéshez szükséges információkat (érintett szolgáltatások, hatókör, naplók, állapot, helyreállítás).

### **ISO/IEC 27001: ISMS keret felhőre is (és miért hasznos)**

Az **ISO/IEC 27001** a világ egyik legismertebb szabványa az **információbiztonsági menedzsment rendszerre (ISMS)**: követelményeket ad arra, hogyan érdemes az információbiztonságot **kockázatalapon** megtervezni, bevezetni, fenntartani és folyamatosan fejleszteni.

Felhőhasználatnál az ISO 27001 gyakorlati értéke különösen abban látható, hogy segít **rendszerszinten** kezelni a felhővel járó kockázatokat (pl. hozzáférések, naplózás, incidenskezelés, üzletmenet-folytonosság, beszállítói kontrollok), és mindezt auditálható módon keretbe foglalni. Ezen belül kifejezetten jól “összeér” a dokumentum **Megosztott felelősség** fejezetével is: az ISO 27001 keretrendszerrel a megosztott felelősségi modellben szereplő felelősségek és kontrollok **leképezhetők**, dokumentálhatók és ellenőrizhetők (például policy-k, eljárások, szerződéses kontrollok, üzemeltetési bizonyítékok formájában).

### **ISO/IEC 27017 (felhőspecifikus kontrollok)**

Ha a cél kifejezetten felhőspecifikus kontrollok és „jó gyakorlatok” beemelése, akkor az **ISO/IEC 27017** nagyon jól illeszkedik az ISO 27001 mellé: **felhőszolgáltatások nyújtására és használatára** ad kiegészítő kontroll-útmutatást (az ISO/IEC 27002 kontrolljaira építve), és kifejezetten foglalkozik a **felhőszolgáltató** és a **felhőügyfél** oldalán értelmezett kontrollokkal és felelősségekkel.

### **ISO/IEC 27018 – GDPR-hoz különösen releváns (PII a public cloudban)**

A GDPR-kapcsolat miatt érdemes külön is kiemelni az **ISO/IEC 27018** szabványt, amely a **személyes adatok (PII) védelméhez** ad gyakorlati kontroll- és iránymutatás-készletet **public cloud** környezetben, tipikusan akkor, amikor a felhőszolgáltató **PII processor** szerepben jár el. Ez a fókusz miatt sok szervezetnél „természetes párja” az ISO 27001/27017 párosnak, ha a felhőben személyes adat is érintett.

Érdemes a verziószámot pontosan jelölni, mert az ISO/IEC 27018:2019 már visszavont kiadás, és jelenleg a 2025-ös verzió az aktuális.

### **Gyakorlati finomság: „tanúsított felhő” ≠ automatikus megfelelés**

Fontos gyakorlati különbség, hogy egy **ISO/IEC 27001 (és/vagy 27017/27018) szerint tanúsított** felhőszolgáltató választása valóban megkönnyítheti a megfelelést (mert sok alapkontroll a szolgáltatói oldalon már auditált módon működik), **de az ügyfél ettől még nem lesz “tanúsított” automatikusan**, és a saját környezetének megfelelő konfigurációjáért továbbra is felelős.

Gyakorlati következmény: az auditok és megfelelési ellenőrzések során a szolgáltatói tanúsítványok jellemzően **bemeneti bizonyítékok**, de a szervezetnek így is kell saját kontrollkészlet (IAM, naplózás, konfigurációmenedzsment, incidenskezelés, beszállítói szerződések, stb.).

### **Erőforrásigény (reális elvárások ISO 27001 esetén)**

Az ISO 27001 bevezetése és fenntartása tipikusan **nem “csak papírmunka”**: szervezeti oldalról időt és kapacitást igényel a kockázatkezelés, a szabályozók és eljárások kialakítása, a bizonyítékgyűjtés, a belső auditok, valamint a folyamatos fejlesztés miatt. Ez különösen igaz olyan szervezeteknél, amelyek korábban nem működtettek formális ISMS-t (Information Security Management System).

## **Megosztott felelősség: ki miért felel a felhőben?**

A felhőbiztonság megértéséhez különösen fontos a **megosztott felelősségi modell (shared responsibility model)**. Ennek lényege, hogy a szolgáltató felel a „felhőért” (az adatközpontok fizikai biztonságáért, a hardverért, az alap infrastruktúra stabil működéséért), de az ügyfél felel a „felhőben” lévő dolgokért (adatok, identitások és jogosultságok, logikai hálózati szabályok, konfigurációk, alkalmazásbiztonság).

A pontos határ attól függ, hogy **SaaS**, **PaaS** vagy **IaaS** szolgáltatásról van-e szó: SaaS esetén több felelősség marad a szolgáltatónál, IaaS esetén sokkal több kerül az ügyfél oldalára, például az operációs rendszer frissítése és **keményítése (hardening)**.

## **Gyakorlati fogalmak: régiók, zónák, hálózat, IAM, IaC**

A gyakorlatban a felhővel kapcsolatban érdemes néhány alapfogalmat is tisztán látni.

A nagy szolgáltatók **régiókra (region)** és azon belül elkülönített **rendelkezésre állási zónákra (availability zone)** osztják az infrastruktúrát; így lehetőség van arra, hogy az alkalmazások több zónában fussanak, és egyetlen zóna kiesése ne okozzon teljes leállást.

A felhőben a hálózat sem “adott”, hanem logikailag épül fel: jellemzően virtuális hálózatokat (**VPC/VNet**), alhálózatokat (**subnet**), útvonalakat, NAT-ot, gateway-eket és tűzfalszabályokat kell tervezni.

Szintén kulcstéma az **IAM (Identity and Access Management)**, vagyis hogy ki, hogyan és milyen feltételekkel érheti el az erőforrásokat. A modern felhőtervezésben gyakori az **infrastructure as code (IaC)** megközelítés is, amikor az infrastruktúrát kódból, deklaratív leírásból hozzák létre, így a környezet reprodukálható, verziózható és auditálható.

## **Nagy felhőszolgáltatók röviden (mit kínálnak?)**

Az alábbi lista nem teljes, de a leggyakrabban használt “nagy” szereplőket foglalja össze, nagyon röviden:

- **Amazon Web Services (AWS)**: rendkívül széles portfólió **compute**, **storage**, **adatbázis** és **serverless** szolgáltatásokkal, tipikusan sok “építőkockával” és finomhangolási lehetőséggel.

- **Microsoft Azure**: erős vállalati integráció (különösen Microsoft ökoszisztémában), széles körű termékkatalógussal, és kiemelt **serverless** lehetőségekkel (például **Azure Functions**).

- **Google Cloud (GCP)**: nagy termékkatalógus, erős adatplatform és felhő-natív képességek; a **serverless** irány és a menedzselt szolgáltatások hangsúlyosak.

- **Oracle Cloud Infrastructure (OCI)**: széles **IaaS és PaaS** katalógus, valamint “distributed cloud / multicloud” fókusz (például Azure-integrációs irányokkal), erős vállalati igényekre pozicionálva.

- **IBM Cloud**: felhős szolgáltatások mellett erős fókusz a **menedzselt Kubernetes** és vállalati/üzemeltetési eszközök irányába (különösen konténeres és hibrid környezeteknél).

- **OVHcloud**: európai szolgáltató, **Public Cloud** portfólióval (compute/storage/network) és **menedzselt Kubernetes** megoldással, gyakran “EU-s / szuverenitási” narratívával is.

## **Példák és összegzés: mikor éri meg a felhő?**

Példákon keresztül talán még jobban látszik, miért praktikus a felhő.

Egy tipikus vállalati webalkalmazás esetén a felhőben egyszerűen összerakható egy skálázható architektúra: **terheléselosztó (load balancer)** előtt fut több alkalmazásszerver, a statikus tartalmakat **CDN** szolgálja ki, az adatbázis **menedzselt** szolgáltatásként fut, és megfelelő monitorozás mellett az egész automatikusan méretezhető.

Ugyanígy, egy mentési és archiválási stratégia is könnyebben megvalósítható **objektumtárolóval**, valamint **életciklus-szabályokkal (lifecycle policies)**, amelyek a régebbi adatokat olcsóbb tárolási osztályba helyezik.

Fejlesztői oldalon pedig külön előny, hogy tesztkörnyezetek gyorsan létrehozhatók és törölhetők, ami költséget és időt spórolhat meg.

### Összegzés

Összességében a felhőszolgáltatások akkor a leghasznosabbak, ha gyorsan kell reagálni igényekre, ha változó terhelést kell kiszolgálni, vagy ha **menedzselt szolgáltatásokkal** szükséges csökkenteni az üzemeltetési terheket.

Ugyanakkor a felhő nem „magától” olcsó vagy „magától” biztonságos: a költségek kontrolljához és a biztonság fenntartásához tudatos tervezés, megfelelő **jogosultságkezelés**, **naplózás**, **monitorozás**, valamint jó folyamatok és felelősségi körök szükségesek.

A legjobb eredmény általában akkor születik, ha a szervezet pontosan meghatározza, milyen célra használ felhőt (milyen **szolgáltatási modellt** választ), milyen adatokat helyez oda (és milyen jogi/**compliance** feltételekkel), és már a bevezetés elején kialakítja a **költség- és biztonsági alapokat**.

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