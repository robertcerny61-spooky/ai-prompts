---
id: sql-query-v1
owner: data-team
purpose: sql_generation
model: gpt-4.1+, claude-3.5+
language: cs
tags: [sql, database, query, optimization]
version: 1.0.0
created: 2026-04-08
last_tested: 2026-04-08
status: active
---

# 🗄️ Univerzální prompt: Příprava SQL dotazů

Pro efektivní generování, optimalizaci a debug SQL dotazů s vědomím datového modelu CPS.

---

## 📋 Kontext: Datový model

Pracuješ s CPS (Credit Processing System) databází. Dostupné schéma:

### Hlavní moduly a tabulky (seznam):
- **CPSCLOG** - Control/Log data (protokolování)
- **CPSCSYS** - System configuration (nastavení)
- **CPSIDATA** - Insurance data (pojistná data)
- **CPSINSDATA** - Insurance details (detaily pojištění)
- **CPSLDATA** - Loan data (půjčka data)
- **CPSMAUDATA** - MAU (?) audit data
- **CPSMDATA** - Master data (základní údaje)
- **CPSPADATA** - Payments/accounts (platby, účty)
- **CPSPDATA** - Product data (data produktů)
- **CPSPENDATA** - Penalties (penalizace)
- **CPSSDATA** - Status/Segment (statusy, segmenty)
- **PSPADATA**, **PSPTDATA** - Partner/Third-party data

**Poznámka**: Přesný seznam sloupců najdeš v DDL schématu.

---

## 🎯 Instrukce: Jak vytvořit SQL dotaz

### 1️⃣ Vstupní data (vyplň vždy)

```
CÍLE:
- Co chceš zjistit? (věcný popis)
- Jaké otázky odpovídáš?

PODMÍNKY:
- Která data potřebuješ? (tabulky)
- Jaké filtry? (WHERE klauzule)
- Jak spojit tabulky? (JOIN, ON)

VÝSTUP:
- Jaké sloupce? (SELECT)
- Jak seskupovat? (GROUP BY)
- Jaké agregace? (COUNT, SUM, AVG...)
- Řazení? (ORDER BY)
- Limity? (TOP N, OFFSET...)

VÝKON:
- Kolik řádků očekáváš?
- Jsou tam potenciální "úzká místa"?
- Potřebuješ index hint?
```

### 2️⃣ Analýza

Podle vstupu:
- ✅ Ověř dostupnost tabulek a sloupců
- ✅ Zkontroluj datové typy (VARCHAR, INT, DATE...)
- ✅ Hledej vhodné JOIN podmínky (cizí klíče)
- ✅ Identifikuj potřebné agregace
- ✅ Rozsuduj filtry (WHERE, HAVING)

### 3️⃣ Generování

Vygeneruj SQL podle SQL Server / Oracle syntaxe:

```sql
SELECT 
    <sloupce>,
    COUNT(*) AS pocet_zaznamu
FROM <hlavní_tabulka>
LEFT JOIN <spojená_tabulka> ON <podmínka>
WHERE <filtry>
GROUP BY <sloupce>
HAVING <agregační_filtry>
ORDER BY <řazení>
```

### 4️⃣ Optimalizace

- **Čitelnost**: Správné formátování, aliasy
- **Výkon**: Minimal JOINy, WHERE před GROUP BY
- **Bezpečnost**: Nikdy dynamický SQL bez parametrizace
- **Výsledky**: Smysluplné sloupce

---

## 📝 Výstupní formát

### Sekce 1: Shrnutí
```
CO DOTAZ DĚLÁ:
[1-2 věty co dotaz odpovídá]

TABULKY:
- <tabulka1> (role)
- <tabulka2> (role)
```

### Sekce 2: SQL kód
```sql
-- [Komentář co dělá]
SELECT ...
```

### Sekce 3: Poznámky
```
VAROVÁNÍ:
- Co kontrolovat?
- Kde jsou rizika?

MOŽNÉ VYLEPŠENÍ:
- Co by šlo optimalizovat?

TESTOVÁNÍ:
- Jak ověřit správnost?
```

---

## 💡 Příklady

### Příklad 1: Počet aktivních půjček

**Vstup:**
```
CÍLE: Kolik je aktivních půjček per klient?
PODMÍNKY: Status = 'ACTIVE', filtruj na poslední 6 měsíců
VÝSTUP: Klient (ID), Počet, Suma
```

