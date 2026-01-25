# Dokument Wymagań Projektowych (PRD): EduBoost (Ultra-MVP)
**Wersja:** 1.1 (Lean)
**Data:** 11 Listopada 2025
**Cel:** Dostarczenie kluczowej pętli wartości (Tekst -> Test -> Wynik) do 14 Grudnia.

## 1. Wprowadzenie i Streszczenie

**EduBoost** to aplikacja internetowa (webowa) zaprojektowana, aby zrewolucjonizować proces nauki poprzez automatyzację metody "Active Recall".

Niniejszy dokument określa zakres **Ultra-MVP** (Minimum Viable Product), którego celem jest walidacja jednej, kluczowej hipotezy: czy jesteśmy w stanie dostarczyć użytkownikom **wartościowy, interaktywny test** wygenerowany przez AI na podstawie ich własnych notatek.

Zakres został celowo i radykalnie ograniczony, aby umożliwić wdrożenie w krótkim czasie. **Cały moduł fiszek został usunięty** z tego etapu.

## 2. Problem Użytkownika

* **Problem:** Pasywne czytanie notatek jest nieefektywną metodą nauki.
* **Idealna Metoda:** Metody oparte na "Active Recall" (np. testy próbne) są naukowo dowiedzione jako najbardziej efektywne.
* **Bariera:** Ręczne tworzenie testów na podstawie własnych notatek jest czasochłonne i demotywujące.

## 3. Rozwiązanie i Cele

### 3.1. Proponowane Rozwiązanie (Ultra-MVP)
Stworzymy aplikację webową **EduBoost**, która pozwala użytkownikowi wkleić tekst (do 5000 znaków), a następnie wygenerować i edytować **Test typu "Uzupełnij lukę"**. Użytkownik może zapisać ten test na swoim koncie, wielokrotnie go rozwiązywać i śledzić swoje wyniki.

### 3.2. Cele Biznesowe i Użytkownika
* **Cel (Użytkownik):** Otrzymać gotowy do rozwiązania, użyteczny test z moich notatek w mniej niż 60 sekund.
* **Cel (Biznes):** Zweryfikować, czy generowane przez AI testy mają wystarczającą jakość, aby użytkownicy chcieli je zapisywać i rozwiązywać.

### 3.3. Kluczowe Kryteria Sukcesu (Ultra-MVP)
1.  **75% testów** wygenerowanych przez AI jest akceptowanych (edytowanych i zapisywanych) przez użytkownika.
2.  Użytkownicy, którzy zapisali test, rozwiązują go co najmniej raz.

## 4. Zakres Funkcjonalności MVP

### 4.1. Funkcjonalności Wchodzące w Zakres (IN)

#### A. Zarządzanie Kontem Użytkownika
* Rejestracja użytkownika (login/adres e-mail, hasło).
* Logowanie użytkownika.

#### B. Generowanie Testu (AI)
* Jeden główny ekran tworzenia z polem `textarea`.
* Pole `textarea` ma limit 5000 znaków, z widocznym licznikiem (np. `4800/5000`).
* Po przekroczeniu limitu przycisk "Generuj Test" staje się nieaktywny (disabled).
* Po wklejeniu tekstu użytkownik ma jeden przycisk: "Generuj Test".

#### C. Moduł Testów (Uzupełnij Lukę)
* **Generowanie:** AI analizuje tekst i zwraca treść z wygenerowanymi lukami (np. `[___________]`).
* **Edycja przed Zapisem (Kluczowa Funkcja):** Użytkownik widzi wygenerowany test i *musi mieć* możliwość edycji przed pierwszym zapisem. Obejmuje to:
    * Edycję oczekiwanej odpowiedzi dla danej luki.
    * Usunięcie luki (kliknięcie "x", które przywraca oryginalne słowo).
* **Zapisywanie:** Użytkownik musi nadać testowi **Tytuł** (pole `input` z placeholderem "Wpisz tytuł") i kliknąć "Zapisz". Test jest zapisywany w bazie danych.
* **Rozwiązywanie:**
    * Użytkownik wypełnia tekstowo wszystkie luki.
    * Walidacja jest niewrażliwa na wielkość liter (case-insensitive), ale wrażliwa na znaki diakrytyczne.
    * Użytkownik klika "Zatwierdź".
    * System oblicza wynik (np. 8/10), zapisuje go w historii i podświetla odpowiedzi na zielono/czerwono.
    * Użytkownik widzi opcję "Spróbuj jeszcze raz" (co resetuje test do pustego stanu).

#### D. Pulpit Główny / Biblioteka Testów
* Jedna lista: "Moje Testy".
* Lista jest sortowana chronologicznie (najnowsze na górze).
* **Widok listy "Moje Testy" (kolumny):**
    1.  Tytuł
    2.  Typ Testu (wartość "Uzupełnij lukę")
    3.  Data Utworzenia
    4.  Ostatni Wynik (np. "8/10" lub "Nierozwiązany")
    5.  Postęp (prosty pasek `progress bar` wizualnie reprezentujący Ostatni Wynik, np. 80%)
    6.  Akcje (Ikona "Usuń")
