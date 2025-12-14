# Bevezetés a személyi számítógépek világába - fogalomtár

A Ruander Oktatóközpont Információbiztonsági rendszerüzemeltető képzésének bevezető részéből készült ez a fogalomtár, amit azért állítottam össze, hogy könnyebbé tegye a tanulást és az ismétlést.

**Források és felhasznált eszközök:**

- [Információbiztonsági rendszerüzemeltető tanfolyam](https://www.ruander.hu/informaciobiztonsagi-rendszeruzemelteto-kepzes.html)
- [ChatGPT](https://chatgpt.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

## Fogalmak

**Személyi számítógép (PC)** – Egyszemélyes használatra tervezett, általános célú számítógép (asztali, mini PC, laptop, all-in-one).

**Hardver / szoftver** – Hardver: fizikai alkatrészek; szoftver: operációs rendszer és programok, amelyek a hardvert vezérlik.

**Számítógépház (case)** – A belső alkatrészeket befogadó, védő és hűtő burkolat.

**Tápegység (PSU)** – Az elektromos hálózat váltakozó áramát alakítja át többfeszültségű egyenárammá a számítógép számára.

**Form factor (formai tényező)** – Az alaplap, ház és tápegység méretét, rögzítési pontjait, csatlakozóit meghatározó szabvány.

**Tápcsatlakozók** – Speciális, kulcsolt csatlakozók (ATX 24 tűs, CPU EPS 4/8 tűs, PCIe 6/8 tűs, SATA), amelyek biztosítják a megfelelő feszültségű tápellátást.

**Ohm törvénye** – Az elektromosság alapösszefüggése: U = I·R, a feszültség, áramerősség és ellenállás kapcsolatát írja le.

**UPS (szünetmentes tápegység)** – Akkumulátoros eszköz, amely áramszünet esetén rövid ideig árammal látja el a számítógépet és védi az áramingadozásoktól.

**Alaplap (motherboard)** – Fő nyomtatott áramköri lap, amelyre a CPU, RAM, bővítőkártyák és csatlakozók kerülnek.

**Chipset / PCH** – Vezérlőlogika, ami a CPU, RAM, háttértárak és perifériák közti adatforgalmat szabályozza; ma sok funkciója a CPU-ba költözött.

**CPU (processzor)** – A gép „agya”, amely az utasításokat végrehajtja; több maggal, cache-szintekkel és gyakran többszálú működéssel.

**RAM (DDR4/DDR5)** – Gyors, felejtő munkamemória, ahol a futó programok adatai tárolódnak.

**PCI Express (PCIe)** – Modern, soros bővítőbusz, amelyen a videokártya és más bővítőkártyák kommunikálnak az alaplappal.

**SSD (SATA / NVMe M.2)** – Félvezetős háttértár, amely sokkal gyorsabb és megbízhatóbb a hagyományos merevlemezeknél.

**Cache memória** – A CPU-hoz nagyon közel lévő, SRAM alapú, kisméretű, de rendkívül gyors memória (L1, L2, L3).

**Hűtés (air / liquid cooling)** – Ventilátorok, hűtőbordák és esetenként vízhűtés együttese a biztonságos működési hőmérsékletért.

**I/O port (Input/Output port)** – Külső csatlakozó, amelyen keresztül perifériákat kapcsolunk a számítógéphez. 

**HDMI** – Digitális videó- és hangcsatlakozó TV-khez, monitorokhoz, konzolokhoz; modern verziói akár 4K 120Hz és 8K felbontást is támogatnak.

**DisplayPort (DP)** – PC-kre optimalizált digitális kijelzőcsatlakozó, nagy frissítési frekvenciával, többmonitoros láncolással és adaptív szinkronnal.

**USB / USB-C / USB4** – Univerzális soros busz perifériákhoz; a modern USB-C/USB4 akár 40 Gbit/s adatátvitelt, videót és töltést is képes egy kábelen kezelni.

**RJ-45 Ethernet** – 8 érintkezős hálózati csatlakozó; helyi hálózathoz, internethez, PoE-eszközökhöz használjuk.

**Beviteli eszköz** – Az adatbevitelre szolgáló perifériák összefoglaló neve (egér, billentyűzet, gamepad, szkenner stb.).

**Kimeneti eszköz** – Olyan periféria, amelyen keresztül a számítógép információt ad ki (monitor, nyomtató, hangszóró).

**Felbontás (resolution)** – A kijelző vízszintes és függőleges pixeleinek száma, pl. 1920×1080, 2560×1440, 3840×2160 (4K).

**Frissítési frekvencia (refresh rate)** – Másodpercenkénti képkockák száma Hz-ben; játékra ma gyakori a 120–240 Hz.

**HDR (High Dynamic Range)** – Olyan megjelenítési mód, amely nagyobb fényerőt és dinamikusabb színeket biztosít.

**Igényfelmérés** – annak kiderítése, hogy a felhasználó pontosan mire használja a gépet (iroda, játék, videóvágás, 3D, fejlesztés stb.).

**Form factor (ATX, mATX, Mini-ITX)** – a ház, alaplap és tápegység méretét és rögzítési pontjait meghatározó szabvány.

**Tápegység headroom** – a komponensek összes fogyasztása fölötti biztonsági tartalék, javasolt 20–30%.

**Chipset / platform (pl. Intel, AMD)** – meghatározza a támogatott CPU-kat, RAM-ot, PCIe-sávokat, I/O-portokat.

**64 bites CPU** – modern processzor, amely nagy mennyiségű RAM-ot képes címezni és több adatot dolgoz fel ciklusonként, mint a régi 32 bitesek.

**DDR4 / DDR5 RAM** – jelenlegi memória-szabványok; a DDR5 nagyobb sávszélességet és kapacitást ad, de drágább és nagyobb késleltetésű.

**SATA SSD vs NVMe SSD** – SATA: akár ~550–600 MB/s, NVMe PCIe-n akár 7 000 MB/s, lényegesen gyorsabb rendszerindítást és programbetöltést ad.

**RAID** – több lemez összefogása egy logikai egységgé a sebesség és/vagy hibatűrés növelésére.

**Külső háttértár** – USB-s vagy hálózati (NAS) eszköz, amely hordozható vagy több gépről is elérhető.

**Munkaállomás** – speciális, nagy teljesítményű PC, professzionális szoftverekhez (CAD, 3D, vágás, mérnöki és tudományos munkák).

**CAD/CAM munkaállomás** – tervezéshez és gyártástervezéshez használt gép, erős CPU-val, professzionális GPU-val és sok RAM-mal.

**Audió–videó szerkesztő munkaállomás** – nagy felbontású anyagok felvételére, vágására, effektezésére optimalizált PC, sok maggal, sok RAM-mal, gyors SSD-vel.

**Virtualizációs munkaállomás / szerver** – több virtuális gépet futtató host rendszer, sok maggal, nagy memóriával és NVMe háttértárral, Hyper-V, VMware, Proxmox stb. futtatására.

**Vékony kliens (thin client)** – egyszerű, kis fogyasztású eszköz, amely egy távoli, erős szerverre csatlakozik (VDI, RDP), a nagy számítást a szerver végzi.

**Játék PC (gaming rig)** – játékra optimalizált erős GPU-val, sok RAM-mal és gyors SSD-vel, gyakran extrém hűtéssel és gaming perifériákkal.

**HTPC (Home Theater PC)** – nappaliba szánt, csendes, kis méretű PC, 4K videó és térhatású hang lejátszására, gyakran médialejátszó szoftverrel (Kodi, Plex).

**Házi szerver / NAS** – otthoni adattárolásra, médiastreamelésre és biztonsági mentésre szolgáló, több lemezes, redundáns tárolót és gigabites/multi-gigabites hálózatot használó gép.

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
