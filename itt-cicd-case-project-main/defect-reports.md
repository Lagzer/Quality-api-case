# Defect Reports

## DEF-001

| Felt | Indhold |
|---|---|
| Defect ID | DEF-001 |
| Titel | Grade-beregning returnerer forkert karakter for score=60 |
| Severity | High |
| Priority | High |
| API endpoint / Modul | `/api/grade` / `QualityService::calculateGrade` |
| Preconditions | API er startet lokalt |
| Steps to Reproduce | 1) Kald endpoint: `/api/grade?score=60` 2) Læs `result` i JSON-respons |
| Expected Result | `result` skal være `D` (grænseværdi ved 60) |
| Actual Result | `result` er `F` |
| Test Type | Black box / Unit test |
| Driftstilstand / Konfiguration | Standard konfiguration |
| Environment | Windows, lokal kørsel, 2026-04-13 |
| Reporter | QA |
| Status | New |

## DEF-002

| Felt | Indhold |
|---|---|
| Defect ID | DEF-002 |
| Titel | Rabat ved amount=100 gives som 0 i stedet for 10 |
| Severity | High |
| Priority | High |
| API endpoint / Modul | `/api/discount` / `QualityService::calculateDiscount` |
| Preconditions | API er startet lokalt |
| Steps to Reproduce | 1) Kald endpoint: `/api/discount?amount=100` 2) Læs `result` i JSON-respons |
| Expected Result | `result` skal være `10` ved grænseværdi 100 |
| Actual Result | `result` er `0` |
| Test Type | Black box / Unit test |
| Driftstilstand / Konfiguration | Standard konfiguration |
| Environment | Windows, lokal kørsel, 2026-04-13 |
| Reporter | QA |
| Status | New |

## DEF-003

| Felt | Indhold |
|---|---|
| Defect ID | DEF-003 |
| Titel | Booking accepterer 6 sæder, selvom grænsen burde afvise |
| Severity | Medium |
| Priority | Medium |
| API endpoint / Modul | `/api/booking` / `QualityService::canBookSeats` |
| Preconditions | API er startet lokalt |
| Steps to Reproduce | 1) Kald endpoint: `/api/booking?seats=6` 2) Læs `result` i JSON-respons |
| Expected Result | `result` skal være `false` ved 6 sæder |
| Actual Result | `result` er `true` |
| Test Type | Black box / Unit test |
| Driftstilstand / Konfiguration | Standard konfiguration |
| Environment | Windows, lokal kørsel, 2026-04-13 |
| Reporter | QA |
| Status | New |

## DEF-004

| Felt | Indhold |
|---|---|
| Defect ID | DEF-004 |
| Titel | Username-formattering lowercaser navn og returnerer ikke Ugyldig for blank input |
| Severity | Medium |
| Priority | Medium |
| API endpoint / Modul | `/api/username` / `QualityService::formatUsername` |
| Preconditions | API er startet lokalt |
| Steps to Reproduce | 1) Kald endpoint: `/api/username?name=%20%20Alice%20%20` 2) Verificer output 3) Kald endpoint: `/api/username?name=%20%20%20` |
| Expected Result | Trimmet navn bevarer case (`Alice`), og blankt input returnerer `Ugyldig` |
| Actual Result | Returnerer `alice` for første input og tom/placeholder-værdi for blankt input |
| Test Type | Black box / Unit test |
| Driftstilstand / Konfiguration | Standard konfiguration |
| Environment | Windows, lokal kørsel, 2026-04-13 |
| Reporter | QA |
| Status | New |

## DEF-005

| Felt | Indhold |
|---|---|
| Defect ID | DEF-005 |
| Titel | Sensor-gennemsnit mister decimaler pga. heltalsdivision |
| Severity | Medium |
| Priority | High |
| API endpoint / Modul | `/api/sensor-average` / `QualityService::calculateSensorAverage` |
| Preconditions | API er startet lokalt |
| Steps to Reproduce | 1) Kald endpoint: `/api/sensor-average?values=1,2` 2) Læs `result` i JSON-respons |
| Expected Result | `result` skal være `1.5` |
| Actual Result | `result` er `1.0` |
| Test Type | Black box / Unit test |
| Driftstilstand / Konfiguration | Standard konfiguration |
| Environment | Windows, lokal kørsel, 2026-04-13 |
| Reporter | QA |
| Status | New |

## DEF-006

| Felt | Indhold |
|---|---|
| Defect ID | DEF-006 |
| Titel | Lokal build fejler pga. NMake-generator uden tilgængelig nmake |
| Severity | High |
| Priority | High |
| API endpoint / Modul | Build-system / CMake konfiguration |
| Preconditions | CMake configure er kørt, men udviklermiljø har ikke nmake i PATH |
| Steps to Reproduce | 1) Kør: `cmake --build c:/Users/sebr1/Downloads/itt-cicd-case-project-main/itt-cicd-case-project-main/build` 2) Observer build output |
| Expected Result | Build gennemføres succesfuldt |
| Actual Result | Build stopper med fejl: `Generator: build tool execution failed, command was: nmake -f Makefile /nologo` |
| Test Type | CI / Lokal build |
| Driftstilstand / Konfiguration | CMake cache bruger `NMake Makefiles` |
| Environment | Windows, lokal kørsel, 2026-04-13 |
| Reporter | QA |
| Status | New |
