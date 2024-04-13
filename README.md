# Úkol: Piškvorky 4/5

Tento úkol navazuje na [Piškvorky 3](https://github.com/Czechitas-podklady-WEB/ukol-piskvorky-3). Tentokrát oživíš i všech zbylých 90 políček a přidáš detekci výhry.

## Zadání

1.  Pokračuj v repozitáři `piskvorky` z předchozích úkolů.

1.  Nastav posluchač události všem políčkům.

    1.  Vyber všechna políčka pomocí `document.querySelectorAll`.

    1.  Metodou `forEach` je všechny projdi a přidej jim posluchač události na kliknutí. Zařiď, aby kliknutí zavolalo funkci, kterou máš nachystanou z předchozího úkolu.

    1.  Původních deset posluchačů smaž. Nejsou díky předchozímu kroku již potřeba.

    1.  Oveř si, že nyní hra reaguje na kliknutí na všechna políčka.

        ![všechna tlačítka oživená](zadani/vsechny.gif)

1.  Po každém tahu ověř, jestli někdo nevyhrál. Využij již hotovou funkci `findWinner` od cizího autora.

    1.  Do tvého javascriptu zapoj funkci `findWinner`. Na první řádek, úplně na začátek tvého javascriptového souboru přidej následující kód.

        ```js
        import { findWinner } from 'https://unpkg.com/piskvorky@0.1.4'
        ```

        To ti umožní používat funkci `findWinner` v tvém kódu.

        Import výše musí být opravdu na prvním řádku tvého javascriptového souboru a v HTML souboru ti u načítání javascriptu nesmí chybět `type="module"`. Jinak načtení funkce selže.

        Funkce `findWinner` očekává jeden vstupní parametr, pole řetězců `'x'` pro křížek, `'o'` pro kolečko a `'_'` pro neobsazené políčko.
        Pole tedy v sobě bude mít 100 prvků (textových řetězců vždy s jendím znakem).
        Začíná se v levém horním políčku a postupuje se po prvním řádku doprava.
        Na konci řádku se přeskkočí na první políčko druhého řádku (to tedy bude v poli na 11. místě, s indexem `10`), až poslední prvek pole s indexem `99` bude obsahovat políčko úplně vpravo dole.
        Zpátky po zavolání vrací, kdo vyhrál.

        ### Návratové hodnoty funkce `findWinner`:

        - `'x'` - vyhrál hráč s křížky
        - `'o'` - vyhrál hráč s kolečky
        - `null` - hra ještě neskončila, zatím nikdo nevyhrál
        - `'tie'` - hra skončila remízou

        ### Ukázka použití:

        Inspiruj se níže zjednodušenou hrou 3x3:

        ```js
        const herniPole = ['_', 'o', 'x', 'x', 'o', '_', '_', 'o', '_']
        const vitez = findWinner(herniPole)
        if (vitez === 'o' || vitez === 'x') {
        	alert(`Vyhrál hráč se symbolem ${vitez}.`) // Vyhrál hráč se symbolem 'o' nebo 'x'.
        }
        ```

        To stejné herní pole lze pro lepší přehlednost zapsat i takto:

        <!-- prettier-ignore -->
        ```js
        const herniPole = [
        	'_', 'o', 'x',
        	'x', 'o', '_',
        	'_', 'o', '_',
        ]
        ```

        První tři prvky odpovídají prvnímu řádku. Druhé tři druhému. Třetí třetímu.

        ![ukázka 3x3](zadani/3x3.png)

    1.  Po každém tahu projdi všech sto políček a vytvoř z nich pole vhodné pro funkci `findWinner`. Podobu pole si můžeš ověřit vypsáním do vývojářské konzole. Mělo by mít sto položek a obsahovat jen řetězce `'x'`, `'o'` a `'_'`. Prvních deset položek by mělo odpovídat prvnímu řádku podobně jako u varianty 3x3.

    1.  Pole předej funkci `findWinner`.

    1.  Pokud ti vrátí, že vyhrál křížek nebo kolečko, zobraz uživateli zprávu o výherci pomocí funkce `alert`. Návratové hodnoty `null` a `'tie'` ignoruj.

    1.  Po tom, co uživatel odklikne `alert`, přenačti stránku voláním zabudované funkce `location.reload()`, která přenačte stránku, aby uživatel mohl začít novou hru.

        ![oznámení o vítězi](zadani/vitez.gif)

    1.  Zkus odehrát pár her a ověřit, že tvůj kód správně pozná výhru křížku i kolečka.

## Bonus

- Pokud se ti poslední symbol nestíhá na obrazovce včas zobrazit, pozdrž zobrazení `alert` hlášky pomocí časovače.

  ![zpoždění oznámení](zadani/zpozdeni.gif)

- Pokud hra skončila remízou, zobraz o tom uživateli zprávu.

  ![remíza](zadani/remiza.png)
