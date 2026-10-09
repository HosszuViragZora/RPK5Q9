## name: Hosszú Virág Zora Neptun: RPK5Q9 id: 2026-NP-02 github:https://github.com/HosszuViragZora/RPK5Q9 gitbuh_project: https://github.com/users/HosszuViragZora/projects/1/views/1

## Comparison of Procedural Map Generation Methods

A projekt lényege, kettő procedurális generálási módszer összehasonlítása. A projekt keretein belül, a Simple Room Placement és a Diffusion-Limited Aggregation generálási módszereket fogom összehasonlítani. Mindezt 2D-s grid reprezentáció segítségével, ahol 4 irányú Neumann topológiát használok. A rendszer különféle objektív szemponton alapján fogja mérni a pályák változatosságát, játszhatóságát és más mérési számait. Ezeken keresztül fogom összehasonlítani a 2 generálási módszert. Ha a pálya nem felel meg, a rendszer eldobja.

## Célok
* Elsődleges cél: A két generálási módszer összehasonlítása objektív mérőszámok alapján
* Célfelhasználók: indie, kezdő játékfejlesztők, akiknek esetleg érdekes lehet hogy melyiket válasszák a játékok megálmodása közben.
* Sikerkritérium: A program képes több száz pálya generálására, az adatok kimutatására és ezek összehasonlítására.
* Fejlesztőkörnyezet: Unity, C#

## Hatókör

### Benne van a hatókörben (Ilyesmire gondoltak ez alatt?)
* Beszerzett adatok elraktározása, kiértékelése grafikonokkal
* Eldobott pályák aránya a használhatóhoz képest
* Pálya méret állítása (egy max és minimum között)
* Generálási mennyiség beállítása

### Nincs benne a hatókörben
* Pályákra nem lehet rálépni, nem játszhatóak (játékmenet)
* Más generálási prodecúra beépítése
* Komplex grafikai megjelenítás

## Jegyzetek (Kell ide ennyi információ?)

Az első prototípus terve az, hogy mindkét Generálási módszert ki tudjuk értékelni a saját szempontjaik alapján. Legyenek ezek egyezőek, vagy nem egyezőek. Miután ez megvan, ez után lehet az összehasonlító mechanikán dolgozni.

| DLA                                                                                                                                                                                                                          | SRP                                                                                                                                                                           |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \* Map nagysága<br> \* Szobák száma <br> \* Szobák min, max mérete <br> \* Min szobák közötti távolsága<br> \* Paritcle pozíció<br> \* Particle-ök száma<br> \* Lövési sugár<br> \* Kill sugár<br> \* Max particle lépésszám<br> \* Particle méret | \* Map Nagysága<br>\* Szobák száma<br>\* Szobák min, max mérete<br>\* Min szobák közötti távolsága<br>\* Max szobaelhelyezési kísérletek<br>* Folyosó létrehozási szabálya, szélesség |
