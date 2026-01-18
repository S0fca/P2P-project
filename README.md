# P2P Bankovní systém
## Základní informace
- **Škola:** SPŠE Ječná
- **Autor:** Sofia Hennelová
- **Datum:** 18.1. 2026

## 1. Úvod
Cílem tohoto školního projektu je vytvořit peer-to-peer (P2P) bankovní systém, kde každý uzel reprezentuje jednu banku.   

Každý uzel je schopen:
- Vytvářet a mazat bankovní účty
- Vkládat a vybírat finanční prostředky
- Kontrolovat zůstatek na účtu
- Zobrazit počet klientů a zůstatek v bance
- Komunikovat s ostatními bankami v síti přes TCP/IP

Aplikace je ovládána ručně pomocí PuTTY nebo telnetu, bez grafického uživatelského rozhraní.  
Komunikace bude probíhat pomocí přesně určených příkazů, které budou zasílný jako text v UTF-8 kódování

## 2. Analýza
### 2.1 Funkční požadavky (Functional Requirements)
- FR1: Banka musí odpovídat na příkaz BC a vracet svou IP adresu jako kód banky.
- FR2: Banka musí umožnit vytvoření bankovního účtu pomocí příkazu AC.
- FR3: Banka musí umožnit vložení peněz na účet pomocí příkazu AD.
- FR4: Banka musí umožnit výběr peněz z účtu pomocí příkazu AW.
- FR5: Banka musí vracet aktuální zůstatek na účtu pomocí příkazu AB.
- FR6: Banka musí umožnit smazání účtu pomocí příkazu AR, pouze pokud je zůstatek účtu 0.
- FR7: Banka musí vracet celkovou částku uloženou ve všech účtech pomocí příkazu BA.
- FR8: Banka musí vracet počet klientů (účtů) pomocí příkazu BN.

Rozšířené funkce (ESSENTIALS BANK NODE)
- FR9: Pokud příkazy AD, AW nebo AB obsahují jiný kód banky (IP adresu), než má aktuální uzel, aplikace se musí připojit na cílovou banku, předat jí příkaz a vrátit odpověď zpět volajícímu.

Pokročilé funkce (HACKER BANK NODE)
- FR10: Banka musí podporovat příkaz RP <number> pouze na vlastním uzlu.
- FR11: Banka musí projít celou P2P síť a zjistit:
  - kolik peněz má každá banka (BA)
  - kolik má klientů (BN)
- FR12: Systém musí navrhnout plán loupeže tak, aby:
  - bylo dosaženo co nejblíže cílové částce
  - bylo okradeno co nejméně klientů
  - bylo možné vyloupit vždy pouze celou banku nebo nic

### 2.2 Ne-funkční požadavky (Non-functional Requirements)
- NFR1: Aplikace musí běžet bez použití IDE.
- NFR2: Aplikace musí naslouchat na TCP portu v rozsahu 65525–65535.
- NFR3: Komunikace probíhá v textovém formátu UTF-8, zprávy jsou jednořádkové.
- NFR4: Každý příkaz musí vrátit odpověď (úspěch nebo ER).
- NFR5: Aplikace musí podporovat více klientů současně (paralelní obsluha).
- NFR6: Aplikace musí mít konfigurovatelný timeout (defaultně 5 sekund).
- NFR7: Aplikace musí logovat svůj provoz i komunikaci s ostatními uzly.
- NFR8: Chybové hlášky musí být srozumitelné a jednoznačné.

## 3. Návrh (Design)

