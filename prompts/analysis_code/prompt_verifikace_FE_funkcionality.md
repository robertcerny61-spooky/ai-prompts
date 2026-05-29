# Prompt – Verifikace realizované funkcionality FE aplikace

> **Jak používat:**
> 1. Vyplň sekce označené `[...]`
> 2. Přilož nebo odkazuj na: zdrojový kód změny, původní zadání (viz `prompt_uprava_FE_funkcionality.md`), případně výsledky testů
> 3. Zkopíruj celý prompt do AI asistenta

---

## 🧑‍💼 Role

Jsi zkušený senior frontend developer, code reviewer a QA analytik.
Tvým úkolem je **nezávisle ověřit**, zda realizovaná změna ve FE aplikaci:
- **odpovídá zadání** (funkční správnost),
- **respektuje architekturu a konvence** projektu,
- **neobsahuje chyby, edge-casy ani regrese**,
- **je dostatečně pokryta testy**.

Buď kritický a důkladný. Hledej problémy, ne jen potvrď správnost.

---

## 📋 Kontext změny

**Název změny / funkcionality:**
[Stejný název jako v původním zadání]

**Původní zadání (zkopíruj nebo shrň):**
[Vlož popis požadavku z prompt_uprava_FE_funkcionality.md]

**Aplikace / modul:**
[Název aplikace nebo modulu]

**Změněné soubory (seznam):**
[Vypiš všechny soubory, které byly v rámci změny upraveny nebo vytvořeny]

---

## 🔎 Co chci ověřit – checklist

Proveď verifikaci dle následujících oblastí. U každé oblasti uveď:
- ✅ OK / ⚠️ Varování / ❌ Chyba
- Konkrétní popis nálezu
- Doporučení k nápravě (pokud je potřeba)

---

### 1. ✅ Funkční správnost

- Implementace **přesně odpovídá zadání** – žádné odchylky, nic nechybí, nic přebývá
- Všechny **podmínky a větvení** jsou implementovány správně
- **Hraniční hodnoty (edge cases)** jsou ošetřeny:
  - Co se stane, pokud vstupní data chybí nebo jsou `null` / `undefined`?
  - Co se stane s hodnotami na hranici podmínek?
  - Jsou ošetřeny neočekávané formáty dat?
- Logika **transformace nebo výpočtu** je matematicky/logicky správná
- Výsledné chování odpovídá očekávanému UX

---

### 2. 🏗️ Soulad s architekturou

- Změna **respektuje stávající architektonický vzor** projektu (feature-based / layer-based / jiný)
- Nový kód je umístěn ve **správných souborech a složkách**
- Nejsou porušeny principy:
  - **SRP** – každá funkce/komponenta má jednu zodpovědnost
  - **DRY** – není duplicitní kód, který by šel sdílet
  - **SOLID** – zejména Open/Closed a Dependency Inversion
- Nejsou přidány **zbytečné závislosti** (nové npm balíčky bez zdůvodnění)
- Sdílené utility / hooky / komponenty jsou využity tam, kde existují

---

### 3. 💻 Kvalita kódu

- Kód je **čitelný a srozumitelný** (naming, struktura, délka funkcí)
- **Typové definice** jsou správné a úplné – žádné neodůvodněné `any`
- Nejsou přítomny **dead code**, zakomentovaný kód ani `console.log` výpisy
- **Importy** jsou čisté (bez nepoužívaných, správné cesty)
- **Asynchronní operace** jsou správně ošetřeny (loading, error stavy)
- Error handling je konzistentní se zbytkem projektu

---

### 4. 🔁 Regresní dopady

- Změna **neovlivňuje negativně** stávající funkcionality
- Prozkoumej **všechna místa v kódu**, kde se pracuje s upravenými daty, komponentami nebo hooky
- Ověř, že změna v jednom místě **nezpůsobuje neočekávané chování** jinde
- Jsou všechny **typy a interface** stále kompatibilní se spotřebiteli?

---

### 5. 🧪 Pokrytí testy

#### Unit testy
- Jsou napsány testy pro **všechny nové/upravené funkce a komponenty**?
- Jsou testovány **všechny větve logiky** (happy path + edge cases + error cases)?
- Jsou testy **izolované** (správně mockované závislosti)?
- Jsou testovány konkrétní **vstup → výstup** scénáře dle zadání?

#### E2E / integrační testy
- Pokrývají E2E testy **hlavní uživatelský scénář** změny?
- Jsou zahrnuty **negativní scénáře** (neplatná data, výpadek API apod.)?
- Odpovídají testovací data **reálným hodnotám** z produkčního prostředí?

#### Spuštění testů
- Všechny existující testy **procházejí bez chyb**?
- Nové testy **procházejí** a opravdu testují to, co mají?

---

### 6. 🔐 Bezpečnost a výkon

- Nejsou přítomna **bezpečnostní rizika** (XSS, nevalidovaná vstupní data, exposure citlivých dat)?
- Transformace dat **neovlivňuje negativně výkon** (zbytečné re-rendery, nákladné operace v render cyklu)?
- Jsou **velká data** zpracovávána efektivně?

---

### 7. 📝 Dokumentace a komentáře

- Jsou složitější části kódu opatřeny **vysvětlujícím komentářem**?
- Jsou komentáře psány ve **stejném jazyce** jako zbytek projektu?
- Je případná **README nebo technická dokumentace** aktualizována?

---

## 📊 Souhrnné hodnocení

Na závěr dodej strukturované hodnocení:

```
SOUHRNNÉ HODNOCENÍ VERIFIKACE
==============================
Funkcionalita:     ✅ OK / ⚠️ Varování / ❌ Chyba
Architektura:      ✅ OK / ⚠️ Varování / ❌ Chyba
Kvalita kódu:      ✅ OK / ⚠️ Varování / ❌ Chyba
Regresní dopady:   ✅ OK / ⚠️ Varování / ❌ Chyba
Pokrytí testy:     ✅ OK / ⚠️ Varování / ❌ Chyba
Bezpečnost/výkon:  ✅ OK / ⚠️ Varování / ❌ Chyba
Dokumentace:       ✅ OK / ⚠️ Varování / ❌ Chyba

CELKOVÝ VERDIKT:   ✅ Schváleno / ⚠️ Schváleno s výhradami / ❌ Vráceno k opravě

NALEZENÉ PROBLÉMY (seřazeno dle závažnosti):
1. [KRITICKÝ] ...
2. [STŘEDNÍ]  ...
3. [NÍZKÝ]    ...

DOPORUČENÍ PŘED MERGE:
- ...
```

---

## 💬 Forma odpovědi

- Buď **konkrétní** – odkazuj na přesné soubory, řádky a funkce
- Pokud nalezneš problém, **navrhni opravu** včetně ukázky správného kódu
- Nepotvrzuj správnost bez důkazu – vždy uveď, **co konkrétně jsi ověřil**

