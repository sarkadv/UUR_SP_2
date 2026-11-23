# Tiny Planet Builder

Aplikace v JavaFX pro vytváření mimozemských kolonií umisťováním dlaždic do 2D mapy. 
Semestrální práce z předmětu KIV/UUR.

## Funkce

- Stavění na **fialové, zelené nebo oranžové planetě**, každá má vlastní sadu dlaždic.
- Volba rozměrů mapy a **denního nebo nočního režimu** planety.
- **Světlý a tmavý režim** aplikace, který ovlivňuje i vzhled mapy (lze vypnout v nastavení).
- Posouvání mapy klávesami **W, S, A, D** a zoomování kolečkem myši. Šipky po stranách mapy ukazují, kterým
  směrem jsou další dlaždice.
- **Nástroje pro práci s mapou:** vybrat, vymazat, kapátko, výběr oblasti, výplň oblasti a výplň hranic oblasti.
- **Zpět** (Ctrl + Z).
- **Ukládání a načítání** mapy do textového souboru s kontrolou vstupu a **export** mapy jako obrázku PNG.
- Okno **Nápověda**, které popisuje všechny funkce a klávesové zkratky.

## Klávesové zkratky

| Zkratka      | Akce                     | Zkratka       | Akce                  |
| ------------ | ------------------------ | ------------- | --------------------- |
| Ctrl + N     | Nová mapa                | Shift + E     | Kapátko               |
| Ctrl + S     | Uložit mapu              | Shift + C     | Výběr oblasti         |
| Ctrl + L     | Načíst mapu              | Shift + F     | Výplň oblasti         |
| Ctrl + E     | Exportovat jako obrázek  | Shift + B     | Výplň hranic          |
| Ctrl + Z     | Zpět                     | Backspace     | Vymazat               |
| Ctrl + M     | Světlý / tmavý režim     | Escape        | Vybrat (zrušit volbu) |
| Ctrl + O     | Nastavení                | ↑ / ↓         | Posun menu dlaždic    |
| Ctrl + H     | Nápověda                 | Ctrl + A      | O aplikaci            |

## Formát uloženého souboru

```
5                          // šířka mapy
5                          // výška mapy
5                          // odmocnina z počtu viditelných dlaždic
2                          // číslo planety (zde oranžová)
D                          // denní / noční režim planety
230 230 230 230 230        // dvojrozměrné pole identifikátorů dlaždic
230 200 170 220 230
230 170 210 170 230
230 220 170 200 230
230 230 230 230 230
```

Při načítání se kontroluje, že soubor obsahuje všechny údaje a že dlaždice patří ke zvolené planetě a režimu.

## Implementace

- **Mapa** je čtvercový `GridPane` složený z `ImageView` jednotlivých dlaždic. Datový model mapy je
  dvojrozměrné pole identifikátorů dlaždic, podle kterého se mapa při každé změně překreslí. Obrázky dlaždic
  načítá třída `ImageLoader` ze spritesheetů.
- **Výběr oblasti** si pamatuje začátek a konec tažení myší ve třídě `DragCoordinates` a vybrané dlaždice
  zvýrazní.
- **Export** poskládá dlaždice do nového okna a uloží jeho snímek metodou `snapshot()`.
- Tmavý režim používá kaskádový styl `darkmode.css` (zkrácená verze oficiálního tmavého režimu JavaFX).

Struktura projektu: `src/model` (mapa, dlaždice, položky nápovědy), `src/view` (okna a komponenty),
`src/controller` (logika hlavního okna a mapy), `src/util` (načítání a ukládání, obrázky, nástroje),
`resources` (spritesheety, ikony, styl pro tmavý režim).
