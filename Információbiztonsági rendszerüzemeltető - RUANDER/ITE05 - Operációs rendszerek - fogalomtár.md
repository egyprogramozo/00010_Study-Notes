# Operációs rendszerek - fogalomtár

A Ruander Oktatóközpont Információbiztonsági rendszerüzemeltető képzésének bevezető részéből készült ez a fogalomtár, amit azért állítottam össze, hogy könnyebbé tegye a tanulást és az ismétlést.

**Források és felhasznált eszközök:**

- [Információbiztonsági rendszerüzemeltető tanfolyam](https://www.ruander.hu/informaciobiztonsagi-rendszeruzemelteto-kepzes.html)
- [ChatGPT](https://chatgpt.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

## Fogalmak

**Operációs rendszer (OS)** – Szoftver, amely a hardver erőforrásait kezeli, és keretet ad az alkalmazások futtatásához.

**Többfelhasználós rendszer** – Egyszerre több felhasználó munkáját kezeli (pl. szerverek, terminálszolgáltatások).

**Multitasking / többszálú működés** – A rendszer párhuzamosan futtat több programot vagy egy program több részét (szálát).

**x86 / x64 architektúra** – 32 bites (x86) és 64 bites (x64) processzor- és operációs rendszer-kialakítás.

**Asztali (kliens) OS** – Egyéni felhasználóknak szánt rendszer (Windows 10/11, macOS, Linux desktop).

**Hálózati/szerver OS** – Nagyobb számú felhasználót, hálózati szolgáltatásokat kiszolgáló rendszer (Windows Server, Linux szerver).

**Frissítés (upgrade)** – Meglévő operációs rendszer újabb verzióra emelése, jellemzően beállítások és adatok megtartásával.

**Adat- és profilmigráció** – Felhasználói dokumentumok, profilok és beállítások átköltöztetése új rendszerre vagy új gépre.

**Tiszta telepítés (clean install)** – Az operációs rendszer teljesen újratelepítése, a meglévő rendszer és adatok figyelmen kívül hagyásával (általában partícionálással és formázással).

**Lemez, partíció, kötet** – A fizikai lemez logikai részekre (partíciókra) osztása; ezekből jönnek létre a kötetek, amelyeket a Windows meghajtóként (C:, D: stb.) lát.

**MBR és GPT** – Kétféle partíciós séma. Az MBR régi, 4 elsődleges partícióval; a GPT modern, nagy lemezekhez, sok partícióval, UEFI-vel használatos.

**Alap- és dinamikus lemez** – Alaplemez: klasszikus partíciók (ajánlott). Dinamikus lemez: logikai kötetek, átnyúló/RAID-szerű megoldások, de ma már inkább Storage Spaces és hardveres RAID használatos.

**Formázás** – Fájlrendszer létrehozása egy partíción (pl. NTFS), hogy a fájlok tárolhatók legyenek. Lehet gyors vagy teljes.

**NTFS, exFAT, ReFS** – A Windows fő fájlrendszerei: NTFS általános rendszerpartícióhoz, exFAT hordozható médiákhoz, ReFS speciális szerveres/archiv célokra.

**UEFI/BIOS, boot-sorrend** – A gép firmware-e, amely indításkor lefuttatja a POST-ot, majd a megadott eszközsorrend szerint megkeresi a bootolható lemezt.

**Windows Boot Manager (BOOTMGR), BCD** – A Windows indítóprogramja és konfigurációs adatbázisa, amely eldönti, melyik operációs rendszer indul (multiboot).

**WinRE (Windows Recovery Environment)** – Előtelepített helyreállító környezet: indítási javítás, rendszer-visszaállítás, rendszerkép-helyreállítás, parancssor stb.

**Lemezkép / image, Sysprep** – Egy előre beállított rendszer teljes „pillanatképe”, melyet több gépre lehet klónozni; a Sysprep készíti elő a képet új hardverekhez.

**PXE / hálózati telepítés** – Operációs rendszer telepítése hálózatról, rendszerindító lemez nélkül, hálózati boot (PXE) segítségével.

**Lemezkezelő (Disk Management)** – Beépített Windows eszköz partíciók létrehozására, bővítésére, zsugorítására, betűjelek és RAID-kötegek kezelésére.

**Jogosultságok, ACL, árnyékmásolat (shadow copy)** – A fájlokhoz való hozzáférést szabályozó listák és az automatikusan készült „korábbi verziók” mechanizmusa.

**GUI (grafikus felhasználói felület)** – Ikonokból, ablakokból, menükből álló felület, ahol egérrel/billentyűzettel dolgozunk.

**Asztal (Desktop)** – A fő munkafelület háttérképpel, ikonokkal és parancsikonokkal.

**Tálca (Taskbar)** – Általában alul futó sáv, rajta a Start gomb, rögzített appok, futó programok, értesítési terület.

**Start menü** – A telepített alkalmazások, beállítások és keresés központi helye.

**Fájlkezelő (File Explorer)** – A fájlok, mappák, meghajtók grafikus kezelője.

**Vezérlőpult (Control Panel)** – Egy „régi” központi konfigurációs felület, sok beállítás még mindig innen érhető el.

**Beállítások (Settings app)** – Modern, érintőképernyő-barát konfigurációs felület Windows 10/11-ben.

**Műveletközpont / Értesítési központ** – Rendszerértesítések, gyors gombok (Wi-Fi, fényerő, fókuszsegéd, stb.).

**Feladatkezelő (Task Manager)** – Futó programok, folyamatok, erőforrás-használat és induló programok kezelése.

**Számítógép-kezelés (Computer Management, MMC)** – Több adminisztratív eszköz egy helyen (Lemezkezelő, Eseménynapló, stb.).

**Eszközkezelő (Device Manager)** – Hardverek és illesztőprogramok felügyelete.

**Szolgáltatások (Services)** – Háttérben futó komponensek, amelyek funkciókat biztosítanak (pl. nyomtatás, frissítések).

**Parancssor / PowerShell** – Szöveges (CLI) felület parancsok, szkriptek futtatására.

**Kliens-oldali virtualizáció** – Amikor egy felhasználói számítógép (PC, laptop) több, egymástól független virtuális gépet futtat.

**Virtuális gép (VM)** – Szoftveresen létrehozott „gép”, amely saját operációs rendszert és alkalmazásokat futtat, a gazdagép erőforrásait használva.

**Hypervisor (Virtual Machine Manager)** – Az a szoftverréteg, amely létrehozza, futtatja és menedzseli a virtuális gépeket, valamint elosztja köztük az erőforrásokat.

**Megelőző karbantartási terv** – Előre megtervezett feladatok és ütemezések együttese, amely csökkenti a leállásokat és növeli a rendszer megbízhatóságát.

**Frissítés (update)** – Operációs rendszerhez, driverekhez vagy firmware-hez kiadott javítás, új funkció vagy biztonsági módosítás.

**Biztonsági mentés (backup)** – Az adatok másolatának készítése, hogy hiba, fertőzés vagy törlés esetén visszaállíthatók legyenek.

**Rendszer-visszaállítási pont** – Az operációs rendszer konfigurációjának pillanatfelvétele, amelyhez probléma esetén vissza lehet térni.

**Hibaelhárítási folyamat** – Strukturált lépéssorozat a problémák azonosítására, megoldására és dokumentálására.

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