* **Usuwanie:** Kliknięcie ikony "Usuń" wyświetla okno modalne z potwierdzeniem ("Czy na pewno chcesz usunąć ten test?").

#### E. Mechanizmy Wsparcia Jakości AI
* Po wygenerowaniu materiału (przed edycją), użytkownik widzi opcje: "Zapisz" (po dokonaniu edycji) lub "Odrzuć" (powraca do pustego `textarea`).
* "Zapisz" = Akceptacja (liczone do kryterium sukcesu).

### 4.2. Funkcjonalności Poza Zakresem (OUT)
* **CAŁY MODUŁ FISZEK:** Generowanie fiszek przez AI, manualne tworzenie, przeglądanie (awers/rewers) i punktacja fiszek są **całkowicie poza zakresem** tego MVP.
* **Samoobsługowy Reset Hasła:** Funkcja "Zapomniałem hasła" nie będzie implementowana.
* **Zaawansowane Ustawienia Konta:** (np. zmiana hasła przez zalogowanego użytkownika).
* **Import plików:** (PDF, DOCX, itp.).
* **Współdzielenie:** testów.
* **Aplikacje mobilne.**
* **Inne typy testów.**

## 5. Historie Użytkownika (User Stories)

| Jako... | Chcę... | Aby... |
| :--- | :--- | :--- |
| Nowy użytkownik | Zarejestrować się w systemie podając e-mail i hasło | Mieć dostęp do zapisywania moich testów. |
| Zarejestrowany użytkownik | Zalogować się na moje konto | Uzyskać dostęp do moich testów. |
| Użytkownik | Wkleić tekst moich notatek (do 5000 znaków) | Użyć go jako bazy do generowania testu. |
| Użytkownik | Kliknąć "Generuj Test" po wklejeniu tekstu | Otrzymać test typu "uzupełnij lukę" gotowy do edycji. |
| Użytkownik | Edytować i usuwać luki wygenerowane przez AI | Poprawić błędy AI lub dostosować test do moich potrzeb przed zapisaniem. |
| Użytkownik | Zapisać mój test, nadając mu tytuł | Zachować go na moim koncie do późniejszej nauki. |
| Użytkownik | Otworzyć zapisany test z mojej biblioteki | Rozwiązać go (test powinien być pusty, gotowy do nauki). |
| Użytkownik | Otrzymać punktację (np. 7/10) po kliknięciu "Zatwierdź" | Zmierzyć moją wiedzę i zobaczyć, gdzie popełniłem błędy. |
| Użytkownik | Kliknąć "Spróbuj jeszcze raz" po rozwiązaniu testu | Ponownie podejść do testu, aby poprawić wynik. |
| Użytkownik | Przeglądać listę wszystkich moich testów z wynikami | Szybko znaleźć materiał i monitorować moje postępy. |
| Użytkownik | Trwale usunąć test, którego już nie potrzebuję | Utrzymać porządek w mojej bibliotece. |

## 6. Wymagania Niefunkcjonalne i Ograniczenia

### 6.1. Ograniczenia Projektowe (Kluczowe)
* **Brak Resetowania Hasła (Samoobsługa):** W ramach Ultra-MVP **nie będzie** zaimplementowanej funkcji automatycznego resetowania zapomnianego hasła przez e-mail. Proces odzyskiwania konta odbywa się wyłącznie manualnie przez administratora.
* **Tylko Web:** Aplikacja jest dostępna wyłącznie przez przeglądarkę internetową.

### 6.2. Wymagania Techniczne
* **Śledzenie Użycia AI:** Backend musi zliczać i zapisywać każdą udaną generację AI powiązaną z ID użytkownika (na potrzeby przyszłej monetyzacji).
* **Śledzenie Akceptacji AI:** Backend musi śledzić stosunek zapisów do odrzuceń (na potrzeby pomiaru kryterium sukcesu 75%).
* **Słownik Typów Testów:** Typ testu ("Uzupełnij lukę") musi być przechowywany w bazie danych jako klucz obcy do oddzielnej tabeli (słownika), aby umożliwić łatwe dodawanie nowych typów w przyszłości.

### 6.3. Obsługa Błędów
* **Błąd Generacji AI:** Jeśli AI nie zwróci poprawnych danych, użytkownik musi zobaczyć jasny komunikat (np. "Nie udało się wygenerować testu z tego tekstu. Spróbuj użyć innego fragmentu.").
* **Błąd Zapisu:** Jeśli zapis do bazy danych nie powiedzie się, użytkownik musi zobaczyć komunikat o błędzie, ale **nie może** utracić danych, które wprowadził (powinien pozostać na ekranie edycji z nienaruszonymi danymi).