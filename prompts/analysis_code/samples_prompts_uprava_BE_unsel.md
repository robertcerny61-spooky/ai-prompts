Jsem solution analytik.
Požadavek:
Na BE aplikaci UNSEL požaduji upravit následující funkčnosti:
1) UC BSL1455B Příprava folderu pro podpis dokumentace v SIGMA
2) UC BSL1442N_B Aktualizace folderu pro podpis dokumentace
3) REL1445_PUT Uložení návratové Url adresy FUNSEL SIGMA na folder

Popis jednotlivých úprav:
1) UC BSL1455B Příprava folderu pro podpis dokumentace v SIGMA
- potřebují upravit plnění služby na založení folderu pomocí POST /v1/sigma/folders a to následovně:
    - v metadatech se nebudou plnit data pro category = "BIO_SIGN_CALLBACK_PARAMS"
    - nově se bude plnit objekt dat traceParams a to atribut:
        - traceCorrelationId - plnit číslo žádosti CaseId
    - v metadatech se nově budou plnit data pro category "INSIGN_SIGN_PARAMS" jako:
      {
      "category": "INSIGN_SIGN_PARAMS",
      "params": [
      {
      "key": "openMode",
      "value": "IFRAME"
      },
      {
      "key": "continueURL",
      "value": "about:blank"
      }
      ]
      }
        - Atributy se plní vždy bez logiky, konstanty
2) UC BSL1442N_B Aktualizace folderu pro podpis dokumentace
   potřebují upravit plnění služby aktualizace folderu pomocí PUT /api/v1/folders/{folderId}:
    - bude se aktualizovat objekt traceParams, kde se atributy budou plnit:
        - traceCorrelationId - plnit číslo žádosti CaseId
        - traceChannel - plnit "FUNSEL"
        - traceSourceChannel - plní se následovně:
            - Pokud je na aktuálním úkolu uložena Zdrojová aplikace, která spouští FE úvěrového procesu (tj. currentTask.sourceApplication is not null), pak se plní (překlad přes číselník CB_ApplicationSystem).
            - Jinak systém plní hodnotu sourceSystem jako CDM ID z číselníku SYSTEM.
3) REL1445_PUT Uložení návratové Url adresy FUNSEL SIGMA na folder
    - odstraň plnění pro category "BIO_SIGN_CALLBACK_PARAMS"


Použij:
- C#
- clean architecture
- modular structure
- reusable functionaliy

Po každém kroku vysvětli:
- proč to děláš
- tradeoffs
- možné alternativy

Proveď:
1) vysvětlení kódu
2) dopady změny
3) návrh úprav
4) architekturní validaci
5) nevymýšlej nové patterny

Vše vygeneruj do MD souboru