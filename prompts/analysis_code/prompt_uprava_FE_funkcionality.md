# Prompt – Úprava funkcionality FE aplikace

> **Jak používat:** Vyplň sekce označené `[...]` a zkopíruj celý prompt do AI asistenta.
> toto znamená, že se zakomentuje kapitola a v promptu je ignorovány
<!--
### Krok 5 – Unit testy
- Dodej unit testy pro všechny nové/upravené komponenty...
-->

---

## 🧑‍💼 Role

Jsi zkušený senior frontend developer a solution analytik.
Pracuješ na existující FE aplikaci a tvým úkolem je **bezpečně a správně implementovat zadanou změnu** s plným respektováním stávající architektury, konvencí a technologického stacku.

---

## 📋 Zadání

**Název změny / funkcionality:**
Změna ve zpracování response služby /v1/electronic-documents/dossiers a /v1/electronic-documents/dossiers/products/{id}

**Popis požadavku:**
SLužba /v1/electronic-documents/dossiers a /v1/electronic-documents/dossiers/products/{id} vrací jako response objekt DOSSIERS s daty. Potřebuji při načtení response služby provést úpravu hodnoty atributu id u dossiers a parentId. FE aplikace následně s daty dossiers pracuje. Atribut id a parentId bude upraven pouze v následujícím případě:
Pokud "id" i parentId obsahuje zleva znaky:
- první 2 znaky = CA
- třetí a čtvrtý znak je = LS
- zbylé znaky jsou pouze čísla <0,9> a zároveň počet zbylých čísel musí být > než 5 znaků
potom hodnotu "id" i parentId uprav způsobem, že odstraníš znaky "LS" 

**Změna se týká aplikace / modulu:**
docui-fe

---

## 🛠️ Technologický stack (zjisti ze zdrojového kódu)

Před návrhem řešení **prozkoumej kódovou základnu** a zjisti:

- [ ] Použitý framework a verze (React / Angular / Vue / jiný)
- [ ] Jazyk (TypeScript / JavaScript)
- [ ] State management (Redux / Zustand / NgRx / Context API / jiný)
- [ ] Stylování (CSS Modules / Tailwind / Styled Components / SCSS / jiný)
- [ ] Způsob routování (React Router / Angular Router / Next.js / jiný)
- [ ] Testovací frameworky (Jest / Vitest / Cypress / Testing Library / jiný)
- [ ] Architektonický vzor (feature-based / layer-based / monorepo / micro-frontend / jiný)
- [ ] Způsob volání API (Axios / Fetch / React Query / Apollo / jiný)

---

## 🔍 Analýza dopadů (POVINNÁ před návrhem řešení)

Před implementací proveď **důkladnou analýzu celé kódové základny** a odpověz na tyto otázky:

### 1. Dopad na komponenty
- Které existující komponenty budou změnou ovlivněny?
- Je nutné vytvořit nové komponenty?
- Existují sdílené/reusable komponenty, které lze využít?

### 2. Dopad na datový model
- Jaká data jsou potřeba pro novou funkcionalitu?
- Odkud data pochází (API, store, props, context)?
- Je nutné rozšířit typové definice (interfaces / types)?

### 3. Dopad na state management
- Ovlivňuje změna globální stav?
- Je nutné přidat nové selektory, akce nebo reducery?

<!--
### 4. Dopad na routing
- Přibývají nové routy?
- Mění se parametry stávajících rout?
-->

### 5. Dopad na API
- Je nutné volat nové endpointy nebo upravit stávající?
- Mění se request/response kontrakt?

### 6. Dopad na výkonnost zpomalení aplikace
- Nepřináší změna výkonnostní problémy a zpomalení aplikace

### 7. Dopad na konfigurace a prostředí
- Přibývají nové env proměnné nebo konfigurační hodnoty?
- Je nutné změnit build konfiguraci?

<!--
### 8. Dopad na testy
- Které existující testy budou vyžadovat úpravu?
- Co vše je nutné nově otestovat?
-->

---

## ✅ Co chci dodat jako výstup

Proveď následující kroky **v tomto pořadí**:

### Krok 1 – Vysvětlení stávajícího kódu
- Popiš, jak relevantní část aplikace aktuálně funguje
- Identifikuj klíčové soubory, komponenty, hooky a utility

### Krok 2 – Kompletní analýza dopadů
- Vypiš **všechny soubory a místa v kódu**, která budou změnou dotčena
- Uveď, zda se jedná o přímý nebo nepřímý dopad

### Krok 3 – Návrh implementace
- Navrhni konkrétní řešení respektující stávající architekturu
- Uveď, které soubory budou **upraveny** a které **nově vytvořeny**
- Dodej **kompletní ukázky kódu** pro každou změnu

### Krok 4 – Architekturní validace
- Ověř, že návrh je v souladu se stávajícím architektonickým vzorem
- Upozorni na případná porušení principů (DRY, SRP, SOLID apod.)
- Navrhni alternativní přístupy, pokud existují

<!--
### Krok 5 – Unit testy
- Dodej unit testy pro všechny nové/upravené komponenty, hooky a utility
- Použij testovací framework, který je v projektu již zaveden
-->

<!--
### Krok 6 – E2E testy
- Dodej E2E testy (Cypress / Playwright / jiný dle projektu) pokrývající hlavní scénáře
- Zahrň pozitivní i negativní scénáře
-->

### Krok 7 – Rizika a doporučení
- Popiš možná rizika implementace
- Navrhni mitigační opatření
- Uveď, zda je nutné provést code review specifických částí

---

## 📐 Konvence a pravidla (respektuj vždy)

- Používej **stejný coding style** jako zbytek projektu (naming, struktura souborů, exporty)
- Nepřidávej nové závislosti (npm balíčky) bez explicitního zdůvodnění
- Pokud přidáváš novou závislost, uveď proč a jakou verzi
- Veškerý kód musí být **plně typovaný** (žádné `any` bez zdůvodnění)
- Komentáře v kódu piš ve stejném jazyce, jako je zbytek projektu

---

## 💬 Forma odpovědi

Po každém kroku uveď:
- **Proč** jsi zvolil toto řešení
- **Tradeoffs** daného přístupu
- **Možné alternativy** a kdy by dávaly větší smysl

