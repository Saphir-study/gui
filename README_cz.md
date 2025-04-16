# GUI: Tkinter (grafické uživatelské rozhraní)

### Než začneš
1. Ujisti se, že máš nainstalovaný Python 3.x. Používáme vestavěnou knihovnu, takže není potřeba nic instalovat navíc.
2. Stáhni si ZIP soubor z tohoto GitHub repozitáře.
3. Zkus spustit kód. Pokud narazíš na chybu, zkopíruj kód, vlož ho do nového prázdného souboru a ulož jako Python soubor (.py).
4. Pokud problém přetrvává, kontaktuj někoho z mého týmu.

V tomto dokumentu mluvím o knihovně Tkinter. V každé části nejprve uvidíš jednoduchý příklad pro přehlednost a poté ukázku, jak je to použité v mém kódu.

---

## Co je to Tkinter?

**Tkinter** je standardní knihovna Pythonu pro vytváření grafických uživatelských rozhraní (GUI). Umožňuje vytvářet okna, tlačítka, textová pole a další prvky rozhraní. Tkinter je založen na knihovně Tk, která byla původně vytvořena pro jazyk Tcl.

---

## Základní principy Tkinteru

### 1. Hlavní okno

Každá Tkinter aplikace začíná vytvořením hlavního okna pomocí třídy `Tk`.

#### Jednoduchý příklad:
```python
import tkinter as tk  # Import knihovny Tkinter

root = tk.Tk()        # Vytvoření hlavního okna
root.title("Moje aplikace")  # Nastavení názvu okna
root.mainloop()       # Spuštění hlavní smyčky událostí
```

#### Example from my code:
```python
root = tk.Tk()                  # Vytvoření hlavního okna kalkulačky
root.title("Calculator")         # Nastavení názvu okna
root.geometry("300x400")         # Pevná velikost okna
```




### 2. Widgets

**Widgets** — jsou prvky uživatelského rozhraní jako tlačítka, popisky (label), vstupní pole atd. V Tkinteru je každý widget instancí určité třídy.

- **`tk.Label`** — textový popisek.
- **`tk.Button`** —  tlačítko, které po kliknutí provede akci.
- **`tk.Entry`** — vstupní textové pole.
- **`tk.Frame`** — kontejner pro seskupení widgetů.


#### Vytvoření tlačítka:
```python
button = tk.Button(
    root,                 # Rodičovské okno
    text="Klikni na mě",  # Text na tlačítku
    command=some_function # Funkce spuštěná po kliknutí
)
button.pack()             # Umístění tlačítka do okna
```


#### Ukázky z mého kódu:

**`tk.Entry`** — vstupní pole:
```python
input_field = tk.Entry(
    input_frame,                     # Nádoba (Frame)
    font=('arial', 18, 'bold'),      # Písmo a jeho vlastnosti
    textvariable=input_text,         # Propojení s proměnnou typu StringVar
    width=50,                        # Šířka v počtu znaků
    bg="#eee",                       # Barva pozadí (světle šedá)
    bd=0,                            # Tloušťka okraje (0 – bez okraje)
    justify=tk.RIGHT                 # Zarovnání textu vpravo
)
```

**`tk.Button`** — tlačítka kalkulačky:
```python
tk.Button(
    buttons_frame,                   # Kontejner pro tlačítka
    text=button,                     # Text na tlačítku (číslo nebo operátor)
    fg="black",                      # Barva textu
    width=10,                        # Šířka tlačítka
    height=3,                        # Výška tlačítka
    bd=0,                            # Tloušťka okraje
    bg="#fff",                       # Barva pozadí
    cursor="hand2",                  # Styl kurzoru při najetí
    command=lambda x=button:         # Funkce po kliknutí:
        button_click(x) if x != '='  # Pro čísla a operátory
        else button_equal()          # Pro tlačítko "="
)
```

