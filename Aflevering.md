# Aflevering: Quality API CI/CD Projekt

## GitHub Repository
Alle kildekoder, tests og konfigurationsfiler kan findes her:
[https://github.com/Lagzer/Quality-api-case](https://github.com/Lagzer/Quality-api-case)

## Defect Reports
Jeg har dokumenteret og rettet følgende fejl fundet under testfasen. Den fulde rapport kan findes i projektet:
[defect-reports.md](defect-reports.md)

**Oversigt over rettede fejl:**
- **DEF-001:** Grade-beregning returnerede forkert karakter ved grænseværdien 60 (F i stedet for D).
- **DEF-002:** Rabat ved beløb på 100 blev beregnet som 0% i stedet for 10%.
- **DEF-003:** Booking-systemet tillod 6 sæder, selvom grænsen krævede afvisning.
- **DEF-004:** Brugernavn-formatering tvang tekst til små bogstaver og håndterede ikke blanke input som "Ugyldig".
- **DEF-005:** Sensor-gennemsnit mistede præcision pga. heltalsdivision (f.eks. 1.5 blev til 1.0).

## GoogleTest - Unit Tests
Projektet indeholder en omfattende suite af automatiserede unit tests placeret i [tests/quality_service_test.cpp](tests/quality_service_test.cpp). Testene dækker:
- Grænseværdier for karaktergivning.
- Kombinationsregler for rabatter (loyalitet, kuponer, produktionstilstand).
- Adgangskontrol og sikkerhedsregler for booking.
- Validering og trimning af inputdata.

Alle tests kører automatisk i CI/CD-pipelinen og skal bestå 100%, før koden kan merges eller deployes.

## Forklaring af CI/CD Pipeline
Pipelinens workflow er defineret i [.github/workflows/ci-cd.yml](.github/workflows/ci-cd.yml) og består af to hovedjob:

1.  **Build & Test:**
    *   **Miljø:** Kører på `ubuntu-latest`.
    *   **Build:** Bruger `CMake` og `Ninja/g++` til at konfigurere og kompilere koden.
    *   **Test:** Kører de automatiserede GoogleTest-enhedstests via `ctest`. Hvis blot én test fejler, stopper pipelinen her, og deployment afbrydes.
2.  **Deployment (GitHub Pages):**
    *   **Betingelse:** Kører kun hvis build og test er succesfulde på `main` branchen.
    *   **Handling:** Uploader indholdet fra `web/` mappen som et artifact og deployer det til GitHub Pages, så frontend-delen er tilgængelig online.

## Refleksion: Manuel Black Box vs. Automatiseret CI/CD Test
**Manuel Black Box-test** er effektiv til at validere brugeroplevelsen (UX) og finde uforudsete fejlkombinationer, som en programmør måske ikke har tænkt på. Det kræver dog mange ressourcer og er fejlbehæftet over tid, da man nemt kan glemme at teste en specifik edge-case.

**Automatiseret test i CI/CD** giver derimod en "sikkerhedsnet"-effekt. Hver gang koden ændres, verificeres alle tidligere fundne fejl (regressionstest) på få sekunder. Det sikrer en høj kodekvalitet og tillader hurtigere releases, da man har matematisk vished for, at den eksisterende logik stadig fungerer. Ulempen er, at det kun tester det, man eksplicit har skrevet tests for – det er derfor vigtigt at kombinere begge metoder.
