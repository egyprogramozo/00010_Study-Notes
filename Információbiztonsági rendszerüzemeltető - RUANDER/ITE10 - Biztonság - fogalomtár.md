# ITE - Biztonság - fogalomtár

A Ruander Oktatóközpont Információbiztonsági rendszerüzemeltető képzésének bevezető részéből készült ez a fogalomtár, amit azért állítottam össze, hogy könnyebbé tegye a tanulást és az ismétlést.

**Források és felhasznált eszközök:**

- [Információbiztonsági rendszerüzemeltető tanfolyam](https://www.ruander.hu/informaciobiztonsagi-rendszeruzemelteto-kepzes.html)
- [ChatGPT](https://chatgpt.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

## Fogalmak

**Belső és külső fenyegetések** – A biztonsági kockázatok származhatnak belső szereplőktől is, például jogosultsággal rendelkező felhasználók szándékos visszaélése vagy gondatlansága miatt, valamint külső támadóktól, akik illetéktelen hozzáférést, adatlopást vagy szolgáltatáskimaradást próbálnak előidézni. A korszerű védekezés mindkét típust hozzáférés-kezeléssel, naplózással, felügyelettel és incidenskezeléssel kezeli.

**Fizikai és adatbiztonság** – A fizikai biztonság az eszközök, helyiségek és adathordozók védelmét jelenti lopás, rongálás, jogosulatlan hozzáférés vagy környezeti károk ellen, míg az adatbiztonság az információk bizalmasságát, sértetlenségét és rendelkezésre állását védi. A két terület együtt ad valós védelmet, mert az adatok biztonsága nem választható el az azokat kezelő eszközök biztonságától.

**Malware** – Gyűjtőfogalom minden olyan rosszindulatú szoftverre vagy kódra, amely illetéktelen műveletet hajt végre, adatot lop, rendszert módosít vagy működést akadályoz. Ide tartoznak többek között a vírusok, férgek, trójaiak, spyware-megoldások, egyes adware-ek és a zsarolóprogramok is.

**Adware, spyware, grayware** – Az adware kéretlen hirdetéseket jelenít meg, a spyware titokban adatot gyűjt a felhasználóról vagy a rendszerről, a grayware pedig olyan határesetű szoftverek gyűjtőneve, amelyek nem mindig minősülnek klasszikus malware-nek, de zavaró, kockázatos vagy nem kívánt működést okozhatnak. A mai gyakorlatban ezeket sokszor PUA (Potentially Unwanted Application, potenciálisan nemkívánatos alkalmazás) vagy PUP (Potentially Unwanted Program, potenciálisan nemkívánatos program) kategóriaként kezelik.

**Adathalászat (Phishing)** – Olyan megtévesztési technika, amelyben a támadó hitelesnek látszó e-maillel, weboldallal, üzenettel vagy más csatornán próbál érzékeny adatokat, hitelesítő adatokat vagy jóváhagyást megszerezni. Az adathalászat a social engineering egyik leggyakoribb formája, ezért a modern védelemben a felhasználói tudatosság mellett a többtényezős, lehetőleg adathalászatnak ellenálló hitelesítés is fontos.

**Vírus** – Olyan önmásoló kártékony programrészlet, amely más fájlhoz vagy programhoz kapcsolódik, és annak futtatásakor aktiválódik. A vírus önmagában nem működik gazdaprogram nélkül, ezért a terjedéséhez általában valamilyen felhasználói vagy rendszeroldali futtatás szükséges.

**Féreg (Worm)** – Olyan önállóan futó, önmagát terjesztő kártevő, amely hálózaton keresztül képes más rendszerekre átmásolni magát, általában gazdaprogram vagy közvetlen felhasználói beavatkozás nélkül. Hálózati környezetben különösen veszélyes, mert gyorsan és nagy területen tud terjedni.

**Trójai (Trojan horse)** – Olyan program, amely hasznos vagy legitim alkalmazásnak látszik, valójában azonban rejtett rosszindulatú funkciót tartalmaz. Gyakori célja a távoli hozzáférés megnyitása, adatszivárgás, további kártevők letöltése vagy a biztonsági mechanizmusok megkerülése.

**Rootkit** – Olyan rejtőzködő eszköz- vagy szoftverkészlet, amely a támadó jelenlétének elrejtésére és a megszerzett magas jogosultság fenntartására szolgál. Különösen veszélyes, mert képes a rendszer normál működését manipulálni úgy, hogy a fertőzés nehezen észlelhető maradjon.

**Vírusvédelem és frissítések** – A mai védelem nem áll meg a hagyományos vírusirtónál: a korszerű végpontvédelem valós idejű vizsgálatot, viselkedéselemzést, fenyegetésészlelést és EDR (Endpoint Detection and Response, Végpontszintű észlelés és válaszadás)-képességeket is használ. Ehhez elengedhetetlen az operációs rendszer, az alkalmazások és a védelmi komponensek folyamatos frissítése, mert az elavult rendszerek gyorsan támadhatóvá válnak.

**Webes biztonság** – A modern webes védelem a rosszindulatú webhelyek, adathalász oldalak, veszélyes letöltések és ártalmas domainek felismerésére és blokkolására épül. A korszerű böngészők és végpontvédelmi megoldások ilyen célra URL-szűrést, hírnévalapú ellenőrzést és böngészővédelmi funkciókat használnak; az olyan régi technológiák, mint az Internet Explorer és az ActiveX, ma már örökségmegoldásnak számítanak.

**Spam** – Kéretlen, tömegesen küldött elektronikus üzenet, amely lehet egyszerű reklám, de gyakran adathalászat, malware-terjesztés vagy csalás eszköze is. Biztonsági szempontból a spam azért veszélyes, mert a felhasználót káros linkre, hamis oldalra vagy fertőzött melléklet megnyitására próbálja rávenni.

**DoS és DDoS** – A DoS (Denial of Service, szolgáltatásmegtagadás) célja egy erőforrás vagy szolgáltatás túlterhelése, hogy a jogos felhasználók ne férjenek hozzá, a DDoS (Distributed Denial of Service, elosztott szolgáltatásmegtagadás) pedig ennek elosztott változata, amikor a támadás számos gépről egyszerre érkezik. Ezek a támadások elsősorban a rendelkezésre állást veszélyeztetik.

**SYN flood, spoofing, man-in-the-middle, replay, DNS-mérgezés** – Ezek olyan hálózati támadások, amelyek hamisítással, kapcsolatmanipulációval, üzenetek visszajátszásával vagy névfeloldás befolyásolásával próbálnak jogosulatlan előnyt szerezni. Ide tartozik például a hamis forráscím használata, a kommunikáció közbeékelődő lehallgatása és módosítása, korábban elfogott hitelesítési adatok újraküldése, illetve a DNS-válaszok vagy gyorsítótár megtévesztése.

**Social engineering** – Az emberi tényezőt kihasználó támadási módszer, amely megtévesztéssel, bizalomépítéssel vagy nyomásgyakorlással próbál érzékeny információt, hozzáférést vagy jóváhagyást szerezni. Nem technikai hibát támad, hanem az embert, ezért a képzés és a tudatosság ugyanannyira fontos ellene, mint a technikai védelem.

**Adattörlés és adattárolók megsemmisítése** – A biztonságos adattörlés nem egyszerű fájltörlést jelent, hanem olyan adatszanitizálási eljárást, amely ésszerű erőfeszítéssel ellehetetleníti az adatok visszaállítását. A mai gyakorlatban ennek fő szintjei a clear, purge és destroy; SSD-knél és felhős vagy titkosított környezetben a cryptographic erase is fontos lehet, míg a degaussolás nem megfelelő minden adattípushoz, például SSD-hez sem.

**Biztonsági házirend** – Olyan szervezeti szabályrendszer, amely meghatározza a kockázatkezelés, a hozzáférés-szabályozás, a védelem, az észlelés, a reagálás és a helyreállítás alapelveit. Egy jó házirend nemcsak tiltásokat sorol fel, hanem szerepeket, felelősségeket, incidenskezelést, kommunikációt és ellenőrizhető működési elvárásokat is rögzít.

**Felhasználónevek és jelszavak** – A felhasználónév–jelszó páros továbbra is alap hitelesítési forma, de önmagában már nem tekinthető elégséges védelemnek. A korszerű gyakorlat ezt többtényezős hitelesítéssel egészíti ki, és ahol lehet, előnyben részesíti az adathalászatnak ellenálló hitelesítési megoldásokat.

**Erős jelszó** – Az erős jelszó ma elsősorban hosszú, egyedi és más szolgáltatásoktól eltérő, lehetőleg jelszókezelővel tárolt vagy generált jelszó. A mai ajánlások szerint fontos a gyakori vagy kompromittált jelszavak tiltólistás szűrése, a jelszókezelők támogatása, és nem az önkényes időközönkénti kötelező csere vagy a túl merev összetételi szabályok jelentik a legjobb védelmet.

**Fájl- és mappajogosultságok** – A hozzáférési jogosultságok határozzák meg, hogy egy felhasználó vagy csoport mit olvashat, módosíthat, futtathat vagy törölhet. A korszerű jogosultságkezelés csoportalapú, részletesen szabályozható, és az objektumokhoz rendelt hozzáférési listákon alapul.

**Legkevesebb jogosultság elve** – Az a biztonsági alapelv, hogy a felhasználó, folyamat vagy szolgáltatás csak a feladatához minimálisan szükséges jogosultságokat kapja meg. Ez csökkenti a hibák, visszaélések és sikeres támadások következményeit, ezért az egyik legfontosabb hozzáférés-védelmi elv.

**NTFS és FAT32 különbsége** – Biztonsági szempontból az NTFS (New Technology File System) a korszerűbb fájlrendszer, mert támogatja a részletes hozzáférés-szabályozást és a Windows biztonsági modelljét. A FAT32 (File Allocation Table 32) ezzel szemben egyszerűbb, de nem kínál ilyen szintű jogosultságkezelést, ezért védett munkaállomásokon és szervereken nem ez a megfelelő választás.

**Szoftveres tűzfal** – A végponton futó védelmi réteg, amely szabályok alapján engedélyezi vagy tiltja a hálózati kapcsolatokat alkalmazás, port, protokoll vagy hálózati profil szerint. Fontos szerepe van a nem kívánt bejövő és kimenő forgalom korlátozásában, valamint az alkalmazások hálózati viselkedésének kontrollálásában.

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