**`tk.Frame`** — kontejnery pro seskupení prvků:
```python
input_frame = tk.Frame(
    root,                            # Hlavní okno
    width=312,                       # Šířka v pixelech
    height=50,                       # Výška v pixelech
    bd=0,                            # Tloušťka okraje
    highlightbackground="black",     # Barva orámování
    highlightcolor="black",          # Barva aktivního orámování
    highlightthickness=1             # Tloušťka orámování
)

buttons_frame = tk.Frame(
    root,                            # Hlavní okno
    width=312,                       # Šířka v pixelech
    height=272.5,                    # Výška v pixelech
    bg="grey"                        # Barva pozadí
)
```




### 3. Správa geometrie (umístění prvků)

Pro zobrazení prvků je potřeba je umístit pomocí jednoho ze tří správců geometrie:

- **`pack()`** — automaticky umisťuje prvky.
- **`grid()`** — uspořádává prvky do tabulky (řádky a sloupce).
- **`place()`** — umožňuje zadat přesné souřadnice.

#### Příklad s **`grid()`**:

```python
label = tk.Label(
    root,                    # Hlavní okno
    text="Hello, Tkinter!"   # Text štítku
)
label.grid(
    row=0,       # Číslo řádku v mřížce
    column=0     # Číslo sloupce v mřížce
)
```


#### Příklad z mého kódu

**`pack()`** — umístění prvků:
```python
input_frame.pack(
    side=tk.TOP  # Umístění nahoře v okně
)
buttons_frame.pack()  # Umístění pod předchozím prvkem
```

**`grid()`** — arranging buttons in a table format:
```python
tk.Button(buttons_frame, ...).grid(
    row=row,     # Číslo řádku
    column=col,  # Číslo sloupce
    padx=1,      # Horizontální odsazení
    pady=1       # Vertikální odsazení
)
```



### 4. Zpracování událostí (Event Handling)

Tkinter umožňuje reagovat na akce uživatele, jako je **kliknutí na tlačítko** nebo **vstup textu**. This is done using the `command` parameter in widgets (e.g., buttons) or event binding with the `bind` method.

#### Příklad: reakce na kliknutí tlačítka:
```python
def button_click(item):
    global expression            # Použití globální proměnné
    expression += str(item)      # Přidání znaku do výrazu
    input_text.set(expression)   # Aktualizace textu ve vstupním poli
```

#### Příklad z mého kódu
**`button_click`**  — zpracování kliknutí na tlačítko:
```python
def button_clear():
    global expression        # Použití globální proměnné
    expression = ""          # Resetování výrazu
    input_text.set("")       # Vymazání vstupního pole
```

**`button_clear`** — vymazání vstupního pole:
```python
def button_equal():
    global expression        # Použití globální proměnné
    try:
        result = str(eval(expression))  # Vyhodnocení výrazu
        input_text.set(result)          # Zobrazení výsledku
        expression = result             # Uložení výsledku
    except:
        input_text.set("Error")         # Zobrazení chyby
        expression = ""                 # Resetování výrazu
```

**`button_equal`** — výpočet výsledku:
```python
def button_equal():
    global expression
    try:
        result = str(eval(expression))     # Vyhodnocení výrazu
        input_text.set(result)             # Zobrazení výsledku
        expression = result                # Uložení výsledku
    except:
        input_text.set("Error")            # Zobrazení chyby
        expression = ""                    # Resetování výrazu
```


### 5. Proměnné v Tkinteru

Tkinter poskytuje speciální typy proměnných jako ( **`StringVar`**,  **`IntVar`**,  **`DoubleVar`** etc.) apod., které umožňují propojit data s widgety. Například **`StringVar`** uchovává text, který lze navázat na štítek nebo vstupní pole.

```python
text_var = tk.StringVar()
label = tk.Label(root, textvariable=text_var)
text_var.set("Hello, Tkinter!")
```

#### Příklad z mého kódu
**`tk.StringVar`** — propojení textu se vstupním polem:
```python
input_text = tk.StringVar()     # Vytvoření proměnné typu StringVar
input_field = tk.Entry(
    ...,                        # Ostatní parametry vstupního pole
    textvariable=input_text     # Navázání proměnné na vstupní pole
)
```
