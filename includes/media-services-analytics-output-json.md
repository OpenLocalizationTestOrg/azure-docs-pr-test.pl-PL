zadanie Hello generuje dane wyjściowe JSON zawierający metadane dotyczące wykrytego i śledzonych kroje. Witaj metadanych zawiera współrzędne wskazującą lokalizację hello kroje, a także krój identyfikator numer wskazujące hello śledzenia tej osoby. Numery identyfikatorów krój są podatne tooreset czynników podczas krój czołowego hello zostanie utracony lub pokrywający się w ramce hello spowodować, że niektóre osoby pobierania przypisanych wiele identyfikatorów.

Witaj danych wyjściowych JSON zawiera hello następujące atrybuty:

| Element | Opis |
| --- | --- |
| Wersja |Odnosi się wersja toohello hello wideo interfejsu API. |
| Indeks | (Dotyczy tylko tooAzure Redactor nośnika) definiuje indeksu ramki hello hello bieżącego zdarzenia. |
| skali czasu |"Impulsów" na sekundę hello wideo. |
| Przesunięcie |Jest to przesunięcie czasu hello sygnatur czasowych. W wersji 1.0 interfejsów API, wideo ta będzie zawsze równa 0. W przyszłości scenariusze, które firma Microsoft obsługuje, ta wartość może zmienić. |
| szybkość klatek |Klatek na sekundę hello wideo. |
| fragmenty |metadane Hello jest fragmentaryczne się w różnych segmentach fragmenty. Każdy fragmentu zawiera rozpoczęcia, czas trwania, liczba interwałów i zdarzenia. |
| rozpoczynanie |Witaj uruchomienie hello pierwsze zdarzenie parametrem "ticks". |
| Czas trwania |Długość Hello fragmentu hello w parametrem "ticks". |
| interval |Interwał powitania każdego wpisu zdarzeń w obrębie fragmentu hello, w parametrem "ticks". |
| zdarzenia |Każde zdarzenie zawiera kroje hello wykryte i śledzone w tym czas trwania. Jest tablicą tablicy zdarzeń. Tablica zewnętrzne Hello reprezentuje jeden interwał czasu. Tablica wewnętrzny Hello składa się z 0 lub więcej zdarzeń, które wystąpiły w danym momencie. [] Nawiasu pusty oznacza, że nie wykryto żadnych kroje. |
| id |Identyfikator Hello hello krój, który jest śledzona. Ta liczba może spowodować niezamierzoną zmianę, jeśli krój staje się niewykryte. Danej osoby powinny mieć hello IDENTYFIKATORA takie same w całej hello ogólne wideo, ale to nie można zagwarantować termin toolimitations w algorytmie wykrywania hello (okluzji itp.) |
| x, y |Witaj w lewym górnym rogu X i Y współrzędne powierzchni hello obwiedni w skali znormalizowane 0.0 too1.0. <br/>-X i Y współrzędne są zawsze, toolandscape względną, więc jeśli pionowo wideo (lub dołu, w przypadku hello systemu IOS), konieczne będzie tootranspose hello współrzędne odpowiednio. |
| szerokość, wysokość |wysokość i szerokość krój hello obwiedni w skali znormalizowane 0.0 too1.0 Hello. |
| facesDetected |To znajduje się na końcu hello hello wyniki JSON i zawiera podsumowanie liczby hello kroje tego algorytmu hello wykryte podczas hello wideo. Ponieważ hello identyfikatorów można zresetować przypadkowo Jeśli krój staje się niewykryte (np. krój wychodzeniu ekranu, wygląda optymalizacji), ta liczba nie zawsze równa true liczba kroje wideo hello hello. |

