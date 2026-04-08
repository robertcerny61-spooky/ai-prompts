
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