<h1>📊Analiza Najczęściej Pobieranych Aplikacji na Androida</h1>

![Dashboard](img/img1.png)

## 🎯Wstęp

Dashboard przedstawia analizę **najczęściej pobieranych aplikacji na system Android** dostępne w sklepie _Google Play Store_.

Dane pozyskane ze strony _[Kaggle.com](https://www.kaggle.com/)_. Zawierają informacje o: developerach, ogólnej liczbie pobrań, datach publikacji i osiągnięcia wysokich pułapów pobrań, ceny, kategorii, typie i pre-instalacji.

#### Plik Dashboard

Plik z dashboardem znajduje się w [Google Play Store Dashboard.xlsx](Google_Play_Store_Dashboard.xlsx).

### Problem analityczny

Celem analizy jest sprawdzenie, jakie aplikacje są **najczęściej pobierane** na świecie, odkrycie wzorców, **dominujących kategorii**, wpływ **wbudowanych aplikacji** na liczbę pobrań. Jakie **firmy** przejęły rynek mobilny postawiony na Androidzie? Ogólny **zysk** z najpopularniejszych aplikacji, które są płatne.

Krótka, osobna analiza aplikacji, które osięgnły liczbę pobrań w przedziale 1mld-5mld.

#### Pytania analityczne:

1. Jakie aplikacje należą do topki?
2. Jakie kategorie są najczęściej pobierane?
3. Który developer góruje na rynku? Który ma najwięcej aplikacji?
4. Ile zarobiły płatne aplikacje?

## ⚙️ Przygotowanie danych

W pierwszej kolejności dane zostały poddane standardowym procedurom ETL. Wykorzystane zostało do tego narzędzie Power Query.

![Dashboard](img/img2.png)

1. Zmiana pierwszego wiersza na nagłówki.
2. Usunięcie dublikatów i pustych wierszy, których nie było w tej bazie danych.
3. Wszystkie dane były odczytane jako tekstowe, więc wykonanie transformacji niektórych kolumn w celu ujednolicenia, głównie kolumny "Price".
4. Zmiana typów danych.
5. Dodano kolumnę, w której zmieniono "Downloands" na typ liczbowy biorąc dolne granice przedziałów
   ![Dashboard](img/img3.png)

6. Brakujące wartości:
   - brak jednej wartości w "Date_reached" oraz czterech w "Date_published" - pozostawiono je,
   - brak jednej wartości w "Pre-installed" dla aplikacji "Google Hangouts", odnaleziono jednak informację, że apliakcja ta niegdyś była domyślnie instalowana na urządzeniach mobilnych, więc uzupełnioną tę informację.

## 🧠 Analiza

### 1️⃣ Jakie aplikacje należą do topki?

Do analizy wybrano kolumny z nazwą, liczbą pobrań i informacją o pre-instalaji. Celem było pokazanie 5-ciu topowych aplikacji, jednak ze względu na za mało dokładne dane pokazane zostały wszystkie aplikacje o takiej samej liczbie pobrań.

W celu wyłonienia 5-ciu najczęściej pobieranych aplikacji użytko formuły:

`=FILTRUJ(STOS.POZ(Dane[App]; Dane[Downloads_Numeric]); Dane[Downloads_Numeric] >= MAX.K(Dane[Downloads_Numeric];5))`

Dane zawierają kolumnę "Pre-installed", co oznacza że część aplikacji zostało pobranych przez producenta i mogło to znacząco wpłynąć na wyniki.

![Dashboard](img/img5.png)

Formuły kolejno pokazujące 5 najlepszych aplikacji pre-instalowanych i nie pre-instalowanych:

`=SORTUJ(FILTRUJ(STOS.POZ(Dane[App]; Dane[Downloads_Numeric]); (LEWY(Dane[Pre_installed];3) = "Yes") * Dane[Downloads_Numeric] >= MAX.K(FILTRUJ(Dane[Downloads_Numeric]; LEWY(Dane[Pre_installed];3) = "Yes"); 5)); 2; -1)`

`=SORTUJ(FILTRUJ(STOS.POZ(Dane[App]; Dane[Downloads_Numeric]); (Dane[Pre_installed]= "No") * Dane[Downloads_Numeric] >= MAX.K(FILTRUJ(Dane[Downloads_Numeric]; Dane[Pre_installed] = "No"); 5)); 2; -1)`

Tabele:

![Dashboard](img/img4.png)

#### Wnioski

Pre-instalacja ma decydujący wpływ na popularność i zasięg danej aplikacji. Użytkownicy rzadziej szukają alternatyw dla aplikacji, które otrzymali wraz z zakupem urządzeń mobilnych.

Kolorami zostały porównanie powtarzające się wartości, jedynie jedna aplikacja znalazła się w ścisłej czołówce i jest to _WhatsApp Messenger_, co świadczy o niezwykłej popualrności tej aplikacji i świadomym wyborze użytkowników.

### 2️⃣ Jakie kategorie są najczęściej pobierane?

Prócz informacji, czy aplikacje zostały preinstalowane, ważna jest także informacja na temat ich kategorii. Preinstalowane aplikacje to w większości wypadków apliakcja potrzebne lub pomagające w codziennym funkcjonowaniu użytkownika.
Ponadto 10% topowych aplikacji to apliakcje nie preinstalowane, więc informacja o najczęstrzych kategoriach również jest ważna.

![Dashboard](img/img6.png)

#### Wnioski

Zdecydowanie widać dominację komunikatorów, do których zalicza się m.in. _WhatsApp Messenger_, nie jest to dziwne zważywszy na ogólnodostępną sieć komórkową przez co użytkownicy coraz częściej wybierają darmowe aplikacja niż połączenie telefoniczne czy sms'y.

Urządzenia mobilne, choć wciąż służące głównie jako komunikaotry, coraz częściej służą także rozrywce
