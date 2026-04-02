# Agilis projektmenedzsment eszközei – kiberbiztonsági, SOC Analyst fókuszú tananyag

**Források és felhasznált eszközök:**

- [Training360](https://www.training360.com/), [Az agilitás alapkoncepciói tanfolyam](https://e-learning.training360.com/courses/az-agilitas-alapkoncepcioi), [Az agilis projektmenedzsment eszközei tanfolyam](https://e-learning.training360.com/courses/az-agilis-projektmenedzsment-eszkozei)

- [ChatGPT](https://chatgpt.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

A modern IT- és biztonsági környezetet ma már nem a ritka, nagy kiadások világa jellemzi, hanem a folyamatos változás. Új szolgáltatások jelennek meg, API-k módosulnak, logstruktúrák változnak, automatizmusok kerülnek be a működésbe, és mindezzel együtt a fenyegetési felület is átalakul. Egy SOC számára ez azt jelenti, hogy a biztonsági megfigyelés nem maradhat külön, a fejlesztéstől független utólagos tevékenység. A láthatóságot, a detekciót és a reagálást ugyanabban a ritmusban kell fejleszteni, ahogyan a rendszer is változik. Ebből a szempontból az agilis eszköztár nem pusztán projektmenedzsment-megoldás, hanem működési keret a gyors alkalmazkodáshoz, a visszacsatoláshoz és a folyamatos javításhoz.

## 1. Az agilis gondolkodás alapja: folyamatos fejlesztés és gyors visszacsatolás

Az agilis működés gyökere nem önmagában a Scrum vagy a Kanban, hanem egy régebbi szemlélet: a folyamatos fejlesztés. A Kaizen lényege, hogy a szervezet nem egyszeri, nagy átalakításokban gondolkodik, hanem kis lépésekben, rendszeres javításban. Ehhez szorosan kapcsolódik a PDCA-ciklus, vagyis a Plan–Do–Check–Act logika. Ennek üzenete egyszerű: tervezzünk, próbáljuk ki, ellenőrizzük az eredményt, majd a tanulságokat építsük be a következő körbe. Ez a gondolkodás a SOC világában különösen fontos, mert a detekciók, a playbookok, a logolási szabályok és a reagálási eljárások ritkán lesznek elsőre tökéletesek. A jó működés abból születik, hogy a csapat gyorsan tanul, mér, majd javít.

A Lean ehhez rendszerszintű szemléletet ad. A központi kérdés az, hogy mi teremt valódi értéket, és mi számít pazarlásnak. Lean környezetben a cél több értéket létrehozni kevesebb erőforrással és kevesebb fölösleges tevékenységgel. Ez nem csak költségcsökkentést jelent, hanem fókuszt is: a csapatoknak érdemes azt a munkát előnyben részesíteniük, amely ténylegesen javítja az ügyfélélményt, a működést vagy a kockázati helyzetet. SOC oldalról nézve pazarlás lehet például a túl zajos riasztás, a rosszul strukturált log, a fölösleges kézi lépés, vagy az olyan ticket, amelyből nem derül ki egyértelműen, mi a teendő. A Lean tehát nem elméleti háttér, hanem a SOC mindennapi minőségjavításának egyik legerősebb alapja.

## 2. Miért került előtérbe az agilis működés?

A hagyományos, vízieséses megközelítés a munkát egymás után következő szakaszokra bontja: követelményfelmérés, tervezés, megvalósítás, tesztelés, átadás. Ez akkor működik jól, ha a környezet viszonylag stabil, a változások ritkák, és a kezdeti követelmények hosszabb ideig érvényesek maradnak. A mai digitális rendszerek többségénél azonban a valóság ennél sokkal mozgékonyabb. Ha a visszajelzés csak későn érkezik meg, akkor a hibák, félreértések és hiányzó biztonsági szempontok kijavítása drága és lassú lesz. Az agilis működés erre a problémára ad választ: rövidebb ciklusokkal, gyakoribb ellenőrzéssel és gyorsabb alkalmazkodással.

A szoftverprojektek nehézségeire sokszor a Standish Group CHAOS jelentéseit szokás felhozni, mert ezek régóta hivatkozott iparági jelzések arról, hogy sok projekt csak részben teljesíti a céljait, vagy jelentős eltéréssel zárul. Ugyanakkor fontos szakmailag korrekt módon kezelni ezt a témát: a CHAOS jelentések kategóriái és következtetései több kutatás szerint vitathatók, ezért ezekre inkább figyelmeztető iparági jelzésként érdemes tekinteni, nem megdönthetetlen statisztikai igazságként. A lényeg nem a pontos szám, hanem az üzenet: a hosszú, merev, későn visszacsatoló működés kockázatos.

## 3. Az Agilis Kiáltvány üzenete

Az Agilis Kiáltvány nem módszertan, hanem értékrend. Azt mondja ki, hogy a sikeres szoftverfejlesztésben bizonyos dolgokat előrébb kell sorolni: az emberek és az együttműködés fontosabbak, mint a túlzottan merev folyamatok; a működő megoldás fontosabb, mint a túlburjánzó dokumentáció; az ügyféllel való együttműködés fontosabb, mint a szerződés körüli alkudozás; a változásra való reagálás fontosabb, mint egy terv merev követése. Az alapelvek ehhez hozzáteszik a gyakori szállítást, a rövid visszacsatolást, a technikai kiválóságot, a fenntartható tempót és a rendszeres önreflexiót.

SOC nézőpontból ennek nagyon gyakorlati jelentése van. Nem elég azt mondani, hogy a rendszer „elkészült”, ha közben a naplózás hiányos, a detekció vakfoltos, vagy az incidens esetén nem követhető vissza, mi történt. A biztonsági láthatóságot is ugyanúgy működő eredménynek kell tekinteni, mint magát a funkciót. Ha egy új szolgáltatás fut, de a SOC nem látja a kulcseseményeket, akkor valójában még nincs teljes értékűen átadva. Ezért az agilis értékrend a SOC számára nem elmélet, hanem napi működési elv.

## 4. Scrum: hogyan ad ritmust a munkának?

A Scrum egy konkrét keretrendszer. A 2020-as Scrum Guide szerint a Scrum Team három elszámoltathatósági területből áll: Product Owner, Scrum Master és Developers. A csapat együtt felel azért, hogy minden sprint végén értékes, használható inkrementum jöjjön létre. A sprint fix hosszúságú időkeret, legfeljebb egy hónap, amelyen belül a csapat tervez, dolgozik, ellenőriz és alkalmazkodik.

A Scrum eseményei nem adminisztratív kötelező körök, hanem ellenőrzési pontok. A Sprint Planning során a csapat eldönti, min dolgozik. A Daily Scrum rövid napi szinkron a haladásról és az akadályokról. A Sprint Review célja a bemutatás és a visszajelzés, a Sprint Retrospective pedig a működés javítása. SOC szemmel nézve ezek mind fontos kapcsolódási pontok. A refinement és a planning ideális hely arra, hogy a logolási és monitorozási igények még időben bekerüljenek a munkába. A review jó alkalom annak ellenőrzésére, hogy az új funkció tényleg termel-e használható telemetriát. A retrospective pedig arra szolgál, hogy a hiányosságokból tanulás legyen.

Fontos különbséget tenni a régebbi és az újabb Scrum szóhasználat között. A régebbi Scrum Guide még külön Development Teamként beszélt a fejlesztői oldalról, a jelenlegi megfogalmazás viszont a Scrum Team egységét hangsúlyozza, és ezen belül definiálja a Developers szerepkörét. A gyakorlati tanulság ugyanaz: a fejlesztői munka nem külön miniszervezet, hanem a közös sprintcél része. Ez SOC oldalról azért lényeges, mert a biztonsági telemetria és a detekciós támogatás sem „külső mellékmunka”, hanem a termékminőség része.

## 5. Backlog, user story, átvételi kritériumok és kész definíció

A backlog az agilis működés egyik legfontosabb eleme. Ez a priorizált munkalista, amelyből a csapat dolgozik. A backlog nem puszta feladathalmaz, hanem annak lenyomata, hogy mi számít most fontosnak. SOC nézőpontból ez kulcsfontosságú, mert a megfigyelt hiányosságok, incidensek utáni tanulságok, logolási igények, detekciós fejlesztések és automatizációs ötletek csak akkor jutnak el a megvalósításig, ha konkrét backlog-elemmé válnak. A backlog tehát a SOC tapasztalatainak végrehajtható formája.

A user story egy gyakori megfogalmazási forma, amely segít abban, hogy a kérés ne technikai töredék legyen, hanem üzleti vagy működési céllal együtt jelenjen meg. SOC-ban sok backlog-tétel valójában nem funkcionális követelmény: auditlog, naplómező, korrelációs információ, trace-elhetőség, riasztási feltétel vagy automatizáció. Ilyen esetben is hasznos történetként gondolkodni, mert ettől tisztább lesz, kinek mire van szüksége és miért. Például: „Mint SOC elemző, szeretném, ha minden jogosultságmódosítás külön audit eseményként jelenne meg, hogy rendellenes adminisztrátori aktivitás esetén gyorsan vissza tudjuk követni a változásokat.”

Az Acceptance Criteria azt rögzíti, milyen feltételek teljesülése esetén fogadható el egy backlog-elem. A Definition of Done ennél tágabb: azt írja le, mitől tekint a csapat valamit valóban késznek. A Scrum Guide szerint az inkrementumhoz kapcsolódó commitment a Definition of Done. SOC-környezetben a jó DoD gyakran tartalmazza azt is, hogy a kulcsesemények naplózódnak, a szükséges mezők rendelkezésre állnak, a log eljut a központi gyűjtőbe vagy a SIEM-be, és szükség esetén a hozzá kapcsolódó detekció vagy dashboard is frissült. Ezzel szemben a Definition of Ready nem hivatalos Scrum elem, hanem kiegészítő gyakorlat: azt segíti, hogy a csapat ne félkész, zavaros tételeket húzzon be a sprintbe.

## 6. Priorizálás SOC környezetben

A priorizálás a SOC-ban nem pusztán üzleti kényelmi kérdés. Itt a sorrendet gyakran a kockázat, a kitettség, az időkritikusság és a potenciális hatás határozza meg. Egy internet felől elérhető rendszer hiányzó auditlogja, egy aktívan kihasználható sérülékenységhez kapcsolódó detekció, vagy egy magas jogosultságú fiók anomáliájának monitorozása jellemzően előrébb kerül, mint egy kevésbé kockázatos finomhangolás. Az agilis működés itt abban segít, hogy ez a változó sorrend ne kaotikus legyen, hanem látható és indokolható.

A jó priorizálás egyik fontos eleme az indoklás. Nem kell minden tickethez hosszú esszé, de hasznos röviden rögzíteni, miért sürgős egy tétel: aktív fenyegetés, auditkövetelmény, magas üzleti kockázat, ismétlődő false positive, hiányzó attribúció vagy lassú incidensvizsgálat. Ez később megkönnyíti a döntések visszakövetését, és segít abban is, hogy a fejlesztői, üzemeltetői és biztonsági oldalak ugyanazt értsék a prioritás mögött.

## 7. Kanban és a folyamatos áramlás

A Kanban különösen jól illeszkedik a SOC működéséhez, mert a SOC munkája jellemzően nem sprintekben érkezik, hanem folyamatosan. A Kanban alapgondolata a munka vizualizálása, a folyamatban lévő munka korlátozása, a szabályok láthatóvá tétele, a flow aktív menedzselése és a visszacsatolási hurkok beépítése. A WIP limitek azért fontosak, mert arra ösztönzik a csapatot, hogy ne újabb és újabb ügyeket kezdjen el, hanem vigye is végig a már megnyitott munkát.

SOC-ban egy Kanban tábla tipikus oszlopai lehetnek például: beérkezett, triage, kivizsgálás, containment, handoff vagy javítás alatt, validáció, lezárva. Ez a vizualizáció nem csupán státuszkövetés. Segít észrevenni, hol torlódik a munka, hol kevés a kapacitás, mely ponton sok a várakozás, és hol keletkezik túl sok félkész ügy. A WIP limitek különösen hasznosak ott, ahol az elemzők hajlamosak párhuzamosan túl sok esetet futtatni, mert ez széttördeli a figyelmet, növeli az átadási hibák esélyét és lassítja a lezárást.

A Kanban flow-szemlélete jól kombinálható a Scrum ritmusával is. Erre külön útmutató is létezik Scrum csapatok számára. A gyakorlati üzenet az, hogy a Scrum adhat ütemet és ellenőrzési pontokat, miközben a Kanban segíthet a munka áramlásának javításában. SOC környezetben ez különösen hasznos ott, ahol vannak sprintben megvalósuló fejlesztések és közben állandó operatív eseményáramlás is.

## 8. Logolás és monitorozás: a láthatóság beépítése

A SOC számára a logolás nem melléktermék, hanem az észlelés nyersanyaga. Egy új funkció, új szolgáltatás vagy új integráció bevezetése biztonsági szempontból csak akkor tekinthető teljesnek, ha az események megfelelően naplózódnak, értelmezhetők, kereshetők és összekapcsolhatók. Ha ez hiányzik, akkor a SOC nem tud különbséget tenni legitim és gyanús aktivitás között, és nem tud gyorsan reagálni incidens esetén. Agilis környezetben ezért a logolási követelményeket nem szabad a fejlesztés végére hagyni. A telemetria tervezése a terméktervezés része.

A jó logolási követelmény konkrét. Nem azt mondja, hogy „kell több log”, hanem megnevezi, mely eseményekre van szükség és milyen minimális mezőkkel. Ilyen kulcsinformáció lehet például a felhasználó azonosítója, az időbélyeg, a forrás IP, a kliens típusa, az érintett erőforrás, a művelet eredménye, a hibakód vagy a session azonosító. Minél jobban strukturált a log, annál gyorsabb és megbízhatóbb a keresés, korreláció és kivizsgálás. SOC-szempontból a cél nem pusztán a naplózás növelése, hanem az, hogy a naplók valódi detekciós és vizsgálati értéket adjanak.

## 9. Detection engineering és backlog-alapú fejlesztés

A detection engineering nem külön sziget, hanem a SOC egyik legfontosabb fejlesztési ága. Ide tartozik az új szabályok építése, a meglévők finomhangolása, a hamis pozitívok csökkentése, a hiányzó észlelési pontok pótlása és a korrelációk javítása. Agilis működésben ezek akkor lesznek kezelhetők, ha backlog-elemként jelennek meg, becsülhetők, priorizálhatók és visszamérhetők. Egy rosszul működő riasztás nem „örök adottság”, hanem javítandó termékelem.

Jó példa erre, amikor egy vizsgálat során kiderül, hogy egy kulcsmező hiányzik a logból, és emiatt nem lehet gyorsan elkülöníteni a legitim adminisztrátori tevékenységet a gyanús műveletektől. Ilyenkor a SOC feladata nem csak a panasz megfogalmazása, hanem a technikai igény backlogba fordítása. A jó backlog-elem megmondja, milyen új mezőre vagy eseményre van szükség, milyen detekciót tesz ez lehetővé, és hogyan ellenőrizhető majd az eredmény. Ezzel a SOC a fejlesztési folyamat nyelvén kezd beszélni, ami jelentősen javítja az együttműködést.

## 10. DevSecOps és CI/CD nézőpontból

A DevSecOps lényege nem pusztán az, hogy a biztonság „hamarabb” jelenik meg, hanem az, hogy a biztonsági kontrollok a változási folyamatba épülnek be. SOC oldalról ebben két terület különösen fontos. Az egyik az alkalmazás- és infrastruktúra-telemetria folyamatos bekötése a központi megfigyelésbe. A másik a pipeline-események, deployok, konfigurációváltozások és buildfolyamatok láthatóvá tétele. Ha egy anomália egy friss kiadással esik egybe, sokkal gyorsabban eldönthető, hogy konfigurációs hiba, hibás release vagy támadói aktivitás áll-e a háttérben, ha ezek az információk naplózva és kereshetően rendelkezésre állnak.

A pipeline önmagában is detekciós felület lehet. Szokatlan időben indított kiadás, váratlan környezetre történő telepítés, ismeretlen felhasználó vagy szolgáltatásfiók általi változtatás, sikertelen majd ismételt futások, jogosultság-emelkedéssel járó buildlépések mind olyan jelek, amelyek SOC szemmel relevánsak lehetnek. Ezért a CI/CD telemetria nem csak üzemeltetési adat, hanem biztonsági információ is.

## 11. A SOC helye az agilis eseményekben

A SOC akkor tud igazán értéket adni, ha nem csak incidensnél kapcsolódik be, hanem a változásfolyamat természetes része lesz. A backlog-refinement során lehet pontosítani a logolási, monitorozási és auditkövetelményeket. A planning során lehet eldönteni, mely biztonsági vagy láthatósági igény kerül be ténylegesen a következő ciklusba. A review ideális pont annak ellenőrzésére, hogy az új funkció valóban kibocsátja-e a szükséges eseményeket, és ezek valóban megjelennek-e a megfigyelőrendszerben. A retrospective pedig lehetőséget ad arra, hogy egy incidens vagy elhúzódó vizsgálat tanulságai ne vesszenek el.

Ebből következik, hogy a SOC számára az agilis események nem idegen meetingek, hanem olyan munkapontok, ahol a biztonsági szempontok költséghatékonyan beépíthetők. Minél később derül ki, hogy egy fontos esemény nincs naplózva vagy egy kulcsdetekció hiányzik, annál drágább lesz a javítás. A korai bekapcsolódás tehát nem adminisztratív igény, hanem hatékonysági és kockázatcsökkentési kérdés.

## 12. Incidenskezelés, post-mortem és visszacsatolás

A jó SOC nem csak reagál az incidensekre, hanem tanul is belőlük. A post-incident review vagy post-mortem célja nem a bűnbakkeresés, hanem annak feltárása, hogy mi látszott, mi nem látszott, mi működött jól, hol volt késés, és hogyan lehet a rendszert ellenállóbbá tenni. Agilis környezetben akkor van valódi értéke a post-mortemnek, ha a tanulságok backlog-elemmé válnak. Egy hiányzó alert új detekcióvá alakul, egy túl zajos szabály tuningfeladattá, egy gyenge attribúció plusz logmező igénnyé, egy bizonytalan átadás pedig playbook-frissítéssé.

Ez a ciklus nagyon közel áll a Kaizen és PDCA logikájához. Az incidens után a szervezet nem egyszerűen dokumentál, hanem javít. A tanulság nem melléklet, hanem fejlesztési input. Ez az a pont, ahol az agilis működés és a SOC szemlélet a legerősebben találkozik.

## 13. Skálázott működés: amikor már több csapat dolgozik együtt

Amikor egy szervezetben már több csapat dolgozik ugyanazon a terméken vagy szolgáltatási láncon, megjelenik a skálázás kérdése. Itt a fő probléma a függőségek, a koordináció és az egységes irány megtartása úgy, hogy közben ne fulladjon minden bürokráciába. A LeSS egyik alapelve, hogy egy terméken több csapat is dolgozhat közös Product Backlogból, tehát nem csapatonként külön backlogból. Ez segíti a közös prioritáskezelést és a teljes termékre vonatkozó gondolkodást.

A SAFe másképp közelít: az Agile Release Train fogalmával több agilis csapat összehangolt, tartós együttműködését szervezi közös vízió és ütemezés mentén. Ez nagyvállalati környezetben hasznos lehet, ha sok a függőség, a közös architektúra és a koordinálandó szállítás. SOC szempontból a lényeg nem az, hogy egy szervezet melyik keretrendszert használja, hanem az, hogy a biztonsági láthatóság, a közös standardok és a kockázati prioritások ne essenek szét csapatonként.

A nagyobb szervezetekben külön szerepet kaphatnak a tudás- és standardközpontok is. A Center of Excellence tipikusan olyan szakértői csoport, amely vezetést, tudásmegosztást, coachingot és közös mintákat biztosít egy adott területen. Ezzel szemben a guild, chapter vagy community of practice inkább szakmai hálózat: segíti a tudás terjedését, a közös nyelv kialakulását és a minták újrafelhasználását. Fontos azonban tudni, hogy ezek nem egységes szabványok, hanem szervezeti minták. A Spotify maga is hangsúlyozta, hogy a saját modelljét nem kész receptként, hanem fejlődésben lévő kultúraként mutatta be.

## 14. Milyen kompetenciák kellenek egy SOC Analystnak agilis környezetben?

Agilis környezetben a jó SOC Analyst nem csak riasztásokat elemez, hanem érti a változás ritmusát is. Szüksége van alapvető agilis fogalmi tudásra: backlog, sprint, Kanban, WIP, review, retrospective, Definition of Done. Emellett értenie kell a logolás, a telemetria, a parsing, a korreláció és a detekció gyakorlati oldalát. Tudnia kell azt is, hogyan kell egy biztonsági hiányosságot fejleszthető, ellenőrizhető követelménnyé fordítani.

Ugyanilyen fontos a kommunikáció. A SOC akkor tud jól együttműködni a fejlesztői és üzemeltetői oldallal, ha nem általánosságban kér „több logot”, hanem pontosan megfogalmazza, mire van szüksége, miért fontos, milyen kockázatot csökkent, és hogyan fogja ellenőrizni az eredményt. Ez a gyakorlat a ticketingben, a backlog-elemek megírásában, a refinement során feltett kérdésekben és az incidens utáni visszacsatolásban is megjelenik. A technikai tudás és a működési gondolkodás együtt tesz valakit igazán hatékony SOC elemzővé.

## 15. Rövid működési checklist SOC csapatoknak

Új funkció vagy szolgáltatás esetén mindig érdemes ellenőrizni, hogy megvannak-e a minimális naplózási események, a szükséges mezők, és az adatok ténylegesen eljutnak-e a központi loggyűjtőbe vagy a SIEM-be. Nem elég az, hogy a fejlesztő szerint „ír logot”; a SOC számára az számít, hogy a log értelmezhető, kereshető és használható-e.

Incidens vagy majdnem-incidens után rövid értékelést kell készíteni, és a tanulságokat konkrét backlog-elemekké kell alakítani. Ha valami hiányzott a láthatóságból, azt ne jegyzetként őrizzük meg, hanem fejlesztési feladatként vigyük tovább.

A napi működésben hasznos, ha a SOC látja a friss változásokat is: deployok, konfigurációmódosítások, új integrációk, új logforrások. Ez jelentősen gyorsíthatja annak eldöntését, hogy egy anomália rendszerváltozás vagy támadói aktivitás következménye.

A biztonsági együttműködés akkor érett, ha a SOC rendszeresen jelen van a megfelelő kapcsolódási pontokon, és vannak kijelölt szakmai hidak a csapatok között, például security championok, közös review-k vagy tudásmegosztó közösségek.

## Összegzés

Az agilis működés SOC nézőpontból nem divatszó, hanem gyakorlati válasz a gyorsan változó rendszerek problémájára. A Kaizen, a PDCA és a Lean a folyamatos javítás gondolkodását adják. Az Agilis Kiáltvány az értékrendet adja meg: gyors visszacsatolás, együttműködés, alkalmazkodás. A Scrum ritmust és ellenőrzési pontokat ad, a Kanban pedig flow-szemléletet és kapacitásvédelmet. A backlog teszi végrehajthatóvá a tanulságokat, a Definition of Done teszi teljessé a minőségi elvárást, a post-mortem pedig új fejlesztési inputot ad. Mindez együtt teszi lehetővé, hogy a SOC ne csak reagáljon az eseményekre, hanem folyamatosan javítsa a láthatóságot, a detekciót és a reagálási képességet.

# Fogalomtár

**Agilitás** – Olyan működési szemlélet, amely gyors visszacsatolással, rövid ciklusokkal és rugalmas alkalmazkodással támogatja az értékteremtést.

**Kaizen** – Folyamatos, kisléptékű fejlesztésre épülő szemlélet, amely a napi működés állandó javítását helyezi előtérbe.

**PDCA** – A Plan–Do–Check–Act ciklus rövidítése; tervezésből, kipróbálásból, ellenőrzésből és beépítésből álló fejlesztési hurok.

**Lean** – Olyan gondolkodásmód, amely a vevő számára értékes tevékenységekre fókuszál, és csökkenti a pazarlást.

**Waterfall / víziesés** – Szakaszos megközelítés, amely egymást követő fázisokra bontja a munkát, és kevésbé alkalmas a gyors változások kezelésére.

**Agilis Kiáltvány** – Az agilis működés alapértékeit és alapelveit összefoglaló nyilatkozat.

**Scrum** – Iteratív keretrendszer, amely sprintalapú ritmust, közös felelősséget és meghatározott eseményeket ad a munkának.

**Scrum Team** – A Product Ownerből, Scrum Masterből és Developers szerepkörből álló közös csapat.

**Sprint** – Fix időkeretű munkaciklus, amelyben a csapat egy sprintcél mentén értékes inkrementumot hoz létre.

**Product Owner** – Az a szerepkör, amely a termék értékének maximalizálásáért és a backlog prioritásáért felel.

**Scrum Master** – A Scrum működését támogató szerepkör, amely segíti a csapatot és a szervezetet a keretrendszer helyes alkalmazásában.

**Developers** – A Scrum Team azon tagjai, akik a sprintcél teljesítéséhez szükséges megoldásokat létrehozzák.

**Backlog** – Priorizált munkalista, amelyből a csapat dolgozik. SOC-környezetben ide kerülhetnek incidensekből származó tanulságok, logolási igények és detekciós fejlesztések is.

**User story** – Rövid, célorientált megfogalmazás egy igényről, amely megmutatja, kinek mire van szüksége és miért.

**Acceptance Criteria** – Konkrét átvételi feltételek, amelyek alapján eldönthető, hogy egy backlog-elem elfogadható-e.

**Definition of Done** – Közös minőségi megállapodás arról, mitől tekinthető egy inkrementum valóban késznek.

**Definition of Ready** – Nem hivatalos Scrum-elem; olyan helyi kritériumrendszer, amely segíti annak eldöntését, hogy egy backlog-elem elég tiszta-e a sprintbe húzáshoz.

**Kanban** – Flow-alapú munkaszervezési módszer, amely vizualizálja a munkát és korlátozza a párhuzamosan futó feladatokat.

**WIP limit** – A folyamatban lévő munka felső korlátja; segít megőrizni a fókuszt és javítani az átfutást.

**Flow** – A munka áramlása a folyamaton keresztül a beérkezéstől a lezárásig.

**SOC** – Security Operations Center; a biztonsági megfigyelésért, észlelésért, reagálásért és folyamatos fejlesztésért felelős funkció.

**Telemetria** – Minden olyan napló, esemény, metrika vagy nyomkövetési adat, amelyből a rendszer működése és a biztonsági jelzések megfigyelhetők.

**Logforrás** – Olyan rendszer vagy komponens, amely naplóadatot termel, például alkalmazás, API gateway, identitáskezelő vagy CI/CD pipeline.

**SIEM** – Központi naplógyűjtő és elemző rendszer, amely támogatja a keresést, korrelációt és riasztásképzést.

**Detection engineering** – A detekciós szabályok, korrelációk és észlelési logikák tervezése, fejlesztése és finomhangolása.

**False Positive** – Téves riasztás; olyan jelzés, amely végül nem valódi biztonsági eseményhez kapcsolódik.

**False Negative** – Elmaradt észlelés; olyan valós esemény, amelyre a rendszer nem adott jelzést.

**Triage** – Gyors elsődleges besorolás, amely eldönti, mennyire súlyos az esemény és mi legyen a következő lépés.

**Incident** – Olyan biztonsági esemény, amely vizsgálatot, reagálást vagy beavatkozást igényel.

**Playbook / Runbook** – Lépésről lépésre követhető eljárás egy adott típusú esemény kezelésére.

**DevSecOps** – Olyan működési megközelítés, amely a biztonságot a fejlesztési és üzemeltetési folyamatokba integrálja.

**CI/CD** – Folyamatos integrációt és folyamatos szállítást vagy telepítést támogató folyamat- és automatizációs gyakorlat.

**Post-mortem / post-incident review** – Incidens utáni értékelés, amelynek célja a tanulságok feltárása és backlog-elemmé alakítása.

**LeSS** – Skálázási megközelítés, amely több csapat közös Product Backlogból történő munkáját hangsúlyozza.

**SAFe** – Nagyvállalati skálázási keretrendszer, amely több csapat összehangolt értékszállítását támogatja.

**Agile Release Train** – A SAFe egyik központi fogalma; tartósan együttműködő, közös célokra szervezett agilis csapatok együttese.

**Center of Excellence (CoE)** – Olyan szakértői központ, amely tudást, standardokat, coachingot és szakmai irányt ad egy szervezetben.

**Guild / Chapter / Community of Practice** – Olyan szakmai közösségek vagy szervezeti minták, amelyek a tudásmegosztást és a közös gyakorlatok terjedését segítik. Nem egységes szabványok, hanem alkalmazott szervezeti megoldások.

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
