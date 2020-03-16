# Výpisy chyb ze zanořených funkcí

Teď si ukážeme (nebo zopakujeme), jak Python vypíše chybu, která
nastane v zanořené funkci.

Pročti si následující ukázkový příklad.

> [note]
> Tohle je absurdní ilustrační příklad, ne ukázka jak dobře programovat!

<!-- XXX: automatic line numbers? -->

```python
def podel(delenec, delitel):
    """Podělí čísla mezi sebou a vrátí výsledek."""
    return delenec / delitel        # řádek 3


def podel_nulou(cislo):
    """Vydělí dané číslo nulou a vrátí výsledek."""
    return podel(cislo, 0)          # řádek 8


def ukaz_priklad():
    """Spočítá ukázkový příklad a výsledek vypíše (nevrátí!)"""
    vysledek = podel_nulou(3)       # řádek 13
    print(vysledek)

ukaz_priklad()                      # řádek 16
```

Co se stane, ktyž tohle pustíš?

```pycon
Traceback (most recent call last):
  File "ukazka.py", line 16, in <module>
    ukaz_priklad()
  File "ukazka.py", line 13, in ukaz_priklad
    vysledek = podel_nulou(3)
  File "ukazka.py", line 8, in podel_nulou
    return podel(cislo, 0)
  File "ukazka.py", line 3, in podel
    return delenec / delitel
ZeroDivisionError: division by zero
```

Všimni si, že každá z funkcí, jejíž volání vedlo k chybě, je uvedena ve výpisu.
Skutečná chyba (tedy místo, které musíme opravit) je asi někde poblíž těchto
míst:

- Na řádku 3, ve funkci `podel`, vzniklo dělení nulou.
  Měla by funkce `podel` zjistit, jestli dostane nulu, a nějak na to
  zareagovat?
- Na řádku 8, ve funkci `podel_nulou`, voláme `podel` s dělitelem 0.
  Má to tak opravdu být?
- Na řádku 13, ve funkci `ukaz_priklad`, voláme funkci `podel_nulou`.
  Kdybychom to nedělali, chyba by taky nevznikla!
- Na řádku 16, ne ve funkci, voláme funkci `ukaz_priklad`.
  Možná by to chtělo použít jiný příklad?

Ale Python (a asi ani ty) nemůže vědět, co tím programem programátor myslel,
a kdy by tedy bylo nejlepší chybu opravit.
Ukáže tedy v programu všechna místa, která k chybě vedla.
Je na programátorovi, aby z nich vybral to nejvhodnější a zaměřil se na něj.

Tahle ukázka je samozřejmě jen teoretická, ale v reálných programech vypadá
hlášení chyb stejně.
Až takovou složitou hlášku uvidíš, nepanikař!
Python se snaží co nejvíc napovědět a usnadnit ti chybu najít a opravit.
Sice stroze a anglicky, ale snaží.
Vyjdi mu vstříc a nauč tyhle se hlášky číst.
