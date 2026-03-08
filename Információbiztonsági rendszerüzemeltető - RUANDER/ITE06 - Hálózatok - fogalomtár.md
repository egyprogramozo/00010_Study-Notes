# Hálózatok - fogalomtár

A Ruander Oktatóközpont Információbiztonsági rendszerüzemeltető képzésének bevezető részéből készült ez a fogalomtár, amit azért állítottam össze, hogy könnyebbé tegye a tanulást és az ismétlést.

**Források és felhasznált eszközök:**

- [Információbiztonsági rendszerüzemeltető tanfolyam](https://www.ruander.hu/informaciobiztonsagi-rendszeruzemelteto-kepzes.html)
- [ChatGPT](https://chatgpt.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

## Fogalmak

**Hálózat (network)** – Egymással összekapcsolt eszközök rendszere, amely adatok, erőforrások és szolgáltatások megosztására szolgál.

**PAN / LAN / WLAN / MAN / WAN** – Hálózattípusok a lefedett terület szerint: személyi, helyi, vezeték nélküli helyi, nagyvárosi és nagy kiterjedésű hálózat.

**Peer-to-peer és kliens–szerver modell** – Erőforrás-megosztás két alapvető szervezési módja: minden gép egyenrangú vs. központi szerverek szolgálják ki a klienseket.

**Csomag és keret** – Az átvitt adat kisebb egységei; a keret tartalmazza a forrás- és célcímet, valamint vezérlőinformációt.

**Sávszélesség és késleltetés** – Az időegység alatt továbbítható adatmennyiség, illetve az útvonalon fellépő „várakozási idő”.

**Simplex / half-duplex / full-duplex** – Az adatáramlás iránya: egyirányú, váltakozó irányú, illetve kétirányú, egyszerre.

**MAC-cím és IP-cím** – Fizikai cím a hálózati kártyán, illetve logikai cím a hálózaton való irányításhoz.

**IPv4 és IPv6** – Két elterjedt IP-verzió; 32 bites vs. 128 bites címtér, címformátumok és írásmódok.

**Statikus IP, DHCP, APIPA** – Kézi címkiosztás, automatikus címzés kiszolgálóról, illetve ideiglenes „önkiosztott” cím tartomány.

**DNS és ICMP (ping)** – Névfeloldás domainnévről IP-címre, illetve vezérlő/hálózati diagnosztikai üzenetek protokollja.

**TCP és UDP** – Kapcsolat-orientált, megbízható adatátvitel vs. egyszerű, gyors, „legjobb szándékú” küldés.

**Kapcsoló (switch), forgalomirányító (router), hozzáférési pont (AP)** – A hálózat logikai és fizikai központi eszközei.

**PoE, NAS, IP-telefon, tűzfal** – Speciális hálózati technológiák: áram Etherneten, központi fájlszerver, IP-alapú telefon, biztonsági szűrő.

**UTP/STP és Cat-kategóriák** – Csavart érpáras kábelek típusai, jellemző sebességgel és zavartűréssel.

**Optikai szál (multimódusú / egymódusú)** – Fényt használó átviteli közeg nagy sebességre és távolságra.

**Logikai topológia** – Azt írja le, hogyan jutnak el az adatok a hálózati közegen, milyen hozzáférési szabályok vannak.

**Fizikai topológia** – A kábelek, eszközök (switch, router, AP) tényleges elrendezése.

**Csillag- és hierarchikus topológia** – Modern LAN-ok alapja, központi switch(ek) köré épülő struktúra.

**Ethernet (IEEE 802.3)** – A vezetékes helyi hálózatok de facto szabványa, ma jellemzően 1 Gbit/s vagy gyorsabb.

**Wi-Fi (IEEE 802.11)** – Vezeték nélküli LAN-szabványok családja (Wi-Fi 4/5/6/6E), eltérő frekvenciákkal és sebességekkel.

**TCP/IP- és OSI-modell** – Rétegmodellek, amelyek segítenek rendszerezni a protokollokat és a hálózati működést.

**NIC (Network Interface Card)** – Hálózati kártya, a gép “csatlakozója” a hálózathoz (vezetékes vagy vezeték nélküli).

**DHCP és statikus IP** – IP-cím automatikus kiosztása (DHCP) vagy kézi beállítása.

**VPN (Virtual Private Network)** – Titkosított “alagút” nyilvános hálózaton át, távoli biztonságos eléréshez.

**Szélessáv (broadband)** – Nagy sebességű, folyamatosan rendelkezésre álló internetkapcsolat (DSL, kábel, optika, mobil, műhold stb.).

**DSL / ADSL / VDSL** – Réztelefon-vonalon működő, folyamatos, szélessávú kapcsolat; ADSL aszimmetrikus, VDSL gyorsabb, rövidebb távolságra.

**Kábeles internet (DOCSIS)** – Koaxiális kábelen nyújtott internet, a kábel-TV hálózatán; modern verziói több gigabites sebességet is tudnak.

**FTTH (optikai, üvegszál, fiber)** – Nagyon nagy sávszélességű kapcsolat, az üvegszál egészen az előfizetőig ér (tipikusan 1–10 Gbit/s).

**Mobilhálózat (4G/5G)** – Rádiós (cellás) hálózat, amely hangot és adatot továbbít; modern 5G hálózatok valós körülmények között is gyakran 100–300 Mbit/s sebességet nyújtanak.

**Műholdas internet (geostacionárius, LEO)** – Nagy területet lefedő, de jellemzően nagyobb késleltetésű kapcsolat; új LEO rendszerek már jóval alacsonyabb pinget (20–40 ms) kínálnak.

**Megelőző karbantartás** – Tervezett, rendszeres ellenőrzések és tisztítás, frissítések, mentések, amelyek csökkentik a meghibásodás esélyét.

**Hibaelhárítási folyamat** – Lépésről lépésre végzett eljárás: probléma azonosítása, okok szűkítése, tesztelés, megoldás, ellenőrzés, dokumentálás.

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
