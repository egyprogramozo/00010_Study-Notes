# A számítógép összeszerelése - fogalomtár

A Ruander Oktatóközpont Információbiztonsági rendszerüzemeltető képzésének bevezető részéből készült ez a fogalomtár, amit azért állítottam össze, hogy könnyebbé tegye a tanulást és az ismétlést.

**Források és felhasznált eszközök:**

- [Információbiztonsági rendszerüzemeltető tanfolyam](https://www.ruander.hu/informaciobiztonsagi-rendszeruzemelteto-kepzes.html)
- [ChatGPT](https://chatgpt.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

## Fogalmak

**Számítógépház (case)** – A hardverelemeket védő és rögzítő burkolat, amely a légáramlást is befolyásolja.

**Tápegység (PSU)** – A hálózati feszültséget alakítja át a számítógép számára megfelelő feszültségszintekre.

**CPU és foglalat (socket)** – A központi feldolgozó egység és annak alaplapi csatlakozója.

**Hővezető paszta és CPU-hűtő** – A CPU és a hűtőborda közti jó hőátadást, illetve a hő elvezetését biztosítják.

**RAM modul (DDR4/DDR5)** – A processzor gyors, átmeneti munkaterülete, amely a gép teljesítményét erősen befolyásolja.

**Háttértárak (SATA SSD, HDD, M.2 NVMe)** – Az adatok hosszú távú tárolására szolgáló eszközök.

**Bővítőkártya (PCIe)** – Extra funkciókat ad (videokártya, Wi-Fi, hangkártya, stb.), az alaplap bővítőhelyeibe csatlakozik.

**ATX tápcsatlakozók (24-pines, 8-pines CPU, PCIe, SATA)** – Az alaplap és az alkatrészek tápellátását biztosító csatlakozók.

**Előlapi csatlakozók (front panel)** – A power/reset gomb, LED-ek, USB, audio és USB-C portok alaplapi bekötése.

**Kábelmenedzsment** – A kábelek rendezett elvezetése a jobb légáramlás és könnyebb szerelhetőség érdekében.

**POST (Power-On Self Test)** – Bekapcsoláskor lefutó hardverteszt, amely ellenőrzi a memória, CPU, videokártya és egyéb alapvető komponensek működését.

**BIOS/UEFI firmware** – Az alaplapba égetett alapprogram, amely elindítja a gépet, kezeli az alap hardvereket és átadja a vezérlést az operációs rendszernek.

**Sípkódok** – A BIOS/UEFI által kiadott rövid sípsorozatok, amelyek konkrét hardverhibákat jeleznek (pl. memória-, VGA-hiba).

**CMOS/NVRAM és elem** – A firmware-beállításokat tároló memória, amelyet egy gombelem segít megtartani; modern rendszereken többnyire nem felejtő (NVRAM).

**Boot sorrend** – Az eszközök listája, amely meghatározza, milyen sorrendben próbál a gép operációs rendszert indítani (SSD, hálózat, USB, stb.).

**Virtualizáció (Intel VT-x, AMD-V)** – Hardveres támogatás több virtuális gép párhuzamos futtatásához ugyanazon a fizikai gépen.

**TPM (Trusted Platform Module)** – Biztonsági chip, amely titkosítási kulcsokat, hitelesítő adatokat tárol és támogatja a lemeztitkosítást, Secure Bootot.

**RAID** – Több lemezből felépített logikai tömb, amely teljesítménynövelést, redundanciát vagy mindkettőt biztosíthat.

**BIOS/UEFI frissítés (flash)** – A firmware új verziójának telepítése, új hardvertámogatás vagy hibajavítás érdekében.

**Alaplap/CPU/RAM korszerűsítés** – A fő hardverkomponensek cseréje a nagyobb teljesítmény vagy új funkciók érdekében, kompatibilitási szempontok figyelembevételével.

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
