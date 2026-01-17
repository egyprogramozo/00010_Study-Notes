# Linux könyvtárszerkezete (Ubuntu)

**Források és felhasznált eszközök:**

- [ChatGPT](https://chatgpt.com/), [DeepSeek](https://www.deepseek.com/)

**A jegyzetet készítette:**

    Hajdu Gergely, [https://egyprogramozo.github.io](https://egyprogramozo.github.io/)

A Linux egy **Unix-szerű** operációs rendszer, ahol a rendszer “gerince” a **kernel** (hardverkezelés, folyamatok, memória, driverek), és erre épülnek a **felhasználói térben futó eszközök** (shell, parancsok, szolgáltatások, grafikus felület). A mindennapi munka kulcsa a **fájl–jogosultság–folyamat** hármas: szinte mindent fájlként érsz el (eszközök is a `/dev` alatt), a hozzáférést jogosultságok/ownership (tulajdonos/csoport) szabályozza, és a rendszer sok külön folyamatból áll össze. Ubuntu alatt adminisztrációra jellemzően **sudo**-t használsz (nem “állandó root” munkát), és fontos alapelv, hogy a konfigurációk általában szövegfájlokban vannak, a hibakeresés pedig logokon és rendszerállapoton (pl. `/var/log`, `journalctl`, `/proc`, `/sys`) keresztül történik.

## Gyorslista (gyakran használt mappák):

- `/` – a fájlrendszer gyökere (minden innen indul)

- `/home` – felhasználói fájlok és beállítások

- `/etc` – rendszer- és szolgáltatáskonfigurációk

- `/usr` – telepített programok és megosztott erőforrások “fő helye”

- `/usr/bin` – parancsok/programok többsége

- `/var` – változó adatok (állapot, cache, logok)

- `/var/log` – naplók, hibakereséshez kulcs

- `/tmp` – ideiglenes fájlok (nem garantáltan tartós)

- `/run` – futásidejű adatok (boot óta él, gyakran memóriában)

- `/dev` – eszközfájlok (lemezek, terminálok, stb.)

- `/proc` – folyamat- és kernel információk (virtuális)

- `/sys` – eszköz/driver/kernel nézet (virtuális)

- `/boot` – boothoz szükséges fájlok (kernel, initramfs, stb.)

- `/media` – automatikus csatolási pontok (USB, külső meghajtó)

- `/mnt` – kézi/ideiglenes csatolási pont

- `/opt` – külső/vendor jellegű “külön” szoftverek

- `/srv` – szolgáltatások által kiszolgált adatok (konvenció)

- `/root` – a root felhasználó home könyvtára

- `/snap` – Snap csomagok “látható” tartalma (Ubuntu-n gyakori)

- `/var/tmp` – ideiglenes fájlok, amelyeknek reboot között is meg kell maradniuk (ritkábban takarítják, mint `/tmp`)

- `/var/lib/snapd` – snapd állapot és adatok (Snap)

## Könyvtárak (mappák) Ubuntu alatt

Az Ubuntu (Debian-alapú rendszerként) a legtöbb Linux disztróhoz hasonlóan a **Filesystem Hierarchy Standard (FHS)** logikáját követi: a fájlrendszer egy **egyetlen fa**, aminek a teteje a **gyökérkönyvtár: `/`**. Minden útvonal innen indul, még akkor is, ha fizikailag több lemezen/partíción vannak az adatok (mountolás). 

A kezdők egyik leggyakoribb félreértése: a “root” két külön dolgot jelenthet.

- **`/` (root directory / gyökérkönyvtár):** a fájlrendszer “teteje”.

- **`root` (root user / szuperuser):** egy felhasználó, aki mindent megtehet a rendszeren.  
  Ubuntu alatt a root felhasználó **létezik**, de a **jelszava alapból zárolt**, ezért közvetlen “root login” általában nincs; rendszergazdai műveleteket a saját felhasználóddal, **`sudo`**-val végzel.

## Könyvtárak (mappák) részletezése

**`/` – a gyökér (root directory)**  
Ez a “főkapu”: minden más könyvtár ebből ágazik. Ha valami útvonalat látsz (pl. `/etc/ssh/sshd_config`), az mindig a `/`-től értendő. 

**`/etc` – rendszerkonfiguráció (host-specifikus)**  
Itt vannak a gép beállításai: szolgáltatások konfigurációi, hálózati configok, user- és rendszer-szintű defaultok. Nagyon tipikus minta: *ha valamit beállítasz*, annak nyoma sokszor itt van. Fontos: az `/etc` “konfig”, nem “program”: nem ide telepítesz binárisokat, hanem beállításokat kezelsz.

**`/home` – felhasználói adatok és beállítások**  
Minden normál felhasználónak itt van a saját könyvtára (pl. `/home/gergely`). Itt vannak a dokumentumaid, és rengeteg alkalmazás-konfig a rejtett fájlokban (`~/.config`, `~/.ssh`, stb.). Ha egy alkalmazás “felhasználói szinten” állítódik, az jellemzően itt történik.

**`/root` – a root felhasználó home könyvtára**  
Ez **nem** a `/`! Ez a root user saját “home”-ja. Gyakori oka, hogy külön van a `/home`-tól: ha a `/home` külön partíción van és nem csatolódik fel, a root akkor is tud dolgozni vészhelyzetben.

**`/bin` és `/sbin` – “alap” parancsok (történelmileg)**  
Klasszikusan a **`/bin`** a minden felhasználónak fontos alap parancsok (pl. `ls`, `cp`), a **`/sbin`** pedig a rendszeradmin eszközök helye. **Modern Ubuntu/Debian rendszereken viszont gyakori az ún. “/usr merge”**: a `/bin`, `/sbin`, `/lib` sokszor csak **symlink** a `/usr/...` megfelelőjére (pl. `/bin → /usr/bin`). Emiatt ma sokszor azt látod: “minden a /usr alatt van”, miközben a régi útvonalak kompatibilitásból megmaradnak.

**`/usr` – a “telepített rendszer” (programok, library-k, share)**  
Itt van a legtöbb telepített program és erőforrás:

- **`/usr/bin`** – parancsok/programok

- **`/usr/sbin`** – admin jellegű programok

- **`/usr/lib`** – könyvtárak (library-k)

- **`/usr/share`** – architektúra-független adatok (manpage, locale, ikonok, stb.)  
  Gondolkodj úgy, hogy `/usr` inkább “vendor/system content”, és kevésbé “gép-specifikus konfiguráció” (az inkább `/etc`).

**`/lib` (és variánsai) – alap könyvtárak (történelmileg)**  
A rendszer indulásához és a legfontosabb binárisok futásához szükséges library-k hagyományos helye. /usr merge esetén gyakran ez is symlink a `/usr/lib` felé. Ha 64-bites rendszeren látsz olyat, hogy `lib64`, az architektúra-szétválasztás miatt van.

**`/var` – változó adatok (logok, cache, állapot)**  
Ha azt kérdezed: “hol nő a lemezfoglalás?”, sokszor a válasz: `/var`. Itt vannak logok (`/var/log`), cache-ek (`/var/cache`), és rengeteg szolgáltatás futás közben változó állapota (`/var/lib`). Az FHS (Filesystem Hierarchy Standard) kifejezetten ide sorolja a folyamatosan változó tartalmakat.

**`/var/log` – naplók**  
Klasszikus szöveges logok itt laknak (pl. `auth.log`, `syslog`, szolgáltatás-logok). Systemd-s rendszeren a naplózás nagy része **journald**-ba is megy; ennek a tárolása tipikusan **`/run/log/journal`** (nem tartós) vagy **`/var/log/journal`** (tartós, ha engedélyezve van).

**`/var/lib` – tartós állapotadatok (például csomagkezelés)**  
Itt sok “belső adatbázis” él. Példa: a Debian/Ubuntu csomagkezelés (dpkg) admin adatbázisa alapból **`/var/lib/dpkg`**. Emiatt ezt a területet kézzel “takarítani” nagyon veszélyes: ha törölsz belőle, az csomagkezelési hibákhoz vezethet.

**`/etc/apt` – APT (Advanced Package Tool) beállítások (repo lista, kulcsok, policy)**  
Ha Ubuntu alatt repository-kat kezelsz, a fő konfigok itt vannak. A forráslisták tipikusan a **`/etc/apt/sources.list`**-ben és a **`/etc/apt/sources.list.d/`** könyvtárban vannak (külön fájlokba szervezve).

**`/tmp` – ideiglenes fájlok**  
Átmeneti tároló: programok ide pakolnak “munkafájlokat”. Fontos, hogy a `/tmp` tartalma **nem garantáltan tartós**: sok rendszeren rebootkor ürülhet, és gyakran memóriából (tmpfs) is szolgálódhat ki, illetve automatikus takarítás is futhat rajta. Ha olyan ideiglenes fájl kell, ami nagyobb eséllyel megmarad reboot után is, akkor erre a célra jellemzőbb a **`/var/tmp`**.

**`/run` – futásidejű (boot óta élő) adatok**  
Ez modern, rendszeresen **tmpfs** (memóriában él), és a “most futó rendszer” runtime állapotait tartalmazza (Process ID-k, socketek, lockok, stb.). Ha újraindítasz, ez újraépül.

**`/dev` – eszközfájlok**  
Itt jelennek meg a hardverek/virtuális eszközök “fájlként” (pl. diszkek, terminálok). Klasszikus példa: `/dev/sda`, `/dev/nvme0n1`, `/dev/null`. Nem “adatot tárolsz” itt, hanem interfészeket használsz.

**`/proc` – folyamatok és kernel infó (virtuális FS)**  
Ez nem “valódi” fájlrendszer a diszken, hanem a kernel által generált nézet. Példák: `/proc/cpuinfo`, `/proc/meminfo`, folyamat-specifikus mappák (`/proc/<pid>/`). Hibakeresésnél aranybánya, de kezdőként ne kezdd el “takarítani”.

**`/sys` – eszközök/driver-ek/kernel funkciók (sysfs)**  
Szintén virtuális nézet, strukturáltabban “hardware/driver” fókuszban. Például hálókártyák: `/sys/class/net`. Haladó admin műveletek néha írnak is ide, de ez már a “tudatosan, pontosan” kategória.

**`/boot` – boothoz szükséges fájlok**  
Kernel(ek), initramfs, bootloaderhez kapcsolódó dolgok. Ha kernel frissül, itt történik mozgás. Általában nem itt dolgozol kézzel, csak ha valami boot-probléma van.

**`/media` – automatikus csatolási pontok**  
Ha bedugsz egy USB-t, a desktop környezet gyakran ide mountolja (pl. `/media/<user>/<label>`). Tanulási tipp: nézd meg `mount` vagy `lsblk` kimenettel, hova került.

**`/mnt` – kézi/ideiglenes mount pont**  
Tipikusan admin használja, ha “most gyorsan ide felmountolok valamit”. A különbség `/media`-hoz képest inkább konvenció: `/media` automatikus, `/mnt` manuális.

**`/opt` – külső/extra szoftverek**  
Ha valami nem a disztró csomagkezelőjével jön “szokványosan”, vagy vendor telepítő rakja fel, gyakran ide kerül (pl. nagyobb, önálló alkalmazáscsomagok).

**`/srv` – szolgáltatott tartalmak**  
Az FHS szerint ide kerülhetnek a szolgáltatások által “kiszolgált” adatok (pl. web, ftp). A gyakorlatban sokszor látod még `/var/www`-t is, de a koncepció: “amit a service ad ki, annak legyen rendezett helye”.

**`/snap` – Snap csomagok “kibontott/mountolt” tartalma**  
Ubuntu alatt gyakori a Snap. A `/snap` könyvtárban jelennek meg a snap csomagok fájljai: pl. `/snap/<snapname>/<revision>` (mountpoint), és gyakran van `current` symlink is. Ezt jó tudni, mert első ránézésre olyan, mintha “tele lenne fájlokkal”, valójában sokszor mountolt tartalom.
A **Snap** egy Canonical által fejlesztett **csomagolási és terjesztési forma + csomagkezelő rendszer** Ubuntuhoz (és más disztrókhoz is). A lényege, hogy egy alkalmazás “egyben” érkezik (sokszor a függőségeivel együtt), a rendszer pedig **`snapd`** segítségével telepíti, frissíti és futtatja.
A Snap csomagok tartalma tipikusan egy **read-only SquashFS** fájlrendszerként kerül a gépre, és **mountolva** jelenik meg a **`/snap`** alatt.

**`/var/lib/snapd` – Snap tárolt állományai és állapota**  
A snapd a saját tartós adatait jellemzően a `/var/lib/snapd` alatt tartja. A snap telepítéskor letöltött `.snap` (SquashFS) fájl a dokumentáció szerint a **`/var/lib/snapd/snaps`** alatt találhatók (egyes dokumentációkban **`/var/lib/snaps/snaps`** is szerepel), és innen loop mountolódik a **`/snap`** alá. Egyes rendszereken/telepítésekben a Snap körüli állományok több revisionje a **`/var/lib/snapd/snaps`** környékén is jelentős helyet foglalhat, ezért a takarítást érdemes **snap parancsokkal** végezni, nem kézi törléssel.

## Gyors tanulói “iránytű”

- “**Hol a beállítás?**” → nagy eséllyel **`/etc`** (vagy user-szinten a **`~`** alatt).

- “**Hol a log?**” → **`/var/log`** és/vagy **`journalctl`** (journald).

- “**Hol a program?**” → többnyire **`/usr/bin`**, **`/usr/sbin`** (usr-merge miatt a régi `/bin` is ide mutathat).

- “**Mi fut most?**” → runtime: **`/run`**, állapot: **`/var/lib`**, diagnosztika: **`/proc`**, **`/sys`**.

- “**Admin jog kell?**” → Ubuntu mintázat: **`sudo ...`**, nem “rootként élek egész nap”. 
