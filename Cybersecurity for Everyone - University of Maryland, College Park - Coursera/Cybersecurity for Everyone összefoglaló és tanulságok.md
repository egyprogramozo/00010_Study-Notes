# Cybersecurity for Everyone összefoglaló és tanulságok

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

**Források:**

- [Cybersecurity for Everyone - University of Maryland, College Park](https://www.coursera.org/learn/cybersecurity-for-everyone)

## Bevezető gondolatok

Amikor nekiálltam ennek a kiberbiztonsági tananyagnak, már volt némi informatikai hátterem, köszönhetően a több mint 15 évnyi IT-tapasztalatomnak. Ismertem az OSI-modellt és a TCP/IP alapjait, találkoztam vírusirtókkal és tűzfalakkal, és tudtam, hogy mindig van kockázat, ha valami csatlakozik a hálózathoz. A kiberbiztonság viszont részben még elvont fogalom volt számomra, amelyet leginkább a hírekben szereplő „hackerincidensekkel” azonosítottam. Ahogy lépésről lépésre végigmentem a kurzuson, és közben rengeteg dolognak utánaolvastam, teljesen máshogy kezdtem látni ezt az egész világot. Nemcsak új fogalmakat tanultam, hanem egy **keretet**, amin keresztül értelmesen el tudom helyezni a híreket, az eseteket, és a saját jövőbeli kiberbiztonsági tanulmányaimat is.

## Néha érdemes más szemmel nézni ugyanazt

Az első gondolatébresztő az volt, hogy külön vettük a **cyber**, a **biztonság** és a **kiberbiztonság** fogalmait. Korábban hajlamos voltam a „kibert” egyszerűen azonosítani a „számítógépes dolgokkal”. Most már sokkal inkább úgy gondolok rá, mint egy **összetett rendszerre**, ahol technológia, emberek és szervezetek egységet alkotnak. A hálózatok, eszközök, felhasználók, cégek, államok, szabályozások, üzleti érdekek mind hatnak egymásra.

A biztonság fogalmát is több szinten kellett újrasúlyoznom: egyéni, vállalati és állami szinten is mást jelent, de mindenhol közös a lényeg: **miből mennyit vagyunk hajlandók kockáztatni**. A klasszikus **CIA-triád** (bizalmasság, integritás, rendelkezésre állás) persze már korábban is ismerős volt, de a példáknak köszönhetően most tényleg „életre kelt”. Rájöttem, hogy gyakorlatilag minden kiberincidens ennek a három elemnek valamelyikét vagy ezek kombinációját érinti.

Nagyon hasznos volt az a gondolat is, hogy a kibertér kockázataira nem lehet feketén-fehéren tekinteni. A kérdés nem az, hogy „van-e kockázat”, hanem az, **mekkora a kockázat**, és **mekkora hatással jár**, ha valami tényleg bekövetkezik. Ez a szemlélet – valószínűség × hatás – végigkísérte az egész anyagot, és szerintem az egyik legfontosabb dolog, amit ebből az időszakból magammal viszek.

## Az internet története és rétegzett felépítése, avagy az alapok új fényben

Mivel korábbról már volt valamilyen OSI- és TCP/IP-ismeretem, az internet evolúciós része első ránézésre ismétlésnek tűnt. De az, hogy ezeket **kiberbiztonsági szemüvegen keresztül** néztem újra, teljesen más élmény volt.

A történeti rész – Licklider „galaktikus hálózata”, az ARPANET, majd a TCP/IP és a DNS kialakulása – rámutatott, hogy az internet tervezése során nem volt prioritás a biztonság, hanem a megbízható kapcsolatra és a rugalmasságra helyezték a fókuszt. A mai sebezhetőségek jó része abból fakad, hogy egy eredetileg akadémiai-katonai kísérleti infrastruktúra nőtte ki magát globális közművé, miközben a biztonsági megoldások sokszor utólag lettek implementálva.

Az OSI-modell rétegeit már tudatosabban kötöm össze azzal, hogy hol jelennek meg a támadási pontok.

Például:

- Alkalmazási réteg: webalkalmazás-sebezhetőségek, SQL injection, hibás vagy gyenge hitelesítés.
- Hálózati réteg: IP-cím manipulálása, BGP-eltérítés.
- Fizikai réteg: kábelek, rádiós átviteli eszközök, alap infrastruktúra elleni támadások.

A „kapszulázás” (encapsulation) gondolata segített megérteni, hogyan épülnek egymásra a kommunikáció egyes rétegei. Emellett az is világosabbá vált számomra, hogy egy DNS-t érintő támadás több, névfeloldásra épülő szolgáltatás működését is megzavarhatja. Ma már, ha egy incidensről olvasok, automatikusan felteszem magamnak a kérdést, hogy **melyik réteget vagy szolgáltatást érinti, és hogyan gyűrűzhet tovább a hatása?**

## A kormányzás, az IoT és a városi infrastruktúra mint támadási felület

A tananyag fontos része volt az is, hogy az internetet ne csak technikai rendszerként, hanem **kormányzási kérdésként** is lássam. A „governance” itt azt jelenti, hogy szabályok, intézmények, szereplők és normák együtt határozzák meg, hogyan működik az online világ.

Ahogy beleástam magam az anyagba és kapcsolódó cikkekbe, egyre világosabb lett számomra, hogy nincs egyetlen globális „kiberszabályozó szerv”. Inkább sok kisebb szabályozási rendszer, szabványosító testület és nemzetközi kezdeményezés mozaikját látjuk. Ez egyszerre rugalmas és kaotikus. Előnye, hogy gyorsan lehet innoválni, ugyanakkor nehéz egységesen kezelni a biztonsági kérdéseket.

Különösen erős benyomást tett rám az, amikor az **IoT-ről, automatizálásról, megavárosokról** volt szó. Egy modern városban szinte már minden hálózatba kötött. Közlekedési lámpák, vízellátási rendszerek, energiahálózatok, közlekedési rendszerek és szenzorhálózatok is kapcsolódhatnak digitális felügyeleti rendszerekhez. Egy rosszul védett ipari vezérlőrendszer (ICS) vagy IoT-elem nemcsak adatvédelmi incidenshez, hanem valódi fizikai károkhoz is vezethet. Ez volt az a pont, ahol végleg összeállt bennem, hogy a kiberbiztonság **nem maradhat az IT-osztály zárt dobozában**, mert a hatásai messze túlnyúlnak rajta.

## Nem minden threat actor egyforma

Az egyik leggyakorlatiasabb tapasztalat számomra az volt, hogy mennyire nem mindegy, **ki támad**. A „hacker” szó a médiában gyakran egy leegyszerűsített képet idéz fel, itt viszont szépen kirajzolódtak a különböző **fenyegető szereplő-típusok**.

A **hobbi hackerek** (vagy sokszor pejoratíve „script kiddie-k”) tipikusan olyan emberek, akik kész eszközökkel dolgoznak, és sokszor látványos, de technikailag nem túl kifinomult dolgokat csinálnak. A könnyen kihasználható sebezhetőségekre jó hazai példa a BKK online jegyrendszerének 2017-es esete. Egy 18 éves felhasználó a webes felület hibáját kihasználva 50 forintért tudott bérletet vásárolni, majd jelezte a problémát. Az eset számomra azt mutatta meg, hogy súlyos következményekhez nem feltétlenül kell különösen kifinomult támadás. Egy alapvető alkalmazáslogikai hiba is elegendő lehet.

A **kiberbűnözői csoportok** teljesen más szintet képviselnek. Ők szervezetten, üzemszerűen dolgoznak. A csapatukat jellemzően malware-fejlesztők, exploit írók, pénzmosásért felelős emberek, botnet-üzemeltetők alkotják. A motiváció itt egyértelműen a pénz. Ransomware-kampányok, bankkártyaadat-lopások, kompromittált webshopok – ezek mind ennek az ökoszisztémának a termékei. Ahogy utánaolvastam, nagyon érdekes volt látni, hogy létezik gyakorlatilag **„ransomware-as-a-service”** modell is, ahol a kevésbé technikai támadók egyszerűen „bérlik” az infrastruktúrát.

A **hacktivisták** esetében a cél inkább az **üzenetközvetítés**. Jellemző motivációik a politikai tiltakozás, a társadalmi igazságosság és a környezetvédelem. Tipikus eszközeik a weboldal-defacement, a DDoS-támadás vagy bizonyos adatok nyilvánosságra hozatala. Itt a technikai kifinomultság gyakran alacsonyabb, viszont **kommunikációs szempontból** sokszor hatásosabbak. Egy elcsúfított főoldal vagy egy leállt kormányzati portál óriásit tud szólni a médiában.

Az **APT-k (Advanced Persistent Threat-ek)** külön ligában játszanak. Gyakran állami vagy államilag támogatott, geopolitikai célokat követő szereplőkhöz kötődnek. A fogalom lényege azonban elsősorban a célzott, tartós és rejtett jelenlét. Ezek a szereplők hosszú időn keresztül maradhatnak észrevétlenek a rendszerekben, egyedi kártevőkkel, kifinomult exploitokkal, valamint rejtett parancs- és vezérlőcsatornákkal. Ipari kémkedés, diplomáciai információk megszerzése, kritikus infrastruktúrák zavarása – mind szóba jöhet. Ezeknél a csoportoknál már nem lehet csak „IT-szinten” gondolkodni, elengedhetetlen a **nemzetbiztonsági** perspektíva is.

Ehhez társul a **kiber-feketepiac** képe, ahol ellopott adatok, botnet-hozzáférések, zero-day exploitok, ransomware-készletek és pénzmosási szolgáltatások cserélnek gazdát.

Ahogy jobban utánanéztem ennek a világnak, úgy láttam, hogy a kiberbűnözés mögött is **piaci logika** működik szerepkörökkel, specializációval, árképzéssel és egyfajta ügyfélszolgálattal.

## A hackelés mint több lépésből álló folyamat

A legelején még én is kicsit hollywoodi fejjel gondolkodtam. A hacker leül, pár sor kódot beüt, és már bent is van. Az elsajátított tudásanyag meggyőzött arról, hogy a valóság sokkal szisztematikusabb. A hackelés **folyamat**, nem pedig egy varázsmozdulat.

A **Lockheed Martin Cyber Kill Chain** modellje szépen végigvisz ezen a folyamaton:

- felderítés (reconnaissance),
- fegyverré alakítás (weaponization),
- kézbesítés (delivery),
- kihasználás (exploitation),
- telepítés (installation),
- parancs- és vezérlés (command and control),
- és végül a cél szerinti műveletek (actions on objectives).

A felderítésnél például ma már nemcsak IP-címekre és portokra gondolok, hanem legalább ugyanannyira a **szociális és szervezeti információkra** is, például ki és hol dolgozik, milyen technológiákat használnak, kik a beszállítók. Ezekből később nagyon jól felépíthető egy célzott adathalász kampány, vagy eldönthető, hogy a fővállalatot vagy inkább egy gyengébb láncszemet érdemes támadni.

A fegyverré alakítás, a kézbesítés, a kihasználás és a telepítés lépései együtt azt mutatják meg, hogyan válhat egy absztrakt sebezhetőségből **konkrét támadás**. Egy CVE-ben (Common Vulnerabilities and Exposures) dokumentált sérülékenység kihasználására exploit készülhet, amely például fertőzött dokumentumon vagy linken keresztül juthat el a célponthoz.

A **Command and Control** fázis talán az egyik legkreatívabb terület. Itt jelenik meg a rejtett, titkosított kommunikáció, a közösségi oldalak használata, a többlépcsős proxy-láncok és botnetek. Itt kapcsolt be nálam az attribúció problémája. Minél többet tudtam meg arról, hogyan rejtik el a támadók a nyomukat, annál érthetőbbé vált számomra, hogy miért olyan nehéz biztosan, kétséget kizáróan bizonyítani, hogy egy adott támadás mely szereplőkhöz köthető.

A Lockheed Martin Cyber Kill Chainhez nagyon jól passzolt a **MITRE ATT&CK** keretrendszer, amelyet részben a kurzus, részben saját kutatómunkám alapján ismertem meg. Az ATT&CK nem egyszerűen lineáris időrendben, hanem **taktikákban és technikákban** írja le a támadói viselkedést. Ennek köszönhetően egy valós támadást nemcsak elmesélni lehet, hanem egy közös szakmai nyelven is le lehet írni.

## A hatások nem állnak meg IT-szinten

Az egyik legnagyobb szemléletváltás az volt, amikor a támadó szereplők vizsgálatában átálltunk arról, hogy „hogyan támadnak”, arra, hogy **„mit okoznak”**. Itt jöttek képbe az elsődleges, másodlagos és tágabb társadalmi hatások.

Az **elsődleges hatások** közvetlenül az IT-eszközökön jelennek meg: adatlopás, titkosítás, törlés, szolgáltatásmegtagadás, ipari rendszerek manipulálása. Ezeknél különbséget lehet tenni zavaró (disruptive) és kihasználó (exploitative) események között. Jó példa egy zavaró hatásra egy zsarolóvírus, amely leállítja egy gyár vezérlőrendszerét, kihasználó eseményre pedig a POS-terminálokból bankkártyaadatokat ellopó malware, amely úgy gyűjti a kártyaszámokat, hogy a pincér, a pénztáros észre sem veszi, mi történik.

A **másodlagos hatások** már az üzleti működés szintjén jelentkeznek: bevételkiesés, leállt gyártósorok, túlórák, eszközcserék költségei, jogi eljárások, bírságok, reputációs károk. Ha „csak” egy weboldal felülete van megrongálva (defacement), amit fél óra alatt vissza lehet állítani, a másodlagos hatás kicsi. Ha viszont három napra leáll egy teljes üzem vagy egy légitársaság jegykiadó rendszere, akkor a közvetett következmények már sokszorosan meghaladják az eredeti technikai kárt.

Számomra a **tágabb társadalmi hatások** voltak a legijesztőbbek. Ezek már a társadalmat, a gazdaságot vagy a fizikai környezetet érintik. Ilyen következménnyel járhat például egy energiahálózat elleni támadás, amely több százezer embert hagy áram nélkül, vagy egy nagy kikötő megbénítása, amely az ellátási láncok globális zavarához vezet. Ilyenkor már nem lehet azt mondani, hogy „egy cég magánügye”.

Harry és Gallagher taxonómiája sokat segített az elsődleges hatások kategorizálásában. A kurzus hatásközpontú megközelítése pedig arra tanított, hogy ne csak technikai szinten, hanem az **IT–üzlet–társadalom** összefüggésében is vizsgáljam a következményeket. Ez egyfajta gondolkodási mátrixot adott.

Ha egy incidens történik, akkor fel tudom tenni magamnak a következő kérdéseket:

- Milyen típusú eseményről van szó (adatsértés, szolgáltatásmegtagadás, zaklató esemény, identitáslopás, rendszermódosítás)?
- Mi látszik mindebből IT-szinten, mi az üzleti hatás, és van-e társadalmi következménye a történteknek?

## Attribúció és a stratégiai gondolkodás fontossága

Ahogy beleástam magam a kibertámadások elkövetőinek azonosításába és a stratégiai gondolkodás fontosságának kérdésébe, egyre inkább az jött le, hogy a **technikai bizonyítékok önmagukban ritkán elégségesek**. Az IP-cím lehet hamisított, a gép lehet botnet-tag, a szerver lehet bérelt VPS egy harmadik országban. A logok hiányosak vagy manipuláltak lehetnek, a nemzetközi jogi környezet pedig lassú és töredezett. Mindez azt jelenti, hogy még ha technikailag sejtjük is, ki áll egy támadás mögött, a jogi és politikai térben ez közel sem ennyire egyszerű.

Ez vezetett el ahhoz a gondolathoz, hogy a kiberbiztonságra **stratégiai kérdésként** kell tekinteni. Nem minden támadás igényel állami beavatkozást, de vannak olyan események, amelyek túlmutatnak a magánszférán. A kulcs itt az, hogy értsük a **hatásszinteket**, és ennek megfelelően döntsünk arról, mikor lép be a kormány, mikor elég a piaci önszabályozás, és mikor van szükség új nemzetközi normákra.

## Záró gondolat

Ha össze kellene foglalnom, hogy mit adott nekem ez a kurzus, azt mondanám, hogy **egy új gondolkodásmódot**.

- Már nemcsak eszközöket és protokollokat látok, hanem **összefüggéseket**: technológia, ember, szervezet, jog és politika együtt alakítja a kibertér kockázatait.
- Tudom, hogy a támadások mögött különböző **threat actor-típusok** állnak, más motivációkkal és erőforrásokkal.
- Van egy világos képem arról, hogy a hackelés **folyamat**, nem trükk, és hogy a Kill Chain és a MITRE ATT&CK hogyan segít ezt modellezni.
- Megtanultam a hatásokat **elsődleges, másodlagos és tágabb társadalmi** szinten nézni, és ezzel együtt arról gondolkodni, hogy mikor beszélünk csak egy cég problémájáról, és mikor valami olyasmiről, ami már a társadalom stabilitását is érinti.
- És végül megértettem, hogy az attribúció, a kormányzás és a nemzeti stratégia miért elválaszthatatlan része a kiberbiztonsági képletnek.

Összességében **ez a kurzus és az elvégzése során végzett kutatómunkám** megtanított arra, hogy a kiberbiztonság nem egy egyszerű „IT-s hobbi”, hanem **komplex stratégiai kérdés**, ahol a technikai részletek és az emberi, szervezeti, társadalmi szempontok elválaszthatatlanul összefonódnak. Ezt a szemléletet fogom magammal vinni a további tanulmányaim során.
