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
