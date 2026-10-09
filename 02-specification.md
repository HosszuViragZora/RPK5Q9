# Project_outline: [sample linkje]

## Comparison of Procedural Map Generation Methods

## 1. Szereplők és jogosultságok

| Szerep | Igény | Hozzáférés |
|:---|:---|:---|
| Felhasználó | Generálási adatok kinyerése | Be tudja állítani a generálási paramétereket és hozzáfér az adatokhoz |

## 2. User case-ek
### Pályák generálásának módja
* Szereplő: Felhasználó 
* Fő folyamat:
    1. Kiválasztja melyik generálási módszert szeretné futattni (egyszerre is lehet)
    2. Beállíthatja a megegyező paramétereket (pl: pályák mérete, min szobák száma) 
    (ha ezeket nem akarja megadni, alap paraméterekkel dolgozik a rendszer)
    3. Beállítja a különböző paraméreteket (pl: kill timer) 
    (ha ezeket nem akarja megadni, alap paraméterekkel dolgozik a rendszer)
    4. Kiválasztja hányszor szeretné végifuttatni a generálásokat
    5. Kiválasztja, hogy egyszerre futtatja a kettőt vagy egymás után
    6. Lehetősége van lelőni a rendszert futtatás közben
    7. A végén megnézheti a kiértékelést vagy
        1. Külön- külön (értsd: Mindkettő adatait külön kilistázva)
        2. Összehasonlítás alapont (értsd: egy táblázatban) 
    8. Lehetősége van újra generálni

* Alternatív, hiba folyamatok: Mi történik ha a felhasználó túl nagy paramétereked as meg, vagy a kód beragad: Ha a DLA time-outól, vagy az SRP max_attemps számlálója elérte a max korlátot és nem tudtak pályát generálni, a rendszer ezt eldobja és egy újat kezd el generálni. Ha a felhasználó szakítja meg a folyamatot, akkor a részleges statisztikák kerülnek kiértékelésre.
* Utófeltétel: Mi a folyamat végeredménye? A legenerált pályák statisztikai adatai (pl. generálási idő, sűrúség, kanyargósság stb.) bekerülnek a rendszer memóriájában, készen a grafikus megjelenítésre vagy exportálásra.

## 3. Funkcionális követelmények

| Követlemény | Elfogadási kritérium | Prioritás |
|:---|:---|:---|
| A felhasználó megadja a paramétereket | A rendszer a megadott feltételek alapján képes a pályát generálni | Kötelező |
| A felhasználó kiválaszthatja, hogy egyszerre vagy egymás után futtatja a generálásokat (Erőforrás alapján) | A rendszer képes külön megvizsgálni a generálási módszereket | Kötelező |
| A felhasználó megnézheti a statisztikákat a 2 pálya generálásáról (pl. eldobott pályák aránya) | A rendszer ezeket tárolja és képes ezeket megjeleníteni | Kötelező |
| A rendszer megtartja ezeket a statisztikákat | A rendszer képes tárolni ezeket a statisztikákat pár (5) generálásig, mieéőtt törli ezeket | Ajánlott |
| A felhasználó láthassa a statisztikákat külön-külön is | Nem csak egy közös rendszerbe szedi össze a statisztikákat, külön tárolja ezeket, majd képes grafikusan megjelníteni | Ajánlott |
| A felhasználó láthasson egy tier-rendszert | A rendszer képes a nem eldobott pályákat külön szempontok alapján egy tier rendszerbe besorolni, ezt grafikusan megjeleníteni | ajánlott |
| A felhasználó tudja a tier-besorolás szempontjait állítani | A rendszer képes a leszűkített szempontok alapján tier-rendszerbe tenni a megfelelő pályákat és ezt grafikusan megjeleníteni | Lehetséges |
| A felhasználó képes kiválasztani melyik szobákat szeretné a generáláshoz használni | A rendszer képes a felhasználó megadása alapján csak az adott szobákat használni a generáláshoz, ez alapján megfelelő pályákat ad vissza és a statisztikai adatokat se rontja el. | Lehetséges |
| A felhasználó képes a statisztikai adatokat ki-exportálni | A rendszer képes a tárolt adatokat egy felhasználó-barát formátumban elmenthetővé tenni | Ajánlott |

## 4. Üzleti szabályok és korlátok

| Szabály vagy korlát | Indoklás |
|:---|:---|
| A felhasználó csak megadott min és max paraméterek között dolgozhat | Statisztikai relevancia miatt érdemes lekorlátozni ezeket. |
| A pálya akkor játszható, ha sikerült start, exit pontot legenerálni (1 tile a "játékos", akkor 3x3 terület szükséges ehhez) | Ezek nélkül nem tudunk bejutni, kijutni a pályáról |
| A pálya akkor játszható, ha minden szobályába el lehet jutni | Ha üres szobákat generálunk, ahol mondjuk a boss van, és nem tudunk eljutni oda, akkor a pálya kijátszhatatlan |
| A pálya akkor valid, hogyha elég szobával rendelkezik (min 2) | Ha nincs hely az exit és start letevésének, akkor a pályára nem lehet belépni/elhagyni |
| A pálya akkor valid, ha nincs benne túl sok szoba.  | Túl sok szoba esetén a játék élvezhetetlen lehet. |
| A kezdőpont és a végpont közötti legrövidebb út hoszsa nem haladja meg két pont közötti légvonalbeli távolság 400%-át |  A játékosnak egy hosszú folyosón való szaladgálás lehet unalmas, és frusztráló játék szempontjából |

## 6. Nem funkcionális követlemények

| Követelmény | Ellenőrzés módja |
|:---|:---|
| Időkorlát a pályák lefutására | A 2 módszer saját módszerei alapján egy körülbelüli idő kiszámolható, ehhez képest mérjük mennyi időnél tartunk. |
| Algoritmus izoláció. Ha mindkettő egyszerre fut, akkor mindkettőnek legyen lehetősége a CPU-val dolgozni | Rendszerhívások???? |
| Statiszikai probléma, a kiugró adatok kezelése | Hiba határon kívül eldobjuk az adatot? Vagy hát pont nem, mivel a statisztikát akarjuk kinyerni, akkor is, ha van benne kiugró adat |
| Szálak. Miközben futnak a generálások, a felhasználó felületnek használhatónak kell maradnia |  |
| Grafikonok olvashatósága | Skálázható legyen a grafikon |
| Konfigurációs rugalmasság. Bárki tudjon generálást indítani. | ALapvető lehetőségek a fő fülben és lehetőség egy "haladó" módra, amit megnyitva a többi lehetőséghez is hozzáfér |

## 7. Nyitott kérdések és kockázatok

## 8. Kezdeti technikai javaslat

