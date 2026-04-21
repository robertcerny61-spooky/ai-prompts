
Potřebuji v tabulce T1500CASE provést update sloupce SERVICE_MODE_NORMALIZED a to pokud obsahuje hodnotu, která není null. 
Změna hodnoty bude provedena mapovací tabulkou Současná hodnota na Nová hodnota
| Současná hodnota | Nová hodnota |
|------------------|--------------|
| ClientAbsent | CLIENT_ABSENT |
| AssistedBranchDevice | ASSISTED_BRANCH_DEVICE |
| HAssistedClientDevice | ASSISTED_CLIENT_DEVICE |
| ClientAlone | CLIENT_ALONE |
| ExternalAdviserAlone | EXTERNAL_ADVISER_ALONE |
| Remote | REMOTE |
| AutomaticServerOperation | AUTOMATIC_SERVER_OPERATION |
| PhoneCall | PHONE_CALL |
| OnetimeRepresentation | ONETIME_REPRESENTATION |
Navrhni SQL dotaz

Potřebuji připravit migrační sql script pro produkční prostředí, který má provést:
1.Potřebuji v tabulce T1661TASK_STEP_BASE provést update sloupce SERVICE_MODE_NORMALIZED a to pokud obsahuje hodnotu "null" a zároveň sloupec UNSEL_INTERACTION_MODE není NULL.
2. Hodnota, kterou budeme aktualizovat sloupec SERVICE_MODE_NORMALIZED se bere z mapovací tabulky sloupec SERVICE_MODE_NORMALIZED. Tabulka obsahuje 2 sloupce:
- UNSEL_INTERACTION_MODE - hodnota vstupního sloupce záznamu T1661TASK_STEP_BASE
- SERVICE_MODE_NORMALIZED - hodnota výstupní
3. Logika mapování dle tabulky:
- hodnota UNSEL_INTERACTION_MODE se mapuje na hodnotu SERVICE_MODE_NORMALIZED
4. Script musí být optimalizovaný, protože se bude aktualizovat cca. 5 miliónů záznamů.
5. Navrhni řešení bez dočasné tabulky a vytvoření indexů. Nenavrhuj batch řešení
