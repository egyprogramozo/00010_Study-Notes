# AI Mindenkinek (AI For Everyone)

Az AI For Everyone (Coursera) kurzus tananyaga alapján készült ez a fogalomtár, amit azért állítottam össze, hogy könnyebbé tegye a tanulást és az ismétlést.

**Források és felhasznált eszközök:**

- [AI For Everyone - DeepLearning.AI](https://www.coursera.org/learn/ai-for-everyone)
- [ChatGPT](https://chatgpt.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

## Fogalomtár

**Mesterséges intelligencia (Artificial Intelligence, AI)** – Gyűjtőfogalom minden olyan számítógépes módszerre, amely valamilyen emberi intelligenciához kapcsolódó feladatot utánoz vagy automatizál. Az AI nagyon erős lehet jól körülhatárolt feladatokban, de nem képes minden problémát megoldani.

**Szűk mesterséges intelligencia (Artificial Narrow Intelligence, ANI)** – Olyan AI-rendszer, amely egy konkrét feladatra specializálódik. Ilyen például a spam-szűrő, a beszédfelismerő vagy egy önvezető autó egyes moduljai.

**Általános mesterséges intelligencia (Artificial General Intelligence, AGI)** – Elméleti cél, amely szerint a gép bármilyen értelmi feladatot el tudna végezni, amit egy ember is. Ettől még messze vagyunk, ezért a vele kapcsolatos túlzó félelmek sokszor félreértésből erednek.

**Generatív AI (Generative AI)** – Olyan AI, amely új tartalmat hoz létre, például szöveget, képet vagy hangot. Ide tartoznak a nagy nyelvi modellekre épülő rendszerek is, amelyek emberhez hasonló szöveget tudnak generálni.

**Gépi tanulás (Machine Learning)** – Az AI egyik legfontosabb ága, amelyben a rendszer adatokból tanul meg mintázatokat. A cél jellemzően az, hogy egy bemenetből helyes kimenetet állítson elő anélkül, hogy minden szabályt kézzel programoznánk le.

**Felügyelt tanulás (Supervised Learning)** – Olyan gépi tanulási módszer, ahol a modell ismert bemenet–kimenet párokból tanul. Ez a modern AI egyik legfontosabb alapja, és sok gyakorlati alkalmazás erre épül.

**Felügyelet nélküli tanulás (Unsupervised Learning)** – Olyan tanulási megközelítés, ahol a rendszernek nincs előre megadott helyes címkéje vagy válasza. Ilyenkor a modell az adatok szerkezetét, csoportjait vagy rejtett mintáit próbálja felismerni.

**Megerősítéses tanulás (Reinforcement Learning)** – Olyan tanulási módszer, amelyben egy ügynök próbálkozások és visszajelzések alapján tanul jó döntéseket hozni. Jutalom vagy büntetés alapján javítja a viselkedését.

**Mélytanulás (Deep Learning)** – A gépi tanulás egyik legerősebb alága, amely többrétegű neurális hálókat használ. Különösen hasznos nagy mennyiségű adat esetén, például képfelismerésnél, hangfeldolgozásnál vagy nyelvi modelleknél.

**Neurális hálózat (Neural Network)** – Sok összekapcsolt számolóegységből álló matematikai modell. Sok egyszerű „legókocka” összekapcsolását, amelyek együtt nagyon összetett összefüggéseket tudnak megtanulni.

**Neuron (Neuron)** – A neurális háló legkisebb alapegysége. Egy egyszerű matematikai műveletet végez, de sok ilyen egység együtt már bonyolult viselkedést tud kialakítani.

**Nagy nyelvi modell (Large Language Model, LLM)** – Olyan modell, amely hatalmas mennyiségű szövegből tanulja meg, milyen szavak következnek egymás után. Ennek köszönhetően tud értelmesnek tűnő, folyékony szöveget létrehozni.

**Prompt (Prompt)** – A felhasználó által megadott kezdő utasítás vagy szöveg, amelyre a generatív modell válaszol. A modell ezt használja kiindulópontként a folytatáshoz vagy a válasz előállításához.

**Bemenet (Input)** – Az az adat, amit a modell megkap feldolgozásra. Ez lehet szöveg, kép, hangfelvétel, szenzoradat vagy táblázatos adat.

**Kimenet (Output)** – Az az eredmény, amit a modell előállít a bemenet alapján. Ez lehet címke, becslés, fordítás, felismerés vagy generált tartalom.

**A→B leképezés (A-to-B Mapping)** – Egy fogalma arra, hogy a modell megtanulja, milyen kimenet tartozik egy adott bemenethez. Ez a gépi tanulás legegyszerűbb és legfontosabb szemléleti modellje.

**Adat (Data)** – Minden olyan információ, amelyből a modell tanulni vagy dolgozni tud. Az adat lehet strukturált, például táblázat, vagy nem strukturált, például kép, szöveg vagy hang.

**Adatkészlet / adathalmaz (Dataset)** – Az adatok rendezett gyűjteménye, amelyből a modell tanul vagy amelyet elemzésre használunk. Minősége és relevanciája alapvetően meghatározza az eredményt.

**Strukturált adat (Structured Data)** – Táblázatos, jól szervezett adat, amely oszlopokból és sorokból áll. Ilyen például egy adatbázis vagy Excel-tábla, ahol a mezők jelentése egyértelmű.

**Nem strukturált adat (Unstructured Data)** – Olyan adat, amely nem klasszikus táblázatos formában jelenik meg. Ilyen a kép, a hang és a szabad szöveg, amelyek feldolgozása általában nehezebb.

**Adatcímkézés / annotálás (Data Labeling / Annotation)** – Az a folyamat, amikor emberek vagy eszközök megjelölik, hogy egy adott adat mit tartalmaz. Például képeken bejelölik az autókat vagy megadják, hogy egy hangfelvételen milyen szó hangzik el.

**Adatminőség (Data Quality)** – Annak mértéke, hogy az adat mennyire pontos, teljes és használható. A rossz adat gyenge modellt eredményez, még akkor is, ha az algoritmus önmagában jó.

**„Szemét be, szemét ki” elv (Garbage In, Garbage Out)** – Azt fejezi ki, hogy hibás vagy zajos adatokból hibás eredmény születik. Ez az AI-projektek egyik legalapvetőbb gyakorlati tanulsága.

**Adattisztítás (Data Cleaning)** – A hibás, hiányos vagy téves adatok javítása, eltávolítása vagy kezelése. Ez sokszor az AI- és data science-projektek egyik legfontosabb előkészítő lépése.

**Adattudomány (Data Science)** – Olyan terület, amely az adatokból üzleti vagy működési felismeréseket nyer ki. Nem feltétlenül futó AI-rendszert hoz létre, hanem döntéstámogató következtetéseket.

**Modellbetanítás (Model Training)** – Az a folyamat, amikor a modell az adatok alapján megtanulja az összefüggéseket. Ez ritkán sikerül elsőre jól, ezért általában sok ismétlés és finomítás szükséges.

**Bevezetés / üzembe helyezés (Deployment / Deploy)** – A már betanított modell valódi környezetbe helyezése. Ekkor derül ki igazán, hogy a rendszer mennyire működik jól a gyakorlatban.

**Iteráció (Iteration)** – Ismétlődő fejlesztési ciklus, amelyben a csapat új adatokat gyűjt, módosítja a modellt, majd újra tesztel. Az AI-projektek szinte mindig iteratív módon fejlődnek.

**Technikai átvilágítás (Technical Diligence)** – Annak előzetes felmérése, hogy egy AI-projekt technikailag megvalósítható-e. Ilyenkor megvizsgálják a rendelkezésre álló adatokat, a bemenet–kimenet kapcsolatot és a feladat nehézségét.

**Data science munkafolyamat (Data Science Workflow)** – Jellemzően adatgyűjtésből, elemzésből és cselekvési javaslatok kialakításából áll. A cél itt nem mindig egy modell, hanem a jobb döntéshozatal.

**Gépi tanulási munkafolyamat (Machine Learning Workflow)** – Tipikus lépései az adatgyűjtés, a modell betanítása és a bevezetés. Ez a háromlépéses logika sok különböző AI-rendszerre alkalmazható.

**Beszédfelismerés (Speech Recognition)** – Olyan AI-feladat, ahol a rendszer hangfelvételből szöveget vagy parancsot állapít meg. Jó példa arra, hogyan tanul a modell hangmintákból.

**Számítógépes látás (Computer Vision)** – Olyan terület, ahol a gép képekből vagy videókból próbál információt kinyerni. Ide tartozik például az objektumfelismerés, az arcfelismerés és a képi hibadetektálás.

**Objektumfelismerés (Object Detection)** – Olyan feladat, amikor a modell nemcsak felismeri, hogy mi van a képen, hanem azt is, hogy hol található. Az önvezető autóknál ez kulcsfontosságú.

**Arcfelismerés (Face Recognition)** – A számítógépes látás egyik összetett alkalmazása, amelyben a rendszer arcok alapján próbál személyeket megkülönböztetni vagy azonosítani.

**Természetesnyelv-feldolgozás (Natural Language Processing, NLP)** – Az a terület, amely az emberi nyelv számítógépes feldolgozásával foglalkozik. Ide tartozik a fordítás, az összefoglalás, a szövegértés és a generált válaszadás is.

**Képviselet- vagy reprezentációtanulás (Representation Learning)** – Az a folyamat, amikor a modell maga tanulja meg, milyen belső jellemzők segítik legjobban a döntést. Ez a mélytanulás egyik nagy előnye, mert nem kell minden köztes fogalmat kézzel megadni.

**A/B tesztelés (A/B Testing)** – Két vagy több változat összehasonlítása valós felhasználói adatok alapján. Az internetes és AI-érett cégek ezt gyakran használják gyors tanulásra és optimalizálásra.

**Pilotprojekt (Pilot Project)** – Kisebb, kezdeti AI-projekt, amelynek célja a tapasztalatszerzés és a kockázat csökkentése. Gyakran ez az első lépés egy vállalati AI-átalakításban.

**AI-stratégia (AI Strategy)** – A vállalat tudatos terve arra, hogy hol és hogyan használ AI-t üzleti érték teremtésére. Nem csak technikai kérdés, hanem üzleti és szervezeti döntés is.

**AI-transzformáció (AI Transformation)** – Az a folyamat, amely során egy cég fokozatosan AI-érett szervezetté válik. Ide tartozik a kultúra, az adatinfrastruktúra, a csapat és a döntéshozatal átalakítása is.

**Stratégiai adatgyűjtés (Strategic Data Collection)** – Tudatos adatgyűjtés abból a célból, hogy az adatok később AI-projektek alapjai lehessenek. A jó AI-cégek ezt előre megtervezik.

**Egységes adatarchitektúra (Unified Data Architecture)** – Olyan adatkezelési felépítés, ahol az adatok nem elszigetelten, sok külön rendszerben vannak tárolva. Ez megkönnyíti az AI-csapat számára az összekapcsolást és az értékteremtést.

**AI-érettség (AI Maturity)** – Annak szintje, hogy egy szervezet mennyire képes rendszeresen és hatékonyan AI-t használni. Nem attól lesz magas, hogy van egy modellje, hanem attól, hogy egész rendszerként működik jól.

**Automatizálás (Automation)** – Olyan feladatok gépesítése, amelyeket korábban emberek végeztek. Az AI különösen az ismétlődő, szabályos és jól körülírható feladatok automatizálásában erős.

**Gépi tanulási mérnök (Machine Learning Engineer, MLE)** – Olyan szakember, aki AI-modelleket fejleszt, tanít és javít. Feladata, hogy a modell ne csak elméletben működjön, hanem valódi problémákra is használható legyen.

**Adatmérnök (Data Engineer)** – Az adatok gyűjtéséért, mozgatásáért, tárolásáért és előkészítéséért felelős szakember. Nélküle az AI-csapat gyakran nem jut megfelelő minőségű és formájú adathoz.

**MLOps (MLOps)** – Olyan gyakorlat és szerepkör, amely a modellek üzemeltetésére, frissítésére és megbízható működtetésére fókuszál. Lényege, hogy az AI-rendszer hosszú távon is stabilan használható maradjon.

**Szoftvermérnök (Software Engineer)** – Az AI köré épített teljes rendszer fejlesztője. A modell önmagában még nem kész termék, kell köré robusztus szoftveres környezet.

**Adversariális támadás (Adversarial Attack)** – Olyan támadás, amelynél a támadó szándékosan úgy módosítja a bemenetet, hogy a modell hibás döntést hozzon. Ez rámutat arra, hogy az AI sebezhető lehet még akkor is, ha elsőre pontosnak tűnik.

**Torzítás / elfogultság (Bias)** – Olyan torzulás, amely miatt a modell bizonyos csoportokkal vagy helyzetekkel szemben igazságtalanul működik. Ennek oka gyakran az elfogult adat vagy a rosszul kialakított tanítási folyamat.

**Deepfake (Deepfake)** – AI-val előállított vagy manipulált média, amely valósnak látszó, de hamis képet, videót vagy hangot hoz létre. Komoly társadalmi és biztonsági kockázatot jelenthet.

**Goldilocks-szabály (Goldilocks Rule)** – Olyan szemléleti szabály, amely segít reálisan megítélni az AI képességeit. A lényege, hogy ne becsüljük alá, de ne is várjunk az AI-tól lehetetlent.

**Ökölszabály az 1 másodperces feladatokra (One-Second Rule of Thumb)** – Hegy ember nagyjából egy másodperc alatt meg tud oldani egy feladatot, akkor jó eséllyel a mai AI is megtanítható rá. Ez nem tökéletes szabály, de hasznos első szűrő.

**Hipotézis (Hypothesis)** – Olyan feltételezés, amelyet a csapat adatok alapján vizsgál. A data science-projektekben a hipotézisek segítenek megtalálni, milyen változtatások hozhatnak javulást.

**Értékesítési tölcsér (Sales Funnel)** – Az a folyamat, ahogyan az érdeklődőből vásárló lesz. A data science ezt elemzéssel és optimalizálással tudja javítani.

**Munkaerőpiaci átalakulás (Workforce Transformation)** – Az AI hatására bizonyos feladatok automatizálhatók, mások pedig felértékelődnek. Az AI nemcsak megszüntet, hanem át is alakít munkaköröket.

**Fejlődő gazdaságok felzárkózása (Leapfrogging in Developing Economies)** – Arra utal, hogy egyes országok bizonyos régebbi technológiai szakaszokat akár át is ugorhatnak, és közvetlenül modernebb megoldásokat vezethetnek be. Az AI ilyen helyzetekben gyors fejlődést is lehetővé tehet.

**Reális AI-kép (Realistic View of AI)** – A kurzus egyik fő üzenete, hogy az AI-t sem túlmisztifikálni, sem lebecsülni nem érdemes. Akkor lehet jól használni, ha egyszerre értjük az erejét és a korlátait.

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