**Výstup:**
```
CO DOTAZ DĚLÁ:
Vrací počet a celkovou sumu aktivních půjček per klient.

TABULKY:
- CPSLDATA (informace o půjčkách)
- CPSMDATA (info o klientech)
- CPSSDATA (status půjčky)

SQL:
SELECT 
    c.KlientID,
    c.KlientJmeno,
    COUNT(l.PujckaID) AS pocet_pujcek,
    SUM(l.Castka) AS celkova_suma
FROM CPSMDATA c
INNER JOIN CPSLDATA l ON c.KlientID = l.KlientID
INNER JOIN CPSSDATA s ON l.StatusID = s.StatusID
WHERE s.Status = 'ACTIVE'
  AND l.DatumZalozeni >= DATEADD(MONTH, -6, GETDATE())
GROUP BY c.KlientID, c.KlientJmeno
ORDER BY pocet_pujcek DESC;

VAROVÁNÍ:
- Ověř stejná jména sloupců v CPSLDATA a CPSMDATA
- Zkontroluj formát datumů

MOŽNÉ VYLEPŠENÍ:
- Přidej HAVING COUNT(*) > 1 pokud chceš jen klienty s více půjčkami
```

### Příklad 2: Nejčastější pojistné škody

**Vstup:**
```
CÍLE: Top 10 typů pojistných škod za rok 2025
PODMÍNKY: Year(datum) = 2025
VÝSTUP: Typ, Počet, Průměr
```

**Výstup:**
```
CO DOTAZ DĚLÁ:
Zobrazuje top 10 nejčastějších typů pojistných škod v roce 2025.

TABULKY:
- CPSIDATA (pojistná data)
- CPSINSDATA (detaily pojištění)

SQL:
SELECT TOP 10
    i.TypSkody,
    COUNT(*) AS pocet_skod,
    AVG(CAST(i.CastkaSkoky AS FLOAT)) AS prumernaSkoda
FROM CPSIDATA i
WHERE YEAR(i.DatumSkody) = 2025
GROUP BY i.TypSkody
ORDER BY pocet_skod DESC;

VAROVÁNÍ:
- Ověř datový typ CastkaSkoky (možná je STRING)
- Zkontroluj přesné jméno sloupce "DatumSkody"

TESTOVÁNÍ:
- Spusť dotaz s YEAR = 2024 a porovnej s reálností
```

---

## 🔧 Pokročilé

### Parametrizované dotazy (doporučeno!)

```sql
DECLARE @KlientID INT = ?;
DECLARE @OdData DATETIME = ?;

SELECT ...
WHERE KlientID = @KlientID
  AND DatumZalozeni >= @OdData;
```

### Častá rozšíření

**Cohort analýza** (skupiny klientů):
```sql
SELECT 
    YEAR(DatumZalozeni) AS rok,
    QUARTER(DatumZalozeni) AS ctvrtleti,
    COUNT(DISTINCT KlientID) AS pocet_novych
FROM CPSMDATA
GROUP BY YEAR(DatumZalozeni), QUARTER(DatumZalozeni)
ORDER BY rok, ctvrtleti;
```

**Trend (MoM, YoY)**:
```sql
SELECT 
    DATEFROMPARTS(YEAR(d), MONTH(d), 1) AS mesic,
    SUM(Castka) AS total,
    LAG(SUM(Castka)) OVER (ORDER BY DATEFROMPARTS(YEAR(d), MONTH(d), 1)) AS predchozi_mesic
FROM <tabulka>
GROUP BY YEAR(d), MONTH(d)
ORDER BY mesic DESC;
```

---

## ⚙️ Bezpečnost a Best Practices

1. **NIKDY** nevkládej surová data do dotazu → vždy parametrizuj (`@Param`)
2. **Aliasy**: Použij `AS` pro jasnost (`COUNT(*) AS pocet`)
3. **Komentáře**: Piš SQL komentáře pro komplexní logiku
4. **Testing**: Vždy spi dotaz s `TOP 100` nejdřív
5. **Schéma**: Pokud nejsí jasné jméno sloupce → zeptej se nebo zkontroluj DDL

---

## 🚀 Jak tento prompt používat?

1. Zkopíruj sekci "Vstupní data" do svého promptu
2. Vyplň všechny `<!-- DOPLŇ -->` pole
3. Pošli mi tento prompt + tvé vstupní data
4. Dostaneš hotový SQL + poznámky

**Příklad:**
```
Použij SQL prompt - univerzální.

CÍLE: Chci vidět top 5 klientů podle hodnoty půjček
PODMÍNKY: Status = ACTIVE, za poslední rok
VÝSTUP: KlientID, Jméno, CelkovaHodnota, PocetPujcek
VÝKON: Očekávám max 1000 řádků
```

---

## 📞 Kontakt & Feedback

- Máš návrh na vylepšení? Uprav `CHANGELOG.md` a verzuj.
- Našel jsi chybu v promptu? Zvyš verzi (1.0.0 → 1.0.1)
- Netušíš které sloupce použít? Vrať se k DDL schématu v DATA_MODEL/

---

*Version: 1.0.0 | Last Updated: 2026-04-08 | Status: Active*

