# 🏠 Struktura Danych Nowoczesnego Domu Jednorodzinnego w Firebird SQL

Projekt przedstawia kompletną **relacyjną strukturę danych** dla **nowoczesnego, inteligentnego domu jednorodzinnego**, zaprojektowaną z myślą o zarządzaniu energią, komfortem, bezpieczeństwem oraz automatyką budynkową. System obejmuje m.in. obsługę urządzeń, czujników, pomieszczeń, fotowoltaiki, magazynu energii, taryf, reguł decyzyjnych oraz danych historycznych i prognostycznych.

Modelowany obiekt to **parterowy dom jednorodzinny z garażem w bryle**, zamieszkały przez **4 osoby**, o powierzchni około **100 m²**, zlokalizowany w **Tomaszowie Bolesławieckim**. Projekt został przygotowany jako koncepcyjno–inżynierski model danych pod przyszłą implementację systemu EMS (*Energy Management System*).

---

## 🛠️ Technologie i środowisko

- **Baza danych:** ![Firebird SQL](https://img.shields.io/badge/Firebird-SQL-orange)
- **Środowisko projektowe:** ![IBExpert](https://img.shields.io/badge/IBExpert-DB%20Designer-blue)
- **Model danych:** ![Relational Model](https://img.shields.io/badge/Model-Relacyjny-darkgreen)
- **Podejście projektowe:** ![Normalization](https://img.shields.io/badge/Projektowanie-Normalizacja-informational)
- **Typ projektu:** ![Engineering Concept](https://img.shields.io/badge/Projekt-Koncepcyjno--Inżynierski-purple)

---

## 📌 Główne założenia projektu

Projekt został zaprojektowany tak, aby system mógł:

- monitorować zużycie energii elektrycznej w domu,
- rejestrować dane z czujników środowiskowych i bezpieczeństwa,
- obsługiwać instalację fotowoltaiczną oraz magazyn energii,
- zarządzać ogrzewaniem, CWU, chłodzeniem i buforami cieplnymi,
- uwzględniać dynamiczne ceny energii i taryfy,
- przechowywać prognozy pogody i prognozy produkcji PV,
- definiować scenariusze, harmonogramy i reguły działania,
- analizować historię decyzji systemu automatyki.

---

## 🧩 Funkcje programu / struktury danych

<details>
<summary><strong>📁 DOM</strong> — główna encja projektu</summary>

Tabela nadrzędna całego systemu. Opisuje konkretny budynek i stanowi punkt odniesienia dla większości pozostałych tabel. Przechowuje podstawowe informacje o domu, takie jak nazwa, lokalizacja, współrzędne GPS, powierzchnia, liczba mieszkańców oraz moc przyłączeniowa.

</details>

<details>
<summary><strong>🔋 BATERIA</strong> — konfiguracja magazynu energii</summary>

Tabela opisuje magazyn energii elektrycznej zainstalowany w domu. Zawiera dane techniczne baterii, takie jak pojemność, maksymalna moc ładowania i rozładowania, zakres SoC, sprawność oraz domyślną strategię pracy.

</details>

<details>
<summary><strong>📊 STAN_BATERII</strong> — bieżący i historyczny stan baterii</summary>

Przechowuje historyczne i aktualne stany pracy magazynu energii. Zawiera poziom naładowania, moce ładowania i rozładowania, źródło ładowania oraz tryb pracy baterii w czasie.

</details>

<details>
<summary><strong>⚡ BILANS_ENERGII</strong> — zagregowany bilans energetyczny domu</summary>

Tabela analityczna służąca do zapisu bilansu energetycznego w czasie. Pozwala określić, ile energii pobrano z sieci, oddano do sieci, wyprodukowano z PV, przekazano do baterii oraz jaki był całkowity koszt energii.

</details>

<details>
<summary><strong>🔥 BUFOR_CIEPLA</strong> — konfiguracja magazynu ciepła</summary>

Opisuje bufory ciepła wykorzystywane w domu, np. bufor CO, CWU lub podłogówki. Zawiera informacje o typie bufora, pojemności, temperaturach granicznych i możliwości wcześniejszego nagrzewania.

</details>

<details>
<summary><strong>🌡️ BUFOR_CIEPLA_POMIAR</strong> — pomiary temperatury i energii bufora</summary>

Tabela przechowuje historyczne pomiary stanu bufora ciepła. Rejestruje temperaturę oraz szacowaną ilość zgromadzonej energii cieplnej.

</details>

<details>
<summary><strong>💸 TARYFA_STATYCZNA</strong> — definicje taryf energetycznych</summary>

Tabela słownikowa zawierająca rodzaje taryf energetycznych, np. G11, G12 lub taryfę dynamiczną. Oddziela definicję taryfy od konkretnych cen godzinowych.

</details>

<details>
<summary><strong>🕒 CENA_ENERGII_GODZINOWA</strong> — godzinowe ceny energii</summary>

Przechowuje ceny zakupu i sprzedaży energii dla konkretnej taryfy, daty i godziny. Tabela jest kluczowa dla optymalizacji kosztów pracy urządzeń oraz strategii ładowania baterii.

</details>

<details>
<summary><strong>🚿 CWU_POMIAR</strong> — parametry ciepłej wody użytkowej</summary>

Służy do rejestrowania temperatury i zużycia ciepłej wody użytkowej. Pozwala analizować komfort domowników oraz zapotrzebowanie energetyczne systemu CWU.

</details>

<details>
<summary><strong>🧠 REGULA</strong> — logika decyzyjna systemu</summary>

Tabela przechowuje reguły sterujące inteligentnym domem. Definiuje warunki logiczne, akcje do wykonania oraz aktywność danej reguły.

</details>

<details>
<summary><strong>📜 HISTORIA_DECYZJI</strong> — historia decyzji automatyki</summary>

Rejestruje decyzje podejmowane przez system na podstawie reguł. Umożliwia analizę działania automatyki, audyt oraz debugowanie zachowania systemu.

</details>

<details>
<summary><strong>☀️ INSTALACJA_PV</strong> — konfiguracja instalacji fotowoltaicznej</summary>

Opisuje parametry techniczne instalacji PV, takie jak moc, liczba paneli, orientacja, kąt nachylenia, model falownika oraz data uruchomienia.

</details>

<details>
<summary><strong>📈 PRODUKCJA_PV</strong> — rzeczywiste pomiary produkcji PV</summary>

Przechowuje dane historyczne dotyczące pracy instalacji fotowoltaicznej. Rejestruje chwilową moc DC i AC oraz energię dzienną i całkowitą.

</details>

<details>
<summary><strong>🔮 PROGNOZA_PV</strong> — prognozowana produkcja energii z PV</summary>

Tabela zawiera prognozowaną moc i energię produkowaną przez instalację fotowoltaiczną. Umożliwia planowanie pracy urządzeń i optymalizację autokonsumpcji.

</details>

<details>
<summary><strong>🏠 LICZNIK_GLOWNY</strong> — konfiguracja głównego licznika energii</summary>

Opisuje główny licznik energii elektrycznej domu. Przechowuje dane identyfikacyjne, moc przyłączeniową oraz typ taryfy.

</details>

<details>
<summary><strong>📉 ZUZYCIE_DOMU</strong> — zużycie energii całego budynku</summary>

Tabela rejestruje rzeczywiste zużycie energii elektrycznej przez cały dom. Zawiera dane o mocy chwilowej, imporcie i eksporcie energii.

</details>

<details>
<summary><strong>🌦️ PROGNOZA_POGODY</strong> — dane prognostyczne pogody</summary>

Przechowuje prognozowane warunki pogodowe dla domu, m.in. temperaturę, wilgotność, zachmurzenie, wiatr, opady i nasłonecznienie. Dane te są wykorzystywane np. do prognoz PV i sterowania ogrzewaniem.

</details>

<details>
<summary><strong>👨‍👩‍👧‍👦 DOMOWNIK</strong> — użytkownicy domu</summary>

Opisuje mieszkańców domu i ich podstawowe cechy, takie jak imię, wiek i typ domownika. Tabela wspiera modelowanie obecności, komfortu i profilu zużycia energii.

</details>

<details>
<summary><strong>🛋️ POMIESZCZENIE</strong> — opis pomieszczeń domu</summary>

Przechowuje informacje o wszystkich pomieszczeniach w budynku. Obejmuje nazwę, typ, powierzchnię, wysokość, kubaturę, klasę izolacji oraz priorytet komfortu.

</details>

<details>
<summary><strong>🪟 OKNO_KOMFORTU</strong> — warunki komfortu w czasie</summary>

Definiuje przedziały czasowe oraz dopuszczalne zakresy temperatury i wilgotności w konkretnych pomieszczeniach. Wykorzystywane do sterowania komfortem cieplnym.

</details>

<details>
<summary><strong>🔥 OGRZEWANIE_CONFIG</strong> — konfiguracja systemu ogrzewania</summary>

Opisuje logiczną konfigurację źródeł ogrzewania w domu, np. pompy ciepła i grzałki elektrycznej. Stanowi podstawę dla dalszego sterowania systemem grzewczym.

</details>

<details>
<summary><strong>🔌 URZADZENIE</strong> — urządzenia działające w domu</summary>

Centralna tabela opisująca wszystkie urządzenia w systemie, np. AGD, urządzenia grzewcze, wykonawcze i energochłonne. Zawiera parametry techniczne, sposób sterowania, interfejs komunikacyjny i priorytety działania.

</details>

<details>
<summary><strong>🗂️ GRUPA_URZADZEN</strong> — grupowanie urządzeń</summary>

Tabela służy do logicznego grupowania urządzeń w kategorie, np. AGD, ogrzewanie czy oświetlenie. Ułatwia raportowanie i sterowanie całymi grupami.

</details>

<details>
<summary><strong>🏷️ TYP_URZADZENIA</strong> — słownik typów urządzeń</summary>

Przechowuje klasyfikację urządzeń według ich funkcji i charakteru pracy. Ułatwia rozszerzanie systemu oraz porządkowanie danych.

</details>

<details>
<summary><strong>📥 ZUZYCIE_URZADZENIA</strong> — zużycie energii przez urządzenia</summary>

Tabela zawiera zagregowane dane o zużyciu energii przez poszczególne urządzenia w określonych przedziałach czasu. Umożliwia analizę energochłonności sprzętu.

</details>

<details>
<summary><strong>⚙️ URZADZENIE_PARAMETR</strong> — parametry konfiguracyjne urządzeń</summary>

Tabela typu key–value przechowująca dodatkowe parametry urządzeń, które są zmienne, opcjonalne lub zależne od modelu. Pozwala elastycznie rozszerzać konfigurację urządzeń.

</details>

<details>
<summary><strong>🗓️ PLAN_STEROWANIA</strong> — zaplanowane akcje dla urządzeń</summary>

Przechowuje konkretne zaplanowane działania sterujące dla urządzeń: moment startu, stopu, preferowane źródło energii oraz szacowany koszt wykonania.

</details>

<details>
<summary><strong>⏰ HARMONOGRAM_URZADZENIA</strong> — powtarzalne zasady pracy urządzeń</summary>

Tabela opisuje cykliczne harmonogramy działania urządzeń w wybranych dniach tygodnia i godzinach. Może uwzględniać np. minimalny poziom naładowania baterii.

</details>

<details>
<summary><strong>🎭 SCENARIUSZ_DNIA</strong> — scenariusze funkcjonowania domu</summary>

Definiuje gotowe tryby działania domu, np. dzień roboczy, weekend lub nieobecność. Scenariusze wpływają na urządzenia, reguły i harmonogramy.

</details>

<details>
<summary><strong>🚶 SCENARIUSZ_OBECNOSC</strong> — model obecności domowników</summary>

Opisuje przedziały czasowe obecności lub nieobecności mieszkańców w ramach konkretnego scenariusza dnia. Dane te wpływają na komfort, bezpieczeństwo i oszczędność energii.

</details>

<details>
<summary><strong>📡 CZUJNIK</strong> — konfiguracja czujników</summary>

Centralna tabela warstwy pomiarowej. Opisuje wszystkie czujniki w systemie: środowiskowe, energetyczne i bezpieczeństwa, wraz z ich lokalizacją, jednostką i interfejsem komunikacji.

</details>

<details>
<summary><strong>📥 ODCZYT_CZUJNIKA</strong> — historyczne odczyty z czujników</summary>

Przechowuje właściwe dane pomiarowe zbierane z czujników w czasie. Umożliwia analizę zmian parametrów środowiskowych, bezpieczeństwa i zużycia energii.

</details>

<details>
<summary><strong>🧾 TYP_CZUJNIKA</strong> — słownik rodzajów czujników</summary>

Tabela definiuje typy czujników, np. temperatura, ruch, zalanie czy dym. Zapewnia spójność opisu i interpretacji danych pomiarowych.

</details>

<details>
<summary><strong>🚨 STREFA_ALARMOWA</strong> — logiczne strefy systemu alarmowego</summary>

Opisuje podział domu na strefy alarmowe, np. garaż, parter czy ogród. Ułatwia grupowanie zdarzeń oraz konfigurację systemu bezpieczeństwa.

</details>

<details>
<summary><strong>🔗 STREFA_CZUJNIK</strong> — przypisanie czujników do stref alarmowych</summary>

Tabela łącznikowa przypisująca konkretne czujniki do wybranych stref alarmowych. Dzięki niej system wie, które sensory należą do której strefy.

</details>

<details>
<summary><strong>🚔 ZDARZENIE_ALARMOWE</strong> — historia zdarzeń alarmowych</summary>

Przechowuje log zdarzeń alarmowych wykrytych w domu. Rejestruje czas, strefę, czujnik, typ zdarzenia, status obsługi i dodatkowy opis.

</details>

---

## 🧱 Cechy projektu

- modularna i czytelna struktura relacyjna,
- logiczne powiązania między encjami,
- przygotowanie pod EMS i automatykę domową,
- możliwość rozbudowy o nowe urządzenia, czujniki i scenariusze,
- obsługa danych historycznych oraz prognostycznych,
- możliwość dalszej implementacji algorytmów optymalizacyjnych.

---

## 📂 Przykładowe obszary modelu danych

Projekt obejmuje między innymi:

- zarządzanie domem i jego parametrami,
- zarządzanie pomieszczeniami i komfortem,
- rejestrację danych z czujników,
- sterowanie urządzeniami,
- bilans energetyczny,
- fotowoltaikę i magazyn energii,
- system alarmowy,
- scenariusze i reguły automatyki,
- prognozy pogody i prognozy PV.

---

## 🖼️ Podgląd projektu domu

> Tutaj możesz dodać obraz przedstawiający rzut / widok założonego domu, np. plik:
>
> `docs/widok_domu.jpg`

```md
![Podgląd domu](docs/widok_domu.jpg)